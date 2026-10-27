# Akrites SIRT Maintainer of Last Resort Policy and Guidelines

**Status:** Consolidated Official Policy & Guidelines  
**Applies to:** Akrites SIRT, Working Groups, and Upstream Maintainers  
**Companion / Precedence Note:** This document combines the formal operational framework for Maintainer of Last Resort (MoLR) actions with the plain-language maintainer commitments (*"What Akrites Will and Won't Do to Your Project"*). The plain-language commitments in Part I constitute the non-negotiable floor for all SIRT actions and take precedence over technical operations.

---

# Part I: Plain-Language Maintainer Commitments

### 1. What We Ask For & What We Offer
When the Akrites SIRT reaches out regarding a security issue in an open-source project, our goal is to bring a finished, high-quality solution rather than a burden:
* **The Deliverable**: A written explanation of the problem, a working reproduction (failing unit test / PoC), a proposed patch, and regression tests.
* **Full Coordination Support**: If desired by the maintainer, Akrites handles CVE reservation, advisory drafting, downstream distro notification, and synchronized disclosure timing—at zero cost and with no obligations.
* **Maintainer Authority**: The creator and maintainer retain final authority over their codebase. Maintainers may decline a fix, state that a version is End-of-Life (EOL), or dispute a finding ("WONTFIX" or "not a vulnerability").

### 2. Disagreements & Verbatim Rationale
* **Technical Exchange**: If a maintainer believes a report is not a vulnerability, Akrites engages in a good-faith technical exchange on the merits (sharing reachability traces, deployment assumptions, and reproductions). If the maintainer persuades Akrites, the case is closed, no advisory is created, and reserved CVEs are withdrawn.
* **Verbatim Rationale**: If a technical disagreement persists and Akrites proceeds with an advisory, the maintainer is offered the right to print their exact, word-for-word reasoning in the public advisory. Akrites will show the finished wording to the maintainer prior to publication and will never edit or paraphrase the maintainer's statement.

### 3. Absolute "Won't Do" Boundaries
1. **Never Take a Package Name**: Akrites will **never** ask for, petition for, or accept custody of an upstream package namespace on any registry (npm, PyPI, Maven Central, crates.io, etc.), under any circumstances—including through registry abandonment or dispute policies.
2. **Never Impersonate or Shadow**: Akrites will never publish into an original project's namespace or use an upstream project's name or logo. All security releases are clearly labeled as Akrites security patches and point back to the original project.
3. **No Bug Bounty Claims**: Akrites does not solicit or accept bug bounty payments for vulnerabilities reported to upstream projects.

### 4. 90-Day Silence Floor
Maintainers go quiet for many valid life reasons (illness, bereavement, job changes, lost access). Akrites will **never** declare a project abandoned until it has been silent across all attempted channels for **at least 90 calendar days**. Any sign of life (a commit, issue comment, or registry login signal) resets the 90-day clock completely.

### 5. Returning Maintainer Guarantees
* **Unconditional Handback**: If a maintainer returns after a last-resort security release has been issued, any activity by their verified identity (e.g., in their repository) immediately reclaims full ownership.
* **Zero Friction**: The returning maintainer does not need to justify their absence, explain their security practices, or adopt Akrites tooling. They inherit all patch PRs, test artifacts, and advisory context with zero obligations.
* **Deprecation / Redirection**: If a returning maintainer requests that a last-resort release be taken down, Akrites marks the release as deprecated and redirects users to the maintainer's official releases. (Historical releases and advisories remain published to prevent supply-chain breakage and maintain security history).

### 6. Pre-Registered Intent (`SECURITY.md`)
Maintainers can pre-register their emergency preferences in their `SECURITY.md` or via Akrites. If a maintainer explicitly registers a **"do not fork"** preference, Akrites will strictly honor it: no last-resort release will ever be created, and Akrites will focus entirely on advisories, mitigations, and helping downstream consumers migrate off the dependency.

---

# Part II: Governance & Operational Framework

## 1. Purpose & Scope

### 1.1 The Three Stall Conditions
This policy governs SIRT actions when coordinated vulnerability disclosure (CVD) toward an upstream open-source project stalls under one of three conditions:
1. **Capacity Gap**: The project wants to fix the vulnerability but lacks a private reporting channel, security contacts, CI capacity, or bandwidth.
2. **Deliberate Non-Fix (EOL / WONTFIX)**: The maintainer is reachable and, after a technical exchange on the merits, decides the affected branch will not be patched.
3. **Unresponsive / Abandoned**: No contact is established within the escalation window due to project abandonment, unreachability, or a compromised maintainer.

