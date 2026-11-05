# Attribution and AI-Use Disclosure Policy

**Owner:** Akrites SIRT
**Status:** Draft for Board review
**Applies to:** All Akrites SIRT–coordinated cases and the advisories they produce — reports from Finders and work performed by the SIRT and its Working Groups (WGs)
**Related:** [CVD Policy](./Akrites_CVD_Policy.md) · [Embargo Handling Guidance](./Embargo%20Handling%20Guidance.md) (§4.3) · [Notification Templates](../templates/notification-templates.md) · [Intake Template](../templates/vulnerability-report-intake-template.md)

> This document combines the former *AI and LLM Use Disclosure Policy* and *Acknowledgements & Attribution Guidance* into one source.

---

## Purpose

Artificial-intelligence tooling — most notably large language models (LLMs) — is now used routinely across the vulnerability lifecycle, by both the researchers who report to us and by the SIRT itself. This document defines a single, consistent rule for **telling every stakeholder when AI tooling was used, and giving them a high-level statement of how and when it was used.**

The goal is straightforward: a Finder, Maintainer, Consumer, or downstream provider reading an Akrites case or advisory should never have to guess whether AI contributed to the discovery, analysis, fix, or write-up. We state it plainly — whether AI was used or not — for both the **Finder** and the **Coordinator (Akrites SIRT)**.

It also defines how Finders, their organizations, co-finders, Working Groups, and the Coordinator are **credited** in advisories: by default, honoring any request not to be named, and consistently across advisories.

This document is the authoritative source for AI-use disclosure. The CVD Policy, CVD Playbook, glossary, intake template, and notification templates all point here.

---

## Scope

This policy covers AI/LLM tooling used to **discover, reproduce, analyze, triage, prioritize, patch, test, score, translate, or document** a vulnerability handled by the Akrites SIRT. It applies to two disclosing parties:

1. **Finders** — AI tooling a reporter used before or during their report.
2. **The Akrites SIRT and its Working Groups** — AI tooling the SIRT uses while coordinating, analyzing, patching, or drafting materials for a case.

