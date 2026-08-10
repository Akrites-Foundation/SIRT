# Coordinated Vulnerability Disclosure — A Practical Guide

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
- **The maintainer has final say.** On the fix and the disclosure date, the upstream project decides. The Coordinator advises and facilitates; it does not override.
- **Confidentiality and least privilege.** Information is handled under TLP and shared only with those who have a need to know and can move the fix forward.
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

Each phase below notes what happens, then what "good" looks like for the parties with an active role in it. This guide captures the conceptual process, not the specific mechanics of how these are achieved through automation and agentic workflows (as appropriate). 

### Phase 1 — Discovery & Reporting
A vulnerability is found and reported into a single intake path (the "front door"), so the project isn't approached through many uncoordinated channels.
- **Finder:** submit a clear, reproducible report — affected component and versions, impact, and reproduction steps. Report privately; don't open a public issue or PR.
- **Coordinator:** provide one obvious, low-friction way to report; acknowledge receipt quickly; treat the reporter with respect, not suspicion.
- **Maintainer:** offer a supported private channel (e.g., a `SECURITY.md` and private vulnerability reporting) so reports don't arrive in public.

### Phase 2 — Validation & Triage
The report is confirmed, deduplicated against work already in flight, and scoped.
- **Coordinator:** validate before acting; deduplicate early and automatically; give the benefit of the doubt to under-specified reports and ask for what's missing.
- **Maintainer:** help confirm the issue is real and in scope.
- **Finder:** assist with reproduction where needed.

### Phase 3 — Prioritization
The confirmed issue is assessed for severity and urgency, and resources are allocated.
- **Coordinator:** use severity (e.g., CVSS) and exploitability (e.g., EPSS) as routing and pacing signals — never as a filter to drop a real issue. Note where a "medium" is critical for a specific sector. If your assessment differs from an existing public score, prepare a deviation notice rather than a dispute.
- **Maintainer:** weigh real-world impact and the cost of a fix.
- **Finder:** provide context on impact and exploitability.

### Phase 4 — Read-in & Embargo
The people who will work the case are read in, and the embargo and target public-disclosure (PD) date are set.
- **Coordinator:** read in only those with a need to know who can analyze, patch, test, or stage the fix, at the least-privileged tier sufficient for their role; issue each a read-in notice; propose an embargo. Default to **30 days, deferring to the project's own policy**, with a defined path to extend for good cause.
- **Maintainer:** the project holds final authority over the PD date; the embargo defers to its policy where one exists.
- **Finder:** agree to the embargo and settle attribution preferences (including co-finder handling and declining credit).
- **Consumer (distribution/staging parties):** read in late and narrowly, only as needed to pre-position a fix.

### Phase 5 — Remediation
A patch and/or mitigation is developed and tested privately.
- **Maintainer / working group:** develop the fix; where the maintainer wants help, subject-matter experts contribute patches and testing.
- **Coordinator:** facilitate, supply expertise, and keep the work private until it's ready to move upstream; ensure the fix is tested for regressions.
- **Finder:** verify the fix resolves the issue; offer a workaround for consumers if a full patch will take time.

### Phase 6 — Upstream Engagement
The fix is coordinated with the upstream project for merge and release. (See §4 for detail.)
- **Coordinator:** engage human-to-human first; respect the maintainer's authority, tempo, and preferred workflow; be the single front door to the project.
- **Maintainer:** lead the fix and its release on terms that work for the project.
- **Finder:** stay informed; let the Coordinator handle project contact.

### Phase 7 — Disclosure Preparation
The advisory, identifier, and machine-readable data are prepared for release.
- **Coordinator:** prepare the disclosure package (the VDR) and a machine-readable advisory (CSAF/VEX); favor indicators of compromise over public proof-of-concept; ensure a CVE (or equivalent) and accurate affected-version data.
- **Maintainer:** review and approve the advisory; the project owns what is said about its code.
- **Finder:** confirm credit as agreed.
- **Consumer (staging parties):** finish pre-positioning so remediation can propagate quickly at PD.

### Phase 8 — Public Disclosure
The vulnerability and its remediation are released publicly, in sync.
- **Coordinator:** publish so the fix, advisory, and disclosure land together; keep messaging proportionate and free of hype.
- **Maintainer:** ship the release and its advisory.
- **Finder:** publish any write-up only after the coordinated release, consistent with the agreement.
- **Consumer:** receive an actionable advisory and begin remediation.