### 1.2 Two Operational Tracks
* **Track A: Upstream Assistance**: Supplying capacity, tooling, triage support, patch drafts, and disclosure machinery to maintainers. This is the primary mode of operation.
* **Track B: Last-Resort Action (MoLR)**: A rare, governed exception entered **only** when no party holds both the legal right and demonstrated willingness to ship a fix.

> **Core Principle**: The Maintainer of Last Resort function delivers individual vulnerability fixes; it **does not adopt or maintain projects**. The unit of work is strictly the single vulnerability (CVE).

---

## 2. First Principles for Last-Resort Actions

1. **Protect Downstream, Respect Upstream**: Protect downstream users without seizing upstream projects or enforcing compliance.
2. **License Governs Fork Rights**: Confirm that the open-source license explicitly permits redistribution before touching code.
3. **Akrites Never Takes a Name**: Maintain zero-custody over package namespaces.
4. **Prefer the Patch to the Fork**: Carrying code creates long-term drag. Upstream dependency migration by intermediate maintainers is always preferred over standing up a fork.
5. **Severity Never Accelerates Property Judgments**: Exploit pressure may shorten disclosure timelines, but it never accelerates the 90-day abandonment finding.
6. **Technical Exchanges Before Non-Fixes**: Disagreements on severity or reachability are technical problems first; SIRT must be willing to concede when the maintainer is right.
7. **Document Everything**: Maintain a complete chain-of-custody log for all contact attempts, technical exchanges, and governance approvals.

---

## 3. The Two Clocks

| Clock | Purpose | Speed / Controls |
| :--- | :--- | :--- |
| **Disclosure Clock** | Governs how quickly downstream users are protected via advisories and mitigations. | **SSVC-adjustable** based on severity, EPSS, and active exploitation. Default decision point at **T0 + ~30 calendar days**. |
| **Abandonment Clock** | Governs when Akrites may conclude a project is abandoned and eligible for Track B. | **Hard floor: 90 calendar days of total silence** across all channels. Insensitive to severity or exploit pressure. |

### 3.1 Disclosure Clock Contact & Escalation Protocol
* **Attempt 1 (T0)**: Private report via preferred channel (`SECURITY.md`, GitHub PVR, security email).
* **Attempt 2 (T0 + 5 business days)**: Re-send and widen to commit-history maintainer emails and package registry contacts.
* **Attempt 3 (T0 + 10 business days)**: Escalate to umbrella organizations, foundations (STF, OpenSSF, Alpha-Omega), and distro security teams.
* **Coordinator Handoff (T0 + 15 business days)**: Bring in neutral coordinators (CERT/CC, VINCE, CNA-LR).
* **Decision Point (T0 + ~30 calendar days)**: Classify into a scenario and publish advisory, VEX, and mitigation.

---

## 4. Scenario Decision Matrix

| Signal Observed | Scenario | Primary Path (Track A) | Track B (MoLR) Status |
| :--- | :--- | :--- | :--- |
| Maintainer engages; lacks CI/bandwidth | **§5.1 Capacity Gap** | Assist in place; supply triage, patches, and release engineering. | **No.** Capacity gaps are met with capacity. |
| Maintainer disputes finding | **§5.2.1 Technical Disagreement** | Exchange evidence, run PoC, offer call. Concede if maintainer is right. | **No.** Not a stall condition while live. |
| Maintainer declines to fix after exchange | **§5.2 Deliberate Non-Fix** | Publish advisory, VEX (`will_not_fix`), verbatim rationale, and workarounds. | **Only** if no downstream party will carry the fix. |
| Unresponsive; project active elsewhere | **§5.3a Silent but Alive** | Continue escalation; pursue intermediate maintainer migration. | **No.** Silence is not total; clock restarts. |
| Total silence across all channels ≥ 90 days | **§5.3b Abandoned** | Perform §6 last-resort security release and parallel §7 steward search. | **Yes**, subject to §6.1 entry test. |
| Unreachable + indicators of compromise | **§5.3c Suspect / Compromised** | Treat as security incident; clean-room build from known-good commit. | **Yes**, with heightened provenance vetting. |

---

## 5. Track B: Maintainer of Last Resort (MoLR) Execution

### 5.1 Mandatory Entry Test (All Must Hold)
Track B requires a signed entry test confirming all six criteria:
1. **Absence of Alternatives**: All Track A options (assist in place, distro carry, community successor, maintainer-blessed transfer, intermediate migration) are documented as asked and declined.
2. **Published Criticality Threshold**: The package meets published, objective criticality metrics (e.g., OpenSSF Criticality Score, dependent tree counts, member SBOM prevalence).
3. **Permissive License**: Open-source license explicitly permits redistribution.
4. **Bounded Patch Series**: Fix is deliverable as a patch series against a pinned upstream commit.
5. **Capacity Slot Available**: Akrites maintains a strict cap on concurrent MoLR engagements; a slot must be available.
6. **Per-CVE Approval**: Approval is granted specifically for one CVE ID.

