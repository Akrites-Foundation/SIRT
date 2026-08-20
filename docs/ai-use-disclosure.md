# AI and LLM Use Disclosure Policy

**Owner:** Akrites SIRT
**Status:** Draft for TOC / Board review
**Applies to:** All Akrites SIRT–coordinated cases — reports from Finders and work performed by the SIRT and its Working Groups (WGs)
**Related:** [CVD Policy](../coordinated-vulnerability-disclosure-policy.md) · [Acknowledgements & Attribution Guidance](./acknowledgements-and-attribution.md) · [Embargo Handling Guidance](./Embargo%20Handling%20Guidance.md) (§4.3) · [Notification Templates](../templates/notification-templates.md) · [Intake Template](../templates/vulnerability-report-intake-template.md)

> Spelling note: the standard is **Akrites** (Akrites Foundation, Akrites SIRT). "OSS-SIRT" is a synonym.

---

## Purpose

Artificial-intelligence tooling — most notably large language models (LLMs) — is now used routinely across the vulnerability lifecycle, by both the researchers who report to us and by the SIRT itself. This document defines a single, consistent rule for **telling every stakeholder when AI tooling was used, and giving them a high-level statement of how and when it was used.**

The goal is straightforward: a Finder, Maintainer, Consumer, or downstream provider reading an Akrites case or advisory should never have to guess whether AI contributed to the discovery, analysis, fix, or write-up. We state it plainly — whether AI was used or not — for both the **Finder** and the **Coordinator (Akrites SIRT)**.

This document is the authoritative source for AI-use disclosure. The CVD Policy, CVD Guide, glossary, intake template, and notification templates all point here.

---

## Scope

This policy covers AI/LLM tooling used to **discover, reproduce, analyze, triage, prioritize, patch, test, score, translate, or document** a vulnerability handled by the Akrites SIRT. It applies to two disclosing parties:

1. **Finders** — AI tooling a reporter used before or during their report.
2. **The Akrites SIRT and its Working Groups** — AI tooling the SIRT uses while coordinating, analyzing, patching, or drafting materials for a case.

