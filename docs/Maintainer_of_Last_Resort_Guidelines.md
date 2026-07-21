# Akrites SIRT Maintainer of Last Resort Guidelines - DRAFT v0.1

### Guidelines for VDR Handling, Maintainer of Last Resort, and Stewardship Transition

*A working framework for a PSIRT/CNA coordinating vulnerability disclosure into open source projects that cannot, will not, or do not respond — and for standing up an Akrites SIRT "Maintainer of Last Resort" function.*

> Status: draft for review · Aligns with the Akrites SIRT model (one front door, least privilege, synchronized disclosure, meet maintainers where they are). Adapt org names, timelines, and approval bodies to your charter before adoption.

---

## 1. Purpose and scope

This document governs what your PSIRT (acting as a Finder/coordinator and CNA) and the Akrites SIRT do when a coordinated vulnerability disclosure (CVD) toward an upstream open source project **stalls** for one of three reasons:

1. **No capacity or tooling** — the project wants to fix the issue but has no private reporting channel, no security contact, no CI/release capacity, or no bandwidth to ingest and act on a qualified report.
2. **Deliberate non-fix (EOL / feature-complete / WONTFIX)** — the maintainer is reachable and decides the affected branch will not be patched.
3. **Unresponsive** — no contact is established within the escalation window, for any reason (lost interest, moved on, dead project, maintainer unreachable, or worse — a compromised or hostile maintainer).

It also defines the **Maintainer of Last Resort (MoLR)** function: a time‑bounded, governed fork the SIRT may stand up when scenario 3 (and sometimes 2) leaves widely‑depended‑on critical software unpatched, and the **Stewardship transition** process for handing that fork to a durable long‑term owner.

Out of scope: the mechanics of triage, dedup, and severity scoring already covered by the standard SIRT intake process. This picks up at the point where **the upstream handoff is the problem**.

---

## 2. First principles for these scenarios

These extend the Akrites principles into the hard cases. Keep them in view; every decision below should be traceable to one of them.

- **Downstream protection is the goal, not upstream compliance.** A maintainer's silence or refusal does not relieve you of the duty to protect the people running the software. But it also does not entitle you to seize the project.
- **Right to fork comes from the license, not from the SIRT.** Confirm the license permits your intended action before you touch code. Trademark is separate from copyright — see §9.
- **Least self-help.** Prefer legitimate registry/namespace transfer processes over unilateral publishing. Prefer helping the maintainer act over acting for them. Escalate only as far as the situation requires of you. (Procedures for escalation TBD)
- ** Prioritize the patch over a fork.** Maintaining forks creates an untenable commitment and expands the scope of Akrites. Members may be solicited to take up fork maintenance if there is an expansive need to do so and concurrence to pursue.
- **The fork is a new attack surface.** A hastily‑stood‑up fork with a lightly‑vetted new maintainer is exactly the `xz-utils` (CVE‑2024‑3094) failure mode. Treat MoLR onboarding and steward vetting as a security control, not a formality.
- **Everything is embargoed until it isn't.** TLP governs every artifact and every party from intake to Public Disclosure (PD). Non-fix and unresponsiveness do **not** default a case to open.
- **Document the trail.** Every contact attempt, every maintainer decision, every governance approval is recorded. The record is what makes an eventual fork, disclosure, or namespace petition defensible.
- **How can we help?** Maintainers may be unresponsive due to volume of vulns, we always provide the option of preference engagement (fork or be available to assist in the volume). This allows us to continue protection to downstream.
---

## 3. The engagement clock — contact and escalation protocol

Before any scenario branch is chosen, you must run — and log — a **good‑faith, escalating contact protocol**. This is the evidentiary spine for everything downstream. The clock starts at **T0 = first outbound contact attempt** to the upstream project.

