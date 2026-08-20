# Severity Scoring Methodology

**Owner:** Akrites SIRT
**Status:** Draft for TOC / Board review
**Applies to:** All vulnerabilities coordinated by the Akrites SIRT
**Related:** [CVD Policy, Section 9](../coordinated-vulnerability-disclosure-policy.md); [CVD Guide, Phase 3](Akrites_CVD_Guide.md); [Report Prioritization Process (PR #60)](https://github.com/Akrites-Foundation/SIRT/pull/60)

---

## Purpose

This document defines how the Akrites SIRT assesses, communicates, and publishes
the severity of vulnerabilities it coordinates. It establishes a layered approach
where each tool answers a distinct question:

- **CVSS v4.0** describes the vulnerability technically.
- **The SIRT severity label** communicates operational impact to maintainers and consumers.
- **Exploit state** tracks real-world evidence independently of the technical score.
- **SSVC** informs the SIRT's internal response priority.

These layers are complementary, not competing. Severity describes the
vulnerability. Exploit state describes the evidence. Priority describes what
the SIRT should do next.

---

## Layer 1 — CVSS v4.0 (technical description)

CVSS v4.0 is the required baseline for all vulnerabilities coordinated to public
disclosure. As committed in the CVD Policy (Section 9), the SIRT produces a
v4.0 vector and score for every case.

### Requirements

- Every case that reaches PD must include a **CVSS v4.0 Base (CVSS-B)** vector
  and numeric score.
- The full vector string is always published alongside the numeric score. The
  vector is often more informative than the number alone and allows downstream
  consumers to adjust for their environment.
- **CVSS v3.1** may be included for legacy comparison where downstream consumers
  or databases still require it. When included, it is clearly labeled as legacy.

### CVSS-BT (Threat metrics)

> **Open decision:** Should Akrites publish CVSS-BT (Base + Threat) when exploit
> maturity is known at disclosure, or always publish CVSS-B only?
>
> **Case for CVSS-BT:** Exploit maturity is decision-relevant data. A
> vulnerability with confirmed active exploitation scores differently from one
> that is theoretical, and consumers benefit from seeing that distinction in the
> score itself.
>
> **Case for CVSS-B only:** Threat metrics change over time, making the
> published score a snapshot that may mislead if not maintained. The exploit
> state field (Layer 3) captures the same information without embedding it in
> the score.
>
> **Recommendation:** Publish CVSS-B as the primary score. When exploit maturity
> data is available at PD, publish CVSS-BT as a supplementary score with a clear
> "as of PD date" qualifier. This gives consumers the richer data without
> implying the threat score is static.

### Scoring through the lifecycle

The CVSS assessment shouldn't be a one-time event. It evolves as understanding deepens:

| Lifecycle phase | Scoring activity |
| --- | --- |
| **Intake** | Record the reporter's severity estimate as-is. Do not discard or override it. |
| **Validation** | SIRT analyst produces a provisional CVSS v4.0 vector based on confirmed reproduction and root-cause analysis. |
| **Coordination** | Review the provisional score with the maintainer. If the maintainer or another party scores it differently, preserve both assessments. |
| **Disclosure preparation** | Finalize the vector. Where assessments diverge, publish a **deviation note** documenting the differing assumptions rather than silently replacing one score with another. |
| **PD** | Publish the final CVSS v4.0 vector, numeric score, and any deviation notes. |

### Deviation notes

When the SIRT's assessment differs materially from another party's published
score (e.g., the upstream project, a CNA, or a downstream vendor), the SIRT
documents:

- Which assessments differ and by how much.
- The specific metric(s) where assumptions diverge (e.g., Attack Complexity,
  User Interaction, scope boundaries).
- Why the SIRT reached its conclusion.

Deviation notes are published alongside the advisory. The goal is transparency,
not dispute -- reasonable analysts can reach different conclusions when
environmental assumptions differ.

---

## Layer 2 — SIRT severity label (operational communication)

A four-level severity label provides a concise, plain-language assessment for
maintainers, consumers, and stakeholders who may not have a security background.
The label is informed by the CVSS score but is not mechanically derived from it.

The vocabulary is **Critical / Important / Moderate / Low**. This aligns with
Red Hat, the Linux kernel, and several major downstream consumers. "Important"
avoids the ambiguity of "High" (high compared to what?) and reads more
naturally in coordinator-to-maintainer communication, which is the SIRT's
primary use case.

### Label definitions and CVSS guidance ranges

The label reflects the analyst's holistic assessment. The CVSS ranges below are
guidance, not mechanical cutoffs -- an analyst may assign a label above or below
the range when context warrants it, provided the rationale is documented.

| Label | CVSS v4.0 guidance range | Description |
| --- | --- | --- |
| **Critical** | 9.0 -- 10.0 | Exploitation is straightforward and leads to complete compromise (e.g., unauthenticated RCE, full authentication bypass). Immediate coordinated response. |
| **Important** | 7.0 -- 8.9 | Significant impact but exploitation requires meaningful preconditions (e.g., authenticated access, non-default configuration, user interaction). Urgent but not emergency response. |
| **Moderate** | 4.0 -- 6.9 | Real but limited impact, or exploitability is significantly constrained. Normal coordination timeline. |
| **Low** | 0.1 -- 3.9 | Minimal impact or requires conditions unlikely to occur in practice. Addressed as capacity allows. |

### When the label diverges from the CVSS range

Common reasons an analyst may set the label outside the guidance range:

- **Ecosystem context.** A CVSS 6.8 in a library used by every container
  orchestrator may warrant "Important" because of blast radius.
- **Preconditions in practice.** A CVSS 9.1 that requires a rarely-enabled
  debug mode may warrant "Moderate" because the precondition is uncommon
  outside development environments.
- **Active exploitation.** Evidence of in-the-wild exploitation may elevate a
  label regardless of the base score.

When the label diverges, the analyst documents the rationale in the case record.

---

## Layer 3 — Exploit state (dynamic evidence field)

Exploit state is tracked as a separate field, independent of both the CVSS score
and the severity label. It changes over time as new evidence emerges.

| Value | Meaning |
| --- | --- |
| **Active** | Confirmed exploitation in the wild, supported by credible reporting or direct observation. |
| **Demonstrated** | A working exploit exists and has been demonstrated (e.g., in a controlled environment or security conference), but no evidence of in-the-wild use. |
| **PoC** | Proof-of-concept code exists that demonstrates the vulnerability but may not be weaponized. |
| **Theoretical** | The vulnerability is confirmed but no exploit or PoC is publicly known. |
| **Unknown** | Exploit status has not been assessed or information is insufficient. |

### Operational implications

- **Active** or **Demonstrated** with a low-barrier exploit: strong signal to
  accelerate the coordination timeline. Defenders need the fix now.
- **PoC**: monitor for escalation; factor into the severity label assessment.
- **Theoretical** or **Unknown**: do not treat the absence of evidence as
  evidence of low risk. "Unknown" must never be read as "safe."

Exploit state is updated throughout the case lifecycle and noted in the
published advisory when relevant at PD.

---

## Layer 4 — SSVC (internal triage prioritization)

The CISA/FIRST Stakeholder-Specific Vulnerability Categorization (SSVC) is used
internally by the SIRT to determine response priority -- which cases to staff
first and how urgently. SSVC is not published externally.

### Decision tree: Coordinator

The SIRT uses the SSVC Coordinator decision tree, which evaluates:

| Decision point | What it asks |
| --- | --- |
| **Exploitation** | Is there evidence of active exploitation? (None / PoC / Active) |
| **Technical impact** | If exploited, what is the worst-case technical outcome? (Partial / Total) |
| **Automatable** | Can an attacker automate exploitation at scale? (No / Yes) |
| **Mission prevalence** | How widely is the affected component deployed in critical infrastructure? (Minimal / Support / Essential) |

### SSVC outcomes

The Coordinator tree produces one of three action recommendations:

| Outcome | SIRT response |
| --- | --- |
| **Act** | Staff immediately. Accelerate coordination timeline. Engage maintainer and downstream parties urgently. |
| **Track\*** | Monitor closely. Prioritize for near-term coordination. Allocate analyst time within the current cycle. |
| **Track** | Record and coordinate on normal timeline. |

### Relationship to the severity label

SSVC and the severity label answer different questions. A "Moderate" vulnerability
in an essential, widely-deployed library may be SSVC "Act" because of mission
prevalence and automatable exploitation. A "Critical" vulnerability in a niche
component with no known exploitation may be SSVC "Track*". Both assessments are
valid and serve different audiences.

---

## What is not used: EPSS

FIRST's Exploit Prediction Scoring System (EPSS) estimates the probability that
a published CVE will be exploited in the next 30 days. It is a downstream
prioritization signal, not a coordinator assessment tool:

- EPSS requires a published CVE. Pre-disclosure cases -- the SIRT's primary
  workload -- have no meaningful EPSS value.
- Missing EPSS data must never be interpreted as low risk.
- EPSS may be useful to downstream consumers after PD for their own
  prioritization. The SIRT does not publish or endorse EPSS scores.

---

## What gets published at PD

The public advisory includes:

- CVSS v4.0 vector string and numeric score (required).
- CVSS v3.1 vector and score (when included for legacy comparison, labeled as such).
- CVSS-BT supplementary score (when exploit maturity data is available, with
  "as of" qualifier -- pending the open decision above).
- SIRT severity label (Critical / Important / Moderate / Low -- pending the
  open decision above).
- Exploit state at time of disclosure.
- CWE identifier for root cause.
- CVE ID.
- Deviation notes, if the SIRT's assessment differs from another party's.

SSVC outcomes are internal and not published.

---

## Guidance for analysts

### Communicating severity to maintainers

Many upstream maintainers are security-capable but not security-specialists.
When communicating severity:

- Lead with the severity label and a plain-language description of what an
  attacker can achieve, not the CVSS number.
- Explain preconditions honestly -- what configuration, access, or user
  interaction is required.
- If the maintainer disagrees with the assessment, treat it as a technical
  discussion, not a dispute. Document both perspectives.
- Avoid implying that a "Moderate" issue does not matter. Every confirmed
  vulnerability deserves a fix; the label affects pacing, not whether the
  work happens.

### Potential pitfalls

- **Score anchoring.** Do not let the CVSS number override your judgment. The
  label exists precisely because context matters beyond what the formula
  captures.
- **Inflation pressure.** External parties may pressure for a higher score.
  Score what the evidence supports. If you are uncertain, err toward the
  higher label and document the uncertainty.
- **Stale exploit state.** Exploit state changes. What type of review cadence should we expect? 

---

## References

- FIRST -- [CVSS v4.0 Specification](https://www.first.org/cvss/v4.0/specification-document)
- FIRST -- [CVSS v4.0 Calculator](https://www.first.org/cvss/calculator/4.0)
- CISA -- [SSVC Guide](https://www.cisa.gov/stakeholder-specific-vulnerability-categorization-ssvc)
- FIRST -- [EPSS](https://www.first.org/epss/)
- MITRE -- [CWE](https://cwe.mitre.org/)

---

## Open items (for TOC / Board)

- Decide whether to publish **CVSS-BT** alongside CVSS-B when exploit maturity
  is known at PD.
- Align with the Report Prioritization Process (PR #60) on how SSVC outcomes
  map to response bands and staffing.

---

