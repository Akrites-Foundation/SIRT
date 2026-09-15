# Partner Integration Process — CVD (v1)

**Status:** Draft v0.1 — for review by the Governing Board and extended SIRT members

**Owner:** Policy/Process work stream (CRob)

**Scope:** A lean strategic partners process description for how we integrate with them both on intake and downstream.

---
## Process for Strategic Partners integrations

### Scope
Defines how Strategic Partners (government teams, vendor SIRTs, foundations) integrate with Akrites CVD via two contact points: ingress and egress. Downstream propagation and rollout are out of scope.

### Contact Points
- **Intake**: partner-to-us submissions.
   - Standard API (future implementation).
- **Downstream**: us-to-partner disclosure notifications.
   - Email or partner APIs

### Intake Priority Tiers
- P0 — Members - Akrites Members retain the highest priority for intake processing by the pipeline.
- P1 — Partners - A dedicated tier, lower than the Members, for the partners.
- P2 — Public - The internet-public intake is then after this.

To be enforced at the API layer. Future implementation.

### Downstream Disclosure Flow
1. Gate to engaging with Strategic Partners:
   - Working patch exists and,
   - The Akrites members confirmed a working patch (automated or manual patch).
2. Contact is made, in parallel:
   - Partner notification and
   - Upstream contact with the maintainer(s)

Upon contact, the partner is included in the case based on their answer.

#### Report shape
We will contact partners with a neutered version of the report.
- **TBD** on the template

### Contact Method
- v1, manual: dedicated per-partner email is sent
- Future, automated: formal API function; custom integrations per partner.

### Sharing Classification (TLP)
- Partners looped in at **TLP:AMBER+STRICT** to start.
- Then, relaxed to **TLP:AMBER**; partners need to inform their own trusted/extended partners.

### Partner Responsibilities
- Respect active embargo on the case.
- Confirm patch validity.
- Triage internally and route to the correct internal teams.
- Prepare their own disclosures for their trusted lists (esp. governments).
- Downstream propagation and rollout: out of scope for Akrites.

## Notes
This is v1 and intended to be reshaped. Current process is manual; API functions to follow.