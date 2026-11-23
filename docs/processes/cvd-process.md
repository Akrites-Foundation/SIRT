# CVD Process

**Type:** Process
**Owner:** Akrites SIRT
**Approver:** SIRT Director
**Status:** Draft — for Akrites SIRT review
**Formerly titled:** CVD Playbook — A Practical Guide

*For the SIRT and anyone coordinating a vulnerability disclosure with upstream open source projects.*

This guide offers practical advice for producing the best outcome for every party in a coordinated vulnerability disclosure (CVD): the **Finder**, the **Maintainer**, the **Consumer**, and the **Coordinator**. It is organized around the disclosure lifecycle, and at each step it calls out what "good" looks like for each party.

CVD is a process, not an event — a repeated cycle of "what should I do next, and who else needs to know?" that continues until the answers are *nothing* and *no one*. It is also, inherently, a balancing act: disclosing too early hands attackers an advantage, disclosing too late leaves defenders exposed. Good coordination manages that tension deliberately.

> **How to use this guide.** Read the Principles and the Parties sections first — they frame every decision that follows. Use the Lifecycle as the working spine of a case, and the Troubleshooting section when things go sideways. Templates and sources are listed at the end.

---

## 1. Principles

These principles, drawn largely from long-standing coordination practice, guide every decision:

