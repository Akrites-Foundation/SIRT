# Working Group Governance Policy

**Type:** Policy
**Owner:** Akrites SIRT
**Approver:** SIRT Director
**Status:** Draft — for Akrites SIRT review
**Formerly titled:** Working Group Governance and Operations Guide (Part I)
**Applies to:** All Akrites Working Group (WG) Chairs, Co-Chairs, and Read-In Members
**Related:** [Working Group Operating Procedure](../procedures/wg-operating-procedure.md), [Read-In Policy](read-in-policy.md)
**Precedence:** This policy governs structure, voting, and leadership rules. Where it conflicts with the [Working Group Operating Procedure](../procedures/wg-operating-procedure.md), this policy takes precedence.

---

## 1. Purpose & Precedence
Working Groups (WGs) are where Akrites performs its core technical work: analyzing, patching, testing, and coordinating fixes for vulnerabilities in upstream open-source projects. This section defines the formal rules, voting rights, lifecycle, and governance obligations for all Akrites Working Groups.

**Working Groups are convened as needed.** There are no standing Working Groups at present. The SIRT convenes a WG for a specific case, incident, or defined need, and it ends when the end condition stated at creation is met (§7). The rules drafted for standing WGs are kept in §9 in case the Governing Board approves one; they do not apply today.

In the event of any contradiction or inconsistency between this Governance Policy and tactical operational documents (including the [Working Group Operating Procedure](../procedures/wg-operating-procedure.md)), this Governance Policy takes precedence.

---

## 2. Working Groups

Every WG today is an **as-needed WG**: convened by the SIRT for a specific case, incident, or defined need, with an end condition stated at creation.

| Type | Purpose | Expected Duration | Examples |
| :--- | :--- | :--- | :--- |
| **As-needed** | Analysis, patching, testing, and coordination for a specific case, incident, or defined need. | Ephemeral (weeks to months), ending at the condition stated at creation. | A specific CVE requiring multi-party coordination; a declared Crit-Sit |

Standing WG types are described in §9 and are not in use.

---

## 3. Chair and Co-Chair Roles

### 3.1 Responsibilities
The Chair is an organizer and point of contact, not a manager. Responsibilities include:
* **Triage Decisions**: Maintaining and driving a visible vulnerability triage queue, prioritizing which vulnerabilities the WG works on next.
* **Read-In Nominations**: Nominating new members to the SIRT for read-in when the WG needs additional expertise.
* **Coordination with the SIRT**: Acting as the primary liaison between the WG and the SIRT case coordinator. Reporting status, escalating blockers, and ensuring hand-off checklists are complete before cases move to upstream engagement.
* **Keeping the WG Functional**: Maintaining the private repository and read-in list, ensuring the agreed working cadence is followed, and flagging inactive members.
* **Escalation**: Raising issues the WG cannot resolve internally: disputed findings, cross-WG overlaps, resource shortfalls, or cases that may require Maintainer of Last Resort (MoLR) consideration.

### 3.2 Non-Responsibilities
A Chair does **not**:
* Override the SIRT on read-in decisions, embargo timelines, or upstream engagement.
* Unilaterally disclose or publish case material or advisories.
* Make policy decisions that belong to the Governing Board.
* Represent the WG to external parties (external representation is handled by the SIRT).

### 3.3 Co-Chairs & Replacement Chairs
* **Co-Chairs**: An as-needed WG with more than 3 members must designate a Co-Chair. The Co-Chair shares the Chair's responsibilities and acts in their absence.
* **Organizational Separation**: The Co-Chair **must be from a different member organization** than the Chair to ensure continuity and prevent single-organization dependency.
* **Foundation Staff Review**: Where either the Chair or Co-Chair is employed by the foundation or its fiscal sponsor ("staff"), the other role should be filled by a non-staff member organization whenever possible. WGs where both leadership roles are held by staff are flagged to the Governing Board for review.
* **Replacement Chairs**: If an as-needed WG's Chair steps down or is removed, the SIRT Director or Technical PgM Director designates a replacement from among the WG's members.

---

## 4. Chair Designation

