# Contributing to the Glossary

Thanks for helping keep the **[Akrites SIRT & CVD Glossary](./Akrites_SIRT_CVD_Glossary.md)** accurate and useful. This is a lightweight process — most changes are a one-line edit and a pull request.

## What belongs here

- Terms and acronyms used routinely in the Akrites SIRT program or in Coordinated Vulnerability Disclosure.
- Program-specific vocabulary (e.g., read-in tiers, tooling names) and external standards (e.g., CVE, CVSS, TLP).

Leave out one-off jargon, project code names that aren't in general use, and anything already covered by an existing entry.

## Entry format

Each entry is a single table row in the appropriate section:

```
| **Term (Expansion if it's an acronym)** | One or two sentences, plain language. | [label](https://link) |
```

- The **Reference** column exists only in sections that use it. Use `—` when there is no external source.
- For external standards, link the **authoritative source** (the standards body or program), not a blog or vendor page.
- Keep definitions to one or two sentences. Say what it *is* and, where helpful, how Akrites uses it.
- Mark anything still provisional (e.g., "working default," "pending TOC ratification") rather than stating it as settled.

## Style rules

- **Alphabetical order within each section** — place your entry in the correct spot; don't append to the end.
- Sort by the visible term, case-insensitively (e.g., `akrites.dev` before `AVID`).
- Bold the term with `**…**`. Put an acronym's expansion in parentheses.
- Match the existing sections; if a term doesn't fit any, propose a new section in your PR description rather than inventing one silently.
- Use en dashes/em dashes consistently with the rest of the file and keep links as `[short-label](url)`.

## How to propose a change

1. **Small change (add/edit one term):** open a pull request that edits `Akrites_SIRT_CVD_Glossary.md` directly.
2. **Not sure about wording, scope, or where it belongs:** open a **Discussion** (or an issue) first and tag the Policy/Process work stream.
3. In the PR description, note: the term, why it's needed, and — for external standards — the source you used.

## Review

The **Policy/Process work stream** reviews glossary PRs. Reviewers check that the entry is accurate, concise, correctly placed alphabetically, sourced (for external terms), and consistent with ratified policy. Program-specific definitions may be adjusted to stay aligned with current policy as it evolves.

## Copy-paste templates

Two-column section (no reference):

```
| **Your Term** | Concise definition. |
```

Three-column section (with reference):

```
| **Your Term** | Concise definition. | [source](https://example.org) |
```
