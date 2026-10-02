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
Authorization: Bearer <your-submission-token>
```

`TAP-SUBMISSION-TOKEN: <your-submission-token>` is still accepted, but will be removed;
move to `Authorization`. A request carrying both must carry the same token in each, or
it is refused with a `400`.

A `tap_v1_…` token expires at most a year after it was issued, and can be revoked
sooner; if Akrites disables a member, all its tokens stop working. Any of these is
then refused like an unrecognized token; ask Akrites for a new one.

---

## Endpoints

### `POST /v1/reports`

The submission endpoint. Returns `202` with a receipt and an
[RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288) `Link` header giving the
submission's status URL.

### `GET /v1/submissions/{receipt}`

The status endpoint. Returns the latest status change, e.g. `{"at":"2026-09-25T16:00:13Z","receipt":"SUB-wfd5rx5u64ffq5e2pm","status":"done"}`. **The receipt is the proof-of-submission** — holding one is what
lets a submission be read via this endpoint. Anyone who has it can read the status. A receipt that
does not exist returns `404`.

Members will also be able to get report status information from the Member Portal when it is
available, without the need for receipts.

---

## The report object

`Content-Type: application/json` is required; anything else will return `415` and the body is not
read. Parsing is strict: **unknown fields are rejected**, and the body must be exactly one JSON
document. Provide either `purl`, or both `ecosystem` and `software`. All strings must be valid
UTF-8; the short identifier fields also reject control characters, while `exploit` and `raw`
allow newlines and tabs.

### Core

| Field | Type | Limit | Notes |
|---|---|---|---|
| `purl` | string | ≤512 B | [package-url](https://github.com/package-url/purl-spec), e.g. `pkg:npm/lodash@4.17.20`. Stored in canonical form (the `pkg:` scheme and type are case-folded, encoding normalized). **Required** unless both `ecosystem` and `software` are supplied. |
| `software` | string | 1–256 B | **Required** when `purl` is absent. e.g. `openssl`, `kubernetes`|
| `ecosystem` | string | ≤128 B | **Required** when `purl` is absent. e.g. `npm`, `PyPI`, `Go`. |
| `versions` | string[] | ≤64 entries, ≤64 B each | Affected versions, matching the software's version scheme. |
| `code_path` | string | ≤1024 B | Free-text affected function/lines; `affected_symbol` is preferred. |
| `exploit` | string | ≤1 MiB | Exploitation detail. May be standard base64-encoded binary data, with padding, such as a tarball. **Sensitive: encrypted at rest and never logged.** |
| `exploit_content_type` | string | [content type](#content-types) | The media type of `exploit`. **Required** when `exploit` is present. |

**Note:** If both are provided, `ecosystem` and `purl` must match, unless `ecosystem` has no purl type (`Linux`, `OSS-Fuzz`, `Android`, `GitHub Actions`, `Hardware`).

**Note:** Package-URL types must conform to the [specified types](https://github.com/package-url/purl-spec/tree/main/types).

**Errata:** `exploit` and `raw` can be GZip or BZip'd tar files, or Zip files, to supply multiple attachments. If you wish to supply extra details, like proofs-of-concept, draft patches, and similar, it's recommended that you use obvious naming conventions within such files (`exploit.c`, `fix.patch`, `fix/`, `exploit/`).

**Errata:** `exploit`, `raw`, and their respective content type fields will be changing in a future release. Attachments will be submitted either in a new `attachments` JSON block or as [RFC 2046](https://datatracker.ietf.org/doc/html/rfc2046#section-5.1.3) `multipart/mixed` uploads. For multipart uploads, attachment names, descriptions, and content types will be supplied in the part headers. All attachments will be treated as sensitive.

### Identity

| Field | Type | Limit | Notes |
|---|---|---|---|
| `affected_symbol` | object | — | `{"file": ≤512 B, "function": ≤256 B, "line": int ≥ 0}`. `line` is display-only and is not used for matching. |
| `references` | string[] | ≤16 entries, ≤512 B each | Each must be an `http://` or `https://` URL. |
| `upstream_ids` | string[] | ≤16 entries, ≤128 B each | `CVE-YYYY-NNNN+`, `GHSA-xxxx-xxxx-xxxx`, or `PREFIX-token` (`OSV-`, `GO-`, `RUSTSEC-`, `PYSEC-`). |
| `introduced_commit` | string | 7–64 hex chars | Full or short SHA. |
| `fixed_commit` | string | 7–64 hex chars | Full or short SHA. |
| `raw` | string | ≤1 MiB | The original payload verbatim — an [OSV](https://ossf.github.io/osv-schema/) document, markdown, etc. May be standard base64-encoded binary data, with padding. **Sensitive: encrypted at rest and never logged.** |
| `raw_content_type` | string | [content type](#content-types) | The media type of `raw`; an OSV document is `application/json`. **Required** when `raw` is present. |

### Content types

`exploit_content_type` and `raw_content_type` take one of `text/plain`, `text/markdown`,
`application/json`, `application/pdf`, `application/zip`, `application/gzip` (a `.tar.gz`),
`application/x-bzip2` (a `.tar.bz2`), or `application/octet-stream` for anything else binary,
such as a fuzzer reproducer. The binary types are sent base64-encoded. Matching
ignores case, but parameters are refused: `text/plain; charset=utf-8` is
`invalid_content_type`. A content type without its payload is `missing_field` on the payload.

### Provenance and contact

| Field | Type | Limit | Notes |
|---|---|---|---|
| `package_repo_url` | string | ≤512 B | **Not a purl** — the `http(s)` URL of the affected package's git repository. Other schemes may be rejected. |
| `discovery_method` | string | ≤32 B | Freeform. Suggestions: `manual`, `ai-assisted`, `ai-discovered`, `hybrid`, `automated-scan`, `upstream-report`, `other`. |
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
  "exploit_content_type": "text/plain",
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

Until the Member Portal is available, the receipt is the only handle on your submission —
keep it. The `Link` header
([RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288)) carries that submission's status
URL under `rel="monitor"` ([RFC 5989](https://datatracker.ietf.org/doc/html/rfc5989)) — the
machine-readable form of the poll hint. The ref is root-relative, so resolve it against the
host you submitted to. The `message` field says the same thing in prose — prefer the header
for automation. Poll with backoff rather than in a tight loop.

### Status

```json
{
  "receipt": "SUB-d2mhenw4iave42m4oe",
  "status": "queued",
  "at": "2026-08-18T14:03:21Z"
}
```

| Field | Values |
|---|---|
| `status` | `queued`, `processing`, `done` |
| `at` | [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) timestamp of the last change to `status` |

**Errata:** Dedupe outcome and resulting `vuln` information will be available in a future release.

**Note:** Full status information (when available) requires both the receipt and a submission token from the same member as the original submission.

---

## Errors

Errors are [RFC 9457](https://datatracker.ietf.org/doc/html/rfc9457) problem documents, served
as `application/problem+json`:

```json
{
  "type": "tag:akrites.dev,2026-07:problem/validation",
  "title": "Report failed validation",
  "status": 400,
  "detail": "1 violation; see errors",
  "errors": [
    {"code": "invalid_reference", "field": "references[0]", "reason": "must be an absolute http or https URL"}
  ]
}
```

`type` is a URI, but not a link - it is meant to be machine-readable. `title` and `detail` are prose for
humans. Most errors are `about:blank` — the status is all there is to act on, and `detail` says what
happened. Two types say more:

| `type` | Status | Meaning |
|---|---|---|
| `tag:akrites.dev,2026-07:problem/malformed-json` | `400` | The body is not exactly one JSON report. `detail` names the kind of failure, and the field for a wrong-typed value. |
| `tag:akrites.dev,2026-07:problem/validation` | `400`, `413` | The report parsed but failed validation. `errors` lists every violation, not only the first. |

Each entry in `errors`:

| Field | Meaning |
|---|---|
| `code` | Why the field was refused. Switch on this; a shipped code is never renamed or repurposed. |
| `field` | Path within the report: `software`, `affected_symbol.file`, `versions[0]`. |
| `also_field` | The second field of a cross-field violation, such as a `purl` that disagrees with `ecosystem`. Absent otherwise. |
| `reason` | Human-readable; may be reworded. |

The codes are `missing_field`, `field_too_large`, `too_many_items`, `invalid_utf8`,
`control_characters`, `degenerate_value`, `unknown_ecosystem`, `invalid_purl`,
`purl_ecosystem_mismatch`, `invalid_reference`, `invalid_commit`, `invalid_upstream_id`,
`invalid_symbol_line`, `invalid_notify`, `invalid_email`, `invalid_repo_url`,
`invalid_content_type`, `field_not_allowed`, and `structure_too_deep`. The size codes
(`field_too_large`, `too_many_items`, `structure_too_deep`) make the response a `413`.

A body that is not UTF-8 is `malformed-json`.

| Status | Meaning |
|---|---|
| `400` | `malformed-json`, `validation`, a body that could not be read, or conflicting [submission tokens](#submission-token) (`about:blank`). |
| `401` | Missing, unrecognized, expired or revoked [submission token](#submission-token), or one of a disabled member; the response does not say which. The body is not read. |
| `403` | Blocked by the web firewall. The body is HTML. |
| `404` | Unknown receipt, or unknown path. |
| `405` | Wrong method for the path; `Allow` names the right one. |
| `408` | The body did not arrive in time. Nothing was stored; resend. |
| `413` | Body over the request body limit (`about:blank`), or an oversize field (`validation`). |
| `415` | `Content-Type` is not `application/json`. The body is not read. |
| `429` | Rate limit exceeded. The window is a fixed hour, not a rolling bucket — back off exponentially. |
| `503` | Pipeline saturated or unavailable, or `exploit`/`raw` could not be encrypted. **Your report was not stored.** Honor `Retry-After` and resubmit. |

---

## Limits

| | Limit |
|---|---|
| Request body | 3 MiB |
| `exploit` | 1 MiB |
| `raw` | 1 MiB |

Payload limits count bytes in the JSON-decoded strings; base64 is not decoded, so each
base64-encoded payload can carry at most 768 KiB of binary data. The body limit includes
metadata and JSON escaping, so a heavily escaped report can exceed it even when each
field is within its limit.

---

## Examples

Submit:

```bash
RECEIPT=$(curl -sS -X POST https://intake.tap.akrites.dev/v1/reports \
  -H 'Content-Type: application/json' \
  -H "Authorization: Bearer $TAP_SUBMISSION_TOKEN" \
  -d '{
        "software": "example-lib",
        "ecosystem": "npm",
        "purl": "pkg:npm/example-lib@1.0.1",
        "versions": ["1.0.1"],
        "exploit": "Overlong header overflows a fixed buffer in parseHeader().",
        "exploit_content_type": "text/plain"
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
- [RFC 9457](https://datatracker.ietf.org/doc/html/rfc9457) — problem details (error bodies)
- [RFC 5989](https://datatracker.ietf.org/doc/html/rfc5989) — the `monitor` link relation
- [RFC 8259](https://datatracker.ietf.org/doc/html/rfc8259) — JSON
- [RFC 2046](https://datatracker.ietf.org/doc/html/rfc2046) — MIME media types (`multipart/mixed`)
- [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) — timestamps
