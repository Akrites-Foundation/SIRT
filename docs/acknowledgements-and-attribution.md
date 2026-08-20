# Acknowledgements & Attribution Guidance

**Owner:** Akrites SIRT
**Status:** Draft for TOC / Board review
**Applies to:** Public Disclosure (PD) advisories coordinated by the Akrites SIRT
**Related:** OSS-SIRT F2F — *PD Requirements → Acknowledgements & Attribution*; *Tiered Disclosure → Co-finder attribution*; [AI and LLM Use Disclosure Policy](./ai-use-disclosure.md)

> Spelling note: the standard is **Akrites** (Akrites Foundation, Akrites SIRT). "OSS-SIRT" is a synonym.

---

## Purpose

This document defines how finders, their organizations, tooling, and coordinators are
credited in Akrites-coordinated public advisories. It exists so that credit is:

- **Given where wanted** and **honored where declined** — attribution is opt-in and finder-controlled.
- **Consistent** across advisories, so downstream consumers and maintainers know what each line means.
- **Resistant to gaming** — a controlled vocabulary and a review gate keep AI-vendor marketing out of the credit line.

The finder's attribution preference is captured at intake and confirmed before PD. Once set, the
default is TLP:RED until PD; it becomes public only in the final advisory.

> **Relationship to the AI-use policy.** *Whether and how* AI tooling was used —
> by the finder **and** by the SIRT — is governed by the
> [AI and LLM Use Disclosure Policy](./ai-use-disclosure.md), which is the
> authoritative source and defines the standard two-line advisory block. This
> document governs *credit and attribution*, including the optional publishing of
> specific tool/model names, and reuses the same controlled vocabulary.

---

## Core principles

1. **Attribution is opt-in.** No finder or participant is named without explicit consent.
2. **Individuals vs. groups.** Where an individual declines but the work is attributable to a
   working group (WG), the WG may be credited without naming its members.
