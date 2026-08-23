# Akrites SIRT Maintainer of Last Resort Guidelines - DRAFT v0.2

### Guidelines for VDR Handling, Maintainer of Last Resort, and Stewardship Transition

*A working framework for a PSIRT/CNA coordinating vulnerability disclosure into open source projects that cannot, will not, or do not respond — and for standing up an Akrites SIRT "Maintainer of Last Resort" function.*

> Status: draft for review · Aligns with the Akrites SIRT model (one front door, least privilege, synchronized disclosure, meet maintainers where they are). Adapt org names, timelines, and approval bodies to your charter before adoption.

> **Companion document.** [What Akrites Will and Won't Do to Your Project](./What_Akrites_Will_And_Wont_Do.md) is the plain-language, maintainer-facing statement of the commitments made here. The two documents are released together and must not contradict each other; where they appear to, the companion's promises are the floor.

**What changed in v0.2:** the unit of work is now the *vulnerability*, not the project (§1.2, §6.1); the deliverable is a *patch series against a pinned upstream commit*, not a maintained branch (§6.3); Akrites will never petition for, accept, or hold a package namespace it did not create (§2, §5.3a, §8); the entry test is restated negatively (§6.1); the abandonment clock is decoupled from the disclosure clock and floored at 90 days (§3.2); conflicts of interest are handled by recusal rather than by reclassifying the case (§1.1, §6.2); wind-down freezes the artifact rather than withdrawing it (§7.5).

---

## 1. Purpose and scope

### 1.1 What this document governs

This document governs what your PSIRT (acting as a Finder/coordinator and CNA) and the Akrites SIRT do when a coordinated vulnerability disclosure (CVD) toward an upstream open source project **stalls**. There are three stall conditions:

1. **No capacity or tooling** — the project wants to fix the issue but has no private reporting channel, no security contact, no CI/release capacity, or no bandwidth to ingest and act on a qualified report.
2. **Deliberate non-fix (EOL / feature-complete / WONTFIX)** — the maintainer is reachable and decides the affected branch will not be patched.
3. **Unresponsive** — no contact is established within the escalation window, for any reason (lost interest, moved on, dead project, maintainer unreachable, or worse — a compromised or hostile maintainer).

**Conflicts of interest are not a stall condition.** A maintainer with direct ties into Akrites (Global Board, TOC, or a WG), or an Akrites member whose product depends on the affected package and who is pushing for a particular outcome, creates a *decision-making* problem, not a *classification* problem. A responsive maintainer is a responsive maintainer regardless of their affiliation, and must never be routed toward last-resort machinery because Akrites cannot cleanly decide their case. The remedy is recusal and reassignment to an unconflicted decision-maker (§6.2), and disclosure of the conflict in the case record. Akrites-affiliated maintainers receive neither better nor worse treatment than strangers.

### 1.2 Two tracks, and the line between them

This document describes two tracks that must not be allowed to blur into one another under deadline pressure.

- **Track A — upstream assistance (§§3–5).** Supplying the capacity, tooling, coordination, and disclosure machinery a maintainer lacks. This is the core Akrites product and will cover the overwhelming majority of cases. A capacity gap is met by supplying capacity; a disagreement is met by an advisory and a VEX.
- **Track B — last-resort action (§§6–7).** A rare, governed exception, entered only when Track A has failed for the reason set out in the entry test at §6.1: **there is no party with both the legal right and the demonstrated willingness to ship the fix.**

**The Maintainer of Last Resort (MoLR) function is hospice, not adoption.** The public Akrites commitment is that fixes to the latest version reach everyone in a timely fashion. That is a *fix-delivery* promise, not a maintenance promise. Accordingly:

- **The unit of work is the vulnerability, not the package.** Akrites adopts a CVE, not a project. An approval covers *this fix*; a second vulnerability in the same package is a fresh entry decision with a fresh approval record (fast-pathed under §6.2.1, not waived).
- **What Akrites ships is a last-resort security release, not a maintained fork.** The function keeps its name — it is in the press release, the open letter, and the public record, and renaming it now costs more than it buys. The *artifact* is what gets named narrowly, and §6.3's definition does the work the name will not.

Out of scope: the mechanics of triage, dedup, and severity scoring already covered by the standard SIRT intake process. This picks up at the point where **the upstream handoff is the problem**.

---

## 2. First principles for these scenarios

These extend the Akrites principles into the hard cases. Keep them in view; every decision below should be traceable to one of them.

- **Downstream protection is the goal, not upstream compliance.** A maintainer's silence or refusal does not relieve you of the duty to protect the people running the software. But it also does not entitle you to seize the project.
- **Right to fork comes from the license, not from the SIRT.** Confirm the license permits your intended action before you touch code. Trademark is separate from copyright — see §10.
- **Akrites never takes a name.** Akrites does not petition for, accept, or hold custody of any package namespace it did not itself create, in any registry, under any circumstances. This is unconditional and public (§8). Not holding namespaces is a security control as much as an ethical one.
- **Least self-help.** Prefer helping the maintainer act over acting for them. Escalate only as far as the situation requires. Every escalation stage is documented before the next is opened (§3.1).
- **Prioritize the patch over a fork.** Carrying code creates an open-ended commitment and expands the scope of Akrites. The cheapest durable fix is usually *upstream dependency migration* by an intermediate maintainer, not a fork of the leaf (§8.4).
- **The fork is a new attack surface.** A hastily-stood-up fork with a lightly-vetted new maintainer is exactly the `xz-utils` (CVE-2024-3094) failure mode. Treat MoLR onboarding and steward vetting as a security control, not a formality.
- **Severity accelerates mitigation; it never accelerates a property judgment.** Exploitation pressure compresses the disclosure clock. It does not compress the finding that a maintainer has abandoned their project (§3.2).
- **Everything is embargoed until it isn't.** TLP governs every artifact and every party from intake to Public Disclosure (PD). Non-fix and unresponsiveness do **not** default a case to open.
- **Document the trail.** Every contact attempt, every maintainer decision, every governance approval, every recusal is recorded. The record is what makes an eventual last-resort release or disclosure defensible.
- **How can we help?** A maintainer who is overwhelmed by report volume is offered *help with the volume* — triage, patch authorship, coordination, release engineering — for as long as they want it. They are never offered a fork. An offer to take over is not a form of assistance, and must never be presented to a responsive maintainer as one.

---

## 3. The two clocks

Two separate clocks run in these cases, and v0.1 conflated them. The **disclosure clock** governs how fast downstream gets protected. The **abandonment clock** governs when Akrites is entitled to conclude that a project has no maintainer. They start together and run at different speeds, and the first must never be allowed to drive the second.

*Unit convention: "business days" excludes weekends and the public holidays of the SIRT's operating jurisdiction. "Days" without qualification means calendar days. Where a stage is expressed in business days and a downstream stage in calendar days, log both the elapsed business days and the calendar date so the record is unambiguous.*

### 3.1 The disclosure clock — contact and escalation protocol

Before any scenario branch is chosen, you must run — and log — a **good-faith, escalating contact protocol**. This is the evidentiary spine for everything downstream. The clock starts at **T0 = first outbound contact attempt** to the upstream project.

| Stage | Timing (default; SSVC-adjustable) | Action | Channels attempted |
|---|---|---|---|
| **Attempt 1** | T0 | Private report via preferred channel | `SECURITY.md` / security.txt contact, GitHub/GitLab private advisory, listed security email |
| **Attempt 2** | T0 + 5 business days | Re-send + widen | Maintainer email(s) from commit history, package registry metadata contact, project chat (private DM only) |
| **Attempt 3** | T0 + 10 business days | Escalate to ecosystem | Foundation/umbrella org, funding org (e.g. STF/OpenSSF/Alpha-Omega), distro security teams that carry the package |
| **Coordinator handoff** | T0 + 15 business days | Bring in a neutral coordinator | Akrites SIRT, CERT/CC (VINCE), or the CVE Program CNA-LR |
| **Decision point** | T0 + ~30 calendar days (adjust by severity/EPSS/exploitation) | Classify the case into a §5 scenario; publish advisory, VEX, and mitigation | — |

Rules for the disclosure clock:

- **Severity bends the clock, it doesn't remove stages.** Active exploitation, high EPSS, or critical-infrastructure blast radius compresses the intervals (and may justify emergency distro-only pre-notification). A low-severity issue may extend them. Use SSVC to make and record that call; never skip the *documentation* of an attempt.
- **Each attempt is logged** with timestamp, channel, addressee, and outcome (see Appendix A). "Read receipt but no reply" is a materially different fact from "bounced" — record which.
- **A single acknowledgement resets the interaction to normal CVD**, not to this protocol. If the maintainer engages at any stage, you drop back to standard coordination and the SIRT steps into a supporting role. It also stops the abandonment clock permanently for this case.
- **Never disclose technical detail in escalation messages** to third parties beyond what least-privilege requires. "We have a qualified security finding in project X and cannot reach the maintainer" is usually enough to enlist a foundation's help without leaking the vulnerability.
- **Reaching the decision point is not an abandonment finding.** It classifies the case and releases the advisory, VEX, and any mitigation. Nothing at T0+30 authorizes Track B.

### 3.2 The abandonment clock — the property judgment

An abandonment finding is a statement about a person, not about a schedule. Illness, bereavement, sanctions or export restrictions, loss of connectivity, military service, and unsettled estates all look identical to disinterest from the outside, and these are precisely the cases where being wrong is least defensible. The clock is therefore slower, floored, and insensitive to severity.

- **Floor: no abandonment finding may be made before 90 calendar days of total silence across every attempted channel**, regardless of severity, EPSS, exploitation status, or downstream pressure. There is no emergency exception. If the situation is urgent, the urgency is discharged through advisory, VEX, mitigation, distro coordination, and intermediate-maintainer outreach (§8.4) — all of which are available on the disclosure clock.
- **Silence must be total.** Any signal of life on the account, repo, registry, or elsewhere — a commit, a release, a comment, a login-derived signal a registry is willing to confirm — restarts the clock and routes the case to §5.3a.
- **Check for a declared intent first.** If the maintainer has pre-registered a preference for what happens if they go dark (§7.6), that preference governs and the finding is unnecessary.
- **Make a positive record, not an absence of one.** The finding documents what was checked, when, and by whom: repository activity, release history, registry account state, social and employment signals where lawfully and proportionately obtainable, and outreach to known contributors and co-maintainers.
- **Two named people sign the finding**, at least one outside the case team.

---

## 4. Scenario decision table

Once contact resolves (or fails to), classify and route. Note that "last-resort release on the table" never means *now* — it means the case may become eligible once the §3.2 abandonment clock and the §6.1 entry test are both satisfied.

| Signal observed | Scenario | Primary path (Track A) | Track B on the table? |
|---|---|---|---|
| Maintainer engages, wants fix, lacks channel/CI/bandwidth | §5.1 Capacity gap | **Assist in place** — do the coordination work *for* them, for as long as they want it | **No.** Never. A capacity gap is met by supplying capacity |
| Maintainer engages, declines to fix (EOL / feature-complete / WONTFIX), clearly stated | §5.2 Deliberate non-fix | **Respect + protect downstream** — advisory, VEX, downstream mitigation | Only if the §6.1 entry test is met, which requires that no other party will carry the patch |
| No contact by decision point; project shows life elsewhere | §5.3a Silent but alive | Continue escalation; intermediate-maintainer outreach (§8.4) | No — the abandonment clock has restarted |
| No contact anywhere for ≥90 days; §3.2 finding signed | §5.3b Abandoned | §6 last-resort release + §7 stewardship search | Yes, subject to §6.1 |
| Maintainer unreachable **and** signals of compromise/hostility | §5.3c Suspect | **Security incident** — do not hand credentials; treat as adversarial | Yes, with heightened vetting |

---

## 5. Track A — scenario playbooks

### 5.1 Project lacks tooling or capacity to ingest the report

The project *wants* to do the right thing. Your job is to remove friction, not to take over.

**Do:**
- Offer a **fully qualified bundle**: vulnerability detail, reproducible PoC/PoV, a proposed patch, and tests. Maintainers should be *reviewing a solution*, not solving cold.
- Suggest enabling **PVR (Private Vulnerability Reporting)**: this is our default preference for collaboratively developing a solution, because it allows a temporary private fork to be created and the patch to be developed against it without public exposure.
- Offer to **stand up a private channel** for them (e.g. help enable GitHub/GitLab private security advisories, or run the embargoed thread inside the SIRT's hardened enclave under TLP:AMBER+STRICT).
- Offer to **run the coordination overhead**: CVE assignment (via the appropriate CNA — see §10), advisory drafting, CVSS/CWE/SSVC/EPSS enrichment, VEX generation, distro and downstream notification, and PD messaging support.
- **Let them keep control and credit.** They approve/revise the patch; they set or negotiate the disclosure date; they own their project's public messaging; credit is theirs.
- **Offer sustained help where the problem is volume**, not a one-off. A maintainer buried under reports gets triage capacity, patch authorship, and release engineering for as long as they will accept it.

**Don't:**
- Don't publish anything to the project's namespace yourself, ever — see §8. This is not conditional on their being engaged.
- Don't impose your tooling or process as a condition of help. Meet them where they are.
- **Don't offer a fork.** A responsive maintainer is never presented with a takeover as a menu option, however overloaded they are. If they ask about one unprompted, point them at §7.6 and the companion document.

**Exit:** patch merged and released, advisory published in coordination, SIRT steps back. This scenario must never reach §6.

### 5.2 Deliberate non-fix — EOL, feature-complete, or WONTFIX

A reachable maintainer's decision not to fix is a **legitimate exercise of their authority**, and the guidelines must honor it. Your obligation shifts entirely to protecting the people still running the code.

**First, pin down which kind of non-fix it is** (this changes the downstream story materially):

- **Formally EOL / unsupported branch** — the maintainer has published an end-of-life for the affected version. Clean signal.
- **Feature-complete, still "supported" in principle** — maintainer considers the code done and won't touch it for this class of issue.
- **WONTFIX on the merits** — maintainer disputes severity, considers it out of the threat model, user configuration and advised against in docs, or judges the fix cost unjustified.

**Do:**
- **Record the maintainer's position in their own words**, with date and rationale (Appendix B). This becomes part of the advisory.
- **Issue an advisory anyway.** A vulnerability that will not be fixed upstream is *more* important to communicate to downstream, not less. Assign the CVE through the appropriate CNA (§10), publish through OSV/CVE/EUVD.
- **Publish a VEX statement** conveying the true state: affected, `fix_status: will_not_fix`, plus any mitigation. Downstream scanners and SBOM tooling depend on this to make risk decisions.
- **Offer a downstream mitigation or configuration workaround** even when no code fix will land — e.g. a compensating control, a hardened default, or a patch that consumers can apply locally.
- **Set a disclosure window** consistent with your policy; a maintainer's WONTFIX does not oblige indefinite embargo, but coordinate PD timing with distros/registries carrying the package so downstream can react.
- **Go to the intermediate maintainers** (§8.4). A single dependency change in a widely-used library that depends on this package protects thousands of dependency trees at once and requires nobody to adopt anything.

**Then, and only then, test §6.1.** A WONTFIX on a niche, lightly-used library is a footnote. A WONTFIX (or hard EOL) on something in the critical-infrastructure dependency graph, still shipping in distros and images, may become eligible for §6 — **but the entry test is not "the maintainer said no."** It is that no party anywhere has both the right and the willingness to ship the fix. Exhaust first:
  - a distro, downstream consumer, or dependent project volunteering to carry the patch,
  - a community successor package that already exists,
  - the maintainer blessing a fork, a transfer to a foundation, or a successor.

**Don't:**
- Don't reframe a clear WONTFIX as "unresponsive" to justify a last-resort release. The §5.3 machinery exists for silence, not for disagreement.
- Don't treat maintainer disagreement as a defect of character in public messaging (§9).
- Don't publish into the original namespace under any circumstance (§8).

### 5.3 Unresponsive project

No contact established by the decision point despite the full §3.1 protocol. Split by what the evidence shows.

**5.3a Silent but alive** (recent commits/releases elsewhere, active elsewhere but not on security): the §3.2 clock has restarted and there is no abandonment finding available. Keep escalating through the ecosystem and funders, keep the advisory and VEX current, and shift effort to the routing work in §8 — particularly intermediate-maintainer outreach, which does not require the original maintainer's participation at all.

> **Akrites does not petition for a transfer of the package name.** v0.1 described registry abandonment processes (PEP 541, the npm dispute policy, and their equivalents) as "the legitimate route into the original namespace." That path is closed — see §8 for the commitment and the reasoning. Where a maintainer *wishes* to transfer their project, Akrites facilitates transfer to a durable steward or foundation and takes no custodial role. Where a third party independently pursues a registry process, Akrites does not initiate, sponsor, or advocate for it, and will supply factual case information only if the registry requests it.

**5.3b Demonstrably abandoned/dead** (§3.2 finding signed: no activity across repo, releases, registry account, and contact for ≥90 days; contributors and co-maintainers canvassed): test §6.1 for a **last-resort security release** and, in parallel, launch **§7 stewardship** to find a durable owner.

**5.3c Suspect** (unreachable **and** indicators of compromise, or a maintainer/handoff pattern resembling a social-engineering takeover à la `xz`): stop treating this as a coordination problem and **open a security incident**. Do not transfer credentials, do not accept an unvetted "new maintainer" who conveniently appears, and route provenance concerns to the registry and relevant CERTs. Any release here is built clean-room from a known-good commit, with heightened §7.3 vetting. Note that 5.3c is the one case where the §3.2 90-day floor may be satisfied by evidence of compromise rather than by elapsed time — a compromised account is not an absent maintainer, and the finding to be made is different.

---

## 6. Track B — Maintainer of Last Resort

MoLR is the SIRT publishing a **time-bounded, clearly-marked, governed security release** carrying a specific fix, when abandonment (5.3b), a suspect handoff (5.3c), or a critical-infra non-fix (5.2) would otherwise leave depended-upon software exposed and **no other party will act**. It is deliberately the **least attractive** option — a bridge, not a destination, and hospice, not adoption.

### 6.1 Entry test (all must hold)

The entry test is stated as a **negative**: MoLR requires *the absence of any party with both the legal right and the demonstrated willingness to ship the fix.* Maintainer bandwidth is not an entry condition; it is met by supplying bandwidth. Maintainer disagreement is not an entry condition; it is met by an advisory and a VEX.

1. **No willing rights-holder exists.** The §3.1 protocol was run in full and logged; the §3.2 finding is signed where applicable; and §5 alternatives — assist-in-place, distro or downstream carry, a dependent project volunteering, an existing community successor, a maintainer-blessed transfer, intermediate-maintainer migration (§8.4) — are documented as exhausted or unavailable. Each alternative is recorded as *asked and declined*, not merely *assumed unavailable*.
2. **The software meets a published criticality threshold.** "Critical" must be evidenced, not asserted, against published and versioned inputs, with the evidence attached to the approval record: OpenSSF Criticality Score, count of distros carrying the package, direct and transitive dependent counts, and SBOM prevalence across Akrites members. Absent a published threshold, the packages that clear the bar will skew toward the ones members happen to depend on, and Akrites will be accused of precisely that. Low-use abandonware gets an advisory + VEX, not a release.
3. **The license permits** the redistribution (§10), and the finding is recorded before any code is touched.
4. **The fix is deliverable as a bounded patch series** against a pinned upstream commit (§6.3), and a signed artifact can be produced within a bounded engineering effort defined at approval.
5. **A capacity slot is available.** Akrites publishes a cap on concurrent open MoLR engagements. Entry is permitted only if an unallocated slot exists. Cost control is a gate, not an intention: if the cap is full, the case is queued behind a retirement review (§6.7) of an existing engagement, or routed back to §8.
6. **This specific vulnerability is approved.** Approval attaches to a CVE, not to a package. An existing open MoLR engagement on the same package does not pre-authorize a new fix (§6.2.1).

### 6.2 Approval

- **TOC (Technical Oversight Committee) approval is mandatory** and recorded (Appendix C). No unilateral SIRT releases.
- The approval record states: entry-test evidence including the criticality inputs and the record of alternatives asked and declined, the license finding, the bounded-effort estimate, the capacity slot consumed, the term and sunset conditions, the retirement-review threshold status (§6.7), and the steward-search plan.
- For 5.3c (suspect) cases, add a security/provenance sign-off.
- **Conflict of interest is handled by recusal, not by reclassification (§1.1).** Any decision-maker with a personal tie to the maintainer or the project, and any decision-maker whose employer's product depends materially on the affected package, declares the interest and recuses from the vote. The case is reassigned to an unconflicted decision-maker; the classification of the case does not change. Recusals are recorded. The reciprocal case — an Akrites member advocating for a last-resort release on a package their product depends on — is a conflict of the same kind and is handled the same way.
- **Interim approval authority.** Until the TOC is stood up, a named interim approver exercises TOC authority under this section, with an explicit sunset on the date the TOC's first quorate meeting is held. MoLR-specific composition and recusal rules are adopted at the same time. The first case decided will be the precedent every later case is measured against; it must not be decided ad hoc.

#### 6.2.1 Successive vulnerabilities in the same package — fast path

Per-CVE approval bounds the *obligation*, not the *artifact*. Requiring a full TOC vote for fix #4 during a live incident is theatre if the answer is always yes.

- **First entry carries the full record** under §6.2.
- **Subsequent CVEs inside an open MoLR engagement** need only the SIRT lead plus one non-recused TOC member, conditional on the fix staying within the patch-series constraint (§6.3) and the engagement remaining under the retirement threshold (§6.7).
- **Breach either condition and the case returns to full approval**, and to a retirement review before any further work.

### 6.3 The artifact — a patch series, not a maintained branch

**The deliverable is a patch series against a pinned upstream commit.** This is the mechanism Debian and Red Hat have run for twenty-five years, and it is what reconciles per-CVE obligation with the fact that code accumulates: you cannot ship the second fix without the first underneath it, and no consumer should ever be choosing between them.

- **Structure.** The published artifact is a build of *(frozen upstream commit + N patches)*. Each patch maps to exactly one advisory and is individually reviewable, revertible, and tested. Stacking is append-only and auditable rather than divergent.
- **Draw the line at the carry, not the patches.** The cost is never the patch — it is what happens *between* patches, when the runtime EOLs, a transitive dependency is yanked, and the CI base image disappears. The boundary: **build tooling, CI configuration, and the pinned toolchain may change as needed to produce a signed artifact; library source outside the patch series and the public API surface may not.** When a signed build can no longer be produced within the bounded effort defined at approval, **that is a sunset trigger (§6.7), not a project.**
- **Scope discipline.** Security fixes and the minimum required to keep them building and releasing — not features. Feature drift converts a bridge into a competing project and undermines the eventual handoff.
- **Namespace.** Publish under an Akrites-controlled namespace that does not impersonate the original (§8). Publishing into the *original* namespace is prohibited without exception. **The naming convention itself is deliberately left open in this draft**: it must be settled per registry rather than declared once, because namespacing support, sorting rules, and reserved-prefix policies differ by ecosystem (crates.io, for example, has no namespaces at all). v0.1's proposed `akrites-molr/<project>` is withdrawn — carrying "last resort" in the package name publishes a judgment on the maintainer and ages badly. Whatever is chosen must be neutral, stable across a change of publisher, and resolvable by the advisory pointers in §8.1.
- **Versioning.** The scheme must sort monotonically as patches stack **and** must never shadow or outrank a real release if the maintainer returns. This differs by ecosystem — npm precedence rules ignore build metadata such as `+akrites.1`, and prerelease suffixes sort *below* the base version — so it is settled per registry and recorded in the approval, not declared once here.
- **Clear labeling.** README, registry description, and advisory state plainly that this is a temporary last-resort security release for an unmaintained/abandoned/EOL project, why it exists, who runs it, and the sunset plan. Link the original project and its status.

#### 6.3.1 What MoLR is not — to be quoted verbatim

The following block is reproduced without modification in every last-resort release README, registry description, and advisory:

> This release exists to deliver specific security fixes to consumers of an unmaintained package. Akrites does not accept feature requests, does not review or merge pull requests, does not triage bug reports, does not provide support, and makes no compatibility or availability commitments beyond the security fixes described in the linked advisories. The original project remains the property and the work of its maintainer.

#### 6.3.2 Inbound channels are closed by policy

Issues and pull requests on a last-resort release repository are **disabled, or auto-closed with a template** pointing at the steward search and the original project. This is policy, not a per-release choice: it is the difference between a bounded artifact and an unfunded support desk. Security reports about the release itself route to the SIRT front door like any other report (§10).

### 6.4 Release gate — correctness controls

MoLR is the one place in the ecosystem where a patch — increasingly an AI-assisted one — lands with **no maintainer available to review it**. The usual reviewer is precisely the person who is missing. The verification burden therefore moves to the release CI. Provenance and integrity controls establish that the artifact is what Akrites built; these controls establish that it is *correct*.

**Integrity (all required):**
- Clean-room build from a known-good upstream commit or tag.
- Signed commits and signed releases; per-engagement signing identity, never a shared Akrites key.
- Reproducible builds where feasible; SLSA-style build provenance.
- Two-person publish control on every release.

**Correctness (all required before publish):**
- The **upstream test suite passes** against the patched build.
- A **sample of downstream consumers' test suites passes** — selected at approval, weighted toward the dependents that justified the criticality finding.
- The **public API surface diff is empty** against the pinned upstream commit.
- The build is **reproducible** from the published patch series.
- **Two named human reviewers** sign off, and **any AI involvement in authoring or reviewing the patch is disclosed** in the release record and the advisory.

The release must be *harder* to compromise, and better verified, than the abandoned original — not easier.

### 6.5 Upstream-facing obligations

- **Open every patch upstream at public disclosure**, as a pull request against the original repository, in the project's own format — knowing that nobody may merge it. It costs nothing, it delivers the fix into the maintainer's queue where they will find it if they return, and it is public evidence that Akrites is not taking the project.
- **It also makes handback cheap.** A returning maintainer inherits five discrete patches with advisory links, not an eighteen-month-old fork they have to reverse-engineer.
- Keep upstream PRs open and rebased for as long as the engagement runs. Close them only when the engagement sunsets, with a comment linking the final artifact and advisories.

### 6.6 Disclosure handling under MoLR

- The fix lands under **synchronized disclosure**: distros, registries, PSIRTs, and critical-infra partners enter one CVD window per Tiered Disclosure; the patched release and the advisory publish at PD. No participant gets a head start, including Akrites members.
- Advisory and CVE issue through the appropriate CNA (the Linux Foundation CNA authority per the Akrites charter, or CNA-LR if the project has no CNA and falls outside your scope — §10).
- **VEX and advisory carry a machine-readable "fixed in a different package" pointer** (§8.1) so downstream tooling can route consumers correctly. Human-readable notice alone does not discharge the fix-delivery promise.

### 6.7 Term, retirement review, and sunset

- **Time-bounded from day one.** The term is defined at approval (e.g. 6–12 months, renewable once by TOC).
- **Escalating fix count is diagnostic, not just workload.** Three CVEs in eighteen months in an unmaintained package means either the code is structurally weak or it is under adversarial attention *because* it is known to be unmaintained — and Akrites' own advisories are what made that known. Either way, the answer is not fix #4.
  - **Threshold: 3 shipped fixes, or 2 term renewals, triggers a mandatory retirement review** in place of automatic renewal. The review considers funding a replacement, helping downstream migrate, asking distros to drop the package, and intermediate-maintainer migration (§8.4). Renewal past the threshold requires an explicit TOC finding that retirement is not achievable and a dated plan to reach it.
- **Sunset triggers** — the engagement ends when any of these occur, and the guidelines require you to *actively drive toward one of them*:
  - a durable **steward** is confirmed (§7) and takes ownership,
  - the **original maintainer returns** and reclaims (§6.8),
  - the **software is retired or replaced** downstream and the release is no longer needed,
  - **a signed build can no longer be produced within the bounded effort** (§6.3),
  - the retirement review concludes.
- **Wind-down means freeze, not withdraw (§7.5).** The obligation ends; the artifact does not.
- If no sunset trigger is met by term end, TOC explicitly decides: renew (subject to the threshold above), hand to a steward, or freeze with an EOL advisory. A last-resort release must never quietly become a permanent orphan of the SIRT.

### 6.8 If the maintainer returns

This is the most likely reputational failure in the whole document, and it is handled as a standing commitment rather than a case-by-case negotiation. The promises below are mirrored in the maintainer-facing companion.

- **The reclaim path is always open, low-friction, and unconditional.** It does not require the engagement to be near term end, does not require the maintainer to explain their absence, and is **never conditioned on the maintainer's security practices, release cadence, or willingness to adopt Akrites tooling.**
- **Handback completes within a fixed window** (target: 14 days from verified contact) and transfers **no obligations**. The maintainer inherits patches and advisory context, not a support commitment.
- **Akrites contests nothing.** There is no dispute process, no appeal, and no discretion to refuse. Identity verification exists only to confirm the person is who they say they are — it is not a merits review.
- **Deliverables on handback:** the patch series with per-patch advisory links, the upstream PRs from §6.5, test artifacts, CVE and advisory records, the sunset record, and a public Stewardship/Reclaim Transition Notice.
- **If the maintainer asks Akrites to take the release down:** deprecate and redirect. The release is marked deprecated with a pointer to the maintainer's resumed releases; it is **not unpublished** (§7.5). Security artifacts — advisories, CVEs, VEX — are retained, because the vulnerability history remains true regardless of who maintains the code.
- **Deceased maintainers and unsettled estates.** This will happen. Treat the estate or designated heir as the rights-holder; make no public statement about the maintainer's status beyond what the family has already made public; do not treat probate delay as abandonment; and route any transfer request through counsel. Where a maintainer has pre-registered an intent (§7.6), that intent governs.

---

## 7. Stewardship transition

The last-resort release exists to *buy time to find a real owner*. This section runs in parallel with §6 from the moment Track B is contemplated.

### 7.1 Steward search — solicit, do not broadcast

A public "critical, unmaintained, seeking steward" call is two bad things at once: a targeting list for adversaries, and a recruiting funnel for the exact persona §7.3 warns about. v0.1's public Project Status Notice created the `xz` opportunity two sections after describing it. It is withdrawn.

- **Do not broadcast.** The steward search is conducted through targeted, named channels: distros carrying the package, projects that depend on it, foundations and funders (OpenSSF, STF, Alpha-Omega), Akrites members, and known contributors from the original project's history.
- **Prefer solicited candidates with prior standing** over self-nominated volunteers. Self-selection into an unmaintained high-value project is the attack vector, not the talent pool.
- **Timing.** Nothing about the project's status is published while a fix is pre-PD. Any public notice waits until the fix is out.
- **Never publish "critical + unmaintained + unpatched" in the same breath**, in any artifact, at any time. Where a public notice is issued after PD, it describes status and the steward criteria; it does not characterize exposure.
- **The internal notice** (Appendix D), TLP:AMBER+STRICT to the case circle, states: project name and current status; the release location and term, if one exists; downstream impact and dependency footprint; the steward criteria and process; and the contact point and deadline for expressions of interest.

### 7.2 Steward criteria

A candidate steward should demonstrate:

- **Technical competence** in the language/domain and a credible plan to maintain security *and* functionality going forward. Note that the steward is taking on the maintenance commitment Akrites deliberately did not — a steward may do everything MoLR will not.
- **Continuity capacity** — not a single volunteer with no backup; prefer an organization, a funded individual, or a small team with a bus factor > 1.
- **Provenance and identity** you can stand behind (see vetting).
- **Alignment** with coordinated disclosure and the intent to run, or accept help running, a real security process.

### 7.3 Vetting (this is a security control — treat `xz` as the reference threat)

- **Verify identity and history**: real, checkable identity; contribution history; references. Be actively suspicious of a brand-new persona that materializes offering to take over an abandoned high-value project — that is the exact abandonment-exploitation pattern behind CVE-2024-3094.
- **Two-person integrity** on handoff and on early releases; no single new party gets sole publish rights on day one.
- **Signed commits, signed releases, hardware-backed keys, protected branches** from the outset.
- **Staged trust:** co-maintain under SIRT oversight for a defined ramp before the SIRT withdraws. Trust is earned across releases, not granted at signup.

### 7.4 Decision and handoff

- The **TOC (or a delegated Stewardship panel) approves** the steward with consultation from the Akrites member OSPO representatives, recording the vetting outcome (Appendix E). Recusal rules under §6.2 apply.
- Handoff transfers: repository ownership, release/signing authority (rotated to the steward's keys — never share the SIRT's), the patch series and its advisory mapping, the open upstream PRs from §6.5, advisory/CVE context, and open case material under appropriate TLP.
- **No namespace is transferred, because Akrites holds none.** The steward publishes under their own identity or a namespace they create; the advisory pointers (§8.1) are updated to resolve to it. Akrites does not broker, sponsor, or facilitate a steward's acquisition of the original project's name, and a steward who intends to pursue one does so independently and is told so in writing.
- The SIRT publishes a **Stewardship Transition Notice** and updates all advisories/VEX to point to the new canonical source.

### 7.5 No steward found — freeze, never withdraw

v0.1 required downstream to migrate off within 30–60 days. That is not achievable for a widely deployed transitive dependency, and unpublishing a package that consumers resolve against is its own supply-chain incident.

- **Wind-down freezes the artifact.** The last release stays **published, signed, immutable, and clearly marked "no further fixes"**, with the final advisory and the migration guidance attached. The *obligation* ends; the *artifact* does not.
- **Never unpublish, delete, or yank** a last-resort release, in any registry, for any reason short of a legal order or a confirmed compromise of the artifact itself. This holds after handback (§6.8) and after retirement (§6.7).
- **Publish an EOL advisory** for the release: what it fixed, what it will not fix, what consumers should migrate to, and who to contact.
- **Archive the repository read-only**, with the patch series and build provenance intact so any future party can reproduce and continue from it.
- **Document the good-faith search effort** in the sunset record. Renewal in place of wind-down is prohibited by default and requires explicit TOC approval under §6.7.

### 7.6 Declared intent — let maintainers decide in advance

Every abandonment finding Akrites makes is a judgment about someone who is not in the room. The cheapest way to reduce that class of judgment is to let maintainers answer the question themselves while they are still reachable.

- Maintainers may **pre-register a preference** for what happens if they go dark: whether a last-resort release is welcome or unwelcome, who should be contacted first, and who they would nominate as a steward.
- The mechanism is a `SECURITY.md` convention plus an Akrites-side record, offered publicly and requiring no membership, fee, or relationship.
- **A declared intent governs.** A registered "do not fork" preference is honored: the case ends at advisory, VEX, mitigation, and §8 routing, and §6 is unavailable. A registered nomination is contacted before any other candidate.
- This converts an adversarial determination into a consensual one for every maintainer who opts in, and the maintainers who care most will opt in first. It is described in plain language in the maintainer-facing companion.

---

## 8. Reaching consumers without taking the namespace

### 8.0 The commitment

> Akrites does not petition for, accept, or hold custody of any package namespace it did not itself create, in any registry, under any circumstances — including where a registry's published policy would permit it, and including as part of a stewardship handoff. Where a maintainer wishes to transfer their project, Akrites facilitates transfer to a durable steward or foundation and takes no custodial role.

This is unconditional and public. Beyond the property principle, four reasons:

- **The conflict of interest is unmanageable in appearance.** Founding members include the operator of npm and the steward of Maven Central. A process in which Akrites petitions member-operated registries for other people's package names will be read as a back channel regardless of how scrupulously each individual case is decided. The precedent is the harm.
- **It normalizes the attack shape.** "A trusted third party acquires publish rights to a name you already depend on, and new code arrives with no action on your part" is the `xz` pattern with better paperwork. Akrites cannot simultaneously warn about abandonment-exploitation (§7.3) and institutionalize takeover-by-petition. Attackers imitate paperwork.
- **Silence is not consent, and abandonment findings are error-prone.** Illness, bereavement, sanctions, connectivity, a dormant account behind an unsettled estate. The cases where Akrites is most likely to be wrong are the cases where being wrong is most indefensible.
- **Concentration risk.** An Akrites publishing identity trusted across many ecosystems would become the single highest-value credential in the supply chain.

**The honest counterargument:** a separate namespace means nobody automatically receives the fix. `npm audit` will not route a user from an abandoned package to an Akrites one, and shouting from the mountaintop does not scale. If the fix reaches nobody, MoLR has failed its stated promise. The routing layer is therefore a **deliverable, not an afterthought**, and §§8.1–8.4 are obligations of the function, not aspirations.

### 8.1 Make the routing machine-readable

- **Advocate an OSV schema extension for relocated fixes** — a machine-readable "fixed in a different package" pointer. This gap is real and Akrites is uniquely positioned to close it: the scanner and advisory-database operators are already at the table.
- **Ask registries for a metadata capability, not a transfer.** A "security successor" pointer on an unmaintained package: no ownership change, no publish rights, just a surfaced pointer at install and audit time. Use the member relationships to build a *signal*, not to acquire property.
- **Every last-resort advisory carries the pointer** in signed, machine-readable form (§6.6).

### 8.2 Model the function on the distro security team

Debian and Red Hat have carried patches for unmaintained upstreams for twenty-five years without ever taking upstream's identity. That is the precedent this document follows, and **distro pickup is the most reliable distribution path Akrites has** — engage distro security teams first, at §3.1 Attempt 3, and again at PD.

### 8.3 Specify the data, not the tool

The obvious product here is a scanner that reads a dependency tree, notices an abandoned package where an Akrites release exists, and offers the swap. The interaction shape is right — explicit, opt-in, consumer-side, and it preserves the property principle. **Akrites should not build or own it.**

- **It competes with the funders.** Member scanner and advisory-database operators have distribution Akrites will never match. Shipping a competing CLI also creates precisely the perpetual cross-ecosystem maintenance obligation this document exists to avoid — and Akrites promoting Akrites packages through Akrites tooling is a neutrality problem, however mild.
- **The leverage is the record.** A signed, machine-readable pointer in the advisory, plus a thin reference implementation to prove the format works. Then member tooling surfaces it across millions of repositories and Akrites maintains a schema instead of a product.
- **Design against the new attack surface.** A substitution prompt is a novel UX primitive. Once users are trained to accept "swap this package for that one because it is the safe fork," someone will publish a plausible impostor. **Trust must flow from the signed advisory record, never from recognizing a namespace string** — otherwise this is a typosquat vector with a security rationale attached. Reserve Akrites-controlled identities across every major registry now, defensively, publish the canonical list, and note that not every ecosystem supports namespacing (crates.io does not), which needs an ecosystem-by-ecosystem plan.
- **Know the ecosystem ceiling.** Substitution is a root-level operation everywhere and the primitives are uneven: Go `replace` and Cargo `[patch]` are close to purpose-built but are ignored in dependency modules; Maven has native POM `<relocation>`, the closest thing to a sanctioned redirect anywhere; npm needs `overrides` with an alias, which interacts badly with peer resolution; Python has essentially nothing short of pinning or vendoring.

### 8.4 The leaf is the wrong target

Consumer-side substitution only ever helps the application owner, and most abandonware exposure sits four levels down someone else's dependency tree. **The high-leverage move is the intermediate maintainer**: one dependency change in a widely-used library that depends on the abandoned package fixes thousands of trees at once, requires no downstream action, and needs nobody to adopt an Akrites artifact.

That work is maintainer outreach with a prepared patch — exactly what the SIRT is built to do, and a better use of its engineers than carrying code. It is available in every scenario, including §5.3a where no abandonment finding is possible, and it should be attempted before, during, and after any Track B engagement.

**Consumer-side substitution is the fallback for those already exposed; upstream dependency migration is the fix.**

---

## 9. Communications and TLP handling

- **Default posture:** TLP:RED at intake → TLP:AMBER+STRICT for case/patch material during remediation → step down to TLP:GREEN/CLEAR only at PD, per the SIRT's standard model. Non-fix and unresponsiveness do **not** relax this.
- **Escalation messages** to third parties (§3.1) carry the *minimum* — existence of a finding and a coordination problem — never technical detail, until those parties are formally read into the case circle under TLP.
- **Project status is never published pre-PD**, and "critical + unmaintained + unpatched" is never published in one breath at any time (§7.1).
- **Attribution and credit** to the original maintainer/Finder persist through last-resort releases and steward transitions unless a party opts out.
- **Public messaging at PD** must be neutral and factual about the project's status ("unmaintained," "EOL per maintainer," "maintainer unreachable") — never disparaging, never speculating about why a maintainer went silent, and never framing a WONTFIX as negligence. The goal is downstream safety and a healthy handoff, not blame.
- **The maintainer-facing companion is the public voice of this document.** Where external communications and the companion diverge, the companion wins.

---

## 10. Legal, licensing, regulatory, and CNA considerations

*Practical notes, not legal advice — run material decisions past counsel and your foundation.*

- **Forking rights flow from the license.** Permissive (MIT/BSD/Apache-2.0) forks are straightforward on the copyright axis. Copyleft (GPL/LGPL/MPL) forks are permitted but carry obligations (source availability, notices, and for GPL, downstream licensing). **Confirm and record the license finding before forking.** No license / "all rights reserved" repo → you generally cannot fork; the case ends at advisory + VEX + downstream mitigation + §8 routing.
- **Trademark ≠ copyright.** The right to *copy the code* does not grant the right to *use the project's name or logo*. Project names/marks commonly survive code abandonment. This is why real forks rename (MariaDB, LibreOffice, Rocky/Alma, Valkey, OpenTofu). **A last-resort release never uses the original project's name or marks, regardless of who publishes it** — and under §8 there is no transfer path that would change this.
- **Publishing to the original namespace is prohibited** — not "discouraged," and not conditional on a registry's willingness. See §8.0.
- **CNA routing for the original project:** as a CNA you assign CVEs for **your own scope**. For upstream OSS outside it: use the project's CNA if it has one; otherwise a Root CNA, the CVE Program **CNA-LR (CNA of Last Resort)**, or — per the Akrites charter — the Linux Foundation CNA authority. Publish machine-readable artifacts (CVE, OSV, VEX) so they route into CVE/NVD and EUVD.
- **CNA routing for the last-resort release itself.** The release is a distinct product and will eventually have a vulnerability of its own — either inherited from the pinned upstream or introduced by a patch. **Vulnerabilities in the Akrites-published artifact fall within the publisher's CNA scope and are assigned by the publisher**, not routed to CNA-LR, and are handled through the SIRT's standard intake (§6.3.2). Where a vulnerability affects both the original package and the release, the original's CNA assigns for the original and the advisory cross-references both; a patch-introduced defect that does not exist upstream gets its own CVE against the release alone. State this in the release README so reporters know where to send findings.
- **EU Cyber Resilience Act — decide whether MoLR makes Akrites a Steward, and whether that is what we want.** "Open-source software steward" is a recognized, bounded status under the CRA with materially lighter obligations than "manufacturer," and it may be a reasonable fit for a hospice function. **Accepting it deliberately is defensible; drifting into it by accident is not.** Two notes: the answer is largely determined by who publishes the artifact — if a member with existing publish infrastructure ships it, the obligations most likely attach to them as manufacturer rather than to Akrites — and the obligations are phasing in through 2027. **Get counsel to opine before the first release ships, and record the answer in this document rather than leaving it to the first case.**
- **Attribution obligation** (CC-BY-4.0 for Akrites materials; and license notices for forked code) — preserve notices, credit, and license text in any redistribution.

---

## 11. Metrics and counter-metrics

Measure what the launch actually promised — fix delivery — and instrument the failure modes this document is designed to prevent.

**Delivery metrics:**
- Share of known-affected consumers running a fixed version at **30 and 90 days** post-PD. This is the promise; everything else is a proxy.
- Median time from decision point to fix availability.
- Share of last-resort advisories carrying a resolvable machine-readable successor pointer (§8.1); target 100%.
- Intermediate-maintainer migrations landed (§8.4), and dependent trees remediated per migration.

**Function-health metrics:**
- Steward placement rate, and median time from entry to steward confirmation.
- Engagements open past term (**target: zero**).
- Handback latency from verified maintainer contact to completed reclaim (§6.8); target ≤14 days.
- Cases resolved in Track A without ever testing §6.1 — expected to be the overwhelming majority.

**Counter-metrics — these are supposed to go down:**
- **Rising MoLR volume is a failure signal, not productivity.** More last-resort releases means upstream assistance and dependency migration are not working. Write this into the charter **before anyone's objectives or performance review depends on the number of engagements opened**.
- Engagements exceeding the §6.7 retirement threshold.
- Abandonment findings later contradicted by a returning maintainer — each one is reviewed as a near-miss, not a statistic.
- Concurrent engagements as a share of the published capacity cap (§6.1, criterion 5).

*Deferred to a follow-up:* a dedicated threat model for the last-resort build-and-publish pipeline. Not required for v0.2, but it should be scheduled before the first release ships rather than dropped — the per-engagement signing identities and two-person publish controls in §6.4 are the practical floor until then.

---

## Appendix A — One-page timeline summary

```
DISCLOSURE CLOCK (severity-adjustable)
T0 ──▶ +5bd ──▶ +10bd ──▶ +15bd ──▶ ~+30d (decision point) ──▶ scenario path
 │      │        │         │            │
 att1   att2     eco       coord        classify §5 · advisory + VEX + mitigation ship here
                 escalate  handoff       │
                                         ├─ 5.1 capacity ──▶ assist in place ──▶ maintainer ships fix  [Track B: never]
                                         ├─ 5.2 non-fix  ──▶ advisory + VEX + mitigation + §8.4 outreach
                                         └─ 5.3 unresponsive
                                              ├─ alive   ──▶ keep escalating + §8 routing (clock restarts)
                                              └─ suspect ──▶ security incident + clean-room build + §7.3 vetting

ABANDONMENT CLOCK (never accelerated by severity)
T0 ──────────────────────── 90 days total silence, all channels ────────────▶ finding signed (2 people)
                                                                              │
                                                                              └─▶ 5.3b test §6.1 entry

§6 last-resort release: per-CVE approval · patch series on pinned upstream · Akrites namespace only
   · release gate (upstream + downstream tests, empty API diff, 2 reviewers, AI disclosed)
   · upstream PRs opened at PD · inbound channels closed · capacity slot consumed
   ──▶ sunset: steward confirmed | maintainer returns (§6.8) | software retired
              | signed build no longer producible | retirement review (3 fixes / 2 renewals)
   ──▶ wind-down = FREEZE (published, signed, immutable, marked no-further-fixes) — never unpublish
```

---

## Appendix B — Maintainer position record

[`templates/Maintainer non-fix record .md`](../templates/Maintainer%20non-fix%20record%20.md) — captures a §5.2 non-fix in the maintainer's own words: date, channel, verbatim statement, rationale, which kind of non-fix (EOL / feature-complete / WONTFIX), affected versions, and the maintainer's position on downstream mitigation and on a third party carrying the patch.

## Appendix C — MoLR approval record

[`templates/MoLR decision record .md`](../templates/MoLR%20decision%20record%20.md) — captures the §6.1 entry-test evidence: parties asked and declined, criticality inputs and scores, license finding, bounded-effort estimate, capacity slot, the CVE in scope, the release-gate owners, term and sunset conditions, retirement-threshold status, recusals, and the steward-search plan.

The §3 contact and abandonment record is kept in [`templates/Contact_attempt_log.md`](../templates/Contact_attempt_log.md).

## Appendix D — Internal project status notice

[`templates/Project status notice .md`](../templates/Project%20status%20notice%20.md) — TLP:AMBER+STRICT notice to the case circle per §7.1, for solicited, named-channel distribution only. v0.1's public "seeking steward" broadcast is withdrawn.

## Appendix E — Steward vetting record

[`templates/Steward vetting & approval record .md`](../templates/Steward%20vetting%20&%20approval%20record%20.md) — captures §7.2 criteria assessment and §7.3 vetting outcome: identity verification, contribution history, references, continuity capacity, key management and signing setup, staged-trust ramp, approval decision, handoff checklist, and recusals.

## Appendix F — Maintainer-facing companion

[What Akrites Will and Won't Do to Your Project](./What_Akrites_Will_And_Wont_Do.md). Released with this document; its promises are the floor for everything above.
