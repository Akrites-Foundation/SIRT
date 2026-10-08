# SIRT Report Triage, Validation & Queue Prioritization Policy

## 1. Overview & Objective
This document defines the methodology and process used by the Akrites Security Incident Response Team (SIRT) to ingest, evaluate, and prioritize incoming vulnerability reports.

To maintain total operational clarity and avoid opaque scoring or terminology collisions, this policy strictly decouples three distinct concepts:
1. **Validation Path:** Determined by **Ingestion Provenance** (Source).
2. **Technical Severity:** Determined strictly by intrinsic technical impact (see `SEVERITY_SCORING_METHODOLOGY.md`).
3. **Queue Action Priority:** Determined by combining severity, exploit evidence (PoC), affected scope, and coordination deadlines.

> **Note on Read-in Clearances:** Ingestion Provenance classifies the origin and trust model of the reporting entity. It operates independently of internal Read-in Access Clearance Tiers.

---

## 2. Ingestion Provenance & Validation Paths

Source origin determines the **validation workflow and speed**, NOT the final severity or queue priority. All reports—regardless of source—must be verified before remediation planning.

┌────────────────────────────────────────────────────────────────────────┐
│                        Incoming SIRT Report                            │
└───────────────────┬────────────────────────────────────┘
│
┌──────────────────────────┼──────────────────────────┐
▼                          ▼                          ▼
┌──────────────────┐       ┌──────────────────┐       ┌──────────────────┐
│ Upstream &       │       │ Member & WG      │       │ Community &      │
│ Partner Ingest   │       │ Ingest           │       │ Public Ingest    │
│ (Pre-Validated)  │       │ (High Trust)     │       │ (Unverified)     │
└────────┬─────────┘       └────────┬─────────┘       └────────┬─────────┘
│                          │                          │
▼                          ▼                          ▼
Direct Technical           Internal Ingest &           Validation Gate
Triage & Embargo            WG Coordination           (Spam / AI Filter)

Here is the complete `DOCS/PRIORITIZATION_AND_TRIAGE.md` file formatted in raw Markdown. It includes a standard ASCII/Unicode text flowchart that renders cleanly in GitHub preview, raw text viewers, and terminal environments.

```markdown
# SIRT Report Triage, Validation & Queue Prioritization Policy

## 1. Overview & Objective
This document defines the methodology and process used by the Akrites Security Incident Response Team (SIRT) to ingest, evaluate, and prioritize incoming vulnerability reports.

To maintain total operational clarity and avoid opaque scoring or terminology collisions, this policy strictly decouples three distinct concepts:
1. **Validation Path:** Determined by **Ingestion Provenance** (Source).
2. **Technical Severity:** Determined strictly by intrinsic technical impact (see `SEVERITY_SCORING_METHODOLOGY.md`).
3. **Queue Action Priority:** Determined by combining severity, exploit evidence (PoC), affected scope, and coordination deadlines.

> **Note on Read-in Clearances:** Ingestion Provenance classifies the origin and trust model of the reporting entity. It operates independently of internal Read-in Access Clearance Tiers.

---

## 2. Ingestion Provenance & Validation Paths

Source origin determines the **validation workflow and speed**, NOT the final severity or queue priority. All reports—regardless of source—must be verified before remediation planning.


```

┌────────────────────────────────────────────────────────────────────────┐
│                        Incoming SIRT Report                            │
└───────────────────┬────────────────────────────────────┘
│
┌──────────────────────────┼──────────────────────────┐
▼                          ▼                          ▼
┌──────────────────┐       ┌──────────────────┐       ┌──────────────────┐
│ Upstream &       │       │ Member & WG      │       │ Community &      │
│ Partner Ingest   │       │ Ingest           │       │ Public Ingest    │
│ (Pre-Validated)  │       │ (High Trust)     │       │ (Unverified)     │
└────────┬─────────┘       └────────┬─────────┘       └────────┬─────────┘
│                          │                          │
▼                          ▼                          ▼
Direct Technical           Internal Ingest &           Validation Gate
Triage & Embargo            WG Coordination           (Spam / AI Filter)

