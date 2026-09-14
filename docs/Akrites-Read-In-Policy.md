# Akrites Read-In Policy

**Status:** DRAFT v0.2 — for TOC / Governing Board review
**Supersedes:** *Akrites Read-In Process — Working Groups & Disclosures* (DRAFT v0.1) and *Akrites Read-In Tier Policy*. On ratification, both source documents are retired and this document is the single authoritative reference.
**Applies to:** All Akrites vulnerability Working Groups (WGs) and all pre-disclosure cases handled by the Akrites SIRT.

---

## 0. Purpose and scope

This policy governs **who is admitted to a pre-disclosure case or Working Group, when they are admitted, and how much they see.**

It answers two questions in sequence:

1. **Admission** — Is this person read in at all? Governed by the **Three-Gate Test** (§2) and the **Prerequisites** (§3). Both must be satisfied; neither substitutes for the other.
2. **Placement** — Given admission, which **tier** do they enter, and how does that tier change as the case evolves? Governed by §4–§6.

**Guiding rule — least privilege, always.** A person is read in only to the specific WG or case they are contributing to, only for as long as their task requires, and never across WGs. Only Akrites staff hold cross-cutting visibility, and only through just-in-time access control after demonstrated and confirmed need.

### 0.1 Governing principles

| Principle | Meaning |
|---|---|
| **Least privilege, need-to-know** | Access shrinks and starts later as the tier number rises. |
| **Minimum sufficient access** | A person is placed in the highest-numbered (least-privileged, latest) tier that still lets them do their job. |
| **No issue is dropped** | Severity is a routing and priority signal — never a filter for dropping a confirmed vulnerability. |
| **Everything is time-bounded and logged** | Every placement, escalation, and exception is justified, approved by a named authority, and recorded in the case read-in log. |
| **Consumers are served at public disclosure** | Being an affected user or a generally interested member is not a basis for read-in. |

---

## 1. Definitions

| Term | Definition |
|---|---|
| **Read-in** | A formal, logged, time-bounded grant of access to a specific case or WG workspace, acknowledged by the recipient before access is enabled. |
| **Tier** | The band that determines *when* a person is read in and *how much* case material they receive. |
| **Disclosure boundary** | What information exists or is shared at a given point in the case. Related to, but distinct from, tier — some activities cannot be performed without a disclosure (you cannot test a patch you have not been given). |
| **Case read-in log** | The authoritative per-case record of every grant, change, and revocation. |
| **Sponsor** | A member organization vouching for an individual, or a delegated authority nominating them for a specific case. |
| **Knowers** | The complete set of individuals read in to a given case at any point in time. |

---

## 2. The Three-Gate Test

**A candidate is read in only if *all three* gates are satisfied.** The gates are conjunctive: failure at any one gate ends the evaluation and the candidate is not read in. Passing all three gates establishes *eligibility* only — the Prerequisites in §3 must also be complete before access is enabled.

The gates are evaluated by the **SIRT case coordinator** and recorded, gate by gate, in the case read-in log.

### Gate 1 — Demonstrable Need-to-Know

> *This specific case, or this specific WG domain, genuinely requires this person.*

Need-to-know must be **demonstrable and case-specific**, not inferred from role, seniority, employer, or standing membership.

**Satisfied by** a written statement, from the nominator, of the specific task this person will perform on **this** case or in **this** WG domain, and why the case cannot proceed as effectively without them.

**Not satisfied by:**

- Being an affected user, downstream consumer, or customer of the affected component.
- General interest, situational awareness, or a desire to "stay informed."
- Membership in Akrites, in the TOC, or in a Working Group, taken on its own.
- Seniority, job title, or executive sponsorship on its own.
- Commercial advantage, procurement, or customer-communication needs.

### Gate 2 — Capacity to Contribute

> *The person is able to perform at least one of the three sanctioned contributions below, on this case.*

| Sanctioned contribution | What it means |
|---|---|
| **Analyze / produce a patch** | Validate the finding and develop the fix — and a workaround or alternative mitigation wherever possible. |
| **Test the patch** | Verify the fix resolves the issue without regressions, in a representative environment. |
| **Stage the patch** | Pre-position the fix for a safe, rapid rollout (e.g., distributor, package registry, CDN). |

