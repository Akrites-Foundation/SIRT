# Akrites Working Group Governance and Operations Guide

**Status:** Consolidated Official Draft  
**Applies to:** All Akrites Working Group (WG) Chairs, Co-Chairs, and Read-In Members  
**Governance Precedence:** Part I of this document governs structure, voting, and leadership rules. In any conflict between structural governance and day-to-day tactical guidelines in Part II, **Part I takes precedence**.

---

# Part I: Governance, Leadership & Lifecycle

### 1. Purpose & Precedence
Working Groups (WGs) are where Akrites performs its core technical work: analyzing, patching, testing, and coordinating fixes for vulnerabilities in upstream open-source projects. This section defines the formal rules, voting rights, lifecycle, and governance obligations for all Akrites Working Groups.

In the event of any contradiction or inconsistency between this Governance Policy and tactical operational documents (including day-to-day member operating guides), this Governance Policy takes precedence.

---

### 2. Types of Working Groups
Working Groups are organized by purpose. The type dictates duration, scope, leadership expectations, and lifecycle management:

| Type | Purpose | Expected Duration | Examples |
| :--- | :--- | :--- | :--- |
| **Technology or Component** | Ongoing coverage of a critical upstream project or component family. | Standing (reviewed every 6 months). | Kernel, OpenSSL, Apache ecosystem |
| **Sector or Vertical** | Cross-cutting security concerns for a specific industry or deployment context. | Standing (reviewed every 6 months). | Critical infrastructure, automotive, telco |
| **Critical Incident** | Rapid response to a specific high-severity vulnerability or incident. | Ephemeral (weeks to months). | A specific CVE requiring multi-party coordination |
| **Clearinghouse Coordination** | Cross-WG coordination, deduplication, and triage routing. | Standing. | The SIRT intake function |
| **Enablement or Practice** | Developing tooling, processes, and best practices for use across WGs. | Standing (reviewed every 6 months). | Shared CI/build tooling, process enablement |

---

### 3. Chair and Co-Chair Roles

#### 3.1 Responsibilities
The Chair is an organizer and point of contact, not a manager. Responsibilities include:
* **Triage Decisions**: Maintaining and driving a visible vulnerability triage queue, prioritizing which vulnerabilities the WG works on next.
* **Read-In Nominations**: Nominating new members to the SIRT for read-in when the WG needs additional expertise.
* **Coordination with the SIRT**: Acting as the primary liaison between the WG and the SIRT case lead. Reporting status, escalating blockers, and ensuring hand-off checklists are complete before cases move to upstream engagement.
* **Keeping the WG Functional**: Maintaining the private repository and read-in list, ensuring the agreed working cadence is followed, and flagging inactive members.
* **Escalation**: Raising issues the WG cannot resolve internally: disputed findings, cross-WG overlaps, resource shortfalls, or cases that may require Maintainer of Last Resort (MoLR) consideration.

#### 3.2 Non-Responsibilities
A Chair does **not**:
* Override the SIRT on read-in decisions, embargo timelines, or upstream engagement.
* Unilaterally disclose or publish case material or advisories.
* Make policy decisions that belong to the Governing Board.
* Represent the WG to external parties (external representation is handled by the SIRT).

#### 3.3 Co-Chairs & Interim Chairs
* **Co-Chairs**: Every standing WG must have a Co-Chair. Ephemeral WGs with more than 3 members must also designate one. The Co-Chair shares the Chair's responsibilities and acts in their absence.
* **Organizational Separation**: The Co-Chair **must be from a different member organization** than the Chair to ensure continuity and prevent single-organization dependency.
* **Foundation Staff Review**: Where either the Chair or Co-Chair is employed by the foundation or its fiscal sponsor ("staff"), the other role should be filled by a non-staff member organization whenever possible. WGs where both leadership roles are held by staff are flagged to the Governing Board for review.
* **Interim Chairs**: When a WG has no Chair or Co-Chair (due to vacancy, removal, or new WG formation), the SIRT designates an Interim Chair from among existing WG members. Interim appointments are time-bounded to **30 days**, during which a permanent Chair selection must be completed. If no Chair is selected within 30 days, the SIRT escalates to the Governing Board.

---

### 4. Chair Selection, Terms & Diversity

#### 4.1 Eligibility Requirements
A Chair candidate must:
* Be an active member in good standing of the WG (active contributor, all read-in prerequisites met).
* Demonstrate relevant technical domain expertise for the WG's scope.
* Have explicit member organization support for the required time commitment.
* Not hold Chair roles in more than **two WGs simultaneously**.
* Comply with the organizational diversity cap (§4.4).

