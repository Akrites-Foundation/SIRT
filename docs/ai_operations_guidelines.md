# Akrites SIRT — AI Operations Guidelines

**Owner:** Akrites SIRT
**Status:** Draft for Akrites SIRT review
**Audience:** SIRT staff, case coordinators, and Working Group members who build, run, or rely on AI-assisted tooling
**Companion docs:** [Attribution and AI-Use Disclosure Policy](ai-use-disclosure.md), [CVD Policy](Akrites_CVD_Policy.md) (§8 confidentiality, §13 AI disclosure), [Intake Runbook](intake-runbook.md), [Maintainer of Last Resort Policy](Maintainer_of_Last_Resort_Policy.md) (Part II §5.4), [Communications Playbook](sirt-communications-playbook.md) (Play 18), [Metrics](Akrites_SIRT_Metrics.md)

---

## Purpose

The Akrites SIRT uses large language models (LLMs) and other automated tools for intake, deduplication, prioritization, analysis, and patch drafting. These guidelines set the **operational controls** for that use: which tasks need what level of human oversight, how AI-drafted patches are verified, how case data is protected, and what happens when a model gets something wrong.

They are operating guidance under existing policy, not a new policy. The rules they implement are already set elsewhere:

- **AI use is disclosed, both ways,** and AI-assisted work is always owned by a named human — CVD Policy §13 and the [Attribution and AI-Use Disclosure Policy](ai-use-disclosure.md).
- **Case material only goes through confidential tooling, never public AI services** — the AI-use policy's Confidentiality section and the Intake Runbook's AI Tooling Guardrail.

Where these guidelines and a policy disagree, the policy governs.

---

## 1. AI classes and oversight

Every AI-assisted task falls into one of three classes, set by what goes wrong if the output is wrong.

| AI class | Tasks | Risk | Human oversight |
| --- | --- | --- | --- |
| **Class A — Triage** | Deduplication, CVSS pre-scoring, component matching, formatting | Low | Sampling audit (§3.2); a human confirms any rejection or closure |
| **Class B — Analysis** | Root-cause analysis, crash-dump summaries, threat-intelligence correlation | Medium | A named human reviews before the output is shared beyond the SIRT and its read-in Tier 1 participants |
| **Class C — Generation** | Patch drafting, regression-test generation, advisory and VEX drafting | High | Full verification and named human sign-off before anything leaves the SIRT (§2) |

The class follows the task, not the tool. A tool that does both triage and drafting is held to Class C for its drafting.

---

## 2. Verifying AI-drafted patches (Class C)

AI-drafted code can look right and still be wrong: a fix that does not fix, a new logic flaw, a performance regression, or a fresh vulnerability. No AI-drafted patch or remediation code is offered to an upstream maintainer, or published in an advisory, until it has passed:

1. **Isolated analysis.** Static analysis (SAST) and dynamic testing in an isolated sandbox.
2. **Project tests and a scoped diff.** The project's own test suite passes, and a syntax-tree (AST) diff confirms the patch touches only what the fix needs — no unrelated code or hidden behavior.
3. **Named human sign-off.** At least **one named reviewer** — a Tier 1 analyst or patch author designated by the SIRT case coordinator — reviews and signs off before the patch is submitted upstream. A MoLR last-resort release needs **two named reviewers**, per MoLR Policy Part II §5.4.

The upstream maintainer reviews the patch when it is submitted to them and keeps authority over whether, and how, it is merged.

---

## 3. Triage controls (Class A)

AI-assisted triage reduces noise. It does not make final decisions about reports.

### 3.1 Limits on automatic actions

- **Confidence threshold *(proposed)*.** Automatic deduplication or tagging happens only when model confidence is at least **90%** on similarity to a known report or CVE. Below that, a human decides.
- **No autonomous rejection.** AI never closes, rejects, or marks a report invalid or out of scope. A human confirms every such outcome.
- **Equal treatment of reports.** Every report goes through the same verification, whether or not the Finder disclosed AI use. Disclosing AI use does not affect whether a report is accepted (CVD Policy §4.3), and it never triggers extra scrutiny.

### 3.2 Sampling audit *(proposed)*

Each week, the SIRT case coordinator on duty reviews a random sample of at least **15%** of the reports AI classified as duplicate or low priority, records the error rate, and raises any pattern with the SIRT Director. Results feed the metrics program ([Metrics](Akrites_SIRT_Metrics.md) — automation ratio).

---

## 4. Protecting case data

Pre-disclosure case material — anything at TLP:RED, TLP:AMBER+STRICT, or TLP:AMBER — is processed only through **confidential AI tooling**, as the [Attribution and AI-Use Disclosure Policy](ai-use-disclosure.md) defines it: self-hosted models, enterprise services with contractual no-training and confidentiality terms, or the SIRT's own analysis environment. **Public AI services are never used for case material.**

For any tooling run by a third party:

- **No retention.** The contract confirms that prompts and outputs are neither retained nor used to train models.
- **Scrub first.** Before a report, crash dump, or stack trace is sent to the model, automated scrubbing removes secrets (API keys, tokens), internal addresses, and personal data that the task does not need.

---

## 5. Test data and exploit payloads

- **Synthetic data is fine.** AI may generate abstract test cases, fuzzing inputs, and mock unit tests to check a fix.
- **Real payloads stay contained.** Working exploit payloads for unpatched vulnerabilities stay encrypted in the case's secure storage and are never sent to third-party or public AI services.
- **Label synthetic data.** Datasets generated by AI are tagged `[SYNTHETIC-DATASET]` in Akrites repositories, so they are never mistaken for real-world data or fed back into training or benchmarks.

---

## 6. Provenance and auditability

Every AI-assisted output stored by the SIRT keeps internal provenance:

- model name, version, and checkpoint or build identifier;
- generation settings (for example, temperature);
- the prompt context and system instructions used;
- the named human who reviewed it.

Provenance records contain case material, so they **carry the case's TLP label and retention rules.** They are internal only — the public advisory states AI use at capability level, per the AI-use policy, and never publishes prompts, model-plus-harness details, or configuration.

---

## 7. When a model gets it wrong

If an AI-assisted patch or advisory turns out to contain a non-existent vulnerability, wrong mitigation advice, or a new flaw:

1. **Correct it now.** Withdraw or update the affected pull request, and publish a corrected advisory with a revision-history entry stating what changed.
2. **Review it.** Hold a blameless postmortem — an AI or automation failure is a required trigger under Comms Play 18 — covering prompt changes, model failure modes, and how review missed it.
3. **Step down the automation.** If the cause is model drift, prompt injection, or a failure the controls did not catch, the SIRT Director moves the affected pipeline to manual operation until the cause is fixed and the controls are re-verified.

---

## 8. Open items

- Confirm the proposed figures: the **90%** automatic-deduplication threshold and the weekly **15%** sampling audit.
- Define the **automation ratio** metric (currently "to be defined" in the Metrics document) and how audit error rates are reported.
- Name who owns maintenance of the scrubbing rules and the provenance store.
