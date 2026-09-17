# Akrites Working Group Governance Policy - DRAFT v0.1

**Status:** Draft for review
**Addresses:** Issue #35 ("Working Group about Working Groups"), with implications for #41 (WG archival) and #42 (member retirement)

**Relationship to existing docs:** This policy governs the creation, leadership, accountability, and lifecycle of Working Groups. The [Working Group Operating Guide](./Akrites_WorkingGroup_Operating_Guide.md) remains the day-to-day reference for WG members. The [Read-In Process](./SIRT%20Read-in%20Guidelines.md) and [Read-In Tier Policy](./Read-in%20Tier%20Policy.md) govern access. This policy governs structure.

---

## 1. Purpose

Working Groups are where Akrites does its core work: analyzing, patching, testing, and coordinating fixes for vulnerabilities in upstream open source projects. The Operating Guide tells WG members how to do that work. This policy defines who leads it, how they are selected, what authority they hold, and what happens when a WG is not functioning.

Without defined leadership roles and accountability, WGs stall. Vulnerabilities sit untriaged. Members wait for direction that does not arrive. This policy exists to prevent that.

---

## 2. Types of Working Groups

Working Groups are organized by purpose. The type determines duration, scope, and leadership expectations.

| Type | Purpose | Expected duration | Examples |
|------|---------|-------------------|----------|
| **Technology or component** | Ongoing coverage of a critical upstream project or component family | Standing (reviewed annually) | Kernel, OpenSSL, Apache ecosystem |
| **Sector or vertical** | Cross-cutting security concerns for a specific industry or deployment context | Standing (reviewed annually) | Critical infrastructure, automotive, telco |
| **Critical incident** | Rapid response to a specific high-severity vulnerability or incident | Ephemeral (weeks to months) | A specific CVE requiring multi-party coordination |
| **Clearinghouse coordination** | Cross-WG coordination, deduplication, and triage routing | Standing | The SIRT intake function |
| **Enablement or practice** | Developing tooling, processes, and best practices for use across WGs | Standing (reviewed annually) | This "WG of WGs," shared CI/build tooling |

These types originate from the Operating Guide's WG creation form. The distinction matters for lifecycle management (section 7): ephemeral WGs have a defined end condition, standing WGs have periodic reviews.

---

## 3. Chair and co-chair roles

### 3.1 What a chair does

The chair is an organizer and point of contact, not a manager. The Operating Guide established this framing. This policy makes it operational.

**A chair is responsible for:**

- **Triage decisions.** Prioritizing which vulnerabilities the WG works on next. For standing WGs, this means maintaining a visible queue and driving it forward, not waiting for external direction.
- **Read-in nominations.** Nominating new members to the SIRT for read-in when the WG needs additional expertise. The SIRT still verifies and grants access (per the Read-In Process), but the chair initiates.
- **Coordination with the SIRT.** Acting as the primary liaison between the WG and the SIRT case lead. Reporting status, escalating blockers, and ensuring hand-off checklists are complete before cases move to upstream engagement.
- **Keeping the WG functional.** Maintaining the repo and read-in list, ensuring the agreed working cadence is followed, and identifying when members are inactive or when the WG needs additional capacity.
- **Escalation.** Raising issues the WG cannot resolve internally: disputed findings, cross-WG overlaps, resource shortfalls, or cases that may require MoLR consideration.

**A chair does not:**