#### 4.2 Selection Process
1. **Nomination**: Any WG member may nominate themselves or another willing member. The outgoing Chair, the SIRT, or the Governing Board may also nominate candidates. Nominations remain open for **10 business days**.
2. **Discussion Period**: Candidates state their qualifications and time commitment; WG members may submit questions.
3. **Consensus & Voting**: The WG seeks consensus on selection. If consensus cannot be reached, a **simple majority vote** among active WG members decides. Ties are broken by the SIRT.
4. **Confirmation**: The SIRT confirms and records the selection. No formal Governing Board approval is required for Chair appointments, but the Board is notified.

#### 4.3 Term Length and Rotation Limits
* **Term Length**: **12 months**.
* **Consecutive Limit**: A Chair may serve a maximum of **two consecutive terms (24 months total)** in the same WG, after which they must stand down for at least **12 months** before becoming eligible for re-selection in that WG.
* **Renewal Process**: At the end of each term, the SIRT opens a 10-business-day renewal window. If no alternative candidate is nominated and no member objects, the incumbent is renewed for a second term. If an alternative is nominated or a member objects, the full selection process (§4.2) runs. Incumbents hold no procedural advantage.
* **Stepping Down**: A Chair may step down at any time by written notice to the SIRT and WG. The Co-Chair assumes the Chair role and the 30-day vacancy process (§3.3) begins for a new Co-Chair.

#### 4.4 Organizational Diversity Cap
No single member organization may hold the Chair role in more than **one-third (1/3) of all standing WGs** (rounded up). If an organization reaches this threshold, candidates from that organization are ineligible for Chair selection in additional WGs until the ratio is restored. The SIRT maintains and publishes a current list of Chair assignments by organization to enforce this rule.

---

### 5. Accountability, Stalls & Chair Removal

#### 5.1 Measurement of Accountability
Chairs are accountable for keeping their WG operational, measured by:
* **Active Queue Movement**: Vulnerabilities assigned to the WG are actively prioritized and worked, or explicitly deferred with documented rationale.
* **Status Visibility**: Current work, blockers, and dependencies are clearly tracked.
* **Communication Cadence**: The WG maintains its agreed working cadence. Silence for more than two weeks without explanation constitutes a stall signal.
* **Current Read-In List**: Inactive members are regularly flagged for access revocation.

#### 5.2 Stall Escalation Protocol
A WG is considered stalled when untriaged vulnerabilities accumulate without action and no communication explains the delay:
1. **Week 1 (SIRT Inquiry)**: The SIRT contacts the Chair to identify root causes and blockers.
2. **Week 2 (Remediation Plan)**: The Chair provides a written plan detailing blockers, resource requirements, and a target date to resume active triage. The SIRT may offer additional read-ins, reassign cases, or supply direct support.
3. **Week 3 (Governing Board Notification)**: If inactivity persists without a credible remediation plan, the SIRT notifies the Governing Board with triage queue counts, inactivity logs, and Chair responses. The Board may direct remedial action, reassign the Chair, or initiate WG archival.

#### 5.3 Chair Removal
A Chair may be removed by:
* **The Governing Board**, for cause (sustained inactivity, breach of confidentiality, or failure to maintain the WG).
* **A Two-Thirds (2/3) Vote of Active WG Members**, submitted to the SIRT, which confirms the vote and opens the vacancy process.

Removal is non-punitive by default; it exists to ensure stalled WGs regain leadership when a Chair is unable to step down voluntarily.

---

### 6. WG Creation & Minimum Viable WG

#### 6.1 Creation Triggers
A new WG is warranted when:
* A critical upstream project or component family requires ongoing security coverage not provided by existing WGs.
* A vulnerability or incident requires cross-organization coordination exceeding existing WG scopes.
* A sector or vertical has security concerns cutting across multiple technology WGs.
* An enablement or practice area (tooling, processes, standards) requires dedicated focus.

#### 6.2 Approval Authority
* **Standing WGs**: Require formal Governing Board approval based on a submitted proposal detailing scope, type, standing justification, proposed Chair/Co-Chair, initial member list, and covered upstream domains.
* **Ephemeral WGs**: May be created directly by the SIRT to address urgent incidents. The SIRT notifies the Governing Board within **5 business days**.

#### 6.3 Minimum Viable WG
Every active WG must maintain at least:
* A Chair and a Co-Chair (from different member organizations for standing WGs).
* Two additional members with relevant domain expertise.
* Representation from at least **two distinct member organizations**.