```

### Upstream & Partner Ingest (Pre-Validated / High Trust)
* **Sources:** Clearinghouse partners, trusted open-source security teams (e.g., Linux Kernel Security Team, Apache Software Foundation Security, OpenSSF), national CSIRTs/CERTs.
* **Validation Path:** Fast-tracked under existing bilateral trust frameworks. Assumed pre-validated; bypasses initial noise screening directly into technical verification and embargo tracking.

### Member & WG Ingest (High Trust)
* **Sources:** Akrites Working Groups (WGs), Akrites Foundation Members, maintainers, internal auditing/fuzzing infrastructure.
* **Validation Path:** Direct routing to domain maintainers. Minimal intake friction due to internal context and high signal-to-noise ratio.

### Community & Public Ingest (Unverified)
* **Sources:** Independent security researchers, general public, bug bounty submissions, anonymous reporters.
* **Validation Path:** Subject to mandatory **Public Screening Gate** verification to filter automated scanner outputs, hallucinated/AI-generated reports, and invalid submissions prior to engaging SIRT maintainer bandwidth.

> **Validation Principle:** Validation speed reflects reporting confidence, not priority capping. An anonymous public submission containing a working, unauthenticated RCE PoC is validated immediately and promoted to top queue order, outranking complete member reports for theoretical low-impact issues.

---

## 3. Queue Order & Operational Action Bands

Once validated and assessed for technical severity, reports are placed into the active SIRT operational queue across four **Action Bands**.

| Action Band | Criteria / Escalation Triggers | SIRT Acknowledgment | Target Maintainer Engagement & CVD Window |
| :--- | :--- | :--- | :--- |
| **INCIDENT** | Active exploitation in the wild, unauthenticated RCE with functional PoC, or supply-chain compromise affecting critical infrastructure OSS packages. | $\le$ 2 Hours | Immediate Case Manager assignment; engage upstream maintainers within 12 hours. |
| **URGENT** | High/Critical severity vulnerability with verified PoC or high blast radius across core OSS dependencies, without active exploitation. | $\le$ 12 Hours | Engage upstream maintainers $\le$ 48 hours; initiate CVD embargo tracking. |
| **STANDARD** | Validated Medium/Low severity vulnerabilities, conditional flaws, or non-critical package bugs. | $\le$ 48 Hours | Route to standard maintainer disclosure pipeline ($\le$ 14 days). |
| **NEEDS-INFO** | Incomplete reports, unverified public submissions lacking PoCs, unconfirmed scanner outputs, or awaiting reporter clarification. | $\le$ 72 Hours | Suspended until required verification or PoC is provided. |

### Intra-Band Queue Ordering ("Why Now" Criteria)
Within any given Action Band (e.g., within `URGENT`), cases are prioritized deterministically based on:

1. **Critical Infrastructure Impact:** Exposure level across systemic critical infrastructure dependencies (e.g., finance, energy, health, core cloud stacks).
2. **Exploit Evidence & PoC Quality:** Verified functional exploit payload vs. theoretical/static analysis output.
3. **Attacker Prerequisites:** Unauthenticated/Remote execution vs. Authenticated/Local access requirements.
4. **AI-Enabled Threat Velocity:** Vulnerabilities with high likelihood of rapid AI-assisted automated discovery/weaponization.
5. **Coordination & Embargo Deadlines:** Imminent public disclosure dates or expiring partner embargo windows.
6. **Case Age:** First-in, first-out (FIFO) tie-breaker for identical risk profiles.

---

## 4. Response Time Objectives (SLAs)

Action priority levels establish target Service Level Agreements (SLAs) for initial response, maintainer routing, and disclosure planning:

| Action Priority Level | Initial Acknowledgment | Triage & Validation Target | Remediation & Disclosure Plan Target |
| :--- | :--- | :--- | :--- |
| **INCIDENT** | $\le$ 2 hours | $\le$ 6 hours | Emergency Response Protocol |
| **URGENT** | $\le$ 12 hours | $\le$ 24 hours | $\le$ 7 days |
| **STANDARD** | $\le$ 48 hours | $\le$ 72 hours | $\le$ 14 days / Next Release Cycle |
| **NEEDS-INFO** | $\le$ 72 hours | N/A (Awaiting Info) | Suspended |

---

## 5. Public Screening Gate & Deduplication

### Screening Criteria for Community Ingest
All Community & Public Ingest submissions must pass the following screening criteria before escalating to SIRT Incident Commanders:
1. **Proof of Concept (PoC) Requirement:** Submissions must contain a reproducible script, execution trace, or actionable steps. Unsubstantiated static analysis or automated scanner dumps are closed as `Informational / Non-actionable`.
2. **AI & Automated Report Filtering:** Submissions identified as low-signal AI-generated noise or hallucinated vulnerability patterns will be rejected without secondary review.
3. **TLP & Embargo Agreement:** Reporters must agree to Akrites Coordinated Vulnerability Disclosure (CVD) timelines prior to technical evaluation.

### Deduplication & Co-Finder Preservation
* **Same-Root-Cause Rule:** Multiple incoming reports are merged **only** if they share the exact same root cause and require the same code fix.
* **Co-Finder Credit:** Merging a duplicate report MUST preserve all co-finders/reporters in the incident tracking record and eventual CVE/advisory credit attribution.

---

## 6. Technical Severity Scoring & Lifecycle Link

While Queue Action Priority (`INCIDENT`, `URGENT`, `STANDARD`, `NEEDS-INFO`) determines the SIRT's immediate operational focus, technical severity is assessed independently using CVSS v4.0 vectors and a plain-language 4-level scale.

For full details on scoring metrics across the issue lifecycle—from intake to Public Disclosure (PD)—refer to [Severity Scoring Methodology](SEVERITY_SCORING_METHODOLOGY.md).

```