**Satisfied by** a nominated sanctioned role plus a credible basis for capability — relevant domain expertise, maintainership of the affected code, an entry in the Security Rolodex, a representative test environment, or operation of the distribution channel in question.

**Capacity means capacity *and* commitment.** A person who can contribute but will not, or cannot within the case timeline, does not clear Gate 2. Contribution is a condition of continued access, not only of entry (§8).

**Not satisfied by** the ability to receive, relay, or act on the information alone — including internal-notification, incident-response-readiness, or triage-for-our-own-products rationales. Those needs are served at public disclosure.

### Gate 3 — Vetted Identity & Organizational Affiliation

> *The person is a known, vetted individual whose identity and organizational affiliation have been confirmed, and who is attributable to an accountable organization.*

**Satisfied by all of:**

1. **Verified named individual.** A real, named human — never a shared, role, team, or distribution account.
2. **Confirmed affiliation.** The person is one of:
   - an engineer of an Akrites member organization, or that member's authorized and approved delegate;
   - an engineer of a designated upstream security team for the affected project; or
   - a nominee of a delegated authority (e.g., a coordinating body such as CISA, or the affected maintainer) for this specific case.
3. **An accountable sponsor of record.** A named sponsoring organization that vouches for the individual and to which conduct and embargo obligations attach.
4. **Exclusion check clear.** The SIRT has affirmatively asked and answered: *is there anyone who should specifically not be read in?* — covering conflicts of interest, competitive or antitrust sensitivity, prior embargo breach, sanctions or legal bars, and case-specific sensitivities.

**Gate 3 is about identity and accountability; §3 is about controls.** Gate 3 asks *who is this person and who answers for them*. The Prerequisites ask *what has this person signed, enabled, and been authorized for*. Both are required.

### 2.1 Applying the gates

- **Gates are evaluated per case, per WG domain.** Clearing the gates once does not clear them for the next case (see §7 for how standing WG membership accelerates, but does not replace, this).
- **The burden of proof is on the nomination**, not on the SIRT. An unclear nomination is returned for more information, not approved provisionally.
- **A failed gate is recorded.** The gate that failed and the reason are logged, so that patterns in nominations can be reviewed.
- **No gate may be waived.** Time pressure is handled through the Emergency Read-In prerequisite path (§3.1) and the escalation path (§9) — never by skipping a gate.

---

## 3. Prerequisites — required before any access is granted

Every person, regardless of tier, must have all of the following before access is enabled. **No prerequisite, no access — even if all three gates in §2 are met.**

1. **A verified, named identity** — an individual, never a shared or role account.
2. **Hardware-key 2FA** enabled on the Akrites environment.
3. **Signed agreements on file** — embargo/NDA, the Akrites Code of Conduct, and the antitrust acknowledgment.
4. **A sponsor** — a member organization vouching for them, or a delegated authority (e.g., a coordinating body such as CISA, or the affected maintainer) nominating them for a specific case.
5. **Authorization from the SIRT**, and access granted to the specific incident.

### 3.1 Emergency Read-In

The SIRT may grant **temporary, time-bounded** access to an external SME sponsored directly by an active maintainer or a Premier Member, using fast electronic agreements where possible and software-based TOTP/MFA, for **up to 72 hours** while hardware-key logistics are processed.

Emergency Read-In relaxes the *mechanism* of prerequisites 2 and 3 — it does **not** relax the Three-Gate Test, the sponsor requirement, the exclusion check, or logging. Access lapses automatically at 72 hours unless the full prerequisites are complete.

---

## 4. The tiers at a glance

