# Akrites Read-In Tier Policy

**Owner:** Akrites SIRT · **Status:** Draft for Governing Board review · **Last updated:** 2026-08-24

**Purpose.** This policy defines the read-in tiers referenced in the *[Akrites Read-In Process](https://github.com/Akrites-Foundation/SIRT/blob/main/docs/SIRT%20Read-in%20Guidelines.md)*, the criteria that place a person in one tier rather than another, and the paths for escalation and exceptions. It governs **who sees a pre-disclosure case, when, and with how much information.**

**Relationship to the read-in process.** The read-in process decides *whether* a person is admitted at all (the two-gate test plus prerequisites). This policy decides *which tier* they enter and *how tiers change* during a case.

**Principles.**
- **Least privilege, need-to-know.** Access shrinks and starts later as the tier number rises.
- **No issue is dropped.** Severity is a routing and priority signal, never a filter for dropping a confirmed vulnerability.
- **Minimum sufficient access.** A person is placed in the highest-numbered (least-privileged, latest) tier that still lets them do their job.
- **Sector-neutral, equal access.** Read-in timing and breadth are driven by case role and need-to-know, never by a member's industry, commercial standing, or membership tier. Where several parties have equivalent roles, they are read in on equivalent terms. Formal antitrust documentation covering early or broad read-in is maintained with the Governing Board and legal counsel (see Open items).
- **Everything is time-bounded and logged.** Every placement, escalation, and exception is justified, approved by a named authority, and recorded in the case read-in log.

---

## 1. The tiers at a glance

| Tier | Who | What they do | Information & TLP | Read-in timing |
|---|---|---|---|---|
| **Tier 0** | Reporter / Finder and the maintainer (plus automated intake) | Originate the report; own the fix and final disclosure decision | Full case detail; TLP:RED at intake | Earliest; longest duration |
| **Tier 1** | Subject-matter experts (Akrites members) | Analyze, produce, and test the patch | Case material needed to build/test the fix. TLP classification follows case severity per [Akrites SIRT Severity Guidelines](): **TLP:RED for CRITICAL and HIGH; TLP:AMBER+STRICT for Medium and Low.** When Tier 1 material is TLP:RED, the SME may not share case material within their organization without SIRT case lead approval of specific named individuals, who are logged as additional Tier 1 participants. | When analysis/testing begins |
| **Tier 2** | Distribution partners / maintainer pre-disclosure rings | Prepare a coordinated downstream release | The fix and timing — not full research detail; TLP:AMBER+STRICT | Defined lead time before PD |
| **Tier 3** | Second-order distributors (CDNs, package registries) | Pre-stage the fix for rapid propagation | The artifact and go-live time only; TLP:AMBER+STRICT | Latest; shortest window |
| **Public** | Everyone | — | Fully public | Public disclosure (PD) |

Automated intake (dedup, severity estimation, routing) sits within Tier 0 and requires no SME.

**Severity classification.** Severity ratings used throughout this policy (CRITICAL, HIGH, MEDIUM, LOW) are informed by the [CVSS v4.0](https://www.first.org/cvss/specification-document) qualitative severity rating scale: Critical (9.0–10.0), High (7.0–8.9), Medium (4.0–6.9), Low (0.1–3.9). Where CVSS v4.0 is not yet available for a case (e.g., during initial triage before a full score is assigned), the SIRT case lead assigns a provisional severity based on available information and applies the corresponding TLP classification. The provisional classification is updated when a CVSS score is finalized.

---

## 2. Criteria for tier inclusion

Every candidate must first clear the read-in process (need-to-know + a sanctioned contribution + prerequisites). This policy is used to auto-assign a tier based on **the person's role in resolving this specific case and the minimum information and lead time that role requires.**

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

Each tier receives only the TLP-classified material its task requires. TLP:RED applies at intake (Tier 0) and to Critical/High-severity Tier 1 cases. TLP:AMBER+STRICT applies to Medium/Low-severity Tier 1 cases and to Tier 2 and Tier 3 material regardless of severity. Severity is assessed using the [Akrites SIRT Severity Scale]() and is informed by methodologies like CVSS v4.0 qualitative ratings as defined in the CVD Policy's severity section (*Severity, identifiers, and machine-readable data*), with the threshold between RED and AMBER+STRICT set at the HIGH level. A detailed RACI covering the specific actions each tier may take, and by whom, is to be developed as a companion to this policy.

---

## 4. Escalation path

**Triggers.** A change in severity (Severity scoring rising or falling), scope or blast radius, disproportionate impact on a specific sector (a vulnerability that affects one sector materially more than the broadly-affected population — not merely one that is "critical to" a sector, which is true of most widely-deployed dependencies), a member or Working Group request, or a need for additional resources.

**Levels.**
1. **SIRT case lead.** Adjusts priority, pulls in additional Tier 1 SMEs, or reads a party in earlier — all within existing tier definitions.
2. **Governing Board.** Policy or legal matters: finder patch/customer obligations, antitrust, and government or critical-infrastructure coordination. Exception: _Nothing in this policy restricts members from making disclosures strictly required to comply with applicable laws, regulations, or binding administrative frameworks (e.g., CRA, NIS2, DORA, FedRAMP). In such mandatory cases, members do not need GB approval but MUST notify the Board as soon as legally and practically permissible, provided such notification is not prohibited by law._

**Severity changes.** If the severity rating rises, read-in may widen or accelerate; if it falls, it may narrow or slow. Either way the change is recorded with rationale, and the embargo and PD date are re-evaluated. A severity change that crosses to a new Severity Scale level also changes the TLP classification of Tier 1 material. If severity rises to Critical, Tier 1 material is reclassified from TLP:AMBER+STRICT to TLP:RED. The SIRT case lead notifies all Tier 1 participants of the reclassification and confirms that no further intra-organizational sharing occurs without individual approval. If severity falls below Critical to High, the SIRT case lead may reclassify Tier 1 material from TLP:RED to TLP:AMBER+STRICT.

**Contextual override.** The SIRT case lead may classify Tier 1 material as TLP:RED regardless of Severity score when deployment breadth, evidence of active exploitation, or other contextual factors warrant stricter handling. Reclassifying in the other direction (TLP:RED to TLP:AMBER+STRICT for a case at High or above) requires concurrence of the SIRT case lead and at least one additional SIRT member, with rationale recorded in the case read-in log.

**Extension requests.** Any party may request an embargo or coordination-window extension through the SIRT. The default embargo is 30 days, always deferring to the upstream project's own policy, and may be extended for the greater good. The SIRT coordinates the handling of extension requests with the Finder and maintainer, with the maintainer having the final authority.

**Anti-gaming.** Every escalation requires a stated justification and is logged. Severity re-scores are documented as deviation notices. No party may escalate solely to gain earlier or broader access. A pattern of sector-criticality escalation requests from the same member or Working Group across unrelated cases may be treated as evidence of gaming and referred to the Governing Board.

---

## 5. Exception path

Exceptions are handled case-by-case; each is time-bounded, justified, approved by the named authority, and logged.

- **Additional SME at project request.** The maintainer may request that a specific SME be read in; the SIRT admits them at the appropriate tier.
- **Delegated read-in.** A coordinating body (e.g., CISA, ENISA) or a maintainer may nominate who to loop in, within limits set by the SIRT. Delegates must still meet all prerequisites.
- **Early or broader read-in** for severe or broad-scope issues — handled via escalation (§4), time-bounded.
- **Pre-disclosure sharing by a Finder or member.** Sharing a fix or case material with parties outside the SIRT-managed read-in list before PD is discouraged but cannot be prohibited. Any such sharing must be declared to the SIRT and to the Owner before or, where impracticable, immediately after it occurs. The declaration must identify who received the material, what was shared, and why. The SIRT documents the risks and consequences. Where sharing is driven by customer obligations, applicable law, or binding regulatory frameworks (e.g., CRA, NIS2, DORA, FedRAMP), the regulatory-disclosure exception in Section 4 applies instead of this provision.
- **Pre-disclosure sharing by the SIRT.** When the SIRT reads in additional participants beyond the initial read-in list consulted with the Owner, the SIRT case lead notifies the Owner of the identity and tier of each new participant and the justification for inclusion. The Owner may raise objections; the SIRT case lead considers them and records the outcome. If the Owner objects and the SIRT case lead overrides the objection, the override and its rationale are logged and the matter may be escalated to the Governing Board by either party.
- **Tier 1 or Tier 2 participant sharing with their own customers.** A member organization read into a case may not share case material, patches, or workarounds with its own customers or partners before PD except through the tiered pre-notification process managed by the SIRT. If a member determines that its customer obligations or applicable law require earlier sharing, the member must declare this to the SIRT and the Owner before it occurs. The SIRT may then accelerate the pre-notification schedule or adjust the PD date in consultation with the Owner. Undeclared pre-disclosure sharing by a member is treated as an embargo breach under Section 6.
- **Early mitigations/workarounds.** Expected to be shared when patch development will exceed the agreed embargo or disclosure window.
- **Maintainer of Last Resort / time-bounded hardened fork.** Only with SIRT+WG approval.
- **Government / critical-infrastructure coordination without pre-disclosure.** Applies only to designated critical-infrastructure coordination bodies (e.g., national CERTs/CSIRTs acting for critical-infrastructure sectors), not to individual commercial vendors or a single industry vertical. Whether a party qualifies is a SIRT+WG determination, recorded with rationale, and remains consistent with the standing decision not to pre-disclose to any single government.

---

## 6. Embargo breaches

- If an embargo is broken, the **SIRT coordinates** and notifies affected participants and members, depending on what was broken and how.
- Any member who discovers a breach they **must notify the SIRT as soon as the embargo is suspected to be broken.**
- **Embargo breaks = immediate access suspension.** Report any suspected break to the SIRT immediately. Cases will be escalated to the GB for considering permanent removal from the program.**

---

## 7. Roles & authority

| Body | Authority |
|---|---|
| **SIRT case lead** | Assigns tiers; grants and revokes read-in; Level-1 escalation; coordinates breaches. In edge cases and where delays are beyond expected SLAs (e.g., 24 hours for Critical/High issues), Tier placement and escalation decisions may be performed by WG Lead in concurrence with other SIRT members.  |
| **Finder & maintainer** | Consulted on the initial read-in list, embargo, and PD. Notified when additional participants are read in after initial consultation (Section 5). The maintainer sets the final fix and PD date. The maintainer may object to a proposed read-in; objections are considered by the SIRT case lead and recorded, with escalation to the Governing Board available to either party. |
| **Working Group** | Nominates SMEs; requests escalation for its domain or vertical. |
| **Governing Board** | Policy and legal exceptions (finder obligations, antitrust, government coordination). |

---

## Open items to confirm with the Governing Board

- Default read-in **lead times** for Tier 2 and Tier 3.
- The **RACI** of actions permitted at each tier.
- Whether **Tier 1 should split** into analyze and test sub-stages.
- **Delegation limits** — how far a coordinating body or maintainer may extend read-in.
- **Finder patch / customer-obligation** policy (Board).
- **Antitrust documentation** covering early or broad read-in (see the *Sector-neutral, equal access* principle).

---

## Change history

| Version | Date | Description |
|---|---|---|
| 0.2 | 2026-08-24 | Feedback pass: severity-dependent Tier 1 TLP (CVSS 7.0 threshold) with severity-classification scale, §3 rewrite, and severity-change / contextual-override provisions; maintainer holds final authority on extension requests; tightened the sector-criticality trigger and added anti-gaming referral; dropped the "telco" exception and defined critical-infrastructure coordination; added reciprocal pre-disclosure notification (SIRT→Owner) and member-customer sharing rules; added the sector-neutral / equal-access principle. |
| 0.1 | 2026 | Initial draft. |