### 4.1 Eligibility Requirements
A Chair candidate must:
* Be an active member in good standing of the WG (active contributor, all read-in prerequisites met).
* Demonstrate relevant technical domain expertise for the WG's scope.
* Have explicit member organization support for the required time commitment.
* Not hold Chair roles in more than **two WGs simultaneously**.

### 4.2 Designation
The SIRT Director or the Technical Program Management (PgM) Director designates the Chair, and a Co-Chair where §3.3 requires one, when the WG is created, after consulting the proposed members and their member organizations. The SIRT records the designation and includes it in the creation notice to the Governing Board (§6.2).

### 4.3 Stepping Down
A Chair may step down at any time by written notice to the SIRT and WG. The Co-Chair, if there is one, assumes the Chair role; otherwise the SIRT Director or Technical PgM Director designates a replacement (§3.3).

---

## 5. Accountability, Stalls & Chair Removal

### 5.1 Measurement of Accountability
Chairs are accountable for keeping their WG operational, measured by:
* **Active Queue Movement**: Vulnerabilities assigned to the WG are actively prioritized and worked, or explicitly deferred with documented rationale.
* **Status Visibility**: Current work, blockers, and dependencies are clearly tracked.
* **Communication Cadence**: The WG maintains its agreed working cadence. Silence for more than two weeks without explanation constitutes a stall signal.
* **Current Read-In List**: Inactive members are regularly flagged for access revocation.

### 5.2 Stall Escalation Protocol
A WG is considered stalled when untriaged vulnerabilities accumulate without action and no communication explains the delay:
1. **Week 1 (SIRT Inquiry)**: The SIRT contacts the Chair to identify root causes and blockers.
2. **Week 2 (Remediation Plan)**: The Chair provides a written plan detailing blockers, resource requirements, and a target date to resume active triage. The SIRT may offer additional read-ins, reassign cases, or supply direct support.
3. **Week 3 (Governing Board Notification)**: If inactivity persists without a credible remediation plan, the SIRT notifies the Governing Board with triage queue counts, inactivity logs, and Chair responses. The Board may direct remedial action, reassign the Chair, or initiate WG archival.

### 5.3 Chair Removal
A Chair may be removed by:
* **The Governing Board**, for cause (sustained inactivity, breach of confidentiality, or failure to maintain the WG).
* **A Two-Thirds (2/3) Vote of Active WG Members**, submitted to the SIRT, which confirms the vote and opens the vacancy process.

Removal is non-punitive by default; it exists to ensure stalled WGs regain leadership when a Chair is unable to step down voluntarily.

---

## 6. WG Creation & Minimum Viable WG

### 6.1 Creation Triggers
An as-needed WG is warranted when a case, incident, or defined need requires analysis, patching, or testing expertise, or cross-organization coordination, beyond what the SIRT and the case's read-in participants can provide.

### 6.2 Approval Authority
As-needed WGs are created directly by the SIRT. The SIRT notifies the Governing Board within **5 business days**.

### 6.3 Minimum Viable WG
Every active WG must maintain at least:
* A Chair, and a Co-Chair where §3.3 requires one.
* Two additional members with relevant domain expertise.
* Representation from at least **two distinct member organizations**.

Any WG falling below these minimums for more than **30 days** enters the stall escalation path (§5.2).

---

## 7. WG Lifecycle, Archival & Member Retirement

### 7.1 End of an As-Needed WG
An ephemeral WG has a defined end condition stated at creation (e.g., disclosure completed, fix shipped, or incident resolved). When met:
1. The Chair confirms all hand-off checklists are complete.
2. Open cases are closed or returned to the SIRT.
3. The SIRT archives the WG's private repository (read-only) and closes dedicated Slack channels.
4. Read-in grants for that specific WG expire per the Read-In Policy.

### 7.2 Member Retirement
Individual members who cease active contribution are retired from the WG:
1. The Chair flags the inactive member to the SIRT.
2. The SIRT revokes repository, channel, and case access.
3. The case read-in log and Security Rolodex are updated accordingly.

---

## 8. Reporting & Governance Interfaces

### 8.1 Triage Metrics
Each WG Chair reports the following counts to the SIRT weekly (or on an agreed cadence):
* Count of vulnerabilities pending triage.
* Count of vulnerabilities in active remediation.
* Count of cases handed off to the SIRT for upstream engagement.
* Any active blockers or resource shortfalls.

