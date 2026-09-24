# TAP Intake API

Submit vulnerability reports to the Akrites pipeline and check their status.

There is one submission endpoint plus a status endpoint. Both speak JSON.

---

## Transport

**TLS is required.** All requests must use `https://`. There is no plaintext listener and no
HTTP-to-HTTPS redirect: a request to `http://` fails to connect. TLS 1.2 is the minimum
version. Do not disable certificate verification.

---

## Base URLs

| Environment | Base URL |
|---|---|
| Production | `https://intake.tap.akrites.dev` |
| Staging | `https://intake.taptest.akrites.dev` |

---

## Submission token

Every `POST` must carry a submission token issued by Akrites:

```
TAP-SUBMISSION-TOKEN: <your-submission-token>
```

**Errata:** `Authorization: Bearer <your-submission-token>` will be available in a future release

---

## Endpoints

### `POST /v1/reports`

The submission endpoint. Returns `202` with a receipt and an
[RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288) `Link` header giving the
submission's status URL.

### `GET /v1/submissions/{receipt}`

Status of a submission. **The receipt is the proof-of-submission** — holding one is what lets a
submission be read. Anyone who has it can read the status. A receipt that does not
exist returns `404`.

---

## The report object

`Content-Type: application/json` is required; anything else is `415` and the body is not
read. Parsing is strict: **unknown fields are rejected**, and the
body must be exactly one JSON document. `software` is required, and so is `purl` except for the
ecosystems named in its row. All strings must be valid
UTF-8; the short identifier fields also reject control characters, while `exploit` and `raw`
allow newlines and tabs.

### Core

