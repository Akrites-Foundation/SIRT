# Akrites SIRT — Severity Scoring Guidelines

**Owner:** Akrites SIRT
**Status:** Draft for Akrites SIRT review
**Audience:** SIRT staff, case coordinators, and Working Group analysts who assess and communicate vulnerability severity
**Companion docs:** [CVD Policy](Akrites_CVD_Policy.md) (§8 severity targets, §9 actively exploited vulnerabilities, §10 severity and identifiers), [Intake Runbook](intake-runbook.md), [Critical Situation Playbook](critical_situation_playbook.md), [Communications Playbook](sirt-communications-playbook.md), [Notification Templates](../templates/notification-templates.md), [Metrics](Akrites_SIRT_Metrics.md)
**Credits:** Based on an initial draft by Robb Gatica ([PR #61](https://github.com/Akrites-Foundation/SIRT/pull/61)), with the layered model proposed by Jenny Ferries and review by CRob in [issue #32](https://github.com/Akrites-Foundation/SIRT/issues/32).

---

## Purpose

These guidelines set how the Akrites SIRT assesses, communicates, and publishes the severity of the vulnerabilities it coordinates. They are operating guidance under CVD Policy §10, which sets CVSS v4.0 as the severity standard; where the two differ, the policy governs.

Severity is assessed in four layers, each answering a different question:

| Layer | Answers | Published? |
| --- | --- | --- |
| **1. CVSS v4.0** | How does the vulnerability behave technically? | Yes |
| **2. Severity label** | How serious is it, in plain language? | Yes |
| **3. Exploit state** | What real-world evidence of exploitation exists? | Yes (at PD) |
| **4. SSVC priority** | What should the SIRT do next, and how fast? | No — internal only |

In short: **severity describes the vulnerability, exploit state describes the evidence, and priority describes what the SIRT should do next.**

---

## 1. Layer 1 — CVSS v4.0 (technical description)

- Every case that reaches Public Disclosure (PD) carries a **CVSS v4.0 Base (CVSS-B)** vector and numeric score. CVSS-B is the required published score.
- The **full vector string is always published** with the number. The vector is often more useful than the score, and lets downstream consumers adjust for their own environment.
- **CVSS-BT** (Base + Threat) is **optional**. When exploit maturity is known at PD, it may be published as a supplementary score marked "as of {PD date}", so it is not read as static.
- The SIRT does **not** produce CVSS v3.1 scores. Downstream providers may add other scores for their own constituents.

### Scoring through the lifecycle

| Lifecycle phase | Scoring activity |
| --- | --- |
| **Discover** (intake) | Record the reporter's severity estimate as submitted. Do not discard or overwrite it. |
| **Validate** | An analyst produces a **provisional** CVSS v4.0 vector and severity label from the confirmed reproduction and root-cause analysis. This label sets the case's PD target (CVD Policy §8). |
| **Coordination** | Review the provisional assessment with the maintainer. If another party scores it differently, keep both. |
| **Document** | Finalize the vector and label. Where assessments still diverge materially, prepare a deviation notice. |
| **Disclose** | Publish the final vector, score, label, exploit state, and any deviation notice. |

### Deviation notices

When the SIRT's assessment differs materially from another party's published score — the upstream project, a CNA, or a downstream vendor — the SIRT publishes a short **deviation notice** with the advisory stating which assessments differ, the metrics where assumptions diverge (for example, Attack Complexity or User Interaction), and why the SIRT reached its view. The aim is transparency, not dispute: reasonable analysts reach different conclusions when their assumptions differ.

---

## 2. Layer 2 — Severity label (plain-language communication)

A four-level label gives maintainers, consumers, and stakeholders without a security background a quick, plain-language read. The labels are the ones the CVD Policy uses, and each carries the CVD Policy's target time to PD.

| Label | CVSS v4.0 guidance range | Meaning | Target time to PD (CVD Policy §8) |
| --- | --- | --- | --- |
| **Critical** | 9.0 – 10.0 | Straightforward exploitation leading to complete compromise (e.g., unauthenticated remote code execution, full authentication bypass). | ≤ 24 business days |
| **High** | 7.0 – 8.9 | Significant impact, but exploitation needs meaningful preconditions (e.g., authenticated access, non-default configuration, user interaction). | ≤ 21 business days |
| **Medium** | 4.0 – 6.9 | Real but limited impact, or significantly constrained exploitability. | ≤ 17 business days |
| **Low** | 0.1 – 3.9 | Minimal impact, or conditions unlikely to occur in practice. | ≤ 17 business days |

Every label carries a disclosure target: the label sets the pace, not whether the issue is handled. Actively exploited issues follow the accelerated track in CVD Policy §9 whatever their label.

### When the label departs from the CVSS range

The ranges are guidance, not mechanical cut-offs. The label reflects the vulnerability's technical impact under stated assumptions, so an analyst may set it outside the range only when the **technical** assessment warrants it — for example:

- **Preconditions in practice.** A CVSS 9.1 that needs a rarely enabled debug mode may warrant **Medium**.
- **Compound impact.** A CVSS 6.5 that chains trivially with a common misconfiguration to full compromise may warrant **High**.

Ecosystem prevalence, deployment breadth, and active exploitation change **response priority** (Layer 4), not the label. Whenever the label departs from the range, the analyst records the rationale in the case record.

---

## 3. Layer 3 — Exploit state (evidence)

Exploit state is tracked as its own field, separate from the CVSS score and the label, and changes as evidence emerges.

| Value | Evidence |
| --- | --- |
| **Active** | Credible evidence of in-the-wild exploitation — threat-intelligence reporting, direct observation, or a CISA KEV listing. |
| **Demonstrated** | The SIRT, the maintainer, or another trusted party has independently reproduced the security outcome in a controlled environment. |
| **PoC** | An exploit artifact exists (code, or a write-up with enough detail) but the case team has not independently reproduced it. |
| **Theoretical** | Analysis confirms the flaw is exploitable, but no working exploit is known to the case team. |
| **Unknown** | Not yet assessed, or not enough information to decide. |

### What each state means for the case

- **Active** — the CVD Policy §9 accelerated track applies (actionable guidance within 7 days), and it is a trigger for the SIRT Director to consider a Crit-Sit ([Critical Situation Playbook](critical_situation_playbook.md)).
- **Demonstrated** with a low-barrier exploit — a strong signal to accelerate; raise the SSVC priority.
- **PoC** — monitor for escalation.
- **Theoretical** or **Unknown** — absence of evidence is not evidence of low risk. **"Unknown" never means "safe."**

### Review cadence

Exploit state is re-checked on two kinds of trigger.

**Scheduled checkpoints**
- At every case status update, and **at least daily during a Crit-Sit**.
- Within **24 hours before PD**.
- **Weekly for 30 days after PD** for Critical and High cases.
- A **monthly automated sweep** of published advisories against vulnerability databases and threat feeds.

**Event triggers (immediate)**
- A CISA KEV addition, a public exploit-framework module (for example, Metasploit or Nuclei), or a credible threat-intelligence report.

When exploit state changes after PD, update the advisory's exploit-state field with a new timestamp and a revision-history entry, and re-evaluate SSVC priority internally.

---

## 4. Layer 4 — SSVC priority (internal only)

The SIRT uses CISA's **Stakeholder-Specific Vulnerability Categorization (SSVC)** decision tree to decide response priority — which cases to staff first, and how urgently. SSVC results are **never published**.

| Decision point | Question |
| --- | --- |
| **Exploitation** | Is there evidence of exploitation? (None / PoC / Active) |
| **Technical impact** | If exploited, how much control does the attacker gain? (Partial / Total) |
| **Automatable** | Can an attacker reliably automate exploitation at scale? (No / Yes) |
| **Mission prevalence** | How widely is the component relied on, including in critical infrastructure? (Minimal / Support / Essential) |

| Outcome | SIRT response |
| --- | --- |
| **Act** | Staff immediately; accelerate coordination; engage the maintainer and downstream parties urgently. The Director considers a Crit-Sit. |
| **Attend** | Prioritize; assign an analyst now and coordinate ahead of routine cases. |
| **Track\*** | Monitor closely; coordinate within the current cycle. |
| **Track** | Coordinate on the normal timeline. |

SSVC and the label answer different questions. A **Medium** flaw in a library used by every container orchestrator may be SSVC **Act** because of its prevalence and automatable exploitation; its label stays Medium. A **Critical** flaw in a niche component with no known exploitation may be **Track\***. When exploit state changes, re-evaluate SSVC; the label normally changes only if the technical understanding changes.

### EPSS

FIRST's Exploit Prediction Scoring System (EPSS) estimates the chance that a **published** CVE will be exploited. Embargoed cases — most of the SIRT's work — have no EPSS value, so EPSS is not used to assess them. Where a CVE is already public (for example, a Crit-Sit on a published CVE, or a MoLR case), EPSS may inform SSVC priority alongside other evidence. A missing EPSS value never means low risk, and the SIRT does not publish EPSS scores.

---

## 5. What is published at PD

Every advisory is human-readable and, where possible, accompanied by machine-readable **OSV** and **CSAF 2.0 / VEX** records (CVD Policy §10). It includes:

- CVSS v4.0 Base vector string and numeric score (required)
- CVSS-BT "as of {PD date}" supplementary score (optional)
- Severity label: Critical / High / Medium / Low
- Exploit state at disclosure, with a timestamp
- CWE identifier for the root cause
- CVE ID
- A deviation notice, where applicable

SSVC results are internal and are never published.

---

## 6. Guidance for analysts

### Communicating severity to maintainers

Many upstream maintainers are security-capable but not security specialists. When discussing severity:

- Lead with the label and a plain-language description of what an attacker can achieve — not the CVSS number.
- Be honest about preconditions: the configuration, access, or user interaction required.
- Treat disagreement as a technical discussion, not a dispute, and record both views (see [Communications Playbook](sirt-communications-playbook.md) Play 14).
- Never imply a Medium or Low issue does not matter. Every confirmed vulnerability gets fixed; the label sets the pace, not whether the work happens.

### Pitfalls

- **Score anchoring.** Do not let the CVSS number override judgment; the label exists because context matters.
- **Inflation pressure.** Others may push for a higher score. Score what the evidence supports. When evidence is incomplete, mark the label provisional and record the assumptions rather than defaulting higher — SSVC priority can still fail safe without inflating the severity claim.
- **Stale exploit state.** Follow the review cadence in §3.

---

## References

- FIRST: [CVSS v4.0 Specification](https://www.first.org/cvss/v4.0/specification-document) and [Calculator](https://www.first.org/cvss/calculator/4.0)
- CISA: [Stakeholder-Specific Vulnerability Categorization (SSVC)](https://www.cisa.gov/stakeholder-specific-vulnerability-categorization-ssvc)
- CISA: [Known Exploited Vulnerabilities (KEV) Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- FIRST: [EPSS](https://www.first.org/epss/)
- MITRE: [CWE](https://cwe.mitre.org/)

---

## Open items

- Confirm the post-PD review cadence (weekly for 30 days for Critical and High; monthly automated sweep) once tooling exists to support it.
- Align the report prioritization process ([issue #26](https://github.com/Akrites-Foundation/SIRT/issues/26)) with the SSVC outcomes above.