- **Reduce harm.** The goal is to shrink the window of attacker advantage while a fix is prepared — not to maximize any single party's interest. Every timing and disclosure choice is judged against this.
- **Presume benevolence.** Assume anyone who took the time to report an issue is acting in good faith and wants to reduce risk. Extend the same good faith to maintainers who are slow or stretched.
- **Avoid surprise.** Surprised parties make defensive, adversarial choices. Tell people what to expect, and keep them informed as things change.
- **Reward good behavior.** You cannot force every party to share your values or rules. It works better to make cooperation easy and rewarding than to punish missteps.
- **Act ethically and neutrally.** The Coordinator is an honest broker, not an advocate for one side. Meet maintainers where they are; do not impose process or tooling on them.
- **The maintainer has final say.** On the fix and the disclosure date, the upstream project decides. The Coordinator advises and facilitates; it does not override — except where active exploitation or a public embargo break requires acceleration to protect users (CVD Policy §9).
- **Confidentiality and least privilege.** Information is handled under TLP and shared only with those who have a need to know and can move the fix forward.
- **Be transparent about AI use.** Where AI/LLM tooling materially assisted — whether the Finder's or the Coordinator's — say so, at a capability level, in the case record and the advisory. AI use never removes human accountability, and public AI services are treated as non-confidential (see the [AI and LLM Use Disclosure Policy](https://github.com/Akrites-Foundation/SIRT/blob/main/docs/policies/attribution-and-ai-use-disclosure-policy.md)).
- **Improve continuously.** Review each case blamelessly, capture what worked and what didn't, and feed it back into the process.

---

## 2. The four parties and what a good outcome means

**Finder** — the individual or organization that discovered the vulnerability.
*A good outcome:* their report is validated and acted on, they receive the credit they want (or the anonymity they request), and they are kept informed without being exposed to legal or reputational harm.
*What the guide asks of them:* report clearly and completely, respect the embargo, and don't release details ahead of the coordinated date.

**Maintainer** — the upstream project that owns the affected code.
*A good outcome:* their authority over the fix and timing is respected, the added burden is minimal, they are never surprised or publicly pressured, and they receive a high-quality report (ideally with a patch).
*What the guide asks of them:* engage in good faith and communicate their capacity and constraints early.

**Consumer** — the downstream users and deployers who must act once a fix exists.
*A good outcome:* a timely, accurate, machine-readable advisory with clear remediation, delivered fairly at public disclosure so they are not left exposed.
*What the guide asks of them:* deploy promptly and use the provided data rather than waiting for exploitation.

**Coordinator** — the neutral party (here, the SIRT) facilitating the process.
*A good outcome:* the embargo holds, handoffs are clean, every party is treated fairly, and the process is trusted and improves over time.
*What the guide asks of them:* neutrality, least privilege, and transparency about how the process works.

---

## 3. The coordinated lifecycle

The phases below are the nine phases of the [CVD Policy](../policies/cvd-policy.md) §7, which holds the canonical list. For each phase this guide notes what happens, then what "good" looks like for the parties with an active role in it. It captures the conceptual process, not the specific mechanics of how these are achieved through automation and agentic workflows (as appropriate). The step-by-step actions are in the [Case Handling Procedure](../procedures/case-handling-procedure.md).

```
Discover → Deduplicate & Triage → Validate → Coordination → Patch → Test → Document → Distribute → Disclose
```

### Phase 1 — Discover
A vulnerability is found and reported into a single intake path (the "front door"), so the project isn't approached through many uncoordinated channels.
- **Finder:** submit a clear, reproducible report — affected component and versions, impact, and reproduction steps. Report privately; don't open a public issue or PR. Note whether AI/LLM tooling assisted and whether it was public or confidential — public tooling can foreclose an embargo.
- **Coordinator:** provide one obvious, low-friction way to report; acknowledge receipt quickly; treat the reporter with respect, not suspicion.
- **Maintainer:** offer a supported private channel (e.g., a `SECURITY.md` and private vulnerability reporting) so reports don't arrive in public.

### Phase 2 — Deduplicate & Triage
The report is deduplicated against work already in flight and scoped.
- **Coordinator:** deduplicate early and automatically; give the benefit of the doubt to under-specified reports and ask for what's missing.
- **Maintainer:** help decide whether the report is a vulnerability, a bug, or intended behavior.
- **Finder:** respond to requests for missing detail.

### Phase 3 — Validate
The report is confirmed and reproduced, then assessed for severity and urgency, and resources are allocated.
- **Coordinator:** validate before acting. Use severity (CVSS v4.0 and the severity label) and exploit evidence (exploit state and SSVC priority — see the [Severity Scoring Guidelines](../guidelines/severity-scoring-guidelines.md)) as routing and pacing signals — never as a filter to drop a real issue. The order in which reports are worked is set in the [Case Handling Procedure](../procedures/case-handling-procedure.md). Note where a "medium" is critical for a specific sector. If your assessment differs from an existing public score, prepare a deviation notice rather than a dispute.
- **Maintainer:** help confirm the issue is real and in scope; weigh real-world impact and the cost of a fix.
- **Finder:** assist with reproduction where needed, and provide context on impact and exploitability.

### Phase 4 — Coordination
The people who will work the case are read in, the embargo and target public-disclosure (PD) date are set, and the fix is coordinated with the upstream project. (See §4 for upstream engagement detail.)
- **Coordinator:** read in only those with a need to know who can analyze, patch, test, or stage the fix, at the least-privileged tier sufficient for their role; issue each a read-in notice; propose an embargo. Offer a standard **15-business-day proposed embargo** (targeting total time to Public Disclosure of ≤ 17 bd Low/Med, ≤ 21 bd High, ≤ 24 bd Critical), deferring to the project's own policy, with a defined path to extend for good cause. Engage upstream human-to-human first; respect the maintainer's authority, tempo, and preferred workflow; be the single front door to the project.
- **Maintainer:** the project holds final authority over the PD date; the embargo defers to its policy where one exists. Lead the fix and its release on terms that work for the project.
- **Finder:** agree to the embargo and settle attribution preferences (including co-finder handling and declining credit). Stay informed; let the Coordinator handle project contact.
- **Consumer (distribution/staging parties):** read in late and narrowly, only as needed to pre-position a fix.

### Phase 5 — Patch
A patch and/or mitigation is developed privately.
- **Maintainer / working group:** develop the fix; where the maintainer wants help, subject-matter experts contribute patches.
- **Coordinator:** facilitate, supply expertise, and keep the work private until it's ready to move upstream.
- **Finder:** offer a workaround for consumers if a full patch will take time.

### Phase 6 — Test
The patch is tested privately for regressions.
- **Maintainer / working group:** run regression, smoke, and other testing to confirm the vulnerability is resolved and no new regressions are introduced.
- **Coordinator:** ensure the fix is tested for regressions.
- **Finder:** verify the fix resolves the issue.

### Phase 7 — Document
The advisory, identifier, and machine-readable data are prepared for release.
- **Coordinator:** prepare the disclosure package (the VDR) and machine-readable advisory data (OSV, plus CSAF/VEX where published); favor indicators of compromise over public proof-of-concept; ensure a CVE (or equivalent) and accurate affected-version data. Record the case's AI use — the Finder's and the SIRT's — and include the standard two-line AI-use block in the advisory.
- **Maintainer:** review and approve the advisory; the project owns what is said about its code.
- **Finder:** confirm credit as agreed.

### Phase 8 — Distribute
The patch and documentation are staged so remediation can propagate quickly at PD.
- **Coordinator:** share documentation with read-in Collaborators so they can prepare consistent, tailored communications.
- **Consumer (staging parties):** finish pre-positioning so remediation can propagate quickly at PD.

### Phase 9 — Disclose
The vulnerability and its remediation are released publicly, in sync.
- **Coordinator:** publish so the fix, advisory, and disclosure land together; keep messaging proportionate and free of hype.
- **Maintainer:** ship the release and its advisory.
- **Finder:** publish any write-up only after the coordinated release, consistent with the agreement.
- **Consumer:** receive an actionable advisory and begin remediation.

### After Disclose — deployment and retrospective
Deployment is supported and the case is reviewed. This is not a CVD Policy phase; it follows Phase 9.
- **Consumer:** deploy the fix or mitigation promptly.
- **Coordinator:** support deployment, capture [metrics](../reference/metrics-framework.md), and run a blameless retrospective; feed lessons back into the process.
- **Maintainer & Finder:** recognized for the outcome; input welcomed into the retrospective.

---

## 4. Upstream engagement practices

Working *with* projects — not around them — is the heart of good coordination.
The full practice is in the [Upstream Engagement Guidelines](../guidelines/upstream-engagement-guidelines.md); the essentials:

- **Meet maintainers where they are.** Adapt to the project's workflow and tools; don't impose yours. Many maintainers are volunteers with limited time.
- **First contact is human-to-human.** Reach a real person before any automation. Use the project's stated security contact or private reporting channel; if none exists, gently encourage adopting one.
- **Keep a profile of engagement rules per project** (the Open Door Policy database — see the Glossary): how each project prefers to be contacted, its disclosure policy, and its embargo norms.
- **Operate under a Code of Conduct for engagement** — respectful, non-coercive, and distinct from any general community code.
- **Follow the engagement practices in the Upstream Engagement Guidelines** — respectful, non-coercive, and distinct from any general community code.
- **Respect authority and tempo.** The maintainer decides the fix and the date. If parties move at different speeds, pace the coordination to the constraints rather than forcing a schedule.
- **Reduce burden.** Bring a validated report and, where possible, a tested patch — arrive with a solution, not just a problem.

---

## 5. Troubleshooting — when things go sideways

- **Unresponsive, unmaintained, or overwhelmed maintainer.** Distinguish the three: keep trying to re-establish contact with an unresponsive but active project (see the [contact ladder](../procedures/molr-procedure.md#contact-and-escalation-ladder)); for a genuinely unmaintained one, escalate the response ladder — (1) the maintainer fixes from the disclosure package; (2) the Coordinator publishes a patch; (3) a per-CVE Maintainer of Last Resort release as a carefully bounded last resort, only with Governing Board approval: [Maintainer of Last Resort Policy](../policies/molr-policy.md).
- **Disputed finding or rejected patch.** Handle it blamelessly. If the project declines to act and the risk is real, a deviation notice can document the Coordinator's position without attacking the maintainer.
- **Leak or broken embargo.** Coordinate the response based on what leaked and how; notify affected parties; consider accelerating disclosure. Establish up front that participants must report suspected breaks immediately.
- **Active exploitation in the wild.** Strong signal to accelerate the timeline — defenders need the fix now.  If the SIRT Director declares a Critical Situation, see the [Crit-Sit Playbook](../playbooks/crit-sit-playbook.md).
- **Independent discovery / co-finders.** If more than one party found it, coordinate attribution and consider that the secret may not hold — accelerate if needed.
- **Hype and branding pressure.** A branded vulnerability is not more dangerous; keep prioritization based on risk, and keep messaging proportionate.
- **Embargo extension requests.** Any party may request one through the Coordinator; the maintainer decides, with the Coordinator advising and consulting the Finder, weighing the harm-reduction principle.

---

## 6. Templates & references

**Companion templates & internal artifacts**
- [Read-In Policy](../policies/read-in-policy.md), [Read-In Notice template](../../templates/case-read-in-notice-template.md), [read-in log](../../templates/case-read-in-log-template.csv)
- [Case Handling Procedure](../procedures/case-handling-procedure.md) — the on-duty, step-by-step checklist for each phase
- VDR and deviation-notice formats *(to be published)*
- [Working Group Governance Policy](../policies/wg-governance-policy.md), [Working Group Operating Procedure](../procedures/wg-operating-procedure.md) and the [engineer read-in one-pager](../reference/read-in-engineer-quick-reference.md)
- OpenSSF `SECURITY.md`, embargo-notification, and disclosure-notification templates
- [Attribution and AI-Use Disclosure Policy](../policies/attribution-and-ai-use-disclosure-policy.md), and the intake template's "AI / LLM tooling used" section

**Authoritative sources this guide draws on**
- OpenSSF *Guide to Coordinated Vulnerability Disclosure for OSS* (finder & maintainer guides, templates) — CC-BY-4.0: <https://github.com/ossf/oss-vulnerability-guide>
- CERT/CC *Guide to Coordinated Vulnerability Disclosure*: <https://certcc.github.io/CERT-Guide-to-CVD/>
- FIRST — Traffic Light Protocol, Multi-Party Coordination & Disclosure guidance, and the PSIRT Services Framework: <https://www.first.org/>
- OWASP *Vulnerability Disclosure Cheat Sheet*: <https://cheatsheetseries.owasp.org/>
- ISO/IEC 29147 (vulnerability disclosure) and ISO/IEC 30111 (vulnerability handling)
- CISA — Coordinated Vulnerability Disclosure process

---

*Maintained by the Akrites Policy/Process work stream. Portions adapt CC-BY-4.0 material from the OpenSSF oss-vulnerability-guide. Propose changes via pull request or the repo Discussions.*