It applies regardless of who owns or hosts the tool (public service, enterprise/self-hosted model, or the SIRT's own analysis environment). It does **not** require publishing prompts, model-plus-harness internals, scaffolding, or configuration — those remain internal (see [Confidentiality](#confidentiality-public-ai-tools-and-embargo-eligibility)).

---

## Core principles

1. **Disclose by default, both ways.** Every coordinated case records, and every public advisory states, AI use for **both** the Finder and the SIRT — including an explicit "no AI tooling was used" when that is the case. Silence is not a valid disclosure.

2. **Capability-level, not marketing.** The default statement describes *what phase* AI assisted (e.g., "AI-assisted discovery and patch development"), drawn from the [controlled capability vocabulary](#controlled-capability-vocabulary-how--when). Specific model or tool names are published **only when the disclosing party requests it**, and only from the controlled vocabulary in [Publishable tool / model names](#publishable-tool--model-names). This keeps vendor branding out of the record.

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

### Publishable tool / model names

Only entries on the Akrites-maintained list may appear in a published `Tools:` line; unlisted requests are normalized or held for review.

| Category | Example published names |
| --- | --- |
| LLMs / assistants | *(maintained list — e.g., model family + tier)* |
| SAST / analysis | *(maintained list)* |
| Fuzzing | *(maintained list)* |
| Other tooling | *(maintained list)* |

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
  - Finder: AI-assisted discovery and patch development. Tools: {LLM assistant}, {SAST tool}.
  - Coordinator (Akrites SIRT): AI-assisted triage and advisory drafting, under human review.
```
AI-assisted output is always reviewed and approved by a named human before it is used in a case or published (see Core principle 3).

**Filled example (neither used AI):**

```
AI use
  - Finder: No AI tooling was used.
  - Coordinator (Akrites SIRT): No AI tooling was used.
```

For an **anonymous** Finder, the Finder line is never omitted. If stating the Finder's AI use could help identify them, use: "Finder (anonymous): AI use not disclosed." Otherwise use the normal wording, prefixed "Finder (anonymous):".

Where technical capability exists, model, version, and framework/harness metadata may be captured at the report and API submission layer for internal benchmarking — only with the submitter's knowledge (stated at intake) and never published. This does not replace the Finder's own disclosure.

---

## Credit and attribution

### Principles

1. **Credit by default, consent for detail.** Finders are credited by default under the name or handle they reported with; anonymity is honored on request. Organizations, co-finders' and participants' names appear only with explicit consent.
2. **Individuals vs. groups.** Where an individual declines but the work is attributable to a working group (WG), the WG may be credited without naming its members.
3. **Coordinator credit.** Where no finder attribution is given, the advisory credits the **Akrites SIRT** as coordinator. Public advisories otherwise attribute information to the Akrites SIRT and Akrites Foundation.
4. **Co-finders are honored** up to the attribution cutoff (see [Co-finder handling](#co-finder-handling)).
5. **Preferences are confidential until PD.** The finder's attribution preference is captured at intake and confirmed before PD; it is held TLP:RED and becomes public only in the final advisory.

### The three attribution choices

Per CVD Policy §11, a Finder chooses one of:

- **Named** — individual and, if they wish, organization (Scenario 1).
- **Clearinghouse** — the reporting organization only (Scenario 2).
- **Anonymous** — no Finder credit; the Akrites SIRT is credited as coordinator (Scenario 3).

If the Finder **never stated a preference** and it cannot be confirmed before PD, the SIRT uses the name or handle as submitted and never names an organization without consent (CVD Policy §11). **An explicit request for anonymity always stands.**

### Co-finder handling

When more than one party reports the same issue:

- Each consenting co-finder is credited using the applicable scenario block below.
- Co-finders are honored **up to the attribution cutoff** — the point in the timeline after which additional independent reports are recorded but not added to the published advisory. The cutoff (e.g., patch-ready, or PD date) is set by policy (open item below).
- A declining co-finder is omitted entirely; their preference does not affect other finders' credit.
- Where co-finders are members of a WG, the WG may be credited in place of individuals per Principle 2.

### Acknowledgement scenarios

Every advisory's **Acknowledgements** section uses one of the three scenarios below, followed by the standard AI use block above.

#### Scenario 1 — Named finder (name, optional organization, optional tools)

Use when the finder consents to being named and, optionally, wants the tools used in finding and/or patching recorded.

```
Acknowledgements
----------------
This issue was reported by {Finder Name}{, {Organization}} and coordinated through the
Akrites SIRT.

{Finder Name} identified the vulnerability{ and contributed the patch}.

AI use
  - Finder: AI-assisted {discovery|patch development|discovery and patch development}.
    {Tools: {tool/model names from the controlled vocabulary}.}
  - Coordinator (Akrites SIRT): {No AI tooling was used. / AI-assisted {phase(s)}, under human review.}
```

**Field notes**

- `Organization` is included only if the finder consents to naming their employer/affiliation.
- The `Finder` AI line is required whenever AI materially assisted; state the phase(s).
- `Tools:` is included **only at the finder's request**, from the [controlled vocabulary](#controlled-capability-vocabulary-how--when). Harness/configuration details are never published.

**Filled example**

```
Acknowledgements
----------------
This issue was reported by Jordan Lee, ExampleSec, and coordinated through the Akrites SIRT.

Jordan Lee identified the vulnerability and contributed the patch.

AI use
  - Finder: AI-assisted discovery and patch development. Tools: {LLM assistant}, {SAST tool}.
  - Coordinator (Akrites SIRT): AI-assisted triage and advisory drafting, under human review.
```

#### Scenario 2 — Clearinghouse credited as the finder

Use when the reporting entity is a clearinghouse/coordinator (e.g., a national CERT such as CISA or ENISA, or a trusted vendor program) that wants to be named as the finder rather than an individual analyst.

```
Acknowledgements
----------------
This issue was reported by {Clearinghouse Name} and coordinated through the Akrites SIRT.

{Clearinghouse Name} reported this vulnerability on behalf of its constituency; individual
reporters are not named at the reporter's request.

AI use
  - Finder: AI-assisted {discovery|patch development|discovery and patch development}.
    {Tools: {tool/model names from the controlled vocabulary}.}
  - Coordinator (Akrites SIRT): {No AI tooling was used. / AI-assisted {phase(s)}, under human review.}
```

**Field notes**

- The clearinghouse is the named finder; individual analysts are **not** named.
- Include the finder tooling on the same rules as Scenario 1, if the clearinghouse requests it.
- If the clearinghouse also wants Akrites credited only as coordinator (no clearinghouse name), use Scenario 3.

**Filled example**

```
Acknowledgements
----------------
This issue was reported by the Example National CERT and coordinated through the Akrites SIRT.

Example National CERT reported this vulnerability on behalf of its constituency; individual
reporters are not named at the reporter's request.

AI use
  - Finder: AI-assisted discovery.
  - Coordinator (Akrites SIRT): No AI tooling was used.
```

#### Scenario 3 — Anonymous finder (Akrites SIRT credited as coordinator)

Use when the finder declines any credit. The advisory names only the Akrites SIRT as the coordinating body.

```
Acknowledgements
----------------
This vulnerability was coordinated to disclosure by the Akrites SIRT. The reporter has
requested to remain anonymous.

AI use
  - Finder (anonymous): {AI-assisted {phase(s)}. | No AI tooling was used. | AI use not disclosed.}
  - Coordinator (Akrites SIRT): {No AI tooling was used. / AI-assisted {phase(s)}, under human review.}
```

**Field notes**

- Do **not** name the finder, their organization, or a WG unless the finder later consents. An explicit request for anonymity always stands — the "name as submitted" fallback never applies here.
- The **Finder** AI line is always present. If stating the Finder's AI use could identify the reporter, write "Finder (anonymous): AI use not disclosed."
- The **Coordinator** AI line is always included — it does not implicate the reporter.

**Filled example**

```
Acknowledgements
----------------
This vulnerability was coordinated to disclosure by the Akrites SIRT. The reporter has
requested to remain anonymous.

AI use
  - Finder (anonymous): AI use not disclosed.
  - Coordinator (Akrites SIRT): AI-assisted advisory drafting, under human review.
```

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
| **Intake** | [Intake template](../templates/vulnerability-report-intake-template.md) "AI / LLM tooling used" and "Reporter" sections | Finder states whether/how AI was used, and whether tooling was public or confidential |
| **Acknowledgement** | [Notification Template 1](../templates/notification-templates.md) | SIRT confirms it noted the Finder's AI use and explains the public-tool/embargo caveat if relevant |
| **Triage / case record** | Case file | SIRT records both the Finder's and the SIRT's AI use; classifies embargo eligibility |
| **Embargoed notification** | [Notification Template 3](../templates/notification-templates.md) | Read-in providers see the AI-use block so they can weigh exposure |
| **Public disclosure** | [Notification Template 4](../templates/notification-templates.md) + advisory | The standard two-line AI-use block is published |

### Attribution intake checklist

Captured at intake, confirmed before PD (held TLP:RED until PD):

- [ ] Attribution preference: **named** / **clearinghouse** / **anonymous**
- [ ] If named: exact display name, and whether organization may be shown
- [ ] Finder role: discovery / patch / both
- [ ] AI assistance used by finder? which phase(s)?
- [ ] Finder tooling public or private/confidential? (affects embargo eligibility)
- [ ] Publish specific tool/model names? if yes, list (validated against the controlled vocabulary)
- [ ] Co-finder(s) present? each one's preference
- [ ] Consent confirmed by finder before PD (record date)
- [ ] SIRT AI use recorded for this case (phase[s], or "none")

---

## Governance

- The **controlled vocabulary** (capability phrases and any publishable tool/model names) is maintained by the SIRT and updated without a policy revision; unlisted tool-name requests are normalized or held for review.
- The SIRT **reviews the acknowledgement and AI-use lines before public disclosure** and may normalize vendor names to the controlled vocabulary (anti-gaming gate).
- This policy is maintained in the open; proposed changes are reviewed publicly. Only case-specific embargoed data is ever kept private.

---

## Open items (for Governing Board)

- Ratify the controlled capability vocabulary and the cadence for updating the publishable tool/model list.
- Confirm whether the Coordinator AI-use line is published on **every** advisory or only when AI materially assisted (current draft: every advisory, including the negative case).
- Decide whether SIRT AI use is itemized per phase in public advisories or summarized (current draft: capability-level, summarized).
- Set the concrete **co-finder attribution cutoff** trigger/point in time.
- Confirm whether **WG-level credit** is offered by default when individuals decline.
- Decide whether **date of first report** is included alongside acknowledgements in the advisory.

---

*This is a draft proposal for review by the SIRT and the Governing Board.*