### 5.2 Approval Authority & Recusal
* **Mandatory Recusal**: Any decision-maker with a commercial, personal, or organizational dependency on the affected package must recuse themselves from voting.

### 5.3 The Artifact: Patch Series on a Pinned Commit
* **Structure**: The delivered artifact is a clean build of `(frozen upstream commit + N security patches)`.
* **Scope Discipline**: Build configuration and toolchains may be updated to produce a signed build, but library source outside the patch series and public API surface may not be altered.
* **Naming & Versioning**: Published under an Akrites-controlled namespace using ecosystem-specific, non-shadowing version strings.
* **Closed Inbound Channels**: Pull requests and general issue trackers are disabled on MoLR repositories (except for patch-regression reports) to prevent scope creep into an unfunded support desk.

### 5.4 Release Integrity & Correctness Gates
Before any MoLR security release is published, it must pass all release gates:
* **Integrity**: Clean-room build, signed commits/artifacts using per-engagement keys, SLSA build provenance, and two-person publish controls.
* **Correctness**: Upstream test suite passes, downstream consumer sample tests pass, **public API surface diff is empty** against the pinned commit, and two named human reviewers sign off (disclosing any AI assistance).

---

# Part III: Stewardship Transition & Downstream Routing

### 1. Stewardship Search & Vetting
* **Solicited Search**: Akrites conducts targeted outreach to distros, dependent projects, foundations, and known past contributors. Akrites **never broadcasts** `"critical unmaintained package"` publicly, as this creates an attacker targeting list.
* **Vetting (Reference Threat: `xz` / CVE-2024-3094)**: Candidate stewards must undergo identity verification, contribution history checks, signed commit enforcement, and staged co-maintenance before full handoff.

### 2. Freeze on Wind-Down
If an engagement ends or no steward is found, Akrites **freezes the artifact** (published, signed, immutable, marked `"no further fixes"`). Akrites **never unpublishes, deletes, or yanks** a security release, as doing so breaks downstream builds and causes supply-chain incidents.

### 3. Machine-Readable Routing Without Taking Namespaces
To ensure downstream users receive security fixes without Akrites taking package names:
* **OSV & VEX Pointers**: All advisories publish machine-readable `"fixed_in_different_package"` VEX pointers.
* **Distro Integration**: Fixes are routed directly to Linux distribution security teams (Debian, Red Hat, Alpine, etc.).
* **Intermediate Maintainer Migration**: SIRT works with high-leverage upstream libraries to update their dependency specs to point to the secure patch or alternative package, resolving exposure for thousands of downstream projects at once.

---

# Part IV: Legal, Licensing, & Metrics

### 1. Licensing & Trademark Boundaries
* **Copyright**: Permissive licenses (MIT/BSD/Apache-2.0) permit patch redistribution. Copyleft (GPL/LGPL) requirements (source availability, notice retention, DCO sign-offs) must be strictly fulfilled.
* **Trademark**: Copyright licenses do not grant trademark rights. MoLR releases must **never** use original project logos or trademarked names as the release identity.

### 2. Metrics & Counter-Metrics
* **Headline Metric**: Share of known-affected consumers running a fixed version at 30 and 90 days post-PD.
* **Counter-Metric (Failure Signal)**: **A rising volume of MoLR engagements is a failure signal**, indicating that upstream assistance and dependency migration are failing. MoLR capacity caps enforce this constraint.

---

## Appendix A: One-Page Lifecycle & Decision Flow

```
DISCLOSURE CLOCK (Severity-adjustable; T0+30d default decision point)
T0 ──▶ T0+5bd (Widen) ──▶ T0+10bd (Ecosystem) ──▶ T0+15bd (Coordinators) ──▶ T0+30d (Decision)
                                                                                  │
  ┌───────────────────────────────────────────────────────────────────────────────┴──────────────┐
  │                                                                                              │
  ▼                                                                                              ▼
Track A: Upstream Assistance                                                   Track B: Last-Resort Action
├── Capacity Gap ──▶ Assist in place & build patch                              ├── Requires 90-Day Silence Floor
├── Disagreement ──▶ Technical exchange ──▶ Verbatim rationale                  ├── Signed §6.1 Entry Test
└── Unresponsive ──▶ Intermediate maintainer migration                         ├── Board Approval & Recusal
                                                                                └── Patch Series on Pinned Commit
```