### 8.2 Governing Board Interface
* **SIRT to Board**: The SIRT provides periodic summaries covering WG triage throughput, stall escalations, Chair vacancies, and creation/archival actions.

---

## 9. Standing Working Groups (deferred)

No standing WG exists and none is being formed. The rules below were drafted for standing WGs and are kept so they are available if the Governing Board approves one. Until then, none of this applies.

### 9.1 Standing WG types

| Type | Purpose | Expected Duration | Examples |
| :--- | :--- | :--- | :--- |
| **Technology or Component** | Ongoing coverage of a critical upstream project or component family. | Standing (reviewed every 6 months). | Kernel, OpenSSL, Apache ecosystem |
| **Sector or Vertical** | Cross-cutting security concerns for a specific industry or deployment context. | Standing (reviewed every 6 months). | Critical infrastructure, automotive, telco |
| **Clearinghouse Coordination** | Cross-WG coordination, deduplication, and triage routing. | Standing. | The SIRT intake function |
| **Enablement or Practice** | Developing tooling, processes, and best practices for use across WGs. | Standing (reviewed every 6 months). | Shared CI/build tooling, process enablement |

### 9.2 Creation and approval

A standing WG is warranted when:
* A critical upstream project or component family requires ongoing security coverage not provided by existing WGs.
* A sector or vertical has security concerns cutting across multiple technology WGs.
* An enablement or practice area (tooling, processes, standards) requires dedicated focus.

* **Standing WGs**: Require formal Governing Board approval based on a submitted proposal detailing scope, type, standing justification, proposed Chair/Co-Chair, initial member list, and covered upstream domains.

### 9.3 Co-Chairs and interim Chairs

* **Co-Chairs**: Every standing WG must have a Co-Chair, and the Co-Chair must be from a different member organization than the Chair.
* **Interim Chairs**: When a WG has no Chair or Co-Chair (due to vacancy, removal, or new WG formation), the SIRT designates an Interim Chair from among existing WG members. Interim appointments are time-bounded to **30 days**, during which a permanent Chair selection must be completed. If no Chair is selected within 30 days, the SIRT escalates to the Governing Board.

### 9.4 Chair selection, terms & diversity

#### Selection process
1. **Nomination**: Any WG member may nominate themselves or another willing member. The outgoing Chair, the SIRT, or the Governing Board may also nominate candidates. Nominations remain open for **10 business days**.
2. **Discussion Period**: Candidates state their qualifications and time commitment; WG members may submit questions.
3. **Consensus & Voting**: The WG seeks consensus on selection. If consensus cannot be reached, a **simple majority vote** among active WG members decides. Ties are broken by the SIRT.
4. **Confirmation**: The SIRT confirms and records the selection. No formal Governing Board approval is required for Chair appointments, but the Board is notified.

#### Terms and rotation
* **Term Length**: **12 months**.
* **Consecutive Limit**: A Chair may serve a maximum of **two consecutive terms (24 months total)** in the same WG, after which they must stand down for at least **12 months** before becoming eligible for re-selection in that WG.
* **Renewal Process**: At the end of each term, the SIRT opens a 10-business-day renewal window. If no alternative candidate is nominated and no member objects, the incumbent is renewed for a second term. If an alternative is nominated or a member objects, the full selection process above runs. Incumbents hold no procedural advantage.

#### Organizational diversity cap
No single member organization may hold the Chair role in more than **one-third (1/3) of all standing WGs** (rounded up). If an organization reaches this threshold, candidates from that organization are ineligible for Chair selection in additional WGs until the ratio is restored. The SIRT maintains and publishes a current list of Chair assignments by organization to enforce this rule.

### 9.5 Review and archival

Standing WGs are formally reviewed every **6 months** by the Governing Board to evaluate scope relevance, triage throughput, membership levels, and organizational diversity.

A standing WG is archived when:
* The Governing Board determines its scope is no longer relevant.
* Membership remains below minimum viability (§6.3) for more than 30 days.
* The 6-month review recommends retirement.

Archival sets the private repository to read-only, closes Slack/mailing channels, transfers open cases, and preserves advisories and historical case logs.