### Phase 9 — Post-Disclosure & Retrospective
Deployment is supported and the case is reviewed.
- **Consumer:** deploy the fix or mitigation promptly.
- **Coordinator:** support deployment, capture metrics, and run a blameless retrospective; feed lessons back into the process.
- **Maintainer & Finder:** recognized for the outcome; input welcomed into the retrospective.

---

## 4. Upstream engagement practices

Working *with* projects — not around them — is the heart of good coordination.

- **Meet maintainers where they are.** Adapt to the project's workflow and tools; don't impose yours. Many maintainers are volunteers with limited time.
- **First contact is human-to-human.** Reach a real person before any automation. Use the project's stated security contact or private reporting channel; if none exists, gently encourage adopting one.
- **Keep a profile of engagement rules per project** (the Open Door Policy database): how each project prefers to be contacted, its disclosure policy, and its embargo norms.
- **Operate under a Code of Conduct for engagement** — respectful, non-coercive, and distinct from any general community code.
- **Respect authority and tempo.** The maintainer decides the fix and the date. If parties move at different speeds, pace the coordination to the constraints rather than forcing a schedule.
- **Reduce burden.** Bring a validated report and, where possible, a tested patch — arrive with a solution, not just a problem.

---

## 5. Troubleshooting — when things go sideways

- **Unresponsive, unmaintained, or overwhelmed maintainer.** Distinguish the three: keep trying to re-establish contact with an unresponsive but active project; for a genuinely unmaintained one, escalate the response ladder — (1) the maintainer fixes from the disclosure package; (2) the Coordinator publishes a patch; (3) a working group forks or stewards as a carefully bounded last resort: [Maintainer of Last Resort](https://github.com/Akrites-Foundation/SIRT/blob/main/docs/Maintainer_of_Last_Resort_Guidelines.md), only with oversight approval.
- **Disputed finding or rejected patch.** Handle it blamelessly. If the project declines to act and the risk is real, a deviation notice can document the Coordinator's position without attacking the maintainer.
- **Leak or broken embargo.** Coordinate the response based on what leaked and how; notify affected parties; consider accelerating disclosure. Establish up front that participants must report suspected breaks immediately.
- **Active exploitation in the wild.** Strong signal to accelerate the timeline — defenders need the fix now.
- **Independent discovery / co-finders.** If more than one party found it, coordinate attribution and consider that the secret may not hold — accelerate if needed.
- **Hype and branding pressure.** A branded vulnerability is not more dangerous; keep prioritization based on risk, and keep messaging proportionate.
- **Embargo extension requests.** Any party may request one through the Coordinator, who decides in consultation with the Finder and maintainer, weighing the harm-reduction principle.

---

## 6. Templates & references

**Companion templates & internal artifacts**
- Read-in notice, read-in process, and tier policy (case access control)
- Vulnerability Disclosure Report (VDR) and deviation-notice formats
- Working Group operating guide and the new-engineer conduct one-pager
- OpenSSF `SECURITY.md`, embargo-notification, and disclosure-notification templates

**Authoritative sources this guide draws on**
- OpenSSF *Guide to Coordinated Vulnerability Disclosure for OSS* (finder & maintainer guides, templates) — CC-BY-4.0: <https://github.com/ossf/oss-vulnerability-guide>
- CERT/CC *Guide to Coordinated Vulnerability Disclosure*: <https://certcc.github.io/CERT-Guide-to-CVD/>
- FIRST — Traffic Light Protocol, Multi-Party Coordination & Disclosure guidance, and the PSIRT Services Framework: <https://www.first.org/>
- OWASP *Vulnerability Disclosure Cheat Sheet*: <https://cheatsheetseries.owasp.org/>
- ISO/IEC 29147 (vulnerability disclosure) and ISO/IEC 30111 (vulnerability handling)
- CISA — Coordinated Vulnerability Disclosure process

---

*Maintained by the Akrites Policy/Process work stream. Portions adapt CC-BY-4.0 material from the OpenSSF oss-vulnerability-guide. Propose changes via pull request or the repo Discussions.*