3. **AI assistance is disclosed by capability; specifics are optional and finder-driven.**
   The Akrites default published line states that AI assisted discovery and/or patching.
   Specific model/tool names are published **only when the finder requests it**, drawn from the
   controlled vocabulary in [Appendix A](#appendix-a--controlled-vocabulary). Model-plus-harness
   internals remain internal. AI use is disclosed for **both** the finder and the Akrites SIRT
   (Coordinator) — see [Coordinator AI-use line](#coordinator-sirt-ai-use-line).
4. **Coordinator credit.** Where no finder attribution is given, the advisory credits the
   **Akrites SIRT** as coordinator. Public advisories otherwise attribute information to the
   Akrites SIRT and Akrites Foundation.
5. **Co-finders are honored** up to the attribution cutoff (see [Co-finder handling](#co-finder-handling)).

---

## Scenario 1 — Finder wants to be acknowledged (name + organization + tooling)

Use when the finder consents to being named and, optionally, wants the tools/LLMs used in
finding and/or patching recorded.

**Template**

```
Acknowledgements
----------------
This issue was reported by {Finder Name}{, {Organization}} and coordinated through the
Akrites SIRT.

{Finder Name} identified the vulnerability{ and contributed the patch}.

AI use
  - Finder: AI-assisted {discovery|patch development|discovery and patch development}.
    {Tools used: {tool/model names from the controlled vocabulary}.}
  - Coordinator (Akrites SIRT): {No AI tooling was used. / AI-assisted {phase(s)}, under human review.}
```

**Field notes**

- `Organization` is included only if the finder consents to naming their employer/affiliation.
- The `Finder` AI line is required whenever AI materially assisted; state the phase(s).
- `Tools used` is included **only at the finder's request**. Names must come from
  [Appendix A](#appendix-a--controlled-vocabulary). Harness/configuration details are never published.
- The `Coordinator` AI line is always included (including the negative case) per the AI-use policy.

**Filled example**

```
Acknowledgements
----------------
This issue was reported by Jordan Lee, ExampleSec, and coordinated through the Akrites SIRT.

Jordan Lee identified the vulnerability and contributed the patch.

AI use
  - Finder: AI-assisted discovery and patch development. Tools used: Claude Opus, Semgrep.
  - Coordinator (Akrites SIRT): AI-assisted triage and advisory drafting, under human review.
```

---

## Scenario 2 — Finder represents a Clearinghouse (Clearinghouse credited as the finder)

Use when the reporting entity is a clearinghouse/coordinator (e.g., a national CERT such as
CISA or ENISA, or a trusted vendor program) that wants to be named as the finder rather than
an individual analyst.

**Template**

```
Acknowledgements
----------------
This issue was reported by {Clearinghouse Name} and coordinated through the Akrites SIRT.

{Clearinghouse Name} reported this vulnerability on behalf of its constituency; individual
reporters are not named at the reporter's request.

AI use
  - Finder: AI-assisted {discovery|patch development|discovery and patch development}.
    {Tools used: {tool/model names from the controlled vocabulary}.}
  - Coordinator (Akrites SIRT): {No AI tooling was used. / AI-assisted {phase(s)}, under human review.}
```

**Field notes**

- The clearinghouse is the named finder; individual analysts are **not** named.
- Include the finder AI line/tooling on the same rules as Scenario 1, if the clearinghouse requests it.
- If the clearinghouse also wants Akrites credited only as coordinator (no clearinghouse name),
  fall through to Scenario 3.

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

---

## Scenario 3 — Finder wants no attribution (Akrites SIRT credited as coordinator)

Use when the finder declines any credit. The advisory names only the Akrites SIRT as the
coordinating body.

**Template**

```
Acknowledgements
----------------
This vulnerability was coordinated to disclosure by the Akrites SIRT. The reporter has
requested to remain anonymous.

AI use
  - {Finder: AI-assisted {discovery|patch development|discovery and patch development}.}
  - Coordinator (Akrites SIRT): {No AI tooling was used. / AI-assisted {phase(s)}, under human review.}
```

**Field notes**

- Do **not** name the finder, their organization, or a WG unless the finder later consents.
- The **Finder** AI line is included only if it can be stated without identifying the anonymous
  reporter and the finder does not object; when in doubt, omit it.
- The **Coordinator** AI line is always included — it does not implicate the reporter.
- This is also the fallback when consent cannot be confirmed before PD.

**Filled example**

```
Acknowledgements
----------------
This vulnerability was coordinated to disclosure by the Akrites SIRT. The reporter has
requested to remain anonymous.

AI use
  - Coordinator (Akrites SIRT): AI-assisted advisory drafting, under human review.
```

---

## Co-finder handling

When more than one party reports the same issue:

- Each consenting co-finder is credited using the applicable scenario block above.
- Co-finders are honored **up to the attribution cutoff** — the point in the timeline after which
  additional independent reports are recorded but not added to the published advisory. The cutoff
  (e.g., patch-ready, or PD date) is set by policy per the F2F "co-finder attribution cutoff" action.
- A declining co-finder is omitted entirely; their preference does not affect other finders' credit.
- Where co-finders are members of a WG, the WG may be credited in place of individuals per
  Principle 2.

---

## AI / tooling disclosure convention

- **Default published line:** capability only — e.g., *"AI-assisted discovery and patch development."*
- **Two subjects, always:** the advisory carries an AI-use line for the **finder** and one for the
  **Coordinator (Akrites SIRT)**, including the negative case ("No AI tooling was used"). See the
  [AI and LLM Use Disclosure Policy](./ai-use-disclosure.md) for the authoritative wording.
- **Named tools/models:** published **only when the disclosing party requests it**, and only from the
  controlled vocabulary in [Appendix A](#appendix-a--controlled-vocabulary).
- **Never published:** the specific model-plus-harness combination, prompts, scaffolding, or
  configuration. These are retained internally by the SIRT.
- **Anti-gaming:** because publishing model names attracts vendor marketing, the SIRT reviews the
  tooling line before PD and may normalize vendor names to the controlled vocabulary.

### Coordinator (SIRT) AI-use line

The SIRT discloses its own AI use on the same capability basis as finders:

- The `Coordinator (Akrites SIRT)` line is **present on every advisory**, using the negative form
  where no AI tooling was used.
- It describes SIRT phases such as intake triage/deduplication, analysis, patch development, test
  generation, or advisory drafting — always with the note that the work was under human review.
- SIRT AI use is confined to confidential, access-controlled tooling; the SIRT does not put case
  material through public AI services.

---

## Attribution intake checklist

Captured at intake, confirmed before PD (held TLP:RED until PD):

- [ ] Attribution preference: **named** / **clearinghouse** / **anonymous**
- [ ] If named: exact display name, and whether organization may be shown
- [ ] Finder role: discovery / patch / both
- [ ] AI assistance used by finder? which phase(s)?
- [ ] Finder tooling public or private/confidential? (affects embargo eligibility)
- [ ] Publish specific tool/model names? if yes, list (validated against Appendix A)
- [ ] Co-finder(s) present? each one's preference
- [ ] Consent confirmed by finder before PD (record date)
- [ ] SIRT AI use recorded for this case (phase[s], or "none")

---

## Appendix A — Controlled vocabulary

Only entries on the Akrites-maintained list may appear in a published `Tools used` line. This
list is governed by the SIRT and updated as needed; unlisted requests are normalized or held for
review.

| Category | Example published names |
| --- | --- |
| LLMs / assistants | *(maintained list — e.g., model family + tier)* |
| SAST / analysis | *(maintained list)* |
| Fuzzing | *(maintained list)* |
| Other tooling | *(maintained list)* |

> The concrete entries are maintained by the SIRT rather than hard-coded here so the vocabulary can
> evolve without a policy revision. Harness and configuration details are out of scope for
> publication in all cases.

---

## Open items (from F2F, for Board/TOC)

- Set the concrete **co-finder attribution cutoff** trigger/point in time.
- Ratify the **controlled vocabulary** and its governance/update cadence.
- Confirm whether **WG-level credit** is offered by default when individuals decline.
- Decide whether **date of first report** is included alongside acknowledgements in the advisory.
- Confirm whether the **Coordinator AI-use line** appears on every advisory or only when AI
  materially assisted (current draft: every advisory — aligns with the AI-use policy).
