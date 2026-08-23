# Akrites SIRT Maintainer of Last Resort Guidelines - DRAFT v0.2

### Guidelines for VDR Handling, Maintainer of Last Resort, and Stewardship Transition

*A working framework for a PSIRT/CNA coordinating vulnerability disclosure into open source projects that cannot, will not, or do not respond, and for standing up an Akrites SIRT "Maintainer of Last Resort" function.*

> Status: draft for review · Aligns with the Akrites SIRT model (one front door, least privilege, synchronized disclosure, meet maintainers where they are). Adapt org names, timelines, and approval bodies to your charter before adoption.

> **Companion document.** [What Akrites Will and Won't Do to Your Project](./What_Akrites_Will_And_Wont_Do.md) states these commitments in plain language for maintainers. The two documents ship together and must not contradict each other. Where they appear to, the companion's promises are the floor.

**What changed in v0.2:** the unit of work is the vulnerability rather than the project (§1.2, §6.1); the deliverable is a patch series against a pinned upstream commit rather than a maintained branch (§6.3); Akrites will never petition for, accept, or hold a package namespace it did not create (§2, §5.3a, §8); §6.1 states the entry test as a negative; the abandonment clock is separate from the disclosure clock and floored at 90 days (§3.2); recusal replaces reclassification for conflicts of interest (§6.2); wind-down freezes the artifact rather than withdrawing it (§7.5).

---

## 1. Purpose and scope

### 1.1 What this document governs

This document governs what your PSIRT (acting as a Finder/coordinator and CNA) and the Akrites SIRT do when a coordinated vulnerability disclosure (CVD) toward an upstream open source project **stalls**. There are three stall conditions:

1. **No capacity or tooling.** The project wants to fix the issue but has no private reporting channel, no security contact, no CI/release capacity, or no bandwidth to ingest and act on a qualified report.
2. **Deliberate non-fix (EOL / feature-complete / WONTFIX).** The maintainer is reachable and decides the affected branch will not be patched.
3. **Unresponsive.** No contact is established within the escalation window, for any reason: lost interest, moved on, dead project, maintainer unreachable, or a compromised or hostile maintainer.

Conflicts of interest are not a stall condition. §6.2 handles them by recusal at the point of decision.

### 1.2 Two tracks, and the line between them

Two tracks run through this document, and deadline pressure must not be allowed to blur them.

- **Track A, upstream assistance (§§3–5).** Supplying the capacity, tooling, coordination, and disclosure machinery a maintainer lacks. This is the core Akrites product, and we expect it to resolve the large majority of cases. §11 measures whether it does. A capacity gap is met by supplying capacity; a disagreement is met by an advisory and a VEX.
- **Track B, last-resort action (§§6–7).** A rare, governed exception, entered only on the §6.1 entry test: **no party holds both the legal right and the demonstrated willingness to ship the fix.**

**The Maintainer of Last Resort (MoLR) function delivers fixes. It does not adopt projects.** The public Akrites commitment is that fixes to the latest version reach everyone in a timely fashion. That commits Akrites to delivering a fix, and to nothing about maintenance. Two consequences:

- **The unit of work is the vulnerability.** Akrites approves a fix for one CVE. A second vulnerability in the same package is a fresh entry decision with a fresh approval record, fast-pathed under §6.2.1 rather than waived.
- **Akrites ships a security release.** This document does not change the name of the function. §6.3 defines the artifact narrowly, and that definition is what binds.

Out of scope: the mechanics of triage, dedup, and severity scoring already covered by the standard SIRT intake process. This document picks up where the upstream handoff has become the problem.

---

## 2. First principles for these scenarios

These extend the Akrites principles into the hard cases. Keep them in view; every decision below should trace back to one of them.

- **Protect downstream users. Do not enforce upstream compliance.** A maintainer's silence or refusal does not relieve you of the duty to protect the people running the software. It also does not entitle you to seize the project.
- **Fork rights come from the license, and not from the SIRT.** Confirm the license permits your intended action before you touch code. Trademark is separate from copyright (§10).
- **Akrites never takes a name.** Akrites does not petition for, accept, or hold custody of any package namespace it did not itself create, in any registry, under any circumstances. §8 gives the commitment in full. Declining to hold namespaces is also a security control.
- **Least self-help.** Help the maintainer act rather than acting for them. Escalate only as far as the situation requires. Document each escalation stage before opening the next (§3.1).
- **Prefer the patch to the fork.** Carrying code creates an open-ended commitment and expands the scope of Akrites. The cheapest durable fix is usually an upstream dependency migration by an intermediate maintainer (§8.4).
- **A fork is a new attack surface.** A fork stood up in a hurry, under a new maintainer nobody vetted, is the `xz-utils` (CVE-2024-3094) failure mode. Treat MoLR onboarding and steward vetting as a security control.
- **Severity accelerates mitigation. Severity never accelerates a property judgment.** Exploitation pressure compresses the disclosure clock. It does not compress the finding that a maintainer has abandoned their project (§3.2).
- **Everything is embargoed until it isn't.** TLP governs every artifact and every party from intake to Public Disclosure (PD). Non-fix and unresponsiveness do **not** default a case to open.
- **Document the trail.** Record every contact attempt, maintainer decision, governance approval, and recusal. The record is what makes a later release or disclosure defensible.
- **How can we help?** A maintainer drowning in report volume is offered help with the volume: triage, patch authorship, coordination, release engineering, for as long as they want it. They are never offered a fork. Do not present a takeover to a responsive maintainer as a form of assistance.

---

## 3. The two clocks

Two clocks run in these cases. The **disclosure clock** governs how fast downstream gets protected. The **abandonment clock** governs when Akrites may conclude that a project has no maintainer. They start together, run at different speeds, and the first must never drive the second.

*Unit convention: "business days" excludes weekends and the public holidays of the SIRT's operating jurisdiction. "Days" without qualification means calendar days. Where one stage is expressed in business days and a later stage in calendar days, log both the elapsed business days and the calendar date so the record is unambiguous.*

### 3.1 The disclosure clock: contact and escalation protocol

Before choosing a scenario branch, run and log a **good-faith, escalating contact protocol**. It is the evidentiary basis for every decision that follows. The clock starts at **T0**, the first outbound contact attempt to the upstream project.

| Stage | Timing (default; SSVC-adjustable) | Action | Channels attempted |
|---|---|---|---|
| **Attempt 1** | T0 | Private report via preferred channel | `SECURITY.md` / security.txt contact, GitHub/GitLab private advisory, listed security email |
| **Attempt 2** | T0 + 5 business days | Re-send and widen | Maintainer email(s) from commit history, package registry metadata contact, project chat (private DM only) |
| **Attempt 3** | T0 + 10 business days | Escalate to ecosystem | Foundation/umbrella org, funding org (e.g. STF/OpenSSF/Alpha-Omega), distro security teams that carry the package |
| **Coordinator handoff** | T0 + 15 business days | Bring in a neutral coordinator | Akrites SIRT, CERT/CC (VINCE), or the CVE Program CNA-LR |
| **Decision point** | T0 + ~30 calendar days (adjust by severity/EPSS/exploitation) | Classify the case into a §5 scenario; publish advisory, VEX, and mitigation | n/a |

Rules for the disclosure clock:

- **Severity bends the clock without removing stages.** Active exploitation, high EPSS, or critical-infrastructure blast radius compresses the intervals, and may justify emergency distro-only pre-notification. A low-severity issue may extend them. Use SSVC to make and record that call, and never skip the *documentation* of an attempt.
- **Log each attempt** with timestamp, channel, addressee, and outcome (Appendix A). "Read receipt but no reply" is a different fact from "bounced". Record which.
- **A single acknowledgement returns the case to normal CVD.** If the maintainer engages at any stage, drop back to standard coordination, step into a supporting role, and stop the abandonment clock for good.
- **Never disclose technical detail in escalation messages** beyond what least-privilege requires. "We have a qualified security finding in project X and cannot reach the maintainer" is enough to enlist a foundation's help without leaking the vulnerability.
- **The decision point is not an abandonment finding.** It classifies the case and releases the advisory, VEX, and mitigation. Nothing at T0+30 authorizes Track B.

### 3.2 The abandonment clock: the property judgment

An abandonment finding is a statement about a person. Illness, bereavement, sanctions, loss of connectivity, military service, and an unsettled estate all look the same as disinterest from outside, and a wrong finding in those cases is the hardest to defend. The clock is therefore slower, floored, and insensitive to severity.

- **Floor: make no abandonment finding before 90 calendar days of total silence across every attempted channel**, whatever the severity, EPSS, exploitation status, or downstream pressure. There is no emergency exception. Urgent cases discharge the urgency through advisory, VEX, mitigation, distro coordination, and intermediate-maintainer outreach (§8.4), all of which run on the disclosure clock.
- **Silence must be total.** Any signal of life restarts the clock and routes the case to §5.3a: a commit, a release, a comment, or a login-derived signal a registry will confirm.
- **Check for a declared intent first.** A maintainer who pre-registered a preference under §7.6 has already answered the question, and no finding is needed.
- **Record what you checked, and not what you failed to find.** The finding documents repository activity, release history, registry account state, social and employment signals you can obtain lawfully, and outreach to known contributors and co-maintainers, with dates and names.
- **Two named people sign the finding**, at least one from outside the case team.

---

## 4. Scenario decision table

Once contact resolves or fails, classify and route. "Track B on the table" never means now. It means the case may become eligible once the §3.2 clock and the §6.1 entry test are both satisfied.

| Signal observed | Scenario | Primary path (Track A) | Track B on the table? |
|---|---|---|---|
| Maintainer engages, wants fix, lacks channel/CI/bandwidth | §5.1 Capacity gap | **Assist in place.** Do the coordination work *for* them, for as long as they want it | **No.** A capacity gap is met by supplying capacity |
| Maintainer engages, declines to fix (EOL / feature-complete / WONTFIX), clearly stated | §5.2 Deliberate non-fix | **Respect and protect downstream:** advisory, VEX, downstream mitigation | Only on the §6.1 entry test, which requires that no other party will carry the patch |
| No contact by decision point; project shows life elsewhere | §5.3a Silent but alive | Continue escalation; intermediate-maintainer outreach (§8.4) | No. The abandonment clock has restarted |
| No contact anywhere for 90 days or more; §3.2 finding signed | §5.3b Abandoned | §6 last-resort release, plus §7 stewardship search | Yes, subject to §6.1 |
| Maintainer unreachable **and** signals of compromise/hostility | §5.3c Suspect | **Security incident.** Do not hand over credentials; treat as adversarial | Yes, with heightened vetting |

---

## 5. Track A: scenario playbooks

### 5.1 Project lacks tooling or capacity to ingest the report

The project *wants* to do the right thing. Remove friction, and do not take over.

**Do:**
- Offer a **fully qualified bundle**: vulnerability detail, reproducible PoC/PoV, a proposed patch, and tests. Maintainers should be reviewing a solution rather than solving cold.
- Suggest enabling **PVR (Private Vulnerability Reporting)**. This is our default preference for developing a fix together, because it creates a temporary private fork to develop the patch against without public exposure.
- Offer to **stand up a private channel**, such as helping them enable GitHub/GitLab private security advisories, or running the embargoed thread inside the SIRT's hardened enclave under TLP:AMBER+STRICT.
- Offer to **run the coordination overhead**: CVE assignment through the appropriate CNA (§10), advisory drafting, CVSS/CWE/SSVC/EPSS enrichment, VEX generation, distro and downstream notification, and PD messaging support.
- **Let them keep control and credit.** They approve or revise the patch, they set or negotiate the disclosure date, they own their project's public messaging, and the credit is theirs.
- **Offer sustained help where the problem is volume.** A maintainer buried under reports gets triage capacity, patch authorship, and release engineering for as long as they will accept it.

**Don't:**
- Never publish to the project's namespace (§8). This holds whether or not they are engaged.
- Don't impose your tooling or process as a condition of help. Meet them where they are.
- **Don't offer a fork.** However overloaded a responsive maintainer is, a takeover is not on the menu. If they raise it themselves, point them at §7.6 and the companion document.

**Exit:** patch merged and released, advisory published in coordination, SIRT steps back. This scenario must never reach §6.

### 5.2 Deliberate non-fix: EOL, feature-complete, or WONTFIX

A reachable maintainer's decision not to fix is a **legitimate exercise of their authority**, and these guidelines honor it. Your obligation shifts to protecting the people still running the code.

**First, pin down which kind of non-fix it is.** This changes the downstream story:

- **Formally EOL or unsupported branch.** The maintainer has published an end-of-life for the affected version. Clean signal.
- **Feature-complete, still "supported" in principle.** The maintainer considers the code done and won't touch it for this class of issue.
- **WONTFIX on the merits.** The maintainer disputes severity, considers it outside the threat model or a user configuration the docs already advise against, or judges the fix cost unjustified.

**Do:**
- **Record the maintainer's position in their own words**, with date and rationale (Appendix B). It becomes part of the advisory.
- **Issue an advisory anyway.** An unfixed vulnerability is the one downstream users most need to hear about. Assign the CVE through the appropriate CNA (§10) and publish through OSV/CVE/EUVD.
- **Publish a VEX statement** conveying the true state: affected, `fix_status: will_not_fix`, plus any mitigation. Downstream scanners and SBOM tooling depend on it to make risk decisions.
- **Offer a downstream mitigation or configuration workaround** even where no code fix will land: a compensating control, a hardened default, or a patch consumers can apply locally.
- **Set a disclosure window** consistent with your policy. A maintainer's WONTFIX does not oblige indefinite embargo, but coordinate PD timing with the distros and registries carrying the package so downstream can react.
- **Go to the intermediate maintainers** (§8.4). One dependency change in a widely used library that depends on this package protects thousands of dependency trees and asks nobody to adopt anything.

**Then test §6.1.** A WONTFIX on a niche library is a footnote. A WONTFIX or hard EOL on something in the critical-infrastructure dependency graph, still shipping in distros and images, may become eligible for §6. The entry test is not that the maintainer said no. It is that no party anywhere holds both the right and the willingness to ship the fix. Exhaust first:
  - a distro, downstream consumer, or dependent project volunteering to carry the patch,
  - a community successor package that already exists,
  - the maintainer blessing a fork, a transfer to a foundation, or a successor.

**Don't:**
- Don't reframe a clear WONTFIX as "unresponsive" to justify a release. The §5.3 machinery exists for silence, and not for disagreement.
- Don't treat maintainer disagreement as a defect of character in public messaging (§9).
- Don't publish into the original namespace under any circumstance (§8).

### 5.3 Unresponsive project

No contact by the decision point despite the full §3.1 protocol. Split by what the evidence shows.

**5.3a Silent but alive** (recent commits or releases elsewhere, active but not on security). The §3.2 clock has restarted and no abandonment finding is available. Keep escalating through the ecosystem and funders, keep the advisory and VEX current, and move effort to the routing work in §8. Intermediate-maintainer outreach needs no participation from the original maintainer at all.

> **Akrites does not petition for a transfer of the package name.** Registry abandonment and dispute processes, including PEP 541 and the npm package-dispute policy, are not a route Akrites uses, however well they fit the facts of a case. §8 gives the commitment and the reasoning. Where a maintainer *wishes* to transfer their project, Akrites facilitates transfer to a durable steward or foundation and takes no custodial role. Where a third party pursues a registry process on their own, Akrites does not initiate, sponsor, or advocate for it, and supplies factual case information only if the registry asks.

**5.3b Demonstrably abandoned** (§3.2 finding signed: no activity across repo, releases, registry account, and contact for 90 days or more; contributors and co-maintainers canvassed). Test §6.1 for a **last-resort security release**, and launch **§7 stewardship** in parallel to find a durable owner.

**5.3c Suspect** (unreachable **and** indicators of compromise, or a maintainer handoff resembling the social-engineering takeover of `xz`). Stop treating this as a coordination problem and **open a security incident**. Do not transfer credentials, do not accept an unvetted "new maintainer" who appears at a convenient moment, and route provenance concerns to the registry and the relevant CERTs. Build any release clean-room from a known-good commit, with heightened §7.3 vetting. 5.3c is the one case where evidence of compromise can satisfy the §3.2 floor in place of elapsed time, because a compromised account is a different finding from an absent maintainer.

---

## 6. Track B: Maintainer of Last Resort

MoLR is the SIRT publishing a **time-bounded, clearly marked, governed security release** carrying a specific fix, when abandonment (5.3b), a suspect handoff (5.3c), or a critical-infra non-fix (5.2) would otherwise leave depended-upon software exposed and **no other party will act**. Treat it as the least attractive option available: a bridge to a durable owner.

### 6.1 Entry test (all must hold)

The entry test is a **negative**. MoLR requires *the absence of any party holding both the legal right and the demonstrated willingness to ship the fix.* Maintainer bandwidth is not an entry condition, so supply the bandwidth. Maintainer disagreement is not an entry condition, so publish an advisory and a VEX.

1. **No willing rights-holder exists.** You ran and logged the §3.1 protocol in full, signed the §3.2 finding where applicable, and documented the §5 alternatives as exhausted or unavailable: assist-in-place, distro or downstream carry, a dependent project volunteering, an existing community successor, a maintainer-blessed transfer, and intermediate-maintainer migration (§8.4). Record each alternative as *asked and declined*, and never as *assumed unavailable*.
2. **The software meets a published criticality threshold.** Evidence "critical" against published, versioned inputs, and attach them to the approval record: OpenSSF Criticality Score, count of distros carrying the package, direct and transitive dependent counts, and SBOM prevalence across Akrites members. Without a published threshold, the packages clearing the bar will skew toward the ones members depend on, and Akrites will be accused of that. Low-use abandonware gets an advisory and a VEX.
3. **The license permits** the redistribution (§10), and you recorded the finding before touching code.
4. **The fix is deliverable as a bounded patch series** against a pinned upstream commit (§6.3), and the team can produce a signed artifact within an engineering effort bounded at approval.
5. **A capacity slot is available.** Akrites publishes a cap on concurrent open MoLR engagements, and entry requires an unallocated slot. If the cap is full, the case queues behind a retirement review (§6.7) of an existing engagement, or routes back to §8. Cost control has to gate entry rather than sit in the document as an intention.
6. **This vulnerability is approved.** Approval attaches to a CVE. An open MoLR engagement on the same package does not pre-authorize a new fix (§6.2.1).

### 6.2 Approval

- **TOC (Technical Oversight Committee) approval is mandatory** and recorded (Appendix C). No unilateral SIRT releases.
- The approval record states the entry-test evidence, including criticality inputs and the alternatives asked and declined; the license finding; the bounded-effort estimate; the capacity slot consumed; the term and sunset conditions; the retirement-review threshold status (§6.7); and the steward-search plan.
- For 5.3c cases, add a security and provenance sign-off.
- **Recusal handles conflicts of interest.** A decision-maker with a personal tie to the maintainer or the project, or whose employer's product depends on the affected package, declares the interest and recuses from the vote. The case moves to an unconflicted decision-maker, and its classification does not change: a responsive maintainer is never routed toward Track B because Akrites cannot cleanly decide their case. Record recusals. An Akrites member advocating for a release on a package their own product depends on is the same conflict and gets the same treatment.
- **Interim approval authority.** Until the TOC is stood up, a named interim approver exercises TOC authority here, sunsetting on the date of the TOC's first quorate meeting. Adopt the MoLR-specific composition and recusal rules at the same time. The first case decided sets the precedent for every case after it, so it must not be decided ad hoc.

#### 6.2.1 Successive vulnerabilities in the same package: fast path

Per-CVE approval bounds the obligation. It does not bound the artifact, because code accumulates. A full TOC vote for fix #4 during a live incident is theatre when the answer is always yes.

- **First entry carries the full record** under §6.2.
- **A later CVE inside an open engagement** needs the SIRT lead plus one non-recused TOC member, on condition that the fix stays within the patch-series constraint (§6.3) and the engagement stays under the retirement threshold (§6.7).
- **Breach either condition** and the case returns to full approval, and to a retirement review before further work.

### 6.3 The artifact: a patch series on a pinned upstream commit

**The deliverable is a patch series against a pinned upstream commit.** Debian and Red Hat have run this mechanism for twenty-five years, and it reconciles per-CVE obligation with the fact that code accumulates. You cannot ship the second fix without the first underneath it, and no consumer should have to choose between them.

- **Structure.** The published artifact is a build of *(frozen upstream commit + N patches)*. Each patch maps to one advisory and stays reviewable, revertible, and tested on its own. Stacking becomes append-only and auditable rather than divergent.
- **Draw the line at the carry.** The patch is never the expensive part. The cost arrives between patches, when the runtime EOLs, a transitive dependency is yanked, and the CI base image disappears. The boundary: **build tooling, CI configuration, and the pinned toolchain may change as needed to produce a signed artifact; library source outside the patch series and the public API surface may not.** Once the team can no longer produce a signed build within the effort bounded at approval, that is a sunset trigger (§6.7).
- **Scope discipline.** Ship security fixes and the minimum needed to keep them building and releasing. Feature drift turns a bridge into a competing project and undermines the handoff.
- **Namespace.** Publish under an Akrites-controlled namespace that does not impersonate the original (§8). Publishing into the *original* namespace is prohibited without exception. **The naming convention stays open here on purpose.** Settle it per registry rather than declaring it once, because namespacing support, sorting rules, and reserved-prefix policies differ by ecosystem, and crates.io has no namespaces at all. Whatever you choose must be neutral, must survive a change of publisher, and must resolve against the advisory pointers in §8.1. It must not characterize the project or its maintainer, because a package name that reads as a verdict ages badly once the facts move on.
- **Versioning.** The scheme must sort monotonically as patches stack, and must never shadow or outrank a real release if the maintainer returns. This differs by ecosystem: npm precedence rules ignore build metadata such as `+akrites.1`, and prerelease suffixes sort below the base version. Settle it per registry and record it in the approval.
- **Clear labeling.** The README, registry description, and advisory state that this is a temporary last-resort security release for an unmaintained, abandoned, or EOL project; why it exists; who runs it; and the sunset plan. Link the original project and its status.

#### 6.3.1 What MoLR is not, to be quoted verbatim

Reproduce the following block without modification in every last-resort release README, registry description, and advisory:

> This release exists to deliver specific security fixes to consumers of an unmaintained package. Akrites does not accept feature requests, does not review or merge pull requests, does not triage bug reports, does not provide support, and makes no compatibility or availability commitments beyond the security fixes described in the linked advisories. The original project remains the property and the work of its maintainer.

#### 6.3.2 Inbound channels are closed by policy

Disable issues and pull requests on a last-resort release repository, or auto-close them with a template pointing at the steward search and the original project. This is policy rather than a per-release choice. It separates a bounded artifact from an unfunded support desk. Security reports about the release itself route to the SIRT front door like any other report (§10).

### 6.4 Release gate: correctness controls

MoLR is the one place in the ecosystem where a patch, more and more often an AI-assisted one, lands with **no maintainer available to review it**. The reviewer the ecosystem relies on is the person who is missing, so the verification burden moves to the release CI. Integrity controls establish that the artifact is what Akrites built. Correctness controls establish that it works.

**Integrity (all required):**
- Clean-room build from a known-good upstream commit or tag.
- Signed commits and signed releases, under a per-engagement signing identity and never a shared Akrites key.
- Reproducible builds where feasible, with SLSA-style build provenance.
- Two-person publish control on every release.

**Correctness (all required before publish):**
- The **upstream test suite passes** against the patched build.
- A **sample of downstream consumers' test suites passes**, selected at approval and weighted toward the dependents that justified the criticality finding.
- The **public API surface diff is empty** against the pinned upstream commit.
- The build is **reproducible** from the published patch series.
- **Two named human reviewers** sign off, and **any AI involvement in authoring or reviewing the patch is disclosed** in the release record and the advisory.

The release must be harder to compromise, and better verified, than the abandoned original.

### 6.5 Upstream-facing obligations

- **Open every patch upstream at public disclosure**, as a pull request against the original repository, in the project's own format, knowing nobody may merge it. It costs nothing, it puts the fix in the maintainer's queue where they will find it if they return, and it is public evidence that Akrites is not taking the project.
- **It also makes handback cheap.** A returning maintainer inherits five discrete patches with advisory links rather than an eighteen-month-old fork to reverse-engineer.
- Keep upstream PRs open and rebased for as long as the engagement runs. Close them at sunset, with a comment linking the final artifact and advisories.

### 6.6 Disclosure handling under MoLR

- The fix lands under **synchronized disclosure**. Distros, registries, PSIRTs, and critical-infra partners enter one CVD window per Tiered Disclosure, and the patched release and the advisory publish at PD. No participant gets a head start, Akrites members included.
- Advisory and CVE issue through the appropriate CNA: the Linux Foundation CNA authority per the Akrites charter, or CNA-LR where the project has no CNA and falls outside your scope (§10).
- **VEX and advisory carry a machine-readable "fixed in a different package" pointer** (§8.1) so downstream tooling routes consumers correctly. A human-readable notice on its own does not discharge the fix-delivery promise.

### 6.7 Term, retirement review, and sunset

- **Time-bounded from day one.** Define the term at approval, for example 6 to 12 months, renewable once by the TOC.
- **Treat an escalating fix count as a diagnosis.** Three CVEs in eighteen months in an unmaintained package means either the code is weak in structure, or attackers are working it because they know nobody is watching, and Akrites' own advisories are what told them. Either way the answer is not fix #4.
  - **Threshold: 3 shipped fixes, or 2 term renewals, triggers a mandatory retirement review** in place of automatic renewal. The review considers funding a replacement, helping downstream migrate, asking distros to drop the package, and intermediate-maintainer migration (§8.4). Renewal past the threshold requires an explicit TOC finding that retirement is not achievable, and a dated plan to reach it.
- **Sunset triggers.** The engagement ends on any of these, and you are required to drive toward one:
  - a durable **steward** is confirmed (§7) and takes ownership,
  - the **original maintainer returns** and reclaims (§6.8),
  - downstream **retires or replaces the software** and the release is no longer needed,
  - the team **can no longer produce a signed build** within the bounded effort (§6.3),
  - the retirement review concludes.
- **Wind-down freezes the artifact (§7.5).** The obligation ends. The artifact stays.
- If no trigger is met by term end, the TOC decides explicitly: renew subject to the threshold above, hand to a steward, or freeze with an EOL advisory. A last-resort release must never drift into being a permanent orphan of the SIRT.

### 6.8 If the maintainer returns

A returning maintainer who finds Akrites in possession of their project is the likeliest way this function damages Akrites' standing, so handle it as a standing commitment rather than a case-by-case negotiation. The maintainer-facing companion mirrors these promises.

- **The reclaim path is always open, low-friction, and unconditional.** It does not require the engagement to be near term end, it does not require the maintainer to explain their absence, and it is **never conditioned on the maintainer's security practices, release cadence, or willingness to adopt Akrites tooling.**
- **Handback completes within a fixed window**, targeting 14 days from verified contact, and transfers **no obligations**. The maintainer inherits patches and advisory context, and no support commitment.
- **Akrites contests nothing.** There is no dispute process, no appeal, and no discretion to refuse. Identity verification confirms the person is who they say they are, and reviews nothing else.
- **Deliverables on handback:** the patch series with per-patch advisory links, the upstream PRs from §6.5, test artifacts, CVE and advisory records, the sunset record, and a public Reclaim Transition Notice.
- **If the maintainer asks Akrites to take the release down:** deprecate and redirect. Mark the release deprecated with a pointer to the maintainer's resumed releases, and do **not** unpublish it (§7.5). Retain the security artifacts, advisories, CVEs, and VEX, because the vulnerability history stays true whoever maintains the code.
- **Deceased maintainers and unsettled estates.** This will happen. Treat the estate or designated heir as the rights-holder, make no public statement about the maintainer's status beyond what the family has already said, do not treat probate delay as abandonment, and route any transfer request through counsel. A pre-registered intent (§7.6) governs.

---

## 7. Stewardship transition

The last-resort release buys time to find a real owner. This section runs in parallel with §6 from the moment anyone contemplates Track B.

### 7.1 Steward search: solicit, do not broadcast

A public "critical, unmaintained, seeking steward" call does two harmful things at once. It hands adversaries a targeting list, and it recruits the persona §7.3 exists to screen out. Akrites does not use that channel.

- **Do not broadcast.** Run the steward search through targeted, named channels: distros carrying the package, projects that depend on it, foundations and funders (OpenSSF, STF, Alpha-Omega), Akrites members, and known contributors from the project's history.
- **Prefer solicited candidates with prior standing.** Self-selection into an unmaintained high-value project is the attack vector.
- **Timing.** Publish nothing about the project's status while a fix is pre-PD. Any public notice waits until the fix is out.
- **Never publish "critical + unmaintained + unpatched" in one breath**, in any artifact, at any time. Each fact is publishable on its own. Together they name a high-value target, confirm nobody is watching it, and confirm the hole is still open, which is the whole of an attacker's targeting problem solved in one sentence. A public notice issued after PD describes status and steward criteria, and says nothing about exposure.
- **The internal notice** (Appendix D) goes TLP:AMBER+STRICT to the case circle and states the project name and status; the release location and term, if one exists; downstream impact and dependency footprint; the steward criteria and process; and the contact point and deadline for expressions of interest.

### 7.2 Steward criteria

A candidate steward should demonstrate:

- **Technical competence** in the language and domain, and a credible plan to maintain security and functionality going forward. The steward takes on the maintenance commitment Akrites declined, and may do everything MoLR will not.
- **Continuity capacity.** Prefer an organization, a funded individual, or a small team with a bus factor above 1 over a single volunteer with no backup.
- **Provenance and identity** you can stand behind (see vetting).
- **Alignment** with coordinated disclosure, and the intent to run a real security process or accept help running one.

### 7.3 Vetting: a security control, with `xz` as the reference threat

- **Verify identity and history**: a real, checkable identity, contribution history, and references. Treat a brand-new persona offering to take over an abandoned high-value project as suspect, because that is the abandonment-exploitation pattern behind CVE-2024-3094.
- **Two-person integrity** on handoff and on early releases. No single new party gets sole publish rights on day one.
- **Signed commits, signed releases, hardware-backed keys, and protected branches** from the outset.
- **Staged trust.** Co-maintain under SIRT oversight for a defined ramp before the SIRT withdraws. A steward earns trust across releases rather than at signup.

### 7.4 Decision and handoff

- The **TOC, or a delegated stewardship panel, approves** the steward in consultation with Akrites member OSPO representatives, recording the vetting outcome (Appendix E). The §6.2 recusal rules apply.
- Handoff transfers repository ownership; release and signing authority, rotated to the steward's own keys, because the SIRT never shares its own; the patch series and its advisory mapping; the open upstream PRs from §6.5; advisory and CVE context; and open case material under appropriate TLP.
- **No namespace transfers, because Akrites holds none.** The steward publishes under their own identity or a namespace they create, and the §8.1 advisory pointers update to resolve to it. Akrites does not broker, sponsor, or facilitate a steward's acquisition of the original project's name, and tells any steward who intends to pursue one so in writing.
- The SIRT publishes a **Stewardship Transition Notice** and updates all advisories and VEX to point at the new canonical source.

### 7.5 No steward found: freeze, and never withdraw

Downstream cannot re-architect around a short migration deadline for a widely deployed transitive dependency, and unpublishing a package that consumers resolve against creates its own supply-chain incident.

- **Wind-down freezes the artifact.** The last release stays **published, signed, immutable, and marked "no further fixes"**, with the final advisory and migration guidance attached. The obligation ends and the artifact stays.
- **Never unpublish, delete, or yank** a last-resort release, in any registry, short of a legal order or a confirmed compromise of the artifact. This holds after handback (§6.8) and after retirement (§6.7).
- **Publish an EOL advisory** for the release: what it fixed, what it will not fix, what consumers should migrate to, and who to contact.
- **Archive the repository read-only**, with the patch series and build provenance intact so a future party can reproduce and continue from it.
- **Document the good-faith search effort** in the sunset record. Renewing in place of winding down is prohibited by default and requires explicit TOC approval under §6.7.

### 7.6 Declared intent: let maintainers decide in advance

Each abandonment finding is a judgment about someone who is not in the room. Let maintainers answer the question themselves while they are still reachable, and there are fewer such judgments to make.

- Maintainers may **pre-register a preference** for what happens if they go dark: whether a last-resort release is welcome, who to contact first, and who they would nominate as a steward.
- The mechanism is a `SECURITY.md` convention plus an Akrites-side record, open to anyone, with no membership, fee, or relationship required.
- **A declared intent governs.** Honor a registered "do not fork": the case ends at advisory, VEX, mitigation, and §8 routing, and §6 becomes unavailable. Contact a registered nomination before any other candidate.
- For every maintainer who opts in, this turns an adversarial determination into a consensual one, and the maintainers who care most will opt in first. The companion document describes it in plain language.

---

## 8. Reaching consumers without taking the namespace

### 8.0 The commitment

> Akrites does not petition for, accept, or hold custody of any package namespace it did not itself create, in any registry, under any circumstances, including where a registry's published policy would permit it, and including as part of a stewardship handoff. Where a maintainer wishes to transfer their project, Akrites facilitates transfer to a durable steward or foundation and takes no custodial role.

The commitment is unconditional and public. Beyond the property principle, four reasons:

- **The conflict of interest cannot be managed in appearance.** Founding members include the operator of npm and the steward of Maven Central. Readers will treat a process in which Akrites petitions member-operated registries for other people's package names as a back channel, however carefully each case is decided. The precedent does the damage, case by case.
- **It normalizes the attack shape.** "A trusted third party acquires publish rights to a name you already depend on, and new code arrives with no action on your part" describes the `xz` pattern with better paperwork. Akrites cannot warn about abandonment-exploitation (§7.3) and institutionalize takeover-by-petition at the same time. Attackers will copy the paperwork.
- **Silence is not consent, and abandonment findings go wrong.** Illness, bereavement, sanctions, connectivity, a dormant account behind an unsettled estate. The cases where Akrites is likeliest to be wrong are the cases where being wrong is hardest to defend.
- **Concentration risk.** An Akrites publishing identity trusted across many ecosystems would become the highest-value credential in the supply chain.

**The counterargument, and the answer.** A separate namespace means nobody receives the fix automatically. `npm audit` will not route a user from an abandoned package to an Akrites one, and announcements do not scale. If the fix reaches nobody, MoLR has failed its stated promise. §§8.1 to 8.4 are therefore obligations of the function rather than aspirations, and the routing layer is a deliverable.

### 8.1 Make the routing machine-readable

- **Advocate an OSV schema extension for relocated fixes**: a machine-readable "fixed in a different package" pointer. The gap is real, and Akrites can close it, because the scanner and advisory-database operators are already at the table.
- **Ask registries for a metadata capability rather than a transfer.** A "security successor" pointer on an unmaintained package: no ownership change, no publish rights, a surfaced pointer at install and audit time. Use the member relationships to build a signal, and not to acquire property.
- **Every last-resort advisory carries the pointer** in signed, machine-readable form (§6.6).

### 8.2 Model the function on the distro security team

Debian and Red Hat have carried patches for unmaintained upstreams for twenty-five years without taking upstream's identity. That is the precedent this document follows, and **distro pickup is the most reliable distribution path Akrites has**. Engage distro security teams at §3.1 Attempt 3, and again at PD.

### 8.3 Specify the data, and not the tool

The obvious product here is a scanner that reads a dependency tree, spots an abandoned package where an Akrites release exists, and offers the swap. The interaction shape is right: explicit, opt-in, consumer-side, and it preserves the property principle. **Akrites should not build or own it.**

- **It competes with the funders.** Member scanner and advisory-database operators have distribution Akrites will never match. A competing CLI also creates the perpetual cross-ecosystem maintenance obligation this document exists to avoid, and Akrites promoting Akrites packages through Akrites tooling raises a neutrality problem.
- **The leverage is the record.** A signed, machine-readable pointer in the advisory, plus a thin reference implementation to prove the format works. Member tooling then surfaces it across millions of repositories, and Akrites maintains a schema.
- **Design against the new attack surface.** A substitution prompt is a new UX primitive. Train users to accept "swap this package for that one because it is the safe fork" and someone will publish a plausible impostor. **Trust must flow from the signed advisory record, and never from recognizing a namespace string**, or this becomes a typosquat vector with a security rationale attached. Reserve Akrites-controlled identities across every major registry now, publish the canonical list, and plan ecosystem by ecosystem, because crates.io and others support no namespacing at all.
- **Know the ecosystem ceiling.** Substitution is a root-level operation everywhere, and the primitives are uneven. Go `replace` and Cargo `[patch]` come closest to purpose-built, and both are ignored in dependency modules. Maven has native POM `<relocation>`, the closest thing to a sanctioned redirect anywhere. npm needs `overrides` with an alias, which interacts badly with peer resolution. Python has nothing short of pinning or vendoring.

### 8.4 Go to the intermediate maintainer

Consumer-side substitution helps the application owner, and most abandonware exposure sits four levels down someone else's dependency tree. **The high-leverage move is the intermediate maintainer.** One dependency change in a widely used library that depends on the abandoned package fixes thousands of trees at once, requires no downstream action, and asks nobody to adopt an Akrites artifact.

That work is maintainer outreach with a prepared patch, which is what the SIRT is built to do and a better use of its engineers than carrying code. It is available in every scenario, including §5.3a where no abandonment finding is possible, and you should attempt it before, during, and after any Track B engagement. Consumer-side substitution catches those already exposed; upstream dependency migration is what ends the exposure.

---

## 9. Communications and TLP handling

- **Default posture:** TLP:RED at intake, TLP:AMBER+STRICT for case and patch material during remediation, stepping down to TLP:GREEN/CLEAR only at PD, per the SIRT's standard model. Non-fix and unresponsiveness do **not** relax this.
- **Escalation messages** to third parties (§3.1) carry the minimum, meaning the existence of a finding and a coordination problem, and no technical detail, until those parties are read into the case circle under TLP.
- **Publish nothing about project status pre-PD**, and never publish "critical + unmaintained + unpatched" in one breath (§7.1).
- **Attribution and credit** to the original maintainer and Finder persist through last-resort releases and steward transitions unless a party opts out.
- **Public messaging at PD** stays neutral and factual about the project's status ("unmaintained", "EOL per maintainer", "maintainer unreachable"). Never disparage, never speculate about why a maintainer went silent, and never frame a WONTFIX as negligence. The goal is downstream safety and a healthy handoff.
- **The maintainer-facing companion is the public voice of this document.** Where external communications and the companion diverge, the companion wins.

---

## 10. Legal, licensing, regulatory, and CNA considerations

*Practical notes rather than legal advice. Run material decisions past counsel and your foundation.*

- **Fork rights flow from the license.** Permissive (MIT/BSD/Apache-2.0) forks are straightforward on the copyright axis. Copyleft (GPL/LGPL/MPL) forks are permitted and carry obligations: source availability, notices, and for GPL, downstream licensing. **Confirm and record the license finding before forking.** With no license, or an "all rights reserved" repo, you cannot fork, and the case ends at advisory, VEX, downstream mitigation, and §8 routing.
- **Trademark is not copyright.** A right to copy the code grants no right to use the project's name or logo, and project marks commonly survive code abandonment. Real forks rename for this reason: MariaDB, LibreOffice, Rocky and Alma, Valkey, OpenTofu. **A last-resort release never uses the original project's name or marks, whoever publishes it**, and §8 leaves no transfer path that would change this.
- **Publishing to the original namespace is prohibited**, and not merely discouraged or conditional on a registry's willingness. See §8.0.
- **CNA routing for the original project.** As a CNA you assign CVEs for **your own scope**. For upstream OSS outside it, use the project's CNA where it has one, and otherwise a Root CNA, the CVE Program **CNA-LR (CNA of Last Resort)**, or the Linux Foundation CNA authority per the Akrites charter. Publish machine-readable artifacts (CVE, OSV, VEX) so they route into CVE/NVD and EUVD.
- **CNA routing for the last-resort release itself.** The release is a distinct product and will eventually carry a vulnerability of its own, inherited from the pinned upstream or introduced by a patch. **Vulnerabilities in the Akrites-published artifact fall within the publisher's CNA scope and the publisher assigns them**, rather than routing to CNA-LR, and they run through the SIRT's standard intake (§6.3.2). Where a vulnerability affects both the original package and the release, the original's CNA assigns for the original and the advisory cross-references both. A patch-introduced defect that does not exist upstream gets its own CVE against the release alone. State this in the release README so reporters know where to send findings.
- **EU Cyber Resilience Act: decide whether MoLR makes Akrites a Steward, and whether we want that.** "Open-source software steward" is a recognized, bounded status under the CRA carrying lighter obligations than "manufacturer", and it may fit a fix-delivery function. Accepting the status on purpose is defensible; arriving at it by accident is not. Two notes. Who publishes the artifact largely determines the answer, because if a member with existing publish infrastructure ships it, the obligations attach to them as manufacturer. And the obligations phase in through 2027. **Get counsel to opine before the first release ships, and record the answer here rather than leaving it to the first case.**
- **Attribution obligation.** Preserve notices, credit, and license text in any redistribution, under CC-BY-4.0 for Akrites materials and the license notices for forked code.

---

## 11. Metrics and counter-metrics

Measure the promise the launch made, which is fix delivery, and instrument the failure modes this document exists to prevent.

**Delivery metrics:**
- Share of known-affected consumers running a fixed version at **30 and 90 days** post-PD. This is the promise, and everything else is a proxy for it.
- Median time from decision point to fix availability.
- Share of last-resort advisories carrying a resolvable machine-readable successor pointer (§8.1). Target 100%.
- Intermediate-maintainer migrations landed (§8.4), and dependent trees remediated per migration.

**Function-health metrics:**
- Steward placement rate, and median time from entry to steward confirmation.
- Engagements open past term. **Target: zero.**
- Handback latency from verified maintainer contact to completed reclaim (§6.8). Target 14 days or less.
- Cases resolved in Track A without reaching the §6.1 test. We expect Track A to carry the large majority, and this metric tells us whether it does. A falling ratio is a reason to re-examine the model.

**Counter-metrics, which should fall:**
- **Rising MoLR volume is a failure signal.** More last-resort releases means upstream assistance and dependency migration are not working. Write this into the charter **before anyone's objectives depend on the number of engagements opened**.
- Engagements past the §6.7 retirement threshold.
- Abandonment findings later contradicted by a returning maintainer. Review each one as a near-miss.
- Concurrent engagements as a share of the published capacity cap (§6.1, criterion 5).

*Deferred:* a threat model for the last-resort build-and-publish pipeline. It is not required for v0.2, and it should be scheduled before the first release ships. The per-engagement signing identities and two-person publish controls in §6.4 are the floor until then.

---

## Appendix A: One-page timeline summary

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
   ──▶ wind-down = FREEZE (published, signed, immutable, marked no-further-fixes); never unpublish
```

---

## Appendix B: Maintainer position record

[`templates/Maintainer non-fix record .md`](../templates/Maintainer%20non-fix%20record%20.md) captures a §5.2 non-fix in the maintainer's own words: date, channel, verbatim statement, rationale, which kind of non-fix (EOL / feature-complete / WONTFIX), affected versions, and the maintainer's position on downstream mitigation and on a third party carrying the patch.

## Appendix C: MoLR approval record

[`templates/MoLR decision record .md`](../templates/MoLR%20decision%20record%20.md) captures the §6.1 entry-test evidence: parties asked and declined, criticality inputs and scores, license finding, bounded-effort estimate, capacity slot, the CVE in scope, the release-gate owners, term and sunset conditions, retirement-threshold status, recusals, and the steward-search plan.

The §3 contact and abandonment record lives in [`templates/Contact_attempt_log.md`](../templates/Contact_attempt_log.md).

## Appendix D: Internal project status notice

[`templates/Project status notice .md`](../templates/Project%20status%20notice%20.md) is the TLP:AMBER+STRICT notice to the case circle under §7.1, for solicited, named-channel distribution only. There is no public variant.

## Appendix E: Steward vetting record

[`templates/Steward vetting & approval record .md`](../templates/Steward%20vetting%20&%20approval%20record%20.md) captures the §7.2 criteria assessment and the §7.3 vetting outcome: identity verification, contribution history, references, continuity capacity, key management and signing setup, staged-trust ramp, approval decision, handoff checklist, and recusals.

## Appendix F: Maintainer-facing companion

[What Akrites Will and Won't Do to Your Project](./What_Akrites_Will_And_Wont_Do.md), released with this document. Its promises are the floor for everything above.
