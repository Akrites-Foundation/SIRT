# Akrites Read-In Tier Policy

**Purpose.** This policy defines the read-in tiers referenced in the *Akrites Read-In Process*, the criteria that place a person in one tier rather than another, and the paths for escalation and exceptions. It governs **who sees a pre-disclosure case, when, and with how much information.**

**Relationship to the read-in process.** The read-in process decides *whether* a person is admitted at all (the two-gate test plus prerequisites). This policy decides *which tier* they enter and *how tiers change* during a case.

**Principles.**
- **Least privilege, need-to-know.** Access shrinks and starts later as the tier number rises.
- **No issue is dropped.** Severity is a routing and priority signal, never a filter for dropping a confirmed vulnerability.
- **Minimum sufficient access.** A person is placed in the highest-numbered (least-privileged, latest) tier that still lets them do their job.
- **Everything is time-bounded and logged.** Every placement, escalation, and exception is justified, approved by a named authority, and recorded in the case read-in log.

---

## 1. The tiers at a glance

| Tier | Who | What they do | Information & TLP | Read-in timing |
|---|---|---|---|---|
| **Tier 0** | Reporter / Finder and the maintainer (plus automated intake) | Originate the report; own the fix and final disclosure decision | Full case detail; TLP:RED at intake | Earliest; longest duration |
| **Tier 1** | Subject-matter experts (Akrites members) | Analyze, produce, and test the patch | Case material needed to build/test the fix; TLP:AMBER+STRICT | When analysis/testing begins |
| **Tier 2** | Distribution partners / maintainer pre-disclosure rings | Prepare a coordinated downstream release | The fix and timing — not full research detail | Defined lead time before PD |
| **Tier 3** | Second-order distributors (CDNs, package registries) | Pre-stage the fix for rapid propagation | The artifact and go-live time only | Latest; shortest window |
| **Public** | Everyone | — | Fully public | Public disclosure (PD) |

Automated intake (dedup, severity estimation, routing) sits within Tier 0 and requires no SME.

---

## 2. Criteria for tier inclusion

Every candidate must first clear the read-in process (need-to-know + a sanctioned contribution + prerequisites). This policy then assigns a tier based on **the person's role in resolving this specific case and the minimum information and lead time that role requires.**

| Tier | You belong here if… |
|---|---|
| **Tier 0** | You originated the report (Finder), or you own the affected code and its fix (maintainer). You need full context from the start. |
| **Tier 1** | You will analyze, write, or test the patch. You need code-level case material, read in when that work begins. |
| **Tier 2** | You operate a distribution channel or pre-disclosure ring that must prepare a coordinated release. You need the fix and the timing, not the underlying research. |
| **Tier 3** | You operate second-order distribution (CDN, registry) that must pre-stage for a rapid rollout. You need the artifact and the go-live time only. |
| **None** | You are an affected user or an interested member with no active role. You are served at public disclosure. |

**Placement rules.**
- **One tier per case.** A person is assigned the single most-restrictive tier sufficient for their role.
- **Role determines tier, not seniority or membership.** Standing Working Group membership does not by itself grant a tier — a case role does.
- **When a role spans tasks** (e.g., an analyst who also tests), assign the tier of the earliest/broadest task they own.
- **When in doubt, place lower** (higher tier number, later read-in) and escalate if more is genuinely needed.

---

## 3. Tiers vs. disclosure boundaries

A **tier** governs *when* and *how much* a person is read in. A **disclosure boundary** governs *what information exists or is shared* at a point in the case. They are related but distinct — some activities cannot be performed without a disclosure (you cannot test a patch you have not been given).

Each tier receives only the TLP-classified material its task requires: TLP:RED at intake (case team only), TLP:AMBER+STRICT for remediation material. A detailed RACI — the specific actions each tier may take, and by whom — is to be developed as a companion to this policy.

---

## 4. Escalation path

**Triggers.** A change in severity (CVSS rising or falling), scope or blast radius, criticality to a specific vertical (e.g., a CVSS-6 that is critical for telco), a member or Working Group request, or a need for additional resources.

**Levels.**
1. **SIRT case lead.** Adjusts priority, pulls in additional Tier 1 SMEs, or reads a party in earlier — all within existing tier definitions.
2. **Governing Board.** Policy or legal matters: finder patch/customer obligations, antitrust, and government or critical-infrastructure coordination.

**Severity changes.** If the score rises, read-in may widen or accelerate; if it falls, it may narrow or slow. Either way the change is recorded with rationale, and the embargo and PD date are re-evaluated.

**Extension requests.** Any party may request an embargo or coordination-window extension through the SIRT. The default embargo is 30 days, always deferring to the upstream project's own policy, and may be extended for the greater good. The SIRT decides in consultation with the Finder and maintainer.

**Anti-gaming.** Every escalation requires a stated justification and is logged. Severity re-scores are documented as deviation notices. No party may escalate solely to gain earlier or broader access.

---

## 5. Exception path

Exceptions are handled case-by-case; each is time-bounded, justified, approved by the named authority, and logged.

- **Additional SME at project request.** The maintainer may request that a specific SME be read in; the SIRT admits them at the appropriate tier.
- **Delegated read-in.** A coordinating body (e.g., CISA, ENISA) or a maintainer may nominate who to loop in, within limits set by the SIRT. Delegates must still meet all prerequisites.
- **Early or broader read-in** for severe or broad-scope issues — handled via escalation (§4), time-bounded.
- **Finder with a patch and customer obligations.** Sharing a fix before disclosure or upstream engagement is discouraged but cannot be prohibited. It must be declared to the SIRT; risks and consequences are documented; the Governing Board sets the governing policy.
- **Early mitigations/workarounds.** Expected to be shared when patch development will exceed the agreed embargo or disclosure window.
- **Maintainer of Last Resort / time-bounded hardened fork.** Only with SIRT+WG approval.
- **Government / critical-infrastructure / telco coordination without pre-disclosure.** A SIRT+WG determination; consistent with the standing decision not to pre-disclose to any single government.

---

## 6. Embargo breaches

- If an embargo is broken, the **SIRT coordinates** and notifies affected participants and members, depending on what was broken and how.
- Any member who discovers a breach **must promptly notify the SIRT.**
- An embargo break results in **removal from the program.**

---

## 7. Roles & authority

| Body | Authority |
|---|---|
| **SIRT case lead** | Assigns tiers; grants and revokes read-in; Level-1 escalation; coordinates breaches. In edge cases and where delays are beyond expected SLAs (e.g., 24 hours for Critical/High issues), Tier placement and escalation decisions may be performed by WG Lead in concurrence with other SIRT members.  |
| **Finder & maintainer** | Consulted on the read-in list, embargo, and PD. The maintainer sets the final fix and PD date. |
| **Working Group** | Nominates SMEs; requests escalation for its domain or vertical. |
| **Governing Board** | Policy and legal exceptions (finder obligations, antitrust, government coordination). |

---

## Open items to confirm with the Governing Board

- Default read-in **lead times** for Tier 2 and Tier 3.
- The **RACI** of actions permitted at each tier.
- Whether **Tier 1 should split** into analyze and test sub-stages.
- **Delegation limits** — how far a coordinating body or maintainer may extend read-in.
- **Finder patch / customer-obligation** policy (Board).
- **Antitrust documentation** covering early or broad read-in.