| Stage | Timing (default; SSVC‑adjustable) | Action | Channels attempted |
|---|---|---|---|
| **Attempt 1** | T0 | Private report via preferred channel | `SECURITY.md` / security.txt contact, GitHub/GitLab private advisory, listed security email |
| **Attempt 2** | T0 + 5 business days | Re-send + widen | Maintainer email(s) from commit history, package registry metadata contact, project chat (private DM only) |
| **Attempt 3** | T0 + 10 business days | Escalate to ecosystem | Foundation/umbrella org, funding org (e.g. STF/OpenSSF/Alpha‑Omega), distro security teams that carry the package |
| **Coordinator handoff** | T0 + 15 business days | Bring in a neutral coordinator | Akrites SIRT, CERT/CC (VINCE), or the CVE Program CNA‑LR |
| **Decision point** | T0 + ~30 days (adjust by severity/EPSS/exploitation) | Classify the case into a §5 scenario and choose a path | — |

Rules for the clock:

- **Severity bends the clock, it doesn't remove stages.** Active exploitation, high EPSS, or critical‑infrastructure blast radius compresses the intervals (and may justify emergency distro‑only pre‑notification). A low‑severity issue may extend them. Use SSVC to make and record that call; never skip the *documentation* of an attempt.
- **Each attempt is logged** with timestamp, channel, addressee, and outcome (see Appendix A). "Read receipt but no reply" is a materially different fact from "bounced" — record which.
- **A single acknowledgement resets the interaction to normal CVD**, not to this protocol. If the maintainer engages at any stage, you drop back to standard coordination and the SIRT steps into a supporting role.
- **Never disclose technical detail in escalation messages** to third parties beyond what least‑privilege requires. "We have a qualified security finding in project X and cannot reach the maintainer" is usually enough to enlist a foundation's help without leaking the vulnerability.

---

## 4. Scenario decision table

Once contact resolves (or fails to), classify and route:

| Signal observed | Scenario | Primary path | Fork on the table? |
|---|---|---|---|
| Maintainer engages, wants fix, lacks channel/CI/bandwidth | §5.1 Capacity gap | **Assist in place** — do the coordination work *for* them | No |
| Maintainer engages, declines to fix (EOL / feature‑complete / WONTFIX), clearly stated | §5.2 Deliberate non‑fix | **Respect + protect downstream** — advisory, VEX, optional downstream mitigation | Only if critical‑infra + still widely deployed, and only via §6 |
| No contact by decision point; project shows life elsewhere | §5.3a Silent but alive | Continue escalation; registry abandonment process; consider §6 | Maybe |
| No contact; project demonstrably abandoned/dead | §5.3b Abandoned | §6 MoLR + §7 Stewardship | Yes |
| Maintainer unreachable **and** signals of compromise/hostility | §5.3c Suspect | **Security incident** — do not hand credentials; treat as adversarial | Yes, with heightened vetting |

---

## 5. Scenario playbooks

### 5.1 Project lacks tooling or capacity to ingest the report

The project *wants* to do the right thing. Your job is to remove friction, not to take over.

**Do:**
- Offer a **fully qualified bundle**: vulnerability detail, reproducible PoC/PoV, a proposed patch, and tests. Maintainers should be *reviewing a solution*, not solving cold.
- Suggest enabling PVR: this is our default preference for collaboratively developing a solution that allows  "Start a temporary private fork" to be leveraged to submit the patch against.