- Override the SIRT on read-in decisions, embargo timelines, or upstream engagement
- Unilaterally disclose or publish anything
- Make policy decisions that belong to the Governing Board
- Represent the WG to external parties (that is the SIRT's role)

### 3.2 Co-chair

Every standing WG must have a co-chair. Ephemeral WGs should designate one when membership exceeds three people.

The co-chair shares the chair's responsibilities and can act in the chair's absence. The co-chair must be from a different member organization than the chair to ensure continuity and reduce single-organization dependency. Where one of the chair or co-chair is employed by the foundation or its fiscal sponsor ("staff"), the other should be from a non-staff member organization whenever possible. WGs where both leadership roles are held by staff should be flagged to the Governing Board for review.

### 3.3 Interim chair

When a WG has no chair or co-chair (vacancy, removal, or new WG formation), the SIRT designates an interim chair from among existing WG members. The interim appointment is time-bounded to 30 days, during which a permanent selection must be completed per section 4. If no permanent chair is selected within 30 days, the SIRT escalates to the Governing Board.

---

## 4. Chair selection

### 4.1 Eligibility

A chair candidate must:

- Be a member in good standing of the WG (active contributor, all read-in prerequisites met)
- Have demonstrated domain expertise relevant to the WG's scope
- Have their member organization's support for the time commitment
- Not hold chair roles in more than two WGs simultaneously
- Meet the organizational diversity constraint in section 4.4

### 4.2 Selection process

1. **Nomination.** Any WG member may nominate themselves or another willing member. The outgoing chair, the SIRT, or the Governing Board may also nominate candidates.
2. **Discussion period.** Nominations are open for 10 business days. Candidates state their qualifications and time commitment. WG members may ask questions.
3. **Consensus.** The WG seeks consensus on the selection. If consensus is not reached, a simple majority vote among active WG members decides. Ties are broken by the SIRT.
4. **Confirmation.** The SIRT confirms the selection and records it. No Governing Board approval is required for chair appointments, but the Board is notified.

### 4.3 Term and rotation

Chair terms are 12 months. A chair may serve a maximum of two consecutive terms (24 months) in the same WG, after which they must stand down for at least one full term (12 months) before being eligible for re-selection in that WG. This limit exists to prevent institutional capture and ensure leadership opportunities rotate across the membership.

**Renewal process.** At the end of each term, the SIRT opens a 10-business-day renewal window. Any WG member may nominate an alternative candidate during this window. If no alternative is nominated and no member objects, the incumbent is renewed for a second term. If an alternative is nominated or any member objects, the full selection process in 4.2 runs. Incumbents may run but hold no procedural advantage.

**Stepping down.** A chair may step down at any time by notifying the SIRT and the WG. The co-chair assumes the role and the vacancy process in 3.3 begins for a new co-chair.

### 4.4 Organizational diversity of chairs

No single member organization may hold the chair role in more than one-third of all standing WGs, rounded up. If an organization already chairs one-third or more of standing WGs, candidates from that organization are ineligible for chair selection in additional WGs until the ratio is restored. This constraint does not apply to co-chair roles but the spirit of organizational diversity should be maintained there as well.

The SIRT maintains and publishes a current list of chair assignments by organization to make this constraint transparent and enforceable.

---

## 5. Accountability

### 5.1 What the chair is accountable for

The chair is accountable for keeping the WG operational. The following are the measurable indicators:

- **Triage queue is moving.** Vulnerabilities assigned to the WG are being actively prioritized and worked, or explicitly deferred with documented rationale.
- **Status is visible.** The SIRT and WG members can see what the WG is working on, what is blocked, and what is waiting.
- **Communication cadence is maintained.** The WG meets its agreed working cadence (defined in the Operating Guide at WG setup). Silence for more than two weeks without explanation is a signal that something is wrong.
- **Read-in list is current.** Inactive members are flagged for removal per the Operating Guide and issue #42 (member retirement process, once defined).

### 5.2 What happens when a WG stalls

A WG is considered stalled when untriaged vulnerabilities accumulate without action and no communication explains why. The escalation path:

1. **SIRT inquiry (week 1).** The SIRT contacts the chair to understand the situation. Common causes: chair is unavailable, WG lacks capacity, the work is blocked on an external dependency. Most stalls resolve here.
2. **Remediation plan (week 2).** If the stall continues, the chair provides a written plan: what is blocking the WG, what resources are needed, and a target date for resuming triage. The SIRT may offer additional read-ins, reassign cases to other WGs, or provide direct support.
3. **Governing Board notification (week 3).** If the stall continues without a credible remediation plan, the SIRT notifies the Governing Board with the triage queue count, the timeline of inactivity, and the chair's response (or lack thereof). The Board may direct remedial action, reassign the chair, or initiate WG archival (section 7).

### 5.3 Chair removal

A chair may be removed by:

- **The Governing Board**, for cause (sustained inactivity, breach of confidentiality, failure to maintain the WG)
- **A two-thirds vote of active WG members**, submitted to the SIRT, which confirms the vote and initiates the vacancy process

Removal is not punitive by default. A chair who can no longer commit the time should step down voluntarily (section 4.3). Removal exists for cases where the chair is not stepping down and the WG is suffering as a result.

---

## 6. WG creation

The Operating Guide (section 2) defines the operational steps for creating a WG. This section governs the decision to create one.

### 6.1 When to create a WG

A new WG is warranted when:

- A critical upstream project or component family requires ongoing security coverage and no existing WG covers it
- A vulnerability or incident requires cross-organization coordination that exceeds the scope of an existing WG
- A sector or vertical has security concerns that cut across multiple technology WGs
- An enablement or practice area (tooling, processes, standards) needs dedicated attention

### 6.2 Approval

- **Standing WGs** require Governing Board approval. The proposal must include: scope, type, justification for standing (rather than ephemeral) status, proposed chair and co-chair, initial member list, and the upstream projects or domains covered.
- **Ephemeral WGs** (critical incident response) may be created by the SIRT without Board approval, consistent with the urgency of incident response. The SIRT notifies the Board within 5 business days of creation.

### 6.3 Minimum viable WG

A WG must have at least:

- A chair and a co-chair (from different member organizations for standing WGs)
- Two additional members with relevant domain expertise
- At least two member organizations represented

A WG that falls below these minimums for more than 30 days enters the stall escalation path (section 5.2).

---

## 7. WG lifecycle and archival

### 7.1 Ephemeral WGs

An ephemeral WG has a defined end condition stated at creation (the vulnerability is disclosed and the fix is shipped, the incident is resolved, etc.). When the end condition is met:

1. The chair confirms all hand-off checklists are complete
2. Open cases are transferred to a standing WG or closed
3. The SIRT archives the WG's private repo (read-only) and closes the Slack channel
4. Members' read-in for that WG expires per the Read-In Process (section 6)

### 7.2 Standing WGs

Standing WGs are reviewed annually by the Governing Board. The review considers:

- Whether the WG's scope is still relevant
- Triage throughput and case outcomes over the review period
- Membership levels and organizational diversity
- Whether the WG should be merged with another, split, or archived

### 7.3 Archival

A standing WG is archived when:

- The Governing Board determines its scope is no longer relevant
- Membership falls below the minimum (section 6.3) and cannot be restored within 30 days
- The annual review concludes the WG should be retired

Archival follows the process to be defined under issue #41. At minimum: the repo is set to read-only, the Slack channel is closed, open cases are transferred or closed, and advisories and case records are preserved.

### 7.4 Member retirement

Individual members who are no longer contributing are retired from the WG per the process to be defined under issue #42. At minimum: the chair flags the member, the SIRT revokes access, and the read-in log is updated. Inactivity thresholds and the retirement workflow are deferred to that process.

---

## 8. Reporting and visibility

### 8.1 Triage metrics

Each WG chair reports the following to the SIRT on a cadence agreed at WG creation (default: weekly):

- Count of vulnerabilities pending triage
- Count of vulnerabilities in active work
- Count of cases handed off to the SIRT for upstream engagement in the reporting period
- Any blockers or capacity concerns

The SIRT aggregates these counts across WGs. These counts are the primary input for the stall detection in section 5.2 and for the Governing Board's visibility into WG health.

### 8.2 Governing Board reporting

The SIRT provides the Governing Board with a periodic summary (cadence to be determined) covering:

- WG-level triage throughput and case outcomes
- Stall escalations and their resolution
- Chair vacancies and interim appointments
- WG creation and archival actions

---

## 9. Relationship to other governance bodies

### 9.1 The SIRT

The SIRT is the operational interface between WGs and the rest of Akrites. The SIRT provisions WG infrastructure, manages read-in, coordinates upstream engagement, and monitors WG health. The SIRT does not direct WG technical decisions. WGs are self-organizing within the guardrails of this policy and the Operating Guide.

### 9.2 The Governing Board

The Governing Board approves standing WG creation, conducts annual reviews, resolves stall escalations, and removes chairs for cause. Policy changes to this document require Board approval.

### 9.3 The Technical Oversight Committee

Several Akrites process documents (notably the MoLR Guidelines) assign decision-making authority to a TOC that has not yet been constituted. Where this policy references the Governing Board as the decision-making authority, it does so because no TOC currently exists. If a TOC is stood up, the following responsibilities should be evaluated for transfer from the Board to the TOC:

- Standing WG creation approval
- Annual WG reviews
- Stall escalation resolution
- Chair removal for cause

This section will be updated when the TOC question is resolved.

---


