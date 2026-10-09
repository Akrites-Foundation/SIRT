# TAP Intake API

Submit vulnerability reports to the Akrites pipeline and check their status.

There is one submission endpoint plus a status endpoint. Both return JSON; submissions
accept JSON or `multipart/mixed`.

---

## Transport

**TLS is required.** All requests must use `https://`. There is no HTTP-to-HTTPS redirect: a
request to `http://` is accepted and closed with no response, by which point its token has
already been sent unencrypted. TLS 1.2 is the minimum version. Do not disable certificate
verification.

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

A `tap_v1_…` token expires at most a year after it was issued, and can be revoked
sooner; if Akrites disables a member, all its tokens stop working. Any of these is
then refused like an unrecognized token; ask Akrites for a new one.

---

## Endpoints

### `POST /v1/reports`

The submission endpoint. Returns `202` with a receipt and an
[RFC 8288](https://datatracker.ietf.org/doc/html/rfc8288) `Link` header giving the
submission's status URL.

Requests identified as cross-origin are rejected with `403` before the body is read.
Command-line clients do not need to send an `Origin` header.

### `GET /v1/submissions/{receipt}`

The status endpoint. Returns the latest status change, e.g. `{"at":"2026-09-25T16:00:13Z","receipt":"SUB-wfd5rx5u64ffq5e2pm","status":"done"}`. **The receipt is the proof-of-submission** — holding one is what
lets a submission be read via this endpoint. Anyone who has it can read the status. A receipt that
does not exist returns `404`.

Members will also be able to get report status information from the Member Portal when it is
available, without the need for receipts.

---

## The report object

For JSON submissions, use `Content-Type: application/json`. Parsing is strict:
**unknown fields are rejected**, as is a key repeated at the top level or within an
attachment, and the body must be exactly one JSON document. Provide either `purl`, or both
`ecosystem` and `software`. All strings must be valid UTF-8.
Metadata fields reject control characters, newlines and tabs included. The encrypted
payloads, `exploit`, `raw` and an attachment's `data`, may contain them, using JSON escapes
when submitted as JSON; a binary [content type](#content-types) is sent as base64 instead.

### Core

| Field | Type | Limit | Notes |
|---|---|---|---|
| `purl` | string | ≤512 B | [package-url](https://github.com/package-url/purl-spec), e.g. `pkg:npm/lodash@4.17.20`. Stored in canonical form (the `pkg:` scheme and type are case-folded, encoding normalized). **Required** unless both `ecosystem` and `software` are supplied. |
| `software` | string | 1–256 B | **Required** when `purl` is absent. e.g. `openssl`, `kubernetes`|
| `ecosystem` | string | ≤128 B | **Required** when `purl` is absent. e.g. `npm`, `PyPI`, `Go`. |
| `versions` | string[] | ≤64 entries, ≤64 B each | Affected versions, matching the software's version scheme. A versioned `purl` adds its version to these, under the same limits. |
| `code_path` | string | ≤1024 B | Free-text affected function/lines; `affected_symbol` is preferred. |
| `exploit` | string | ≤1 MiB | **DEPRECATED, use attachments instead.** Binary types are standard base64 with padding. **Sensitive: encrypted at rest and never logged.** |
| `exploit_content_type` | string | [content type](#content-types) | **DEPRECATED, use attachments instead.** The media type of `exploit`. **Required** when `exploit` is present. |

**Note:** If both are provided, `ecosystem` and `purl` must match, unless `ecosystem` has no purl type (`Linux`, `OSS-Fuzz`, `Android`, `GitHub Actions`, `Hardware`).

**Errata:** Accepted `ecosystem` values will be aligned with the [ecosystems published by OSV](https://ossf.github.io/osv-schema/#defined-ecosystems) in a future release.

**Note:** Package-URL types must conform to the [specified types](https://github.com/package-url/purl-spec/tree/main/types).

**Note:** `exploit` and `raw` are stored as attachments named `exploit` (type `exploit-proof-of-concept`) and `raw` (type `other`), after any you sent. They count toward the 16 attachments, and no attachment may download under the same name as either. Each draws a `deprecated_field` [warning](#202-accepted).

Over [`multipart/mixed`](#multipart-submissions), each attachment is an `attachment` part instead, its fields in the part's headers.

### Attachments

`attachments` is an array of at most 16 objects, each one file:

| Field | Type | Limit | Notes |
|---|---|---|---|
| `filename` | string | 1–255 B | **Required.** A file name, not a path: a `/` or `\`, a name of just `.` or `..`, or an invisible formatting character (such as a bidi override) is `invalid_filename`. Unique within the report by the name it downloads under: with its content type's [extension](#content-types) appended unless it already ends in it, ignoring case and Unicode form, so `poc` and `poc.txt`, both `text/plain`, are not. |
| `data` | string | ≤1 MiB | **Required.** The file; binary types are standard base64 with padding. **Sensitive: encrypted at rest and never logged.** |
| `content_type` | string | [content type](#content-types) | **Required.** The media type of `data`. |
| `description` | string | ≤1024 B | Optional, one line. An invisible formatting character is `control_characters`. |
| `type` | string | — | `patch`, `exploit-proof-of-concept`, `reproducer`, `threat-model`, or `other`. Defaults to `other`. An OSV document is an `application/json` attachment of type `other`. |

**Only `data` is encrypted.** `filename`, `content_type`, `description` and `type` are
stored in the clear, so keep exploit detail out of them.

### Identity

| Field | Type | Limit | Notes |
|---|---|---|---|
| `affected_symbol` | object | — | `{"file": ≤512 B, "function": ≤256 B, "line": int ≥ 0}`. `line` is display-only and is not used for matching. |
| `references` | string[] | ≤16 entries, ≤512 B each | Each must be an `http://` or `https://` URL. |
| `upstream_ids` | string[] | ≤16 entries, ≤128 B each | `CVE-YYYY-NNNN+`, `GHSA-xxxx-xxxx-xxxx`, or `PREFIX-token` (`OSV-`, `GO-`, `RUSTSEC-`, `PYSEC-`). |
| `introduced_commit` | string | 7–64 hex chars | Full or short SHA. |
| `fixed_commit` | string | 7–64 hex chars | Full or short SHA. |
| `raw` | string | ≤1 MiB | **DEPRECATED, use attachments instead.** Binary types are standard base64 with padding. **Sensitive: encrypted at rest and never logged.** |
| `raw_content_type` | string | [content type](#content-types) | **DEPRECATED, use attachments instead.** The media type of `raw`. **Required** when `raw` is present. |

### Content types

Attachment `content_type`s, `exploit_content_type` and `raw_content_type`, and a multipart
payload part's `Content-Type`, take one of these, shown with the extension a download gets:
`text/plain` (`.txt`), `text/markdown` (`.md`), `application/json` (`.json`),
`application/pdf` (`.pdf`), `application/zip` (`.zip`), `application/gzip` (`.tar.gz`),
`application/x-bzip2` (`.tar.bz2`), or `application/octet-stream` (`.bin`) for anything
else binary, such as a fuzzer reproducer.

In JSON, the binary types (everything but `text/*` and `application/json`) are sent as
padded standard base64, and are stored as the file it decodes to; base64 that does not
decode, or decodes to no bytes, is `invalid_base64`. Line breaks in the base64, JSON-escaped as `\n`, are
skipped, so wrapped `base64` output decodes. A [multipart](#multipart-submissions) part
is sent as the file
itself. A text or JSON payload must be valid UTF-8 (`invalid_utf8`). Matching ignores
case, but parameters are refused: `text/plain; charset=utf-8` is `invalid_content_type`,
except that a multipart text or JSON part may add `charset=utf-8`.

A content type without its payload is `missing_field` on the payload.

### Provenance and contact

| Field | Type | Limit | Notes |
|---|---|---|---|
| `package_repo_url` | string | ≤512 B | **Not a purl** — the `http(s)` URL of the affected package's git repository. Other schemes may be rejected. |
| `discovery_method` | string | ≤32 B | Freeform. Suggestions: `manual`, `ai-assisted`, `ai-discovered`, `hybrid`, `automated-scan`, `upstream-report`, `other`. |
| `discovery_tooling` | string | ≤128 B | Freeform: the model and/or harness used to find the bug, e.g. `claude-opus-5-5 via Claude Code`. |
| `email` | string | ≤256 B | Optional notification contact. Never echoed back in any response. |
| `notify` | string | — | `off`, `final`, `milestones`, or `all`. Defaults to `milestones` when an email is given; without one, any value but `off` is `missing_field` on `email`. |

### `enrichment`

An optional pre-computed assessment, letting you skip analysis you have already done. Intake
checks only that the object is at most 64 KiB, nests at most 8 levels deep, and has no
control characters in its keys or strings; the fields below are the expected formats.

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
  "attachments": [
    {"filename": "fix.patch", "data": "--- a/src/parse.js\n+++ b/src/parse.js\n...", "content_type": "text/plain", "type": "patch"},
    {"filename": "exploit.txt", "data": "Sending a header longer than 8 KiB overflows the fixed buffer ...", "content_type": "text/plain", "type": "exploit-proof-of-concept"}
  ],
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

## Multipart submissions

Use `Content-Type: multipart/mixed` to send payload bytes without base64 encoding.
This API requires every part to carry `Content-Disposition: attachment; name=...`;
`form-data`, `inline`, and RFC 2231 `name*` are rejected with `400`. The parts may
arrive in any order:

| Part | Contents |
|---|---|
| `report` | Required `application/json` report object, with `exploit`, `raw`, their content type fields, and `attachments` omitted. |
| `exploit` | **Deprecated**: folded into an attachment, with a `deprecated_field` warning, as the JSON field is. Optional payload bytes, up to 1 MiB. The part's `Content-Type` is the payload's [content type](#content-types). |
| `raw` | **Deprecated**: folded into an attachment, with a `deprecated_field` warning, as the JSON field is. Optional payload bytes, up to 1 MiB. The part's `Content-Type` is the payload's [content type](#content-types). |
| `attachment` | Optional, repeatable up to 16: one [attachment](#attachments), up to 1 MiB. The bytes are the file, never base64. `Content-Disposition`'s `filename` is the attachment's `filename`, `Content-Type` its `content_type`, and the optional `Content-Description` and `Content-Akrites-Type` its `description` and `type`. |

Unknown parts, a repeated part other than `attachment`, payload, content type and
`attachments` fields inside `report` (even empty or null), repeated `Content-Disposition`,
`Content-Type`, `Content-Transfer-Encoding`, `Content-Description` or
`Content-Akrites-Type` headers, and `Content-*` headers other than those and
`Content-Length` are rejected with `400`, as are `Content-Description` and
`Content-Akrites-Type` on any part but an `attachment`. An attachment's metadata travels
only in its part's headers. `Content-Transfer-Encoding` may be absent, `binary`, `8bit`,
or `7bit`; other values, including `base64` and `quoted-printable`, are rejected with
`400`. The report follows the same strict JSON and metadata validation rules as a JSON
submission. A nonempty payload part without a `Content-Type` is `missing_field` on
`exploit_content_type`, `raw_content_type` or `attachments[i].content_type`, rather than
MIME's `text/plain` default. Empty `exploit` and `raw` parts are treated as absent, along
with their `Content-Type`; an empty `attachment` part is `missing_field` on
`attachments[i].data`. A repeated `filename`, or RFC 2231's `filename*`, is rejected with
`400` on any part; other than an attachment's, filenames are ignored.

An `attachment` part is judged by the same rules as a JSON attachment, Unicode included:
send a non-ASCII `filename` or `Content-Description` as raw UTF-8, quoting the `filename`
(`filename="pocé.c"`); RFC 2231 and RFC 2047 encodings are not decoded. `attachments[i]`
counts `attachment` parts in body order; `exploit` and `raw`, if sent, are filed after
them. A violation of an attachment's metadata names the `attachments[i]` field, and its
reason names the header.

The audit record preserves the report part's JSON, adding markers for nonempty encrypted
payloads and an `attachments` array for the `attachment` parts, each with its metadata
canonicalized and its marker as `data`. Other part headers and the boundaries are not stored;
each payload's declared content type is stored with the encrypted payload. Acceptance still requires the report
and all encrypted payloads to be committed together.

For example, with metadata in `report.json`:

```json
{"software": "example-lib", "ecosystem": "npm", "purl": "pkg:npm/example-lib@1.0.1"}
```

```bash
curl 'https://intake.tap.akrites.dev/v1/reports' \
  -H "Authorization: Bearer $TAP_SUBMISSION_TOKEN" \
  -H 'Content-Type: multipart/mixed' \
  -F 'report=@report.json;type=application/json' \
  -F 'attachment=@poc.c;type=text/plain;headers="Content-Akrites-Type: exploit-proof-of-concept"'
```

Without the `Content-Type` header, curl sends `multipart/form-data`, which is rejected
with `415`.

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

A report that used a deprecated field is still accepted, and the body adds `warnings`, shaped
like the [error entries](#errors) without `also_field`:

```json
"warnings": [
  {"code": "deprecated_field", "field": "exploit", "reason": "exploit is deprecated; send it as an attachment instead"}
]
```

`deprecated_field` is the only warning code. Like the error codes, it is never renamed or
repurposed. The key is absent when there is nothing to warn about.

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
| `tag:akrites.dev,2026-07:problem/malformed-json` | `400` | The body, or a multipart `report` part, is not exactly one JSON report. `detail` names the kind of failure, and the field for a wrong-typed value. |
| `tag:akrites.dev,2026-07:problem/validation` | `400`, `413` | The report parsed but failed validation. `errors` lists every violation, not only the first, though one may mask others, such as the entries of a list over its limit. |

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
`invalid_content_type`, `field_not_allowed`, `structure_too_deep`, `invalid_filename`,
`invalid_attachment_type`, and `invalid_base64`. An attachment that
[downloads under the same name](#attachments) as another is `invalid_filename`, with
`also_field` naming the first, or `exploit` or `raw` for the name a deprecated payload is
stored under. The size codes (`field_too_large`, `too_many_items`, `structure_too_deep`)
make the response a `413`.

A JSON body or multipart `report` part that is not UTF-8 is `malformed-json`.

| Status | Meaning |
|---|---|
| `400` | `malformed-json`, `validation`, a body that could not be read, a malformed multipart body, or malformed `Content-Type` parameters (`about:blank`). |
| `401` | Missing, unrecognized, expired or revoked [submission token](#submission-token), or one of a disabled member; the response does not say which. The body is not read. |
| `403` | Cross-origin browser submission (`about:blank`), or a web firewall block (HTML). |
| `404` | Unknown receipt, or unknown path. |
| `405` | Wrong method for the path; `Allow` names the right one. |
| `408` | The body did not arrive in time. Nothing was stored; resend. |
| `413` | Body over the request body limit (`about:blank`), or an oversize field (`validation`). |
| `415` | `Content-Type` is neither `application/json` nor `multipart/mixed`. The body is not read. |
| `429` | Rate limit exceeded. The window is a fixed hour, not a rolling bucket — back off exponentially. |
| `503` | Pipeline saturated or unavailable, or `exploit`, `raw` or an attachment could not be encrypted. **Your report was not stored.** Honor `Retry-After` and resubmit. A `503` to a status poll says nothing about the report; poll again. |

---

## Limits

| | Limit |
|---|---|
| Request body | 3 MiB |
| `exploit` | 1 MiB |
| `raw` | 1 MiB |
| `attachments` | 16, each `data` 1 MiB |

For JSON submissions, payload limits count bytes in the decoded strings, before any
base64 is decoded and line breaks included, so each base64-encoded payload can carry at
most 768 KiB of binary data. Multipart payload and attachment limits count each part's
bytes, allowing the full 1 MiB of binary data. The body limit includes metadata, JSON escaping, and any multipart headers and
boundaries, so a request can exceed it even when each field is within its limit. It also
bounds the payloads together: a report cannot carry 16 attachments of 1 MiB.

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
        "attachments": [
          {"filename": "exploit.txt", "data": "Overlong header overflows a fixed buffer in parseHeader().", "content_type": "text/plain", "type": "exploit-proof-of-concept"}
        ]
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