It applies regardless of who owns or hosts the tool (public service, enterprise/self-hosted model, or the SIRT's own analysis environment). It does **not** require publishing prompts, model-plus-harness internals, scaffolding, or configuration — those remain internal (see [Confidentiality](#confidentiality-public-ai-tools-and-embargo-eligibility) and the Acknowledgements guidance).

---

## Core principles

1. **Disclose by default, both ways.** Every coordinated case records, and every public advisory states, AI use for **both** the Finder and the SIRT — including an explicit "no AI tooling was used" when that is the case. Silence is not a valid disclosure.

2. **Capability-level, not marketing.** The default statement describes *what phase* AI assisted (e.g., "AI-assisted discovery and patch development"), drawn from the [controlled capability vocabulary](#controlled-capability-vocabulary-how--when). Specific model or tool names are published **only when the disclosing party requests it**, and only from the controlled vocabulary in the [Acknowledgements & Attribution Guidance](./acknowledgements-and-attribution.md). This keeps vendor branding out of the record.

3. **Human accountability is never transferred.** AI-assisted work is always reviewed and owned by a named human (the Finder for their report; a named WG member or SIRT staffer for SIRT work). Disclosing AI use documents a tool; it does not shift responsibility for the finding, the patch, or the advisory.

4. **Confidentiality is preserved.** Disclosing *that* AI was used never means revealing case detail. And per the [Embargo Handling Guidance](./Embargo%20Handling%20Guidance.md) §4.3, using a **public** AI service can itself defeat an embargo — so AI use is captured at intake precisely so the SIRT can classify embargo eligibility correctly.

5. **Consistency across the record.** The same capability vocabulary and the same two-line format are used at intake, in the case record, in embargoed notifications, and in the public advisory, so the statement means the same thing everywhere.

---

## What is disclosed

For each disclosing party (Finder and SIRT), a case captures three things:

| Element | Required? | Example |
|---|---|---|
| **Whether AI was used** | Always — yes or no | "AI tooling was used." / "No AI tooling was used." |
| **How / when (capability + phase)** | Required whenever AI materially assisted | "AI-assisted discovery and patch development." |
| **Which specific tools/models** | Optional, and only at the disclosing party's request | "Tools: {from the controlled vocabulary}." |

What is **never** published: prompts, the specific model-plus-harness combination, scaffolding, or configuration. These are retained internally by the SIRT.

---

## Controlled capability vocabulary (how / when)

Use these high-level phrases to describe *how and when* AI assisted. Combine as needed (e.g., "discovery and patch development"). This keeps disclosures comparable across cases.

**Applicable to Finders and/or the SIRT:**
- **Discovery** — finding or surfacing the potential vulnerability
- **Reproduction / validation** — confirming the issue reproduces
- **Vulnerability or code analysis** — root-cause or code review assistance
- **Patch development** — drafting or refining the fix
- **Test generation** — producing unit tests or proofs
- **Severity assessment** — drafting a CVSS/EPSS rationale (always human-confirmed)
- **Advisory / documentation drafting** — writing or editing advisory or report text
- **Translation / localization** — rendering material into another language

**SIRT / Coordinator–specific (in addition to the above):**
- **Intake triage / deduplication** — classifying, routing, or de-duplicating incoming reports

If a disclosing party's usage does not fit a listed phase, the SIRT normalizes it to the nearest phrase or holds it for review rather than inventing new public language.

---

## The standard advisory statement

Every Akrites public advisory carries an **AI use** block with one line for the Finder and one for the Coordinator. Both lines are always present — including the negative case.

```
AI use
  - Finder: {{No AI tooling was used. / AI-assisted {phase(s) from the capability vocabulary}.
             Tools: {names — only if the Finder consented}.}}
  - Coordinator (Akrites SIRT): {{No AI tooling was used. / AI-assisted {phase(s)},
             under human review.}}
```

**Filled example (both parties used AI):**

```
AI use
  - Finder: AI-assisted discovery and patch development. Tools: Claude Opus, Semgrep.
  - Coordinator (Akrites SIRT): AI-assisted triage and advisory drafting, under human review.
```

**Filled example (neither used AI):**

```
AI use
  - Finder: No AI tooling was used.
  - Coordinator (Akrites SIRT): No AI tooling was used.
```

For an **anonymous** Finder, the Finder line is included only if it can be stated without identifying the reporter and the reporter does not object; when in doubt, omit the Finder line but always keep the Coordinator line.

---

## Confidentiality: public AI tools and embargo eligibility

Disclosing AI use and preserving confidentiality are two different things, and both matter.

- **Public, hosted LLM services are not confidential.** Prompts and pasted material may be retained, logged, used for training, or reviewed by the provider. Per [Embargo Handling Guidance §4.3](./Embargo%20Handling%20Guidance.md), **a report developed with public LLM tooling is treated as having no embargo available** and is handled on an accelerated / assume-exposed basis.
- **Confidential tooling preserves the embargo option** — self-hosted or enterprise models with contractual confidentiality and no-training guarantees, or the SIRT's own hardened analysis environment.
- **This is why AI use is captured at intake:** so the SIRT can classify embargo eligibility correctly. If a Finder is unsure whether their tooling qualifies as confidential, they should say so at intake.

The SIRT holds itself to the same standard: sensitive case material is only put through confidential, access-controlled AI tooling, never public services.

---

## Where AI use is captured and communicated

| Stage | Where | What |
|---|---|---|
| **Intake** | [Intake template](../templates/vulnerability-report-intake-template.md) "AI usage" section | Finder states whether/how AI was used, and whether tooling was public or confidential |
| **Acknowledgement** | [Notification Template 1](../templates/notification-templates.md) | SIRT confirms it noted the Finder's AI use and explains the public-tool/embargo caveat if relevant |
| **Triage / case record** | Case file | SIRT records both the Finder's and the SIRT's AI use; classifies embargo eligibility |
| **Embargoed notification** | [Notification Template 3](../templates/notification-templates.md) | Read-in providers see the AI-use block so they can weigh exposure |
| **Public disclosure** | [Notification Template 4](../templates/notification-templates.md) + advisory | The standard two-line AI-use block is published |

---

## Governance

- The **controlled vocabulary** (capability phrases and any publishable tool/model names) is maintained by the SIRT and updated without a policy revision; unlisted tool-name requests are normalized or held for review.
- The SIRT **reviews the AI-use lines before public disclosure** and may normalize vendor names to the controlled vocabulary (anti-gaming gate).
- This policy is maintained in the open; proposed changes are reviewed publicly. Only case-specific embargoed data is ever kept private.

---

## Open items (for Board / TOC)

- Ratify the controlled capability vocabulary and the cadence for updating the publishable tool/model list.
- Confirm whether the Coordinator AI-use line is published on **every** advisory or only when AI materially assisted (current draft: every advisory, including the negative case).
- Decide whether SIRT AI use is itemized per phase in public advisories or summarized (current draft: capability-level, summarized).

---

*This is a draft proposal for review by the SIRT and TOC.*
