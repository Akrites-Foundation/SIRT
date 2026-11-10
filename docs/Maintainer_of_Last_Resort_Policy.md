# Akrites SIRT Maintainer of Last Resort (MoLR) Policy

**Status:** Draft — for Governing Board review (v1.0)
**Applies to:** Akrites SIRT, Working Groups, and Upstream Maintainers
**Companion doc:** [MoLR Guidelines and Procedures](molr_guidelines_and_procedures.md) — how the SIRT carries out this policy, step by step.
**Precedence:** The plain-language commitments in Part I are the non-negotiable floor for all SIRT actions and take precedence over the rest of this policy and over the Guidelines and Procedures.

---

# Part I: Plain-Language Maintainer Commitments

### 1. What We Ask For & What We Offer
When the Akrites SIRT reaches out regarding a security issue in an open-source project, our goal is to bring a finished, high-quality solution rather than a burden:
* **The Deliverable**: A written explanation of the problem, a working reproduction (failing unit test / PoC), a proposed patch, and regression tests.
* **Full Coordination Support**: If desired by the maintainer, Akrites handles CVE reservation, advisory drafting, downstream distro notification, and synchronized disclosure timing—at zero cost and with no obligations.
* **Maintainer Authority**: The creator and maintainer retain final authority over their codebase. Maintainers may decline a fix, state that a version is End-of-Life (EOL), or dispute a finding ("WONTFIX" or "not a vulnerability").
* **End-of-Life Branches**: If you declare a branch end-of-life but do not dispute the vulnerability, Akrites may — only with Governing Board approval, and only after telling you in advance — publish a security release for that branch under its own namespace (Part II §4). A WONTFIX or a disputed finding never leads to an Akrites release.

### 2. Disagreements & Verbatim Rationale
* **Technical Exchange**: If a maintainer believes a report is not a vulnerability, Akrites engages in a good-faith technical exchange on the merits. If the maintainer persuades Akrites, the case is closed, no advisory is created, and reserved CVEs are withdrawn.
* **Verbatim Rationale**: If a technical disagreement persists and Akrites proceeds with an advisory, the maintainer is offered the right to print their exact, word-for-word reasoning in the public advisory. Akrites will show the finished wording to the maintainer prior to publication and will never edit or paraphrase the maintainer's statement.

### 3. Absolute "Won't Do" Boundaries
1. **Never Take a Package Name**: Akrites will **never** ask for, petition for, or accept custody of an upstream package namespace on any registry (npm, PyPI, Maven Central, crates.io, etc.), under any circumstances—including through registry abandonment or dispute policies.
2. **Never Impersonate or Shadow**: Akrites will never publish into an original project's namespace or use an upstream project's name or logo. All security releases are clearly labeled as Akrites security patches and point back to the original project.
3. **No Bug Bounty Claims**: Akrites does not solicit or accept bug bounty payments for vulnerabilities reported to upstream projects.
4. **Never a Custodian or Owner**: Akrites does not take ownership of projects, long-term or otherwise, and is not a custodian for un-owned or abandoned projects.
5. **Never Choose Your Successor**: Akrites does not select, appoint, or approve new maintainers or stewards for a project.

### 4. 90-Day Silence Floor
Maintainers go quiet for many valid life reasons (illness, bereavement, job changes, lost access). Akrites will **never** declare a project abandoned until it has been silent across all attempted channels for **at least 90 calendar days**. Any sign of life (a commit, issue comment, or registry login signal) resets the 90-day clock completely. There are no exceptions for urgency or severity: urgent issues are handled through advisories and mitigations under the disclosure clock, never by shortening this floor.

### 5. Returning Maintainer Guarantees
* **Unconditional Precedence**: Akrites never holds ownership of a project. If a maintainer returns after a last-resort security release, any activity by their verified identity (e.g., in their repository) immediately ends the MoLR engagement, and the maintainer's releases take precedence.
* **Zero Friction**: The returning maintainer does not need to justify their absence, explain their security practices, or adopt Akrites tooling. They inherit all patch PRs, test artifacts, and advisory context with zero obligations.
* **Deprecation / Redirection**: If a returning maintainer requests that a last-resort release be taken down, Akrites marks the release as deprecated and redirects users to the maintainer's official releases. (Historical releases and advisories remain published to prevent supply-chain breakage and maintain security history).

### 6. Pre-Registered Intent (`SECURITY.md`)
Maintainers can pre-register their emergency preferences in their `SECURITY.md` or via Akrites. If a maintainer explicitly registers a **"do not fork"** preference, Akrites will strictly honor it: no last-resort release will ever be created, and Akrites will focus entirely on advisories, mitigations, and helping downstream consumers migrate off the dependency.