- Offer to **stand up a private channel** for them (e.g. help enable GitHub/GitLab private security advisories, or run the embargoed thread inside the SIRT's hardened enclave under TLP:AMBER+STRICT).
- Offer to **run the coordination overhead**: CVE assignment (via the appropriate CNA — see §9), advisory drafting, CVSS/CWE/SSVC/EPSS enrichment, VEX generation, distro and downstream notification, and PD messaging support.
- **Let them keep control and credit.** They approve/revise the patch; they set or negotiate the disclosure date; they own their project's public messaging; credit is theirs.

**Don't:**
- Don't publish anything to the project's namespace yourself while they are engaged.
- Don't impose your tooling or process as a condition of help. Meet them where they are.

**Exit:** patch merged and released, advisory published in coordination, SIRT steps back. This scenario should almost never reach §6.

### 5.2 Deliberate non-fix — EOL, feature-complete, or WONTFIX

A reachable maintainer's decision not to fix is a **legitimate exercise of their authority**, and the guidelines must honor it. Your obligation shifts entirely to protecting the people still running the code.

**First, pin down which kind of non‑fix it is** (this changes the downstream story materially):

- **Formally EOL / unsupported branch** — the maintainer has published an end‑of‑life for the affected version. Clean signal.
- **Feature‑complete, still "supported" in principle** — maintainer considers the code done and won't touch it for this class of issue.
- **WONTFIX on the merits** — maintainer disputes severity, considers it out of the threat model, user configuration and advised against in docs, or judges the fix cost unjustified.

**Do:**
- **Record the maintainer's position in their own words**, with date and rationale (Appendix B). This becomes part of the advisory.
- **Issue an advisory anyway.** A vulnerability that will not be fixed upstream is *more* important to communicate to downstream, not less. Assign the CVE through the appropriate CNA, publish through OSV/CVE/EUVD.
- **Publish a VEX statement** conveying the true state: affected, `fix_status: will_not_fix`, plus any mitigation. Downstream scanners and SBOM tooling depend on this to make risk decisions.
- **Offer a downstream mitigation or configuration workaround** even when no code fix will land — e.g. a compensating control, a hardened default, or a patch that consumers can apply locally.
- **Set a disclosure window** consistent with your policy; a maintainer's WONTFIX does not oblige indefinite embargo, but coordinate PD timing with distros/registries carrying the package so downstream can react.

**Then decide whether the code still matters enough to fork.** A WONTFIX on a niche, lightly‑used library is a footnote. A WONTFIX (or hard EOL) on something in the critical‑infrastructure dependency graph, still shipping in distros and images, is a candidate for §6 — **but only after** you have exhausted the legitimate alternatives:
  - a distro or downstream consumer volunteering to carry the patch,
  - a registry‑sanctioned successor package,
  - the maintainer blessing a fork or transfer.

**Don't:**
- Don't reframe a clear WONTFIX as "unresponsive" to justify a fork. The scenario 3 machinery exists for silence, not for disagreement.
- Don't quietly ship your own patched build into the original namespace. If the maintainer won't fix but also won't hand over the namespace, that path is closed to self‑help; it goes through §6/§7 or a registry process, not around them.

### 5.3 Unresponsive project

No contact established by the decision point despite the full §3 protocol. Split by what the evidence shows.

**5.3a Silent but alive** (recent commits/releases elsewhere, active elsewhere but not on security): keep escalating through the ecosystem and funders, and open the **registry‑sanctioned transfer/abandonment process** where one exists — this is the *legitimate* route into the original namespace:
  - **PyPI:** PEP 541 project‑name / abandonment transfer request.
  - **npm:** the registry's package‑dispute and unmaintained‑package policies.
  - Other registries: use their published takeover/transfer policy; if none exists, treat as 5.3b.

  These processes have their own notice periods that run in parallel with your clock. A successful transfer lets a vetted steward publish fixes to the *original* namespace — the best possible outcome short of the maintainer returning.

**5.3b Demonstrably abandoned/dead** (no activity across repo, releases, and contact for an extended period; maintainer accounts dormant): proceed to **§6 Maintainer of Last Resort** and, in parallel, launch **§7 Stewardship** to find a durable owner.

**5.3c Suspect** (unreachable **and** indicators of compromise, or a maintainer/handoff pattern resembling a social‑engineering takeover à la `xz`): stop treating this as a coordination problem and **open a security incident**. Do not transfer credentials, do not accept an unvetted "new maintainer" who conveniently appears, and route provenance concerns to the registry and relevant CERTs. Any fork here is a clean‑room fork from a known‑good commit, with heightened §7 vetting.

---

## 6. Maintainer of Last Resort (MoLR)

MoLR is the SIRT publishing a **time‑bounded, clearly‑marked, governed fork** carrying the fix, when abandonment (5.3b), a suspect handoff (5.3c), or a critical‑infra non‑fix (5.2) would otherwise leave depended‑upon software exposed. It is deliberately the **least attractive** option — a bridge, not a destination.

### 6.1 Entry criteria (all must hold)

1. The §3 protocol was run in full and logged, and §5 alternatives (assist‑in‑place, downstream carry, registry transfer, blessed fork) are exhausted or unavailable.
2. The software is **in the critical‑infrastructure dependency graph and still materially deployed** (evidence: distro inclusion, download volume, SBOM prevalence). Low‑use abandonware gets an advisory + VEX, not a fork.
3. The **license permits** the fork and redistribution (§9).
4. A named SIRT engineer/team can actually maintain the fix through the fork's life, and there is a realistic path to a durable steward (§7).

### 6.2 Approval

- **TOC (Technical Oversight Committee) approval is mandatory** and recorded (Appendix C). No unilateral SIRT forks.
- The approval record states: entry criteria evidence, license finding, planned namespace, the **sunset date/conditions**, and the steward‑search plan.
- For 5.3c (suspect) cases, add a security/provenance sign‑off.

### 6.3 The fork itself

- **Namespace:** publish under a **reserved, non‑confusing namespace** that does **not** impersonate the original (e.g. `akrites-molr/<project>` or a distinct package name), because trademark rights in the original name usually survive abandonment of the code (§9). Publishing into the *original* namespace is only permissible via a registry‑sanctioned transfer (§5.3a) — never as self‑help.
- **Provenance and integrity as first‑class controls:** clean‑room fork from a known‑good commit/tag; signed commits and signed releases; reproducible builds where feasible; SLSA‑style build provenance; two‑person review on every change. The fork must be *harder* to compromise than the abandoned original, not easier.
- **Scope discipline:** the MoLR fork ships **security fixes and the minimum to keep them building/releasing** — not features. Feature drift converts a bridge into a competing project and undermines the eventual handoff.
- **Clear labeling:** README and advisory state plainly that this is a temporary security fork of an unmaintained/abandoned/EOL project, why it exists, who runs it, and the sunset plan. Link the original project and its status.

### 6.4 Disclosure handling under MoLR

- The fix lands under **synchronized disclosure**: distros, registries, PSIRTs, and critical‑infra partners enter one CVD window per Tiered Disclosure; the patched fork release and the advisory publish at PD. No participant gets a head start.
- Advisory and CVE issue through the appropriate CNA (the Linux Foundation CNA authority per the Akrites charter, or CNA‑LR if the project has no CNA and falls outside your scope — §9).
- VEX communicates that a fixed build exists **in the reserved namespace**, so downstream tooling can route consumers correctly.

### 6.5 Duration and sunset

- MoLR is **time‑bounded from day one.** Define the term at approval (e.g. 6–12 months, renewable once by TOC).
- **Sunset triggers** — MoLR ends when any of these occur, and the guidelines require you to *actively drive toward one of them*:
  - a durable **Steward** is confirmed (§7) and takes ownership,
  - the **original maintainer returns** and reclaims (SIRT hands back cleanly, including any CVE/advisory context),
  - a **registry transfer** succeeds and a vetted owner takes the original namespace,
  - the software is **retired/replaced** downstream and the fork is no longer needed.
- If no sunset trigger is met by term end, TOC explicitly decides: renew, hand to Steward, or **wind down with an EOL advisory** for the fork. A MoLR fork must never quietly become a permanent orphan of the SIRT.

---

## 7. Stewardship transition and petition process

The MoLR fork's purpose is to *buy time to find a real owner*. This section runs in parallel with §6 from the moment a fork is contemplated.

### 7.1 Notify members and interested parties

Publish a **Project Status Notice** (Appendix D) to Akrites members and relevant stakeholders. TLP‑gate it: while a fix is pre‑PD the notice is TLP:AMBER+STRICT to the case circle; at/after PD a public "seeking steward" call can go TLP:CLEAR. The notice states:

- project name and current status (unresponsive / abandoned / EOL / WONTFIX),
- the MoLR fork location and term (if one exists),
- downstream impact and dependency footprint,
- an explicit **call for a Steward** and the criteria and process below,
- the contact point and deadline for expressions of interest.

Route it through the parties most likely to yield a good owner: distros carrying the package, dependent projects, foundations/funders (OpenSSF, STF, Alpha‑Omega), and known contributors from the original project's history.

### 7.2 Steward criteria

A candidate Steward should demonstrate:

- **Technical competence** in the language/domain and a credible plan to maintain security *and* functionality going forward.
- **Continuity capacity** — not a single volunteer with no backup; prefer an organization, a funded individual, or a small team with a bus factor > 1.
- **Provenance and identity** you can stand behind (see vetting).
- **Alignment** with coordinated disclosure and the intent to run, or accept help running, a real security process.

### 7.3 Vetting (this is a security control — treat `xz` as the reference threat)

- **Verify identity and history**: real, checkable identity; contribution history; references. Be actively suspicious of a brand‑new persona that materializes offering to take over an abandoned high‑value project — that is the exact abandonment‑exploitation pattern behind CVE‑2024‑3094.
- **Two‑person integrity** on handoff and on early releases; no single new party gets sole publish rights on day one.
- **Signed commits, signed releases, hardware‑backed keys, protected branches** from the outset.
- **Staged trust:** co‑maintain under SIRT oversight for a defined ramp before the SIRT withdraws. Trust is earned across releases, not granted at signup.

### 7.4 Decision and handoff

- The **TOC (or a delegated Stewardship panel) approves** the Steward, recording the vetting outcome (Appendix E).
- Handoff transfers: repository ownership, release/signing authority (rotated to the Steward's keys — never share the SIRT's), namespace (reserved or, if a registry transfer succeeded, original), advisory/CVE context, and open case material under appropriate TLP.
- The SIRT publishes a **Stewardship Transition Notice** and updates all advisories/VEX to point to the new canonical source.
- **No steward found?** Fall back to §6.5 sunset: renew MoLR once, or wind down with an EOL advisory that tells downstream to migrate off. Document that the search was made in good faith.

---

## 8. Communications and TLP handling

- **Default posture:** TLP:RED at intake → TLP:AMBER+STRICT for case/patch material during remediation → step down to TLP:GREEN/CLEAR only at PD, per the SIRT's standard model. Non‑fix and unresponsiveness do **not** relax this.
- **Escalation messages** to third parties (§3) carry the *minimum* — existence of a finding and a coordination problem — never technical detail, until those parties are formally read into the case circle under TLP.
- **Attribution and credit** to the original maintainer/Finder persist through forks and steward transitions unless a party opts out.
- **Public messaging at PD** should be neutral and factual about the project's status ("unmaintained," "EOL per maintainer," "maintainer unreachable") — never disparaging. The goal is downstream safety and a healthy handoff, not blame.

---

## 9. Legal, licensing, and CNA considerations

*Practical notes, not legal advice — run material decisions past counsel and your foundation.*

- **Forking rights flow from the license.** Permissive (MIT/BSD/Apache‑2.0) forks are straightforward on the copyright axis. Copyleft (GPL/LGPL/MPL) forks are permitted but carry obligations (source availability, notices, and for GPL, downstream licensing). **Confirm and record the license finding before forking.** No license / "all rights reserved" repo → you generally cannot fork; the case ends at advisory + VEX + downstream mitigation.
- **Trademark ≠ copyright.** The right to *copy the code* does not grant the right to *use the project's name or logo*. Project names/marks commonly survive code abandonment. This is why real forks rename (MariaDB, LibreOffice, Rocky/Alma, Valkey, OpenTofu). Use a reserved, non‑confusing name for MoLR forks; only use the original name via a legitimate transfer that conveys naming rights.
- **Publishing to the original namespace is a permissions question, not a technical one.** Do it only through the registry's sanctioned transfer/abandonment process (PEP 541, npm dispute policy, etc.), never by self‑help, and never in a 5.3c suspect case.
- **CNA routing:** as a CNA you assign CVEs for **your own scope**. For upstream OSS outside it: use the project's CNA if it has one; otherwise a Root CNA, the CVE Program **CNA‑LR (CNA of Last Resort)**, or — per the Akrites charter — the Linux Foundation CNA authority. Publish machine‑readable artifacts (CVE, OSV, VEX) so they route into CVE/NVD and EUVD.
- **Attribution obligation** (CC‑BY‑4.0 for Akrites materials; and license notices for forked code) — preserve notices, credit, and license text in any redistribution.

---

## 10. Metrics, review, and continuous improvement

Track, per case: time‑to‑first‑contact, contact attempts to resolution, scenario classification, whether MoLR was invoked, MoLR duration, and steward outcome. Review the guideline set at least annually and after any case that reached §6, and after any near‑miss on steward vetting. Feed lessons back into the §3 clock and §7 vetting bar.

---

## Appendix A — Contact attempt log (template)

```
Case ID:
Project / package / affected versions:
Severity (CVSS / EPSS / SSVC decision):
T0 (first attempt):
--
Attempt | Date/Time | Channel | Addressee | Outcome (no reply / bounced / read / acknowledged)
1       |           |         |           |
2       |           |         |           |
3       |           |         |           |
Escalation (coordinator/foundation/funder):
Registry transfer process opened (Y/N, ref):
Decision point date + scenario classification (§5.x):
Analyst / approver:
```

## Appendix B — Maintainer non-fix record (template)

```
Case ID / CVE:
Maintainer position (verbatim quote + link):
Type: [ ] Formal EOL  [ ] Feature-complete  [ ] WONTFIX-on-merits
Stated rationale:
Date / source:
Downstream footprint (distros, registries, SBOM prevalence):
Decision: [ ] Advisory + VEX only  [ ] + downstream mitigation  [ ] Escalate to §6 MoLR
VEX fix_status set to:
Approver / date:
```

## Appendix C — MoLR decision record (template)

```
Case ID / CVE:
Entry criteria evidence (1–4 of §6.1):
License finding (SPDX ID, fork permitted Y/N, obligations):
Reserved namespace / package name:
Fork base commit/tag (known-good):
Integrity controls (signing, 2-person, provenance):
Term (start / end / renewals allowed):
Sunset triggers:
Steward-search plan + owner:
Security/provenance sign-off (required for 5.3c):
TOC approval (names / date):
```

## Appendix D — Project status notice / steward call (template)

```
TLP: [AMBER+STRICT pre-PD | CLEAR at/after PD]
Project: <name> — Status: <unresponsive | abandoned | EOL | WONTFIX>
Summary of situation and contact history:
Security impact / dependency footprint:
MoLR fork (if any): <reserved namespace, term>
We are seeking a Steward. Criteria: <§7.2>. Process: <§7.3–7.4>.
Expressions of interest to: <contact> by <deadline>.
```

## Appendix E — Steward vetting & approval record (template)

```
Candidate (identity verified Y/N, method):
Contribution history / references checked:
Continuity/bus-factor assessment:
Suspicious-persona check (abandonment-exploitation / xz pattern) — findings:
Integrity onboarding: [ ] signed commits [ ] signed releases [ ] hardware keys [ ] 2-person [ ] protected branches
Staged co-maintenance ramp (duration):
TOC / panel approval (names / date):
Handoff completed: [ ] repo [ ] signing authority rotated [ ] namespace [ ] advisory/CVE context [ ] notices published
```

## Appendix F — One-page timeline summary

```
T0 ──▶ +5d ──▶ +10d ──▶ +15d ──▶ ~+30d (decision) ──▶ scenario path
 │      │        │         │            │
 att1   att2     eco       coord        classify §5
                 escalate  handoff       │
                                         ├─ 5.1 assist in place  ─────────▶ maintainer ships fix
                                         ├─ 5.2 non-fix ─▶ advisory+VEX (+mitigation) (±§6 if critical)
                                         └─ 5.3 unresponsive
                                              ├─ alive  ─▶ registry transfer (PEP541/npm)
                                              ├─ dead   ─▶ §6 MoLR (TOC) + §7 steward search
                                              └─ suspect─▶ security incident + clean-room fork + heightened vetting

§6 MoLR: reserved namespace · signed/2-person · security-only scope · time-bounded ─▶ sunset:
   steward confirmed | maintainer returns | registry transfer | software retired | wind-down EOL advisory
```
