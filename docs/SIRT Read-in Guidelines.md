# Akrites Read-In Process — Working Groups & Disclosures - DRAFT v0.1

**Purpose.** Define how people are granted access to vulnerability Working Groups (WGs) and to individual pre-disclosure cases. Access is tightly restricted to parties with a genuine need-to-know who can also meaningfully move a fix forward.

**Guiding rule.** Least privilege, always. A person is read in only to the specific WG or case they are contributing to, only for as long as their task requires, and never across WGs. Only Akrites staff hold cross-cutting visibility.

---

## 1. The read-in test — both gates must be true

A candidate is read in only if **both** are satisfied:

- **Gate 1 — Need to know.** This specific case (or WG domain) genuinely requires this person.
- **Gate 2 — Able to contribute** in one of the three sanctioned roles below.

If a person cannot do at least one of these, they are **not** read in. Being an affected user or a generally interested member is not sufficient — consumers are served at public disclosure (PD), not before.

| Sanctioned contribution | What it means |
|---|---|
| **Analyze / produce a patch** | Validate the finding and develop the fix (and a workaround/alternative whenever possible). |
| **Test the patch** | Verify the fix resolves the issue without regressions, in a representative environment. |
| **Stage the patch** | Pre-position the fix for a safe, rapid rollout (e.g., distributor, package registry, CDN). |

---

## 2. Who sits where

Read-in maps to the tiered-disclosure model. Later tiers are read in **later** and see **less**.

| Party | Role | Tier | Read-in timing |
|---|---|---|---|
| Reporter / Finder | Provides the finding; may assist analysis | Tier 0 | Earliest, longest access |
| Maintainer | Owns the fix and final PD decision | Tier 0 | Earliest |
| WG analyst / patch author (SME) | Analyze and produce the patch | Tier 1 | When analysis/patch work begins |
| Patch tester (SME) | Test the patch | Tier 1 | When a testable alpha exists |
| Distribution / staging party | Stage the fix ahead of PD | Tier 2 / 3 | Latest — minimum lead time for a safe rollout |

---

## 3. Prerequisites — required before any access is granted

Every person, regardless of tier, must first have:

1. **A verified, named identity** — an individual, never a shared or role account.
2. **Hardware-key 2FA** enabled on the Akrites environment.
3. **Signed agreements on file** — embargo/NDA, the Akrites Code of Conduct, and the antitrust acknowledgment.
4. **A sponsor** — a member organization vouching for them, or a delegated authority (e.g., a coordinating body such as CISA, or the affected maintainer) nominating them for a specific case.

No prerequisite, no access — even if both gates in §1 are met.

---

## 4. Read-in workflow (per case)

1. **Nominate.** The Finder, WG, maintainer, or delegated authority proposes a person and states which sanctioned role they will perform.
2. **Verify.** The SIRT case lead confirms both gates (§1) and all prerequisites (§3), and checks the exclusion question: *is there anyone who should specifically not be read in?* (e.g., conflict, embargo sensitivity).
3. **Approve.** The SIRT case lead approves; the Finder and maintainer are consulted on Tier 0/1 additions.
4. **Grant scoped access.** Access is limited to that single case's private repo and comms channel — nothing else.
5. **Log it.** Record in the case read-in log: who, sponsoring org, role, tier, approved by, and expiry.
6. **Time-bound.** Set access to expire (see §6).

---

## 5. Standing Working Group membership

WG membership is durable read-in scoped to a **domain** rather than a single case, and follows the same rules:

- Both gates in §1 apply, evaluated against the WG's focus area; all §3 prerequisites required.
- The member's expertise is entered in the Security Rolodex so the SIRT knows who to pull into future cases.
- Access is limited to **that WG's** workspace only — never cross-WG.
- Membership is reviewed periodically and removed when the member is no longer contributing.

Standing membership does **not** grant automatic read-in to every case in the WG; case-level access still follows §4, though it can be near-instant for active members.

---

## 6. Time-bounding, expiry, and revocation

- **Tiered windows.** Tier 0 holds access longest; each later tier is read in only at the interval needed to complete its task before PD. Staging parties receive the least lead time consistent with a safe rollout.
- **Default expiry.** Case access ends automatically at public disclosure or case closure, whichever comes first.
- **Immediate revocation** on any of: task complete, departure from the sponsoring org, need-to-know ends, or breach of the CoC or embargo.
- Continuing to a future case requires a fresh read-in (or existing standing WG membership).

---

## 7. Audit

Every grant and revocation is logged with justification and approver. Read-in lists are reviewed against least privilege at each case, and member identities are protected from disclosure (anti-doxxing) throughout.

---

## Open items to confirm with the TOC / Governing Board

- **Approver of record** and whether the Finder or maintainer have suggestions to put a veto on additions.
- **Default read-in lead times** per tier.
- **Delegation rules** — how far a coordinating body (e.g., CISA) or a maintainer may extend read-in on the SIRT's behalf.
- **RACI per tier** — the specific actions each tier may take (to be developed).
- **Antitrust documentation** to cover early read-in of competing members.