| Field | Type | Limit | Notes |
|---|---|---|---|
| `purl` | string | ≤512 B | [package-url](https://github.com/package-url/purl-spec), e.g. `pkg:npm/lodash@4.17.20`. Stored in canonical form (the `pkg:` scheme and type are case-folded, encoding normalized). **Required** unless `ecosystem` is one with no purl type: `Linux`, `OSS-Fuzz`, `Android`, `GitHub Actions`, `Hardware`. |
| `software` | string | 1–256 B | **Required.** e.g. `openssl`, `kubernetes`|
| `ecosystem` | string | ≤128 B | e.g. `npm`, `PyPI`, `Go`. |
| `versions` | string[] | ≤64 entries, ≤64 B each | Affected versions, matching the software's version scheme. |
| `code_path` | string | ≤1024 B | Free-text affected function/lines; `affected_symbol` is preferred. |
| `exploit` | string | ≤1 MiB | Exploitation detail. May be base64-encoded binary data, such as a tarball. **Sensitive: encrypted at rest and never logged.** |

**Note:** If both are provided, `ecosystem` and `purl` must match.

**Note:** Package-URL types must conform to the [specified types](https://github.com/package-url/purl-spec/tree/main/types).

**Errata:** In a future release, software will be identified by either `purl` or the combination of `ecosystem` and `software`, with `software` becoming optional unless `purl` is missing. Until then, `software` must match the `purl`, if provided.

**Errata:** In a future release, we will add an `exploit_content_type` field, to indicate the Content-Type of the exploit. It will be mandatory when `exploit` is provided.


### Identity

| Field | Type | Limit | Notes |
|---|---|---|---|
| `affected_symbol` | object | — | `{"file": ≤512 B, "function": ≤256 B, "line": int ≥ 0}`. `line` is display-only and is not used for matching. |
| `references` | string[] | ≤16 entries, ≤512 B each | Each must be an `http://` or `https://` URL. |
| `upstream_ids` | string[] | ≤16 entries, ≤128 B each | `CVE-YYYY-NNNN+`, `GHSA-xxxx-xxxx-xxxx`, or `PREFIX-token` (`OSV-`, `GO-`, `RUSTSEC-`, `PYSEC-`). |
| `introduced_commit` | string | 7–64 hex chars | Full or short SHA. |
| `fixed_commit` | string | 7–64 hex chars | Full or short SHA. |
| `raw_format` | string | ≤32 B | Format label for `raw`, e.g. `osv`, `markdown`, `tar`, `zip`. |
| `raw` | string | ≤1 MiB | The original payload verbatim — an [OSV](https://ossf.github.io/osv-schema/) document, markdown, etc. May be base64-encoded binary data. **Sensitive: encrypted at rest and never logged.** |

**Errata:** In a future release, we will replace `raw_format` with a `raw_content_type` field, to indicate the Content-Type of the raw data. It will be mandatory when `raw` is provided.


### Provenance and contact

| Field | Type | Limit | Notes |
|---|---|---|---|
| `package_repo_url` | string | ≤512 B | **Not a purl** — the `http(s)` URL of the affected package's git repository. Other schemes are rejected. |
| `discovery_method` | string | ≤32 B | `manual`, `ai-assisted`, `ai-discovered`, `hybrid`, `automated-scan`, `upstream-report`, `other`. |
| `discovery_tooling` | string | ≤128 B | Freeform: the model and/or harness used to find the bug, e.g. `claude-opus-5-5 via Claude Code`. |
| `email` | string | ≤256 B | Optional notification contact. Never echoed back in any response. |
| `notify` | string | — | `off`, `final`, `milestones`, or `all`. Defaults to `milestones` when an email is given. |

### `enrichment`

An optional pre-computed assessment, letting you skip analysis you have already done. Intake
checks only that the object is at most 64 KiB and nests at most 8 levels deep; the fields
below are the expected formats.

| Field | Type | Expected format |
|---|---|---|
| `cvss_vector` | string | **[CVSS 4.0](https://www.first.org/cvss/v4.0/specification-document) only** — `CVSS:4.0/...`, not a 3.x vector. |
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
  "package_repo_url": "https://github.com/example/example-lib",
  "discovery_method": "ai-assisted",
  "discovery_tooling": "claude-opus-5-5 via Claude Code",
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
  "message": "accepted; poll /v1/submissions/{receipt} for status"
}
```

The receipt is the only handle on your submission — keep it. The `Link` header
([RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288)) carries that submission's status
URL under `rel="monitor"` ([RFC 5989](https://datatracker.ietf.org/doc/html/rfc5989)) — the
machine-readable form of the poll hint. The ref is root-relative, so resolve it against the
host you submitted to. The `message` field says the same thing in prose — prefer the header
for automation. Poll with backoff rather than in a tight loop.

### Status

The status view is redacted to `queued` or `done`; the dedup outcome and internal
identifiers are withheld:

```json
{
  "receipt": "SUB-d2mhenw4iave42m4oe",
  "status": "queued",
  "at": "2026-08-18T14:03:21.114523Z"
}
```

| Field | Values |
|---|---|
| `status` | `queued`, `processing`, `done` |
| `at` | [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) timestamp of the last change to `status` |

**Errata:** Dedupe outcome and resulting `vuln` information will be available in a future release.

---

## Errors

Errors are a flat `{"error": "<reason>"}` — not RFC 9457 `problem+json`.

| Code | Meaning |
|---|---|
| `400` | Malformed JSON, an unknown field, or a field that failed validation. Field-level messages take the form `report.<field>: <reason>`. |
| `403` | Missing or unrecognized [submission token](#submission-token), or blocked by the web firewall. The body is HTML, not JSON. |
| `404` | Unknown receipt, or unknown path. |
| `405` | Wrong method for the path; `Allow` names the right one. |
| `413` | Body over the door's cap, or an oversize field. |
| `415` | `Content-Type` is not `application/json`. The body is not read. |
| `429` | Rate limit exceeded. The window is a fixed hour, not a rolling bucket — back off exponentially. |
| `503` | Pipeline saturated or unavailable, or `exploit`/`raw` could not be encrypted. **Your report was not stored.** Honor `Retry-After` and resubmit. |

A malformed JSON body always returns the same generic `malformed json` message; validation
failures name the offending field.

**Errata:** We may change to RFC 9457 `problem+json` in the future.


---

## Limits

| | Limit |
|---|---|
| Request body | 1 MiB |
| `exploit` | 1 MiB |
| `raw` | 1 MiB |

**Errata:** Currently the body limit artificially limits the other fields. Increased limits may be available in a future release.

---

## Examples

Submit:

```bash
RECEIPT=$(curl -sS -X POST https://intake.tap.akrites.dev/v1/reports \
  -H 'Content-Type: application/json' \
  -H "TAP-SUBMISSION-TOKEN: $TAP_SUBMISSION_TOKEN" \
  -d '{
        "software": "example-lib",
        "ecosystem": "npm",
        "purl": "pkg:npm/example-lib@1.0.1",
        "versions": ["1.0.1"],
        "exploit": "Overlong header overflows a fixed buffer in parseHeader()."
      }' | jq -r .receipt)
```

Then poll:

```bash
curl -sS "https://intake.tap.akrites.dev/v1/submissions/${RECEIPT}"
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
- [RFC 8259](https://datatracker.ietf.org/doc/html/rfc8259) — JSON