Any WG falling below these minimums for more than **30 days** enters the stall escalation path (§5.2).

---

### 7. WG Lifecycle, Archival & Member Retirement

#### 7.1 Ephemeral WGs
An ephemeral WG has a defined end condition stated at creation (e.g., disclosure completed, fix shipped, or incident resolved). When met:
1. The Chair confirms all hand-off checklists are complete.
2. Open cases are transferred to a standing WG or closed.
3. The SIRT archives the WG's private repository (read-only) and closes dedicated Slack channels.
4. Read-in grants for that specific WG expire per the Read-In Policy.

#### 7.2 Standing WG Review & Archival
Standing WGs are formally reviewed every **6 months** by the Governing Board to evaluate scope relevance, triage throughput, membership levels, and organizational diversity.

A standing WG is archived when:
* The Governing Board determines its scope is no longer relevant.
* Membership remains below minimum viability (§6.3) for more than 30 days.
* The 6-month review recommends retirement.

Archival sets the private repository to read-only, closes Slack/mailing channels, transfers open cases, and preserves advisories and historical case logs.

#### 7.3 Member Retirement
Individual members who cease active contribution are retired from the WG:
1. The Chair flags the inactive member to the SIRT.
2. The SIRT revokes repository, channel, and case access.
3. The case read-in log and Security Rolodex are updated accordingly.

---

### 8. Reporting & Governance Interfaces

#### 8.1 Triage Metrics
Each WG Chair reports the following counts to the SIRT weekly (or on an agreed cadence):
* Count of vulnerabilities pending triage.
* Count of vulnerabilities in active remediation.
* Count of cases handed off to the SIRT for upstream engagement.
* Any active blockers or resource shortfalls.

#### 8.2 Governing Board & TOC Interfaces
* **SIRT to Board**: The SIRT provides periodic summaries covering WG triage throughput, stall escalations, Chair vacancies, and creation/archival actions.
* **Transition to TOC**: When the Technical Oversight Committee (TOC) is fully constituted, decision-making authority for standing WG creation, 6-month reviews, stall escalations, and Chair removals will transfer from the Governing Board to the TOC.

---

# Part II: Operational Execution & Logistics

### 9. Core Definitions & Ground Rules

#### 9.1 Operational Definitions
* **Intake**: The SIRT's process for receiving reports, deduplicating them, and processing qualified reports as a Case.
* **Intake Material**: Data compiled by the SIRT during Intake and shared with WGs.
* **Case**: An Intake matter classified by the SIRT for further processing and remediation.
* **Case Material**: Data generated by the WG while analyzing, testing, or building patches/mitigations.
* **Upstream**: The original open-source project owning the software being worked on.

#### 9.2 Non-Negotiable Ground Rules
1. **Strict TLP Handling**: Treat all Case Material as **TLP:AMBER+STRICT** (shareable only within your organization on a need-to-know basis). Treat Finder and Intake Material as **TLP:RED** (named recipients only).
2. **Named Parties Only**: Discuss a case *only* with individuals explicitly read into that specific case. Un-read-in individuals do not exist with respect to the case.
3. **Work Stays Private**: All technical artifacts reside in the WG's private repository until formal upstream coordination at public disclosure. Never commit fixes to public forks or branches ahead of time.
4. **No Sensitive Artifacts in Chat or Email**: Never paste exploit code, PoCs, or raw patches into Slack or unencrypted email. Use private repository attachments.
5. **Environment Containment & 2FA**: Hardware-key 2FA is required for repository, Slack, and mailing list access. Do not copy Case Material to personal accounts or unapproved local machines.
6. **Immediate Embargo Break Escalation**: Report any suspected or actual embargo break to the SIRT immediately. Embargo breaches result in immediate access suspension and referral to the Governing Board for permanent program removal.

---

### 10. WG Setup Procedure (One-Time)

The SIRT provisions three private spaces for each new WG: a **GitHub repository**, a **Slack channel** (`#wg-<name>`), and a **mailing list**.

#### Setup Checklist
0. **Submit Notification**: Email **`SIRT@Akrites.dev`** with the subject `New-Akrites-WG` containing:
   * WG Name, Purpose/Charter, and Scope.
   * WG Type (Technology, Sector, Critical Incident, Clearinghouse, or Enablement).
   * Initial Chair and Co-Chair names and contact details.
   * Member invitation list and specific engineering resource needs (e.g., protocol developers, test engineers).