| Tier | Who | What they do | Information & TLP | Read-in timing |
|---|---|---|---|---|
| **Tier 0** | Reporter / Finder and the maintainer (plus automated intake) | Originate the report; own the fix and the final disclosure decision | Full case detail; TLP:RED at intake | Earliest; longest duration |
| **Tier 1** | Subject-matter experts (Akrites members) | Analyze, produce, and test the patch | Case material needed to build and test the fix; TLP:AMBER+STRICT | When analysis/testing begins |
| **Tier 2** | Distribution partners / maintainer pre-disclosure rings | Prepare a coordinated downstream release | The fix and timing — not full research detail | Defined lead time before PD |
| **Tier 3** | Second-order distributors (CDNs, package registries) | Pre-stage the fix for rapid propagation | The artifact and go-live time only | Latest; shortest window |
| **Public** | Everyone | — | Fully public | Public disclosure (PD) |

Automated intake — deduplication, severity estimation, and routing — sits within Tier 0 and requires no SME.

### 4.1 Party-to-tier mapping

| Party | Role | Tier | Read-in timing |
|---|---|---|---|
| Reporter / Finder | Provides the finding; may assist analysis | Tier 0 | Earliest, longest access |
| Maintainer | Owns the fix and the final PD decision | Tier 0 | Earliest |
| WG analyst / patch author (SME) | Analyze and produce the patch | Tier 1 | When analysis/patch work begins |
| Patch tester (SME) | Test the patch | Tier 1 | When a testable alpha exists |
| Distribution / staging party | Stage the fix ahead of PD | Tier 2 / Tier 3 | Latest — the minimum lead time consistent with a safe rollout, aligned to standardized, pre-agreed embargo lead times *(working figure: 7–14 days before PD; see Appendix A, item 1)* |
| Affected user / interested member | — | None | Public disclosure |

---

## 5. Tier placement criteria

Every candidate must first clear the Three-Gate Test (§2) and the Prerequisites (§3). Tier is then assigned on **the person's role in resolving this specific case, and the minimum information and lead time that role requires.**

| Tier | You belong here if… |
|---|---|
| **Tier 0** | You originated the report (Finder), or you own the affected code and its fix (maintainer). You need full context from the start. |
| **Tier 1** | You will analyze, write, or test the patch. You need code-level case material, read in when that work begins. |
| **Tier 2** | You operate a distribution channel or pre-disclosure ring that must prepare a coordinated release. You need the fix and the timing, not the underlying research. |
| **Tier 3** | You operate second-order distribution (CDN, registry) that must pre-stage for a rapid rollout. You need the artifact and the go-live time only. |
| **None** | You are an affected user or an interested member with no active role. You are served at public disclosure. |

**Placement rules.**

- **One tier per case.** A person is assigned the single most-restrictive tier sufficient for their role.
- **Role determines tier — not seniority, not membership.** Standing Working Group membership does not by itself grant a tier; a case role does.
- **When a role spans tasks** (e.g., an analyst who also tests), assign the tier of the earliest or broadest task they own.
- **When in doubt, place lower** — higher tier number, later read-in — and escalate if more is genuinely needed.

### 5.1 Tiers vs. disclosure boundaries

A **tier** governs *when* and *how much* a person is read in. A **disclosure boundary** governs *what information exists or is shared* at a point in the case. Each tier receives only the TLP-classified material its task requires: TLP:RED at intake (case team only), TLP:AMBER+STRICT for remediation material.

A detailed **RACI** — the specific actions each tier may take, and by whom — is to be developed as a companion to this policy (Appendix A, item 2).

---

## 6. Read-in workflow (per case)

1. **Nominate.** The Finder, WG, maintainer, or delegated authority proposes a person and states which sanctioned role they will perform.
2. **Verify.** The SIRT case coordinator evaluates and records **each of the three gates** (§2), confirms all prerequisites (§3), and completes the exclusion check.
3. **Approve.** The SIRT case coordinator approves. The Finder and maintainer are consulted on Tier 0 and Tier 1 additions.
4. **Assign tier.** The SIRT **case lead** applies §5 and records the rationale for the tier chosen.
5. **Acknowledge.** The read-in is sent from the SIRT and must be acknowledged by the individual **before** access is enabled.
6. **Grant scoped access.** Access is limited to that single case's private repository and communications channel — nothing else.
7. **Log it.** Record in the case read-in log: who, sponsoring org, role, tier, gate-by-gate determination, approved by, and expiry.
8. **Time-bound.** Set access to expire (§8).

---

## 7. Standing Working Group membership

WG membership is durable read-in scoped to a **domain** rather than a single case, and follows the same rules.

- Only Akrites members and their authorized and approved delegates are eligible to participate.
- **Contribution is a condition of membership.** Access is granted to participants who can actively collaborate to develop and vet a solution to a given issue.
- **All three gates in §2 apply**, evaluated against the WG's focus area; all §3 prerequisites are required.
- The member's expertise is entered in the **Security Rolodex** so the SIRT understands who is available to pull into future cases. Access is always gated by the SIRT and the particulars of a given incident.
- Access is limited to **that WG's** workspace only — never cross-WG.
- Membership is reviewed periodically and removed when the member is no longer contributing.

**Standing membership does not grant automatic read-in to every case in the WG.** Case-level access still follows §6, though it can be near-instant for active members.

**The accelerated path for active members.** An engineer already validated for a standing WG, and recognized for their contributions and domain expertise, is expected to receive read-in approval quickly and without additional paperwork. Concretely, for an active member the SIRT case coordinator may rely on the standing WG record to satisfy **Gate 2** (capacity, already assessed for the domain) and **Gate 3** (identity and affiliation, already verified), and on the existing §3 prerequisites on file. **Gate 1 is always assessed fresh**, against the specific case, and the exclusion check is always re-run. This is a reduction in paperwork, not a waiver of a gate (§2.1).

New members, and members who have been unresponsive or non-contributing for an extended period, follow the full §6 vetting.

Criteria for "active member" will be defined as the SIRT works real cases (Appendix A, item 6).

---

## 8. Time-bounding, expiry, and revocation

- **Tiered windows.** Tier 0 holds access longest; each later tier is read in only at the interval needed to complete its task before PD. Staging parties receive the least lead time consistent with a safe rollout.
- **Default expiry.** Case access ends automatically at public disclosure or case closure, whichever comes first.
- **Immediate revocation** on any of: task complete; departure from the sponsoring organization; need-to-know ends; or breach of the Code of Conduct or the embargo.
- **Continuing to a future case requires a fresh read-in** — or existing standing WG membership, via the accelerated §7 path.

---

## 9. Escalation path

**Triggers.** A change in severity (CVSS rising or falling); a change in scope or blast radius; criticality to a specific vertical (e.g., a CVSS-6 that is critical for telco); a member or Working Group request; or a need for additional resources.

**Levels.**

1. **SIRT case lead.** Adjusts priority, pulls in additional Tier 1 SMEs, or reads a party in earlier — all within existing tier definitions.
2. **TOC.** Cross-cutting or contested calls: vertical-versus-industry severity conflicts, broad-scope resourcing, or spinning up a new Working Group.
3. **Governing Board.** Policy and legal matters: finder patch and customer obligations, antitrust, and government or critical-infrastructure coordination.

**Severity changes.** If the score rises, read-in may widen or accelerate; if it falls, it may narrow or slow. Either way the change is recorded with rationale, and the embargo and PD date are re-evaluated.

**Extension requests.** Any party may request an embargo or coordination-window extension through the SIRT. The default embargo is **30 days**, always deferring to the upstream project's own policy, and may be extended for the greater good. The SIRT decides in consultation with the Finder and the maintainer.

**Anti-gaming.** Every escalation requires a stated justification and is logged. Severity re-scores are documented as deviation notices. **No party may escalate solely to gain earlier or broader access.** Escalation never waives a gate — it may change the tier or timing of an admitted person, or prompt a fresh nomination, but a new person still clears §2 and §3.

---

## 10. Exception path

Exceptions are handled case-by-case. Each is time-bounded, justified, approved by the named authority, and logged.

| Exception | Handling | Authority |
|---|---|---|
| **Additional SME at project request** | The maintainer may request that a specific SME be read in; the SIRT admits them at the appropriate tier. Gates and prerequisites still apply. | SIRT |
| **Delegated read-in** | A coordinating body (e.g., CISA) or a maintainer may nominate who to loop in, within limits set by the SIRT. Delegates must still meet all gates and prerequisites. | SIRT (limits — Appendix A, item 3) |
| **Early or broader read-in** for severe or broad-scope issues | Handled via escalation (§9); time-bounded. | Per §9 level |
| **Finder with a patch and customer obligations** | Sharing a fix before disclosure or upstream engagement is discouraged but cannot be prohibited. It must be declared to the SIRT; risks and consequences are documented. | Governing Board sets governing policy |
| **Early mitigations / workarounds** | Expected to be shared when patch development will exceed the agreed embargo or disclosure window. | SIRT |
| **Maintainer of Last Resort / time-bounded hardened fork** | Permitted only with TOC approval. | TOC |
| **Government / critical-infrastructure / telco coordination without pre-disclosure** | A TOC determination, consistent with the standing decision **not to pre-disclose to any single government**. | TOC |

---

## 11. Embargo breaches

- If an embargo is broken, the **SIRT coordinates** the response and notifies affected participants and members, depending on what was broken and how.
- Any member who discovers a breach **must promptly notify the SIRT**.
- **An embargo break results in removal from the program.**

---

## 12. Audit

- Every grant and revocation is logged with justification and approver.
- The **gate-by-gate determination** is part of the record for every read-in, including failed nominations.
- All read-ins are sent from the SIRT and must be **acknowledged by the involved party before access is granted**.
- Read-in lists are reviewed against least privilege at each case.
- **Member identities are protected from disclosure (anti-doxxing) throughout.**

---

## 13. Roles & authority

| Body | Authority |
|---|---|
| **SIRT case coordinator** | Evaluates the Three-Gate Test and prerequisites; runs the exclusion check; approves read-ins; maintains the case read-in log. |
| **SIRT case lead** | Assigns tiers; grants and revokes read-in; Level-1 escalation; coordinates breach response. |
| **Finder & maintainer** | Consulted on the read-in list, embargo, and PD. The maintainer sets the final fix and PD date. |
| **Working Group** | Nominates SMEs; requests escalation for its domain or vertical. |
| **TOC** | Cross-cutting severity and vertical calls; Maintainer-of-Last-Resort approval; new WG spin-up; grey-area cases. |
| **Governing Board** | Policy and legal exceptions — finder obligations, antitrust, government coordination. |

---

## Appendix A — Consolidated open items

Items carried forward from both source documents, deduplicated, with the body that owns the decision. This appendix is the single list of what remains unresolved; it is expected to shrink to zero before the policy leaves DRAFT status.

| # | Open item | Detail | Owner |
|---|---|---|---|
| 1 | **Default read-in lead times per tier** | Fix the standard lead time for Tier 2 and Tier 3 before PD. A working figure of 7–14 days appears in the source material (§4.1) but is not ratified. | TOC |
| 2 | **RACI per tier** | Define the specific actions each tier may take, and by whom, as a companion document to this policy. | TOC |
| 3 | **Delegation rules and limits** | How far a coordinating body (e.g., CISA) or a maintainer may extend read-in; enforce that the SIRT must approve **all** expansions of the set of Knowers. | TOC |
| 4 | **Approver of record; Finder/maintainer veto** | Confirm the approver of record, and whether the Finder or maintainer may veto — rather than merely be consulted on — additions. | TOC |
| 5 | **Tier 1 sub-staging** | Whether Tier 1 should split into separate *analyze* and *test* sub-stages with distinct read-in timing. | TOC |
| 6 | **"Active member" criteria** | Define what qualifies a standing WG member as active, and therefore eligible for the accelerated §7 path. | SIRT, informed by real cases |
| 7 | **Finder patch / customer-obligation policy** | Governing policy for a Finder who holds a patch and has customer obligations before disclosure. | Governing Board |
| 8 | **Antitrust documentation** | Documentation covering early or broad read-in of competing members. | Governing Board |
| 9 | **Gate 3 vetting standard** | Whether identity verification requires a documented standard (e.g., employer attestation, identity proofing level) beyond sponsor vouching. *(New — surfaced by codifying Gate 3.)* | TOC |
| 10 | **Emergency Read-In ceiling** | Whether the 72-hour Emergency Read-In window may be extended, by whom, and how many times. *(New — surfaced during merge.)* | SIRT / TOC |

---

## Appendix B — Merge notes

Substantive reconciliations made in producing this document from the two source files. Each warrants a confirming glance on review.

| # | Change | Rationale |
|---|---|---|
| 1 | **"Two-gate test" → Three-Gate Test.** The Tier Policy referred throughout to a *two-gate* test (need-to-know + contribution); the Guidelines already carried a third gate (vetted person). | The two documents disagreed. Harmonized to three gates everywhere. |
| 2 | **Gate 2 pass condition clarified.** The Guidelines read "If a person cannot do at least one of these, they are not read in" immediately after a list of three *gates*, which implied the gates were disjunctive. | The gates are conjunctive; the "at least one" applies to the three sanctioned **contributions** within Gate 2. Stated explicitly in §2. |
| 3 | **Gate 3 separated from Prerequisites.** Verified named identity and a sponsor appeared both as Gate 3 content and as prerequisites 1 and 4. | Kept in both, with the distinction stated: Gate 3 = identity and accountability (eligibility); §3 = controls and authorization (enablement). Duplication is intentional, not accidental. |
| 4 | **Emergency Read-In moved from a prerequisite to a relaxation of prerequisites.** It was listed as prerequisite 5 in the Guidelines, alongside the requirements it relaxes. | It is a path, not a requirement. Moved to §3.5 with explicit scope: it relaxes mechanism only, never a gate. |
| 5 | **Gate-by-gate determination added to the log and audit record.** Neither source required recording *which* gate a nomination cleared or failed. | Makes the test auditable and anti-gaming enforceable (§6, §12). |
| 6 | **SIRT case coordinator added to the roles table.** The role performed the verification step in the Guidelines workflow but was absent from the Tier Policy authority table. | Completes the authority table. |
| 7 | **7–14 day staging lead time marked provisional.** The Guidelines stated it inline; the Tier Policy listed it as an unresolved open item. | Retained the figure, flagged as unratified, and pointed at Appendix A item 1. |
| 8 | **Spelling.** Both source documents use *Akrites*; the project workspace is titled *Akreites*. This document uses **Akrites** throughout. | Flagging for a decision on the canonical spelling. |
| 9 | **Evidentiary tests added to each gate.** The "Satisfied by" and "Not satisfied by" criteria under Gates 1, 2, and 3 are **new**. The source documents stated each gate in a single sentence with no test for how it is judged. | Codifying the gates, as requested, requires a decision rule. These criteria are drawn from the sources' stated principles (least privilege; "consumers are served at PD"; contribution as a condition of membership) but are not verbatim from them. **Each bullet is a policy choice and should be read as a proposal, not as carried-forward text.** Items warranting particular attention: the Gate 1 written-nomination requirement; the Gate 1 exclusion of commercial/procurement/customer-communication needs; and the Gate 2 exclusion of internal-notification and incident-response-readiness rationales, which bars a common member expectation. |
| 10 | **Gate 3 affiliation paths extended to three.** The source named two (member-org engineer; designated upstream security team engineer). A third — nominee of a delegated authority — was added. | Both sources elsewhere permit delegated nomination by a coordinating body or maintainer (Prereq 4; Exception "Delegated read-in"). Without a matching Gate 3 path, those provisions could not operate. |
| 11 | **"Gates and prerequisites still apply" added to two exception rows** (*Additional SME at project request*, *Delegated read-in*); **"escalation never waives a gate"** added to §9 anti-gaming; **"no gate may be waived"** added to §2.1. | The sources conditioned delegates on *prerequisites* only, leaving open whether exception and escalation paths could route around the gates. Stated explicitly. **Confirm this is the intended reading.** |
| 12 | **Gate 2 timeline test** — "cannot within the case timeline" — and **Gate 3 exclusion-check scope** — adding prior embargo breach, sanctions, and legal bars to the source's "conflict, embargo sensitivity" — are new. | Reasonable extensions, but not source-derived. Confirm on review. |