---

# Part II: Governance Framework

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
| **Disclosure Clock** | Governs how quickly downstream users are protected via advisories and mitigations. | **SSVC-adjustable** based on severity, EPSS, and active exploitation. Default decision point at **T0 + 15 business days**, aligned with the CVD Policy's 15-business-day upstream window. |
| **Abandonment Clock** | Governs when Akrites may conclude a project is abandoned and eligible for Track B. Does not apply to the EOL-branch path (§4), which never declares a project abandoned. | **Hard floor: 90 calendar days of total silence** across all channels. This period may begin at the T0 of a trusted third party's contact attempts, provided a complete log of those attempts is submitted (see §3.2). Insensitive to severity or exploit pressure. |

### 3.1 Disclosure Clock Contact & Escalation
The SIRT works a fixed contact and escalation ladder from T0 to the T0 + 15 business-day decision point, recording every attempt. The ladder is set out in the [Guidelines and Procedures](molr_guidelines_and_procedures.md#1-contact-and-escalation-ladder).

### 3.2 Trusted Third-Party Clock Start
* **Who qualifies**: For now, a trusted third party is an **active Akrites member organization**. Other coordinators (for example, a government CERT) will be defined once Akrites accepts reports from outside its membership.
* **Evidence required**: A complete log of the third party's contact attempts, covering the same channels as the escalation ladder in §3.1. Without it, the clock starts at the SIRT's own T0.

---

## 4. Scenario Decision Matrix

| Signal Observed | Scenario | Primary Path (Track A) | Track B (MoLR) Status |
| :--- | :--- | :--- | :--- |
| Maintainer engages; lacks CI/bandwidth | **Capacity Gap** (§1.1) | Assist in place; supply triage, patches, and release engineering. | **No.** Capacity gaps are met with capacity. |
| Maintainer disputes finding | **Technical Disagreement** (Part I §2) | Exchange evidence, run PoC, offer call. Concede if maintainer is right. | **No.** Not a stall condition while live. |
| Maintainer declines to fix after exchange (WONTFIX or disputed finding) | **Deliberate Non-Fix** (§1.1) | Publish advisory, VEX (status affected, no fix planned), verbatim rationale, and workarounds; offer the proposed patch to downstream parties (see Guidelines and Procedures). | **No.** The maintainer is reachable and has decided. |
| Maintainer declares the affected branch EOL, does not dispute the vulnerability, and fixes it in supported versions | **EOL Branch** (§1.1) | As for Deliberate Non-Fix; point users to the supported versions. | **Only** if no downstream party will carry the fix, subject to §5.1 (EOL-branch path). |
| Unresponsive; project active elsewhere | **Silent but Alive** | Continue escalation; pursue intermediate maintainer migration. | **No.** Silence is not total; clock restarts. |
| Total silence across all channels ≥ 90 days | **Abandoned** | Perform §5 last-resort security release; Part III applies. | **Yes**, subject to §5.1 entry test. |
| Unreachable + indicators of compromise | **Suspect / Compromised** | Treat as security incident; clean-room build from known-good commit. | **Yes**, with heightened provenance vetting. |

---

## 5. Track B: Maintainer of Last Resort (MoLR)

### 5.1 Mandatory Entry Test (All Must Hold)
Track B requires a signed entry test confirming all seven criteria:
1. **Absence of Alternatives**: All Track A options (assist in place, distro carry, community successor, maintainer-blessed transfer, intermediate migration) are documented as asked and declined.
2. **Published Criticality Threshold**: The package meets published, objective criticality metrics (e.g., OpenSSF Criticality Score, dependent tree counts, member SBOM prevalence), or a documented criticality justification recorded in the MoLR decision record and accepted by the approver.
3. **License Permits Redistribution**: The open-source license explicitly permits redistribution of modified code; any copyleft obligations (Part IV §1) can be met.
4. **Bounded Patch Series**: Fix is deliverable as a patch series against a pinned upstream commit.
5. **Capacity Slot Available**: Akrites maintains a strict cap on concurrent MoLR engagements; a slot must be available.
6. **Per-CVE Approval**: Approval is granted specifically for one CVE ID.
7. **Chain of Custody for Prior Silence**: If relying on a trusted third party's contact attempts to satisfy the 90-day floor, the submitter provides a complete log of those attempts (§3.2).

**EOL-branch path.** For an EOL branch (§4), criteria 1–6 apply and criterion 7 is replaced by: the maintainer's end-of-life statement on record; confirmation that the maintainer does not dispute the vulnerability; the fix available in the project's supported versions; documented absence of any downstream party willing to carry the fix; and advance notice to the maintainer, with the offer of verbatim rationale (Part I §2). The release covers only the end-of-life branch. A "do not fork" preference (Part I §6) still blocks it.

### 5.2 Approval Authority & Recusal
* **Approval**: Track B requires approval by the **Governing Board** (or a MoLR subcommittee the Governing Board designates in writing), granted per CVE and recorded in the MoLR decision record template.
* **Mandatory Recusal**: Any decision-maker with a commercial, personal, or organizational dependency on the affected package must recuse themselves from voting. A conflicted primary submitter may present the technical risk assessment and Track A exhaustion evidence to the Board, but does not vote.

### 5.3 The Artifact
The deliverable is a clean build of a frozen upstream commit plus the approved security patches, published under an Akrites-controlled namespace and never into the original project's namespace. The artifact rules are in the [Guidelines and Procedures](molr_guidelines_and_procedures.md#4-the-artifact-patch-series-on-a-pinned-commit).

### 5.4 Release Integrity & Correctness
No MoLR security release is published until it passes every integrity and correctness gate in the [Guidelines and Procedures](molr_guidelines_and_procedures.md#5-release-integrity--correctness-gates), including two named human reviewers who disclose any AI assistance.

---

## 6. Limits of a MoLR Engagement

* **Operational donation, not ownership**: A MoLR engagement is an operational donation by Akrites of **up to 12 months**, counted from the first last-resort security release. Akrites does not take long-term ownership of any project.
* **Not a custodian**: Akrites is not a custodian for un-owned or abandoned projects. When the engagement ends, the artifact is frozen (Part III §2).
* **No steward approval**: Akrites does not select, appoint, or approve successor maintainers or stewards. It may help a project's community find candidates (Part III §1).
* **No term limits**: Engagements are bounded by the 12-month donation, not by counts of fixes or renewals.
* **Ends early on return**: A returning maintainer ends the engagement immediately (Part I §5).

---

# Part III: Wind-Down & Downstream Routing

### 1. Successor Maintainers
Akrites may help a project's community find a successor through targeted outreach, but never broadcasts that a package is unmaintained and never selects or approves the successor. How the SIRT supports a search is in the [Guidelines and Procedures](molr_guidelines_and_procedures.md#7-successor-maintainers).

### 2. Freeze on Wind-Down
If an engagement ends or no successor emerges, Akrites **freezes the artifact** (published, signed, immutable, marked `"no further fixes"`). Akrites **never unpublishes, deletes, or yanks** a security release, as doing so breaks downstream builds and causes supply-chain incidents.

### 3. Routing Without Taking Namespaces
Downstream users are routed to fixes through machine-readable advisories (OSV, VEX), Linux distribution security teams, and intermediate maintainers — never by taking package names. The routing steps are in the [Guidelines and Procedures](molr_guidelines_and_procedures.md#6-publishing-and-downstream-routing).

---

# Part IV: Legal, Licensing, & Metrics

### 1. Licensing & Trademark Boundaries
* **Copyright**: Permissive licenses (MIT/BSD/Apache-2.0) permit patch redistribution. Copyleft (GPL/LGPL) requirements (source availability, license and notice retention, marking of modifications) must be strictly fulfilled. Commits also carry DCO sign-offs per Akrites practice.
* **Trademark**: Copyright licenses do not grant trademark rights. MoLR releases must **never** use original project logos or trademarked names as the release identity.

### 2. Metrics & Counter-Metrics
* **Headline Metric**: Share of known-affected consumers running a fixed version at 30 and 90 days post-PD.
* **Counter-Metric (Failure Signal)**: **A rising volume of MoLR engagements is a failure signal**, indicating that upstream assistance and dependency migration are failing. MoLR capacity caps enforce this constraint.

---

## Change history

| Version | Date | Description |
| ------- | ---------- | -------------- |
| 1.0 | 2026-11-10 | Split into this policy and the [MoLR Guidelines and Procedures](molr_guidelines_and_procedures.md); operational detail moved there. Incorporates [PR #183](https://github.com/Akrites-Foundation/SIRT/pull/183) by Roman Zhukov (trusted third-party clock start, chain-of-custody criterion, criticality justification, recusal). Adds: 12-month operational donation, no ownership or custody, no steward approval, no term limits, no urgency exception to the 90-day floor, Track B after a deliberate non-fix only for an end-of-life branch whose vulnerability the maintainer does not dispute (EOL-branch path). Prepared for first Governing Board review. |