1. **Develop Charter**: Define the formal purpose and domain boundary.
2. **Announce Internally**: Post an announcement in `#all-akrites` calling for qualified member participation.
3. **Establish Initial Leadership**:
   * *Private WGs*: Akrites SIRT Director acts as initial Chair until selection (§4) completes.
   * *Public WGs*: Akrites Program Manager acts as initial Chair until selection (§4) completes.
4. **Agree on Cadence**: Establish working norms (e.g., async repository tracking plus short weekly syncs) and assign functional roles (analysis, patching, testing).
5. **Verify Access**: Ensure all members complete hardware-key 2FA setup.

---

### 11. Member Nomination & Read-In

Working Group members **cannot** add individuals directly to repositories, Slack channels, or mailing lists. 

#### Nomination Workflow
1. **Apply Self-Check**: Confirm the candidate satisfies both:
   * **Need-to-Know**: Case or domain genuinely requires their specific expertise.
   * **Capacity to Contribute**: Candidate will actively analyze/patch, test, or stage fixes.
2. **Submit Nomination**: Email **`SIRT@Akrites.dev`** with the candidate's name, organizational affiliation, and assigned role.
3. **SIRT Verification & Access**: The SIRT verifies prerequisites (2FA, signed agreements, Three-Gate Test) and grants scoped access.

---

### 12. Vulnerability Ingestion & Remediation Workflow

#### Step-by-Step Remediation Lifecycle
1. **Validate & Dedupe**: Search existing repository issues and notify the SIRT to run deduplication checks before beginning work.
2. **Open Finding Issue**: Create a new issue in the WG repository using the **Vulnerability Finding Template** (Appendix).
3. **Attach Sensitive Artifacts**: Upload PoCs, reproduction scripts, and patch drafts as private repository attachments or private branch commits (never in Slack).
4. **Analyze & Characterize**: Determine root cause (CWE), affected version bounds, and preliminary severity (CVSS v4.0).
5. **Build the Fix**: Develop patches or mitigations in private branches under open-source compatible licenses, adhering to DCO / Signed-off-by requirements for frictionless upstream adoption.
6. **Test**: Run regression tests to verify the fix resolves the root cause without introducing regressions.
7. **Draft CVD Rollout Plan**: Formulate recommendations for embargo window, target Public Disclosure (PD) date, and read-in list.
8. **Hand-Off to SIRT**: Notify the SIRT that the case is ready for Vulnerability Disclosure Report (VDR) generation and upstream engagement.

> ⚠️ **Strict Boundary**: Working Group members **do not contact upstream maintainers directly**. The SIRT acts as the single point of contact to upstream maintainers, co-coordinating with relevant WG members as appropriate.

---

### 13. When to Call the SIRT

Working Group members handle day-to-day analysis independently, but MUST contact the SIRT for:
* Reading new individuals into the WG or a specific case.
* Cross-WG overlap or deduplication questions.
* Requesting an embargo or public disclosure window extension.
* Handling disputed findings, rejected patches, or unresolved technical disagreements.
* Handing cases off for upstream maintainer engagement.
* Reporting any actual or suspected embargo break (**immediate requirement**).

---

### 14. Upstream Hand-Off Checklist

Before passing a case to the SIRT for upstream engagement, confirm the following items:
* [ ] Finding validated and deduplicated against active cases.
* [ ] Patch and/or mitigation developed in private branch.
* [ ] Fix tested (resolves root cause, zero regressions).
* [ ] Read-in list, embargo window, and target PD date proposed.
* [ ] Finding issue template complete and current.

---

## Appendix: Vulnerability Finding Issue Template

*Paste the following markdown block into new GitHub issues within the WG private repository. Do not paste working exploit code inline; link to private branches or encrypted repo attachments.*

```markdown
## Summary
One or two sentences describing the vulnerability.

## Affected Project / Component
- Project:
- Component / module:
- Affected versions:
- Package / ecosystem:

## Type
- CWE (if known):

## Preliminary Severity
- CVSS vector / score (best estimate):
- Notes on real-world impact (e.g., critical for a specific vertical):

## Reproduction
Link to private branch / attachment with steps and PoC (do NOT paste exploit code here):

## Impact
What an attacker can achieve; scope and blast radius:

## Suspected Fix Approach
Patch idea, mitigation, or workaround under consideration:

## Finder & Attribution
- Finder:
- Credit preference (named / clearinghouse / anonymous):

## Handling
- TLP: (RED / AMBER+STRICT)
- Dedupe check done: (yes / no — link)
- Additional read-ins needed (role): (analyze-patch / test / stage)
```
