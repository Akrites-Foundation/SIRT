# Communications Guidelines

**Type:** Guidelines
**Owner:** Akrites SIRT
**Approver:** SIRT Director
**Status:** Draft for Akrites SIRT review
**Formerly titled:** Communications Playbook, Part I
**Audience:** SIRT staff and coordinators; referenced by WGs and read-in participants
**Related:** [Attribution and AI-Use Disclosure Policy](../policies/attribution-and-ai-use-disclosure-policy.md), [Embargo Handling Guidelines](../guidelines/embargo-handling-guidelines.md), [CVD Policy](../policies/cvd-policy.md), [Read-In Policy](../policies/read-in-policy.md)
**Used with:** [Communications Playbook](../playbooks/communications-playbook.md), which gives a template for each situation

> Every outbound message is written as if it may be read back publicly, quoted by a maintainer, or produced in a postmortem; with or without context.

---

## 1. Audience map

| Audience | Who | Default posture | Primary channels |
| --- | --- | --- | --- |
| **Members** | Akrites member orgs, WG participants | Trusted, need-to-know; least privilege | Member Slack, member mailing list, dashboard/API |
| **External security SMEs** | Read-in experts not on staff | Time-boxed, scoped to the case; spun down after | Case channel, case repo |
| **Upstream maintainers / developers** | Project owners receiving a report | Humble, human-to-human, "maintainer keeps authority" | PVR, security.txt contact, direct email (signed) |
| **Coordinators / Clearinghouses / Strategic Partners** | CISA, ENISA, FIRST, national CERTs, vendor SIRTs, IT-ISACs | Peer coordinator; balanced, no single-government favoritism | Established coordinator channels, partner API, signed email |
| **General public** | Downstream consumers, press, ecosystem | Clear, accurate, machine-readable, no exploitation aid | Akrites website, GHSA/OSV, VEX feed, SIREN |

### 1.1 Intake Priority Tiers
Intake processing by the SIRT pipeline enforces three prioritized tiers:
* **P0 — Members**: Highest intake processing priority reserved for Akrites member organizations.
* **P1 — Strategic Partners**: Dedicated tier for strategic partners (government security teams, vendor SIRTs, ISACs) and trusted OSS security teams (for example, the Linux kernel or ASF security teams) reporting an issue in another project.
* **P2 — Public**: Internet-public intake processing.

* Priority affects processing order only. Every report receives the commitments in the CVD Policy §5, and the currently open reporter classes are set by CVD Policy §12. A report with confirmed active exploitation goes first, whatever its tier (CVD Policy §9). The full rules are in the [Case Handling Procedure](../procedures/case-handling-procedure.md).
  
## 2. Core principles

1. **Confidentiality first and foremost.** Default to TLP:RED at intake. Share up a tier only
   with a reason and, where required, approval.
2. **Least privilege.** People are read into only what they need, for as long as they need it,
   then spun down.
3. **Human-to-human first.** Initial upstream and coordinator outreach is from a person, not an
   automated system, except where the project declares a preference for automation. Bias toward the same human coordinating a given relationship to reduce lead
   time. Move to automation only after a relationship is established and project agrees.
4. **People-to-people / "maintainer to maintainer."** We show up humble and useful. The
   maintainer keeps final authority over their project, fix, and disclosure timing. Akrites
   *contributes* fixes; it does not impose process or tooling.
5. **Meet stakeholders where they are.** Match each community's governance, norms, and preferred
   report style (e.g., a failing unit test plus a patch). Fewest words that fully convey the issue.
6. **Plain, verifiable, and accurate.** No hype, no overstated severity, no speculation presented
   as fact. If we're not sure, we say so.
7. **No single-government pre-disclosure.** If we tell one government, we tell all of them. Never
   pre-disclose to a single state entity.
8. **Attribution is opt-in.** Credit finders and participants only as they've consented (see the
   companion attribution doc).
9. **Traceable.** Every material communication is logged (chain-of-custody / event-of-interest);
   assume it can be reproduced in a postmortem, become public, or taken out of context.

## 3. TLP quick reference (as used by Akrites)

| Marking | Meaning in practice |
| --- | --- |
| **TLP:RED** | Named recipients only. Intake and the automated pipeline (Tier 0). No forwarding. |
| **TLP:AMBER+STRICT** | Recipient's organization only, need-to-know. Verification and remediation material (Tiers 1, 1.5, 2). |
| **TLP:AMBER** | Recipient's organization and its clients, need-to-know. Downstream staging (Tiers 3, 3.5). No onward sharing to other organizations. |
| **TLP:GREEN** | Community/peer sharing, not public. **Not used for case material before PD** (CVD Policy §8); use for non-case material such as postmortem summaries and trend reports. |
| **TLP:CLEAR** | Public — only at/after PD. |

Every message carries an explicit TLP label written as FIRST TLP 2.0 specifies: in capitals with no spaces (e.g., `TLP:AMBER+STRICT`), placed directly before the information it covers, and — for email — in the subject line. When in doubt, mark higher and ask. If a message contains mixed levels, the overall marking is the most restrictive.

Standard forms:

```
Subject: [TLP:RED] {Project/Component} — private vulnerability coordination ({tracking-id})
TLP:AMBER+STRICT — Private vulnerability information. Share only with the read-in list for {case-id}.
```

## 4. Authenticity & verification

Impersonation is a real risk; make Akrites easy to verify and hard to spoof.

- Publish and reference the official Akrites GitHub handle and website; list them in `security.txt`.
- Prefer **signed** email (S/MIME) and/or **GPG** signatures for maintainer and coordinator contact.
- Offer a verification path in first-contact messages ("you can confirm this outreach at
  {akrites.dev/verify} or via our listed security.txt").
- Never ask a maintainer to send exploit code or secrets over an unverified channel.

## 5. Tone & style standards

- Lead with what the reader must **do** and **by when**; put detail below.
- Be specific about status and next steps; avoid vague "we're working on it."
- Never paste PoC/exploit code into Slack or email; link to the controlled case repo instead.
- Keep the model-plus-harness and internal tooling details internal; publish AI assistance by
  capability only (see attribution doc).
- Acknowledge uncertainty and the maintainer's authority. Offer, don't demand.
- Use "initial/proposed patch" language when sending fixes upstream, inviting refinement.

## 6. Channel & disclosure matrix

| Content type | Channel | Typical TLP |
| --- | --- | --- |
| New case intake / triage | Case repo (private GH), case channel | RED |
| Remediation / patch work | Private case repo, analyst workbench | AMBER+STRICT |
| Member awareness (no specifics) | Member mailing list / member Slack | AMBER |
| Read-in SME coordination | Case channel (time-boxed) | RED / AMBER+STRICT |
| Strategic Partner & Coordinator Engagement | Partner API / dedicated signed email | TLP:AMBER (≤ 24 h before PD, Tier 3.5) |
| Upstream engagement | PVR / signed email / security.txt contact | AMBER+STRICT (Tier 1.5) |
| Public advisory | Website, GHSA, OSV→CVE/EUVD, VEX feed, SIREN | CLEAR |

**Hard rules:** no files or exploit code on Slack; no WG TLP:RED work conducted in general Slack;
encrypted file share only; no pre-disclosure to any single government.

