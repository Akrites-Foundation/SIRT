# Read-In Procedure

**Type:** Procedure
**Owner:** Akrites SIRT
**Approver:** SIRT Director
**Status:** Draft — for Akrites SIRT review
**Formerly titled:** Read-In Policy §6, and the procedural parts of §7–§11
**Applies to:** SIRT case coordinators, and anyone nominating a person to a case or Working Group
**Implements:** [Read-In Policy](../policies/read-in-policy.md). Where they conflict, the policy governs.
**Related:** [Read-In Notice template](../../templates/case-read-in-notice-template.md), [case read-in log](../../templates/Akrites_ReadIn_Log_CASE.csv), [Read-In Engineer Quick Reference](../reference/read-in-engineer-quick-reference.md)

---

## 1. Purpose

The Read-In Policy says who may be read in, to which tier, and under what limits. This procedure says how the SIRT does it, step by step. It adds no new rules. If a step here seems to allow something the policy forbids, follow the policy.

---

## 2. Per-case read-in

Follow these steps for each person, for each case.

1. **Nominate.** The Finder, WG, maintainer, or delegated authority proposes a person and states which sanctioned role they will perform (policy §2, Gate 2). The nomination includes the written statement of need required by Gate 1.
2. **Verify.** The SIRT case coordinator evaluates and records **each of the three gates** (policy §2), confirms all prerequisites (policy §3), and completes the exclusion check. A nomination that is unclear is returned for more information. It is not approved provisionally.
3. **Approve.** The SIRT case coordinator approves. Consult the Finder and the maintainer on Tier 0, 1 and 1.5 additions. They are consulted, not asked for a veto.
4. **Assign tier.** Apply policy §5 and record the reason for the tier chosen.
5. **Acknowledge.** Send the [Read-In Notice](../../templates/case-read-in-notice-template.md) from the SIRT. The individual must acknowledge it **before** access is enabled.
6. **Grant scoped access.** Give access to that single case's private repository and communications channel, and nothing else.
7. **Log it.** Record in the case read-in log: who, sponsoring organization, role, tier, gate-by-gate determination, approved by, and expiry.
8. **Time-bound.** Set the access to expire (see §5 of this procedure).

If a gate fails, stop. Record which gate failed and why, then tell the nominator.

---

## 3. Previously vetted Working Group participants

Working Groups are convened as needed (see the [Working Group Governance Policy](../policies/wg-governance-policy.md)). When a person has already been read in to earlier WG work, the coordinator may shorten the paperwork. It does not skip a gate.

1. Check the person's earlier vetting record and the [Security Rolodex](../reference/glossary.md) entry. Confirm the record is current: the person is still with the same organization, still contributing, and the prerequisites on file are still valid.
2. If so, the coordinator may rely on the record for **Gate 2** (capacity in that domain) and **Gate 3** (identity and affiliation), and on the §3 prerequisites already on file.
3. **Assess Gate 1 fresh**, against this case. **Re-run the exclusion check.**
4. Continue from step 4 of §2.

If the record is out of date, or the person has been unresponsive or not contributing for an extended period, follow the full §2.

---

## 4. Emergency read-in

Use this only for an external SME sponsored directly by an active maintainer or an Akrites member organization, when the full prerequisites cannot be finished in time.

1. Complete the Three-Gate Test, the sponsor check, the exclusion check and logging exactly as in §2. None of these is relaxed.
2. Collect fast electronic agreements in place of the full agreements, and enable software-based TOTP/MFA in place of hardware-key 2FA.
3. Log the access as **Emergency**, with an expiry **no later than 72 hours** from the grant.
4. Start the hardware-key and full-agreement steps at once.
5. If they are not complete at 72 hours, access lapses. Confirm it was removed and log that.

---

## 5. Expiry and revocation

**Setting expiry.** Set each person's access to end at public disclosure or case closure, whichever comes first. Set an earlier expiry if their task will finish sooner. Later tiers are read in later, so the window shrinks as the tier number rises.

**Revoking.** Revoke access **immediately** when any of these happens:

- the person's task is complete;
- the person leaves the sponsoring organization;
- the need-to-know ends; or
- the person breaches the Code of Conduct or the embargo (then also follow §8).

To revoke, remove repository and channel access, log the revocation and the reason, and confirm to the person that access has ended.

**Another case.** A person needs a fresh read-in for each future case. Use §3 if they qualify.

---

## 6. Escalation

**When to escalate.** A change in severity (CVSS rising or falling); a change in scope or blast radius; criticality to a specific vertical (for example, a CVSS-6 that is critical for telecoms); a member or Working Group request; or a need for additional resources.

**Where it goes.** The levels and who holds each are in the policy (§9). In short:

1. The **SIRT case coordinator** adjusts priority, pulls in more Tier 1 SMEs, or reads a party in earlier, all within existing tier definitions.
2. The **SIRT Director** decides cross-cutting or contested calls, such as vertical-versus-industry severity conflicts, broad-scope resourcing, or convening a Working Group.
3. The **Governing Board** decides policy and legal matters.

**Steps.**

1. Write down the trigger and the justification.
2. Take it to the lowest level that has the authority.
3. Record the decision and the reason in the case log. Record severity re-scores as deviation notices.
4. If severity rose, read-in may widen or speed up. If it fell, it may narrow or slow down. Re-evaluate the embargo and the PD date either way.
5. If a new person is needed, start a fresh nomination at §2. Escalation never waives a gate.

Do not escalate only to get earlier or broader access.

---

## 7. Handling an exception

The exceptions the policy allows, and who approves each, are in the policy (§10).

1. Name the exception being used and the authority that approves it.
2. Write down the reason and the time limit.
3. Get approval from the named authority. Gates and prerequisites still apply unless the policy table says otherwise.
4. Log the exception, the approver and the expiry in the case read-in log.

### Upstream maintainer who cannot sign the Read-In Notice

Use this when an upstream maintainer's published policy says they do not sign NDAs or acknowledgements.

1. Find the project's published policy and confirm it says so. Keep a link or copy in the case.
2. Record the project's own confidentiality and embargo terms in the case read-in log, next to the maintainer's entry.
3. Send the [Read-In Notice](../../templates/case-read-in-notice-template.md) **for information only**, and say so in the message.
4. Share only what those terms allow. If they do not cover something, do not share it. Ask the SIRT Director.
5. Complete the Three-Gate Test, the exclusion check, tier placement, logging and expiry as in §2. Enable hardware-key 2FA only if they are given access to an Akrites case repository or channel.

---

## 8. Responding to an embargo breach

1. **Suspend access immediately** for anyone involved in the breach.
2. **Notify the SIRT** as soon as the breach is discovered. Anyone read in to the case who discovers a breach must do this.
3. The SIRT coordinates the response. It notifies affected participants and members, depending on what was broken and how. See the [Embargo Break Playbook](../playbooks/embargo-break-playbook.md) for the disclosure side.
4. The SIRT escalates the violation to the Governing Board, which decides on permanent removal.
5. If the participant promptly reported an accidental break themselves, review it without blame.
6. Log the breach, the suspension, and the Board's decision.

---

## 9. The case read-in log

Keep one log per case, using the [read-in log template](../../templates/Akrites_ReadIn_Log_CASE.csv). Record every grant, change and revocation. For each read-in include:

- who, and the sponsoring organization;
- role and tier, with the reason for the tier;
- the gate-by-gate determination, including failed nominations;
- who approved it, and when the person acknowledged the Read-In Notice;
- expiry, and any revocation with its reason.

At each case, review the read-in list against least privilege. Keep participant identities out of anything that is shared outside the case.
