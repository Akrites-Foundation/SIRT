# TAP Intake API

Submit vulnerability reports to the Akrites pipeline and check their status.

There are two submission doors — an anonymous public one and an authenticated one for
Working Group, vendor, and member submitters — plus a status endpoint. All three speak JSON.

---

## Transport

**TLS is required.** All requests must use `https://`. There is no plaintext listener and no
HTTP-to-HTTPS redirect: a request to `http://` fails to connect. TLS 1.2 is the minimum
version. Do not disable certificate verification.

---

## Base URLs

| Environment | Base URL |
|---|---|
| Production | `https://intake.tap.u269c.com` (also `https://intake.tap.akrites.dev`) |
| Staging | `https://intake.stap.u269c.com` (also `https://intake.stap.akrites.dev`) |

---

## Authentication

The public door is anonymous by default. The trusted door requires a bearer token
([RFC 6750](https://datatracker.ietf.org/doc/html/rfc6750)):

```
Authorization: Bearer <your-token>
```

**Temporary launch stopgap:** until the trusted door's authenticated edge is ready, a partner
may authenticate on the **public** door with **HTTP Basic** (`base64(<member-id>:<secret>)`,
issued at onboarding). A valid pair lifts the submission above `public`; an absent or wrong one
stays `public` — the public door never `401`s, so check the response `tier`. Retired once the
trusted door is reachable.

Your credential determines the queue tier your submission receives:

| Tier | Who | Priority |
|---|---|---|
| `wg` | Working Group / member orgs | highest |
| `vendor` | vendor tokens | above public |
| `public` | anonymous submissions | lowest |

A request to the trusted door with **no** credential is rejected with `401`. An **unrecognized**
credential (either door) is not an error — it is accepted at `public` tier, so check the `tier`
field in the response to confirm you were recognized.

---

## Endpoints

### `POST /public/v1/reports`

Anonymous by default; a partner may present HTTP Basic (temporary launch stopgap — see
Authentication). Body cap **1 MiB** for everyone. `enrichment` is discarded from an anonymous
submitter but kept from an authenticated partner. Returns `202` with a receipt and an
[RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288) `Link` header giving the
submission's status URL.

### `POST /v1/reports`

Authenticated submission (bearer). Body cap **64 MiB**, with much larger ceilings on the
`exploit` and `raw` fields so full OSV documents, SBOMs, and long proofs-of-concept fit.
`enrichment` is accepted. Returns `202` with a receipt and an
[RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288) `Link` header giving the
submission's status URL.

### `GET /v1/submissions/{receipt}`

Status of a submission. Send the same credential you submitted with. A receipt that is not
yours returns `404`, indistinguishable from one that does not exist.

### `GET /healthz`

Liveness: `{"status": "ok", "app": "intake"}`. This is the only endpoint that sends CORS
headers — cross-origin submission from a browser is not supported.

---

## The report object

`Content-Type: application/json`. Parsing is strict: **unknown fields are rejected**, and the
body must be exactly one JSON document. Only `software` is required. All strings must be valid
UTF-8; the short identifier fields also reject control characters, while `exploit` and `raw`
allow newlines and tabs.

### Core

| Field | Type | Limit | Notes |
|---|---|---|---|
| `software` | string | 1–256 B | **Required.** Rejected if it is only whitespace or punctuation. |
| `ecosystem` | string | ≤128 B | e.g. `npm`, `PyPI`, `Go`. |
| `versions` | string[] | ≤64 entries, ≤64 B each | Affected versions. |
| `code_path` | string | ≤1024 B | Free-text affected function/lines; `affected_symbol` is preferred. |
| `exploit` | string | ≤64 KiB public / ≤64 MiB trusted | Exploitation detail. Sensitive: encrypted at rest and never logged. |

### Identity

| Field | Type | Limit | Notes |
|---|---|---|---|
| `purl` | string | ≤512 B | [package-url](https://github.com/package-url/purl-spec), e.g. `pkg:npm/lodash@4.17.20`. Stored in canonical form (the `pkg:` scheme and type are case-folded, encoding normalized). Optional, but supply it when you can — it identifies the affected package and helps compare reports. |
| `affected_symbol` | object | — | `{"file": ≤512 B, "function": ≤256 B, "line": int ≥ 0}`. `line` is display-only and is not used for matching. |
| `references` | string[] | ≤16 entries, ≤512 B each | Each must be an `http://` or `https://` URL. |
| `upstream_ids` | string[] | ≤16 entries, ≤128 B each | `CVE-YYYY-NNNN+`, `GHSA-xxxx-xxxx-xxxx`, or `PREFIX-token` (`OSV-`, `GO-`, `RUSTSEC-`, `PYSEC-`). |
| `introduced_commit` | string | 7–64 hex chars | Full or short SHA. |
| `fixed_commit` | string | 7–64 hex chars | Full or short SHA. |
| `raw_format` | string | ≤32 B | Format label for `raw`, e.g. `osv`, `markdown`. |
| `raw` | string | ≤256 KiB public / ≤64 MiB trusted | The original payload verbatim — an [OSV](https://ossf.github.io/osv-schema/) document, markdown, etc. |

### Provenance and contact

| Field | Type | Limit | Notes |
|---|---|---|---|
| `package_url` | string | ≤2048 B | **Not a purl** — the `http(s)` URL of the affected package's git repository. Other schemes are rejected. |
| `discovery_method` | string | ≤32 B | `manual`, `ai-assisted`, `ai-discovered`, `hybrid`, `automated-scan`, `upstream-report`, `other`. |
| `email` | string | ≤256 B | Optional notification contact. Never echoed back in any response. |
| `notify` | string | — | `off`, `final`, `milestones`, or `all`. Defaults to `milestones` when an email is given. |

### `enrichment` — trusted door only

An optional pre-computed assessment, letting you skip analysis you have already done. Accepted
on `POST /v1/reports`; discarded on the public door.

| Field | Type | Constraint |
|---|---|---|
| `cvss_vector` | string | **[CVSS 4.0](https://www.first.org/cvss/v4.0/specification-document) only** — must match `CVSS:4.0/...`. A 3.x vector is rejected. |
| `cwe` | string | `CWE-<number>`, optionally followed by a description ([CWE](https://cwe.mitre.org/)). |
| `ssvc` | string | `Track`, `Track*`, `Attend`, or `Act` ([SSVC](https://www.cisa.gov/ssvc)). |
| `vex_status` | string | `under_investigation`, `affected`, `not_affected`, or `fixed` ([OpenVEX](https://github.com/openvex)). |
| `severity` | string | `None`, `Low`, `Medium`, `High`, or `Critical`. |
| `verified` | string | `unconfirmed`, `simulated`, or `confirmed`. |
| `epss` | number | Probability in `[0, 1]` ([EPSS](https://www.first.org/epss/)). |

### Example

```json
{
  "software": "example-lib",
  "ecosystem": "npm",
  "versions": ["1.0.0", "1.0.1"],
  "purl": "pkg:npm/example-lib@1.0.1",
  "affected_symbol": {"file": "src/parse.js", "function": "parseHeader", "line": 142},
  "exploit": "Sending a header longer than 8 KiB overflows the fixed buffer ...",
  "references": ["https://github.com/example/example-lib/issues/451"],
  "upstream_ids": ["CVE-2026-12345"],
  "fixed_commit": "9f8e7d6c5b4a3928",
  "package_url": "https://github.com/example/example-lib",
  "discovery_method": "manual",
  "email": "reporter@example.org",
  "notify": "milestones"
}
```

---

## Responses

### `202 Accepted`

```
Link: </v1/submissions/SUB-d2mhenw4iave42m4oe>; rel="monitor"
```
```json
{
  "receipt": "SUB-d2mhenw4iave42m4oe",
  "tier": "wg",
  "queue_position_estimate": 3,
  "est_seconds": 6,
  "message": "accepted; poll /v1/submissions/{receipt} for status"
}
```

The receipt is the only handle on your submission — keep it. Use `est_seconds` to time your
first status poll. The `Link` header
([RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288)) carries that submission's status
URL under `rel="monitor"` ([RFC 5989](https://datatracker.ietf.org/doc/html/rfc5989)) — the
machine-readable form of the poll hint. The ref is root-relative, so resolve it against the
host you submitted to. The `message` field says the same thing in prose — prefer the header
for automation.

### Status

For a **public** submission, the status view is redacted to `queued` or `done`; the dedup
outcome and internal identifiers are withheld:

```json
{
  "receipt": "SUB-d2mhenw4iave42m4oe",
  "tier": "public",
  "status": "queued",
  "at": "2026-08-18T14:03:21.114523Z"
}
```

For a **trusted** submission you get the full record:

```json
{
  "receipt": "SUB-d2mhenw4iave42m4oe",
  "tier": "wg",
  "status": "done",
  "outcome": "duplicate",
  "vuln_id": "AKRITES-202608-1A2B3C4D",
  "method": "identity-fingerprint",
  "confidence": 0.97,
  "at": "2026-08-18T14:03:21.114523Z"
}
```

| Field | Values |
|---|---|
| `status` | `queued`, `processing`, `done` |
| `outcome` | `new`, `duplicate`, `error` — present once `status` is `done` |
| `vuln_id` | `AKRITES-YYYYMM-NNNNNNNN`, when matched or created |
| `confidence` | `0.0`–`1.0` |
| `at` | [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) timestamp |

---

## Errors

Errors are a flat `{"error": "<reason>"}` — not RFC 9457 problem+json.

| Code | Meaning |
|---|---|
| `400` | Malformed JSON, an unknown field, or a field that failed validation. Field-level messages take the form `report.<field>: <reason>`. |
| `401` | Trusted door with no credential. |
| `404` | Unknown receipt, or one that is not yours. |
| `405` | Wrong method for the path. |
| `413` | Body over the door's cap, or an oversize field. |
| `429` | Rate limit exceeded. The window is a fixed hour, not a rolling bucket — back off exponentially. |
| `503` | Pipeline saturated or unavailable. **Your report was not stored.** Honor `Retry-After` and resubmit. |

A malformed JSON body always returns the same generic `malformed json` message; validation
failures name the offending field.

---

## Limits

| | Public door | Trusted door |
|---|---|---|
| Request body | 1 MiB | 64 MiB |
| `exploit` | 64 KiB | 64 MiB |
| `raw` | 256 KiB | 64 MiB |

---

## Examples

Anonymous submission:

```bash
curl -sS -X POST https://intake.tap.u269c.com/public/v1/reports \
  -H 'Content-Type: application/json' \
  -d '{
        "software": "example-lib",
        "ecosystem": "npm",
        "versions": ["1.0.1"],
        "exploit": "Overlong header overflows a fixed buffer in parseHeader()."
      }'
```

Authenticated submission, then poll:

```bash
RECEIPT=$(curl -sS -X POST https://intake.tap.u269c.com/v1/reports \
  -H 'Content-Type: application/json' \
  -H "Authorization: Bearer $TAP_TOKEN" \
  -d @report.json | jq -r .receipt)

curl -sS "https://intake.tap.u269c.com/v1/submissions/$RECEIPT" \
  -H "Authorization: Bearer $TAP_TOKEN"
```

---

## References

- [OSV schema](https://ossf.github.io/osv-schema/) — vulnerability document format
- [package-url (purl)](https://github.com/package-url/purl-spec) — package identity
- [CVSS v4.0](https://www.first.org/cvss/v4.0/specification-document), [CWE](https://cwe.mitre.org/), [SSVC](https://www.cisa.gov/ssvc), [EPSS](https://www.first.org/epss/), [OpenVEX](https://github.com/openvex) — assessment vocabularies
- [RFC 8446](https://datatracker.ietf.org/doc/html/rfc8446) / [RFC 5246](https://datatracker.ietf.org/doc/html/rfc5246) — TLS 1.3 / 1.2
- [RFC 9110](https://datatracker.ietf.org/doc/html/rfc9110) — HTTP semantics and `Retry-After`
- [RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288) — web linking (the `Link` header)
- [RFC 5989](https://datatracker.ietf.org/doc/html/rfc5989) — the `monitor` link relation
- [RFC 6750](https://datatracker.ietf.org/doc/html/rfc6750) — bearer tokens
- [RFC 8259](https://datatracker.ietf.org/doc/html/rfc8259) — JSON