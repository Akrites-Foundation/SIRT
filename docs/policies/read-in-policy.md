# Read-In Policy

**Type:** Policy
**Approver:** Governing Board
**Status:** Draft — for Governing Board review (v0.9)
**Procedure:** [Read-In Procedure](../procedures/read-in-procedure.md) — the steps the SIRT follows to apply this policy
**Scope:** All Akrites vulnerability Working Groups (WGs) and all pre-disclosure cases handled by the Akrites SIRT.

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
| **Consumers are served at public disclosure** | Being an affected user or a generally interested member engineer is not a basis for read-in. |

---

## 1. Definitions

Definitions are kept in the [Glossary](../reference/glossary.md). This policy uses these terms with the meaning given there: [Read-in](../reference/glossary.md#read-in), [Tier](../reference/glossary.md#tier), [Disclosure boundary](../reference/glossary.md#disclosure-boundary), [Case read-in log](../reference/glossary.md#case-read-in-log), and [Sponsor](../reference/glossary.md#sponsor).

---

## 2. The Three-Gate Test

**A candidate is read in only if *all three* gates are satisfied.** The gates are conjunctive: failure at any one gate ends the evaluation and the candidate is not read in. Passing all three gates establishes *eligibility* only — the Prerequisites in §3 must also be complete before access is enabled.

The gates are evaluated by the **SIRT case coordinator** and recorded, gate by gate, in the case read-in log.

### Gate 1 — Demonstrable Need-to-Know

> *This specific case, or this specific WG domain, genuinely requires this person.*

Need-to-know must be **demonstrable and case-specific**, not inferred from role, seniority, employer, or Working Group membership.

**Satisfied by** a written statement, from the nominator, of the specific task this person will perform on **this** case or in **this** WG domain, and why the case cannot proceed as effectively without them.

**Not satisfied by:**

- Being an affected user, downstream consumer, or customer of the affected component.
- General interest, situational awareness, or a desire to "stay informed."
- Membership in Akrites, on the Board, or in a Working Group, taken on its own.
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

1. **Verified named individual.** A real, named human — never a shared, role, team, or distribution account. Identity is verified by the sponsor's vouching plus an employer email address.
2. **Confirmed affiliation.** The person is one of the following:
   - an engineer of an Akrites member organization, or that member's authorized and approved delegate;
   - an engineer of a designated upstream security team for the affected project; or
   - a nominee of a delegated authority (e.g., a coordinating body such as CISA, or the affected maintainer) for this specific case.
   - the **Finder of this case** (Tier 0), whose identity is verified to the extent needed to communicate securely. A Finder's sponsor of record is the Finder themself (or their organization, if they reported on its behalf). Anonymous Finders are not read in to the case workspace; the SIRT relays information to them through the reporting channel.
3. **An accountable sponsor of record.** A named sponsoring organization that vouches for the individual and to which conduct and embargo obligations attach.
4. **Exclusion check clear.** The SIRT has affirmatively asked and answered: *is there anyone who should specifically not be read in?* — covering conflicts of interest, competitive or antitrust sensitivity, prior embargo breach, sanctions or legal bars, and case-specific sensitivities.

**Gate 3 is about identity and accountability; §3 is about controls.** Gate 3 asks *who is this person and who answers for them*. The Prerequisites ask *what has this person signed, enabled, and been authorized for*. Both are required.

### 2.1 Applying the gates

- **Gates are evaluated per case, per WG domain.** Clearing the gates once does not clear them for the next case (see §7 for how earlier vetting shortens, but does not replace, this).
- **The burden of proof is on the nomination**, not on the SIRT. An unclear nomination is returned for more information, not approved provisionally.
- **A failed gate is recorded.** The gate that failed and the reason are logged, so that patterns in nominations can be reviewed.
- **No gate may be waived.** Time pressure is handled through the Emergency Read-In prerequisite path (§3.1) and the escalation levels (§9) — never by skipping a gate.

---

## 3. Prerequisites — required before any access is granted

Every person, regardless of tier, must have all of the following before access is enabled. **No prerequisite, no access — even if all three gates in §2 are met.**

1. **A verified, named identity** — an individual, never a shared or role account.
2. **Hardware-key 2FA** enabled on the Akrites environment.
3. **Agreements on file** — acceptance of the Read-In Notice (embargo and confidentiality acknowledgement), the Akrites Code of Conduct, and the antitrust acknowledgment under the [Linux Foundation Antitrust Policy](https://www.linuxfoundation.org/antitrust-policy).
4. **A sponsor** — a member organization vouching for them, or a delegated authority (e.g., a coordinating body such as CISA, or the affected maintainer) nominating them for a specific case.
5. **Authorization from the SIRT**, and access granted to the specific incident.

**Finders.** A Finder (Tier 0) needs prerequisites 1, 3 and 5 only; hardware-key 2FA is required only if the Finder is given access to the case repository or channel.

**Upstream maintainers (Tier 1.5).** An upstream maintainer or security team member needs prerequisites 1, 3 and 5 only. Hardware-key 2FA is required only if they are given access to an Akrites case repository or channel. Where prerequisite 3 cannot be met because the project's published policy does not allow its maintainers to sign agreements, see §10.

### 3.1 Emergency Read-In

The SIRT may grant **temporary, time-bounded** access to an external SME sponsored directly by an active maintainer or an Akrites member organization, using fast electronic agreements where possible and software-based TOTP/MFA, for **up to 72 hours** while hardware-key logistics are processed. Sponsorship is not limited by membership level.

Emergency Read-In relaxes the *mechanism* of prerequisites 2 and 3 — it does **not** relax the Three-Gate Test, the sponsor requirement, the exclusion check, or logging. Access lapses automatically at 72 hours unless the full prerequisites are complete.

---

## 4. The tiers at a glance

| Tier | Who | What they do | Information & TLP | Read-in timing |
|---|---|---|---|---|
| **Tier 0** | Reporter / Finder and the SIRT (plus automated intake) | Originate and coordinate the report | Full case detail; TLP:RED at intake | Earliest; longest duration |
| **Tier 1** | Akrites analysts and patch authors (SMEs) | Human & LLM-assisted review of the case, gathering all data, and producing the patch | Case material needed to analyze the issue and build the fix; TLP:AMBER+STRICT | When case analysis begins |
| **Tier 1.5** | Upstream maintainer / security team of the affected project (whether or not an Akrites member) | Human-brokered collaboration to analyze and validate vulnerability, produce the patch | Case material needed to build and test the fix; TLP:AMBER+STRICT | When analysis/testing is ready to share with upstream |
| **Tier 2** | Patch testers; distribution partners / maintainer pre-disclosure rings | Test the patch; prepare a coordinated downstream release | The fix, what is needed to verify it, and the timing — not full research detail; TLP:AMBER+STRICT | When a testable patch exists (testers); defined lead time before PD (distribution) |
| **Tier 3** | Second-order distributors (CDNs, package registries, Linux Distributions and downstream distribution partners) | Pre-stage the fix for rapid propagation | The artifact and go-live time only; TLP:AMBER | Latest; shortest window |
| **Tier 3.5 (Optional)** | International Coordinators and Strategic Partners (as needed) | Pre-stage PD notifications for rapid propagation | The advisory and go-live time only; TLP:AMBER | Latest; at most 24 hours before PD |
| **Public** | Everyone | — | Fully public; TLP:CLEAR | Public disclosure (PD) |

Automated intake — deduplication, severity estimation, and routing — sits within Tier 0 and requires no SME.

**Maintainer authority does not depend on tier.** The upstream maintainer or security team is read in at Tier 1.5 but always holds final authority over the fix and the Public Disclosure date; the SIRT Director is the SIRT's final decision point (CVD Policy §8).

### 4.1 Party-to-tier mapping

| Party | Role | Tier | Read-in timing |
|---|---|---|---|
| Reporter / Finder | Provides the finding; may assist analysis | Tier 0 | Earliest, longest access |
| WG analyst / patch author (SME) | Analyze and produce the patch | Tier 1 | When analysis/patch work begins |
| Maintainer / upstream security team | Owns the fix and the final PD decision | Tier 1.5 | When the analysis and proposed patch are ready to share with upstream |
| Patch tester (SME)	| Test the patch | Tier 2 | When a testable patch exists |
| Distribution / staging party | Stage the fix ahead of PD | Tier 2 / Tier 3 | Latest — the minimum lead time consistent with a safe rollout: typically 7–14 days before PD (CVD Policy §7) |
| International coordinator / strategic partner | Pre-stage PD notifications | Tier 3.5 | At most 24 hours before PD |
| Affected user / interested member engineer | — | None | Public disclosure |

**Membership does not confer read-in.** Akrites membership at any level (Premier, General or Associate) does not by itself entitle a Member or its engineers to be read in to a case. Engineers of Associate Members, like all others, are admitted only when they pass the Three-Gate Test and meet the prerequisites for the tier. Premier status gives representation on the Governing Board, not case access.

---

## 5. Tier placement criteria

Every candidate must first clear the Three-Gate Test (§2) and the Prerequisites (§3). Tier is then assigned on **the person's role in resolving this specific case, and the minimum information and lead time that role requires.**

| Tier | You belong here if… |
|---|---|
| **Tier 0** | You originated the report (Finder), or you are the SIRT coordinating it. You need full context from the start. |
| **Tier 1** | You will review the case, gather the data, or write the patch. You need code-level case material, read in when analysis begins. |
| **Tier 1.5** | You maintain the affected upstream code or run its security team. You receive the analysis and proposed patch when they are ready to share upstream. |
| **Tier 2** | You will test the patch, or you operate a distribution channel or pre-disclosure ring that must prepare a coordinated release. You need the fix and the timing (and, for testing, what is needed to verify it), not the underlying research. |
| **Tier 3** | You operate second-order distribution (CDN, registry) that must pre-stage for a rapid rollout. You need the artifact and the go-live time only. |
| **Tier 3.5** | You are an international coordinator or strategic partner preparing your constituency's notification. You receive the advisory and go-live time only. |
| **None** | You are an affected user or an interested member engineer with no active role. You are served at public disclosure. |

**Placement rules.**

- **One tier per case.** A person is assigned the single most-restrictive tier sufficient for their role.
- **Role determines tier — not seniority, not membership.** Membership of a Working Group does not by itself grant a tier; a case role does.
- **When a role spans tasks** (e.g., an analyst who also tests), assign the tier of the earliest or broadest task they own.
- **When in doubt, place lower** — higher tier number, later read-in — and escalate if more is genuinely needed.

### 5.1 Tiers vs. disclosure boundaries

A **tier** governs *when* and *how much* a person is read in. A **disclosure boundary** governs *what information exists or is shared* at a point in the case. Each tier receives only the TLP-classified material its task requires: TLP:RED at intake (Tier 0), TLP:AMBER+STRICT for verification and remediation material (Tiers 1, 1.5, 2), and TLP:AMBER for downstream staging (Tiers 3, 3.5). See the CVD Policy §8 table.

A detailed **RACI** — the specific actions each tier may take, and by whom — is developed as a companion document owned by the Akrites SIRT, and is tracked in the [Read-In Procedure](../procedures/read-in-procedure.md).

---

## 6. Read-in requirements (per case)

Every read-in meets these requirements. The steps for doing it are in the [Read-In Procedure](../procedures/read-in-procedure.md).

- **Nominated with a stated role.** The Finder, WG, maintainer, or delegated authority proposes the person and the sanctioned role they will perform.
- **Verified and approved by the SIRT case coordinator**, who records each of the three gates (§2), confirms the prerequisites (§3), and completes the exclusion check. The Finder and maintainer are consulted on Tier 0, 1 and 1.5 additions; they do not hold a veto.
- **Tier assigned under §5**, with the rationale recorded.
- **Acknowledged first.** The read-in is sent from the SIRT and the individual must acknowledge it **before** access is enabled.
- **Scoped.** Access covers that single case's private repository and communications channel — nothing else.
- **Logged and time-bound.** Every read-in is recorded in the case read-in log and given an expiry (§8).

---

## 7. Working Group participants and earlier vetting

Working Groups are convened as needed; there are no standing Working Groups (see the [Working Group Governance Policy](wg-governance-policy.md)). Read-in to a WG follows the same rules as read-in to a case.

- Only member engineers — employees of Akrites member organizations and their authorized and approved delegates — are eligible to participate.
- **Contribution is a condition of participation.** Access is granted to people who can actively collaborate to develop and vet a solution to the issue.
- **All three gates in §2 apply**, evaluated against the WG's focus area; all §3 prerequisites are required.
- A participant's expertise is entered in the **Security Rolodex** so the SIRT understands who is available to pull into future cases. Access is always gated by the SIRT and the particulars of a given incident.
- Access is limited to **that WG's** workspace only — never cross-WG.

**Earlier participation does not grant automatic read-in to a later case.** Case-level access still follows §6.

**Reduced paperwork for people already vetted.** A person who was vetted for earlier WG work, and is recognized for their contributions and domain expertise, is expected to receive read-in approval quickly. For such a person the SIRT case coordinator may rely on the earlier record to satisfy **Gate 2** (capacity, already assessed for the domain) and **Gate 3** (identity and affiliation, already verified), and on the §3 prerequisites already on file, provided the record is current. **Gate 1 is always assessed fresh**, against the specific case, and the exclusion check is always re-run. This is a reduction in paperwork, not a waiver of a gate (§2.1).

People whose earlier record is out of date, or who have been unresponsive or not contributing for an extended period, follow the full §6 vetting.

---

## 8. Time-bounding, expiry, and revocation

- **Tiered windows.** Tier 0 holds access longest; each later tier is read in only at the interval needed to complete its task before PD. Staging parties receive the least lead time consistent with a safe rollout.
- **Default expiry.** Case access ends automatically at public disclosure or case closure, whichever comes first.
- **Immediate revocation** on any of: task complete; departure from the sponsoring organization; need-to-know ends; or breach of the Code of Conduct or the embargo.
- **Continuing to a future case requires a fresh read-in**, which may use the reduced-paperwork path in §7. How to set expiry and revoke is in the [Read-In Procedure](../procedures/read-in-procedure.md).

---

## 9. Escalation path

**Levels.**

1. **SIRT case coordinator.** Adjusts priority, pulls in additional Tier 1 SMEs, or reads a party in earlier — all within existing tier definitions.
2. **SIRT Director.** Cross-cutting or contested calls: vertical-versus-industry severity conflicts, broad-scope resourcing, or convening a Working Group.
3. **Governing Board.** Policy and legal matters: antitrust, and government or critical-infrastructure coordination.

Triggers for escalation and the steps to follow are in the [Read-In Procedure](../procedures/read-in-procedure.md). Whatever the trigger, the change is recorded with its rationale and the embargo and PD date are re-evaluated.

**Extension requests.** Any party may request an embargo or coordination-window extension through the SIRT. The proposed upstream embargo is **15 business days** (total target time to PD of ≤ 17 bd Low/Med, ≤ 21 bd High, ≤ 24 bd Critical), always deferring to the upstream project's own policy, and may be extended for the greater good. The maintainer decides, with the SIRT advising and consulting the Finder; the SIRT Director is the SIRT's final decision point (CVD Policy §8).

**Anti-gaming.** Every escalation requires a stated justification and is logged. Severity re-scores are documented as deviation notices. **No party may escalate solely to gain earlier or broader access.** Escalation never waives a gate — it may change the tier or timing of an admitted person, or prompt a fresh nomination, but a new person still clears §2 and §3.

---

## 10. Exception path

Exceptions are handled case-by-case. Each is time-bounded, justified, approved by the named authority, and logged.

| Exception | Handling | Authority |
|---|---|---|
| **Additional SME at project request** | The maintainer may request that a specific SME be read in; the SIRT admits them at the appropriate tier. Gates and prerequisites still apply. | SIRT |
| **Delegated read-in** | A coordinating body (e.g., CISA) or a maintainer may nominate people to read in. The SIRT approves every addition, and nominees must still meet all gates and prerequisites. | SIRT |
| **Early or broader read-in** for severe or broad-scope issues | Handled via escalation (§9); time-bounded. | Per §9 level |
| **Finder with a patch and customer obligations** | Sharing a fix before disclosure or upstream engagement is discouraged but cannot be prohibited. It must be declared to the SIRT; risks and consequences are documented. The SIRT respects the Finder's timeframe for meeting its customer obligations and coordinates the case timeline with it. | SIRT |
| **Early mitigations / workarounds** | Expected to be shared when patch development will exceed the agreed embargo or disclosure window. | SIRT |
| **Upstream maintainer who cannot sign the Read-In Notice** | Where the project's published policy says its maintainers do not sign NDAs or acknowledgements, the SIRT records the project's own confidentiality and embargo terms in the case read-in log and sends the Read-In Notice for information only. The SIRT shares only what those terms allow. The Three-Gate Test, the exclusion check, tier placement, logging and expiry all still apply. | SIRT |
| **Maintainer of Last Resort / time-bounded hardened fork** | Permitted only under the [MoLR Policy](molr-policy.md#52-approval-authority--recusal): the SIRT Director approves each engagement and the Governing Board is informed. | SIRT Director |
| **Government / critical-infrastructure / telco coordination without pre-disclosure** | A Governing Board determination, consistent with the standing decision **not to pre-disclose to any single government**. | Governing Board |

---

## 11. Embargo breaches

- Anyone read in to the case — participant, WG member, or staff — who discovers a breach **must promptly notify the SIRT**.
- **An embargo break results in immediate suspension of access.** The Governing Board decides on permanent removal. An accidental break that the participant promptly self-reports is reviewed blamelessly.
- The SIRT coordinates the response and escalates the violation to the Governing Board, which holds final authority for permanent revocation or further administrative action. The steps are in the [Read-In Procedure](../procedures/read-in-procedure.md), and the incident response to the break itself is in the [Embargo Break Playbook](../playbooks/embargo-break-playbook.md).
- Where the person who broke the embargo is an Akrites Member's representative, the Charter's process applies in addition: violations are reported to the Governing Board, the Chair or a Co-Chair may suspend the Member, and the Member may appeal to the Linux Foundation (Akrites Charter §1(e)(iii)–(iv)).

---

## 12. Audit

- Every grant and revocation is logged with justification and approver. The log fields are in the [Read-In Procedure](../procedures/read-in-procedure.md).
- The **gate-by-gate determination** is part of the record for every read-in, including failed nominations.
- Read-in lists are reviewed against least privilege at each case.
- **Participant and member identities are protected from disclosure (anti-doxxing) throughout.**

---

## 13. Roles & authority

| Body | Authority |
|---|---|
| **SIRT case coordinator** | Evaluates the Three-Gate Test and prerequisites; runs the exclusion check; approves read-ins; assigns tiers; grants and revokes access; maintains the case read-in log; Level-1 escalation; coordinates breach response. |
| **SIRT Director** | Level-2 escalation: cross-cutting severity and vertical calls; broad-scope resourcing; convening a Working Group; approving Maintainer-of-Last-Resort engagements ([MoLR Policy §5.2](molr-policy.md#52-approval-authority--recusal)). |
| **Finder & maintainer** | Consulted on the read-in list, embargo, and PD. The maintainer sets the final fix and PD date. |
| **Working Group** | Nominates SMEs; requests escalation for its domain or vertical. |
| **Governing Board** | Policy and legal exceptions — antitrust, government coordination; informed of new Maintainer-of-Last-Resort engagements; creation of any standing WG (none today); permanent removal after a breach; grey-area cases. |
