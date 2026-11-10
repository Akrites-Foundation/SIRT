# Akrites SIRT — MoLR Guidelines and Procedures

**Owner:** Akrites SIRT
**Status:** Draft — for Akrites SIRT review
**Audience:** SIRT case coordinators and WG engineers working a stalled upstream case
**Companion docs:** [Maintainer of Last Resort (MoLR) Policy](Maintainer_of_Last_Resort_Policy.md), [Upstream Engagement Guidelines](upstream-engagement-guidelines.md), [Communications Playbook](sirt-communications-playbook.md) (Plays 10, 14, 15, 17), [CVD Policy](Akrites_CVD_Policy.md), [Templates](../templates/readme.md#unresponsive-projects-and-maintainer-of-last-resort)

---

## Purpose

This document is how the SIRT carries out the [MoLR Policy](Maintainer_of_Last_Resort_Policy.md): the contact ladder, what to do when a maintainer will not fix, how to prepare a Track B request, and how to build, publish, and wind down a last-resort security release.

The policy sets the rules; this document sets the steps. Where they differ, the policy governs, and the Part I maintainer commitments always come first.

---

## Roles

| Role | Responsibility |
| --- | --- |
| **SIRT case coordinator** | Owns the case: runs the contact ladder, keeps the contact attempt log, classifies the stall, and prepares the Track B request. |
| **WG engineers** | Build and test the patch series; at least two serve as the named human reviewers (§5). |
| **Publishers** | Two people who jointly publish a release under two-person control (§5). |
| **SIRT Director** | Brings the Track B request to the Governing Board and tracks the 12-month engagement (§8). |
| **Governing Board** (or its designated MoLR subcommittee) | Approves or declines each Track B request, per CVE (Policy Part II §5.2). |

---

## 1. Contact and Escalation Ladder

Every attempt is recorded in the [Contact attempt log](../templates/Contact_attempt_log.md), which tracks both clocks.

* **Attempt 1 (T0)**: Private report via preferred channel (`SECURITY.md`, GitHub PVR, security email).
* **Attempt 2 (T0 + 3 business days)**: Re-send and widen to commit-history maintainer emails and package registry contacts.
* **Attempt 3 (T0 + 7 business days)**: Escalate to umbrella organizations, foundations (STF, OpenSSF, Alpha-Omega), and distro security teams.
* **Coordinator Handoff (T0 + 10 business days)**: Bring in neutral coordinators (CERT/CC, VINCE, CNA-LR).
* **Decision Point (T0 + 15 business days)**: Classify into a scenario (Policy Part II §4) and publish advisory, VEX, and mitigation per the CVD Policy.

**Resetting the abandonment clock.** Any sign of life — a commit, an issue comment, or a registry login signal — resets the 90-day clock. Record the signal and its date in the log.

**Starting the clock from a trusted third party.** If an active Akrites member organization already tried to reach the maintainer, the abandonment clock may start at its first attempt (Policy Part II §3.2). Attach its complete contact log to the case; it must cover the same channels as the ladder above. If any channel is missing, use the SIRT's own T0.

---

## 2. When a Maintainer Disagrees or Does Not Want to Fix

A maintainer may dispute a finding, decline a fix, or declare a version End-of-Life. That is their right (Policy Part I §1). The SIRT's job is to protect downstream users without overriding the maintainer.

1. **Exchange on the merits first.** Share reachability traces, deployment assumptions, and reproductions; offer a call. If the maintainer persuades the SIRT, close the case: no advisory, and withdraw any reserved CVE (Policy Part I §2).
2. **Record the decision.** Use the [Maintainer non-fix record](<../templates/Maintainer non-fix record .md>): the maintainer's response verbatim, with link and date, and the reason given (WONTFIX, EOL, or disputed).
3. **Offer the verbatim rationale.** Invite the maintainer to state their reasoning word for word in the advisory. Show them the finished wording before publication; never edit or paraphrase it.
4. **Publish on the disclosure clock.** Publish the advisory and a VEX statement (status: affected, no fix planned), with workarounds and mitigations. For an EOL branch, name the supported versions users should move to.
5. **Make the fix available without releasing it.** Attach the proposed patch to the advisory as a source patch, and offer it to Linux distribution security teams and other downstream parties who may choose to carry it ([Upstream Engagement Guidelines](upstream-engagement-guidelines.md) §2.4).
6. **Help consumers move.** Work with intermediate maintainers to update their dependency specs, and point users to maintained alternatives where they exist.
7. **Track B only for an end-of-life branch.** A WONTFIX or a disputed finding never goes to Track B: the maintainer is reachable and has decided (Policy Part II §4). The one exception is an **EOL branch** — the maintainer has declared the affected branch end-of-life, does not dispute the vulnerability, and has fixed it in supported versions. Only if no downstream party will carry the fix:
   * Tell the maintainer, in advance, that Akrites intends to request a security release for that branch, and offer the verbatim rationale.
   * Prepare the request using the EOL-branch path of the entry test (Policy Part II §5.1) and §3 below.
   * Release only the end-of-life branch, and point users to the supported versions.
8. **If the project later goes silent** on all channels for 90 days, handle it as a new abandonment case.

Communications: Play 14 (disagreement) and Play 17 (rejected patch) in the [Communications Playbook](sirt-communications-playbook.md).

---

## 3. Track B: Preparing the Request

Track B is only for an **Abandoned** or **Suspect / Compromised** project, or an **EOL branch** (§2, step 7), per Policy Part II §4.

1. **Complete the entry test** (Policy Part II §5.1), with evidence for each of the seven criteria:
   * Track A options asked and declined, each documented.
   * Criticality: the published metric, or a written criticality justification for the approver to accept.
   * License check, including any copyleft obligations.
   * The bounded patch series and the pinned upstream commit.
   * A free capacity slot.
   * The single CVE ID.
   * The full contact log, including any trusted third-party log (§1). For an EOL branch, the EOL-branch evidence instead (Policy Part II §5.1).
2. **Fill in the [MoLR decision record](<../templates/MoLR decision record .md>)** — one per CVE.
3. **Check conflicts.** List anyone with a commercial, personal, or organizational dependency on the package. They recuse from the vote; a conflicted submitter may present the evidence but does not vote (Policy Part II §5.2).
4. **The SIRT Director brings the request to the Governing Board** (or its designated MoLR subcommittee). Nothing is built for release until approval is recorded.
5. **Check `SECURITY.md` first.** If the maintainer has pre-registered a "do not fork" preference, Track B is not available (Policy Part I §6).

---

## 4. The Artifact: Patch Series on a Pinned Commit

* **Structure**: The delivered artifact is a clean build of `(frozen upstream commit + N security patches)`.
* **Scope Discipline**: Build configuration and toolchains may be updated to produce a signed build, but library source outside the patch series and public API surface may not be altered.
* **Naming & Versioning**: Published under an Akrites-controlled namespace using ecosystem-specific, non-shadowing version strings.
* **Closed Inbound Channels**: Pull requests and general issue trackers are disabled on MoLR repositories (except for patch-regression reports) to prevent scope creep into an unfunded support desk.

---

## 5. Release Integrity & Correctness Gates

Before any MoLR security release is published, it must pass all release gates:
* **Integrity**: Clean-room build, signed commits/artifacts using per-engagement keys, SLSA build provenance, and two-person publish controls.
* **Correctness**: Upstream test suite passes, downstream consumer sample tests pass, **public API surface diff is empty** against the pinned commit, and two named human reviewers sign off (disclosing any AI assistance).

---

## 6. Publishing and Downstream Routing

To ensure downstream users receive security fixes without Akrites taking package names:
* **OSV & VEX Pointers**: Advisories publish machine-readable pointers to the replacement package: OSV records list it as a reference, and VEX statements carry status affected with an action statement naming the Akrites-namespace package that contains the fix.
* **Distro Integration**: Fixes are routed directly to Linux distribution security teams (Debian, Red Hat, Alpine, etc.).
* **Intermediate Maintainer Migration**: SIRT works with high-leverage upstream libraries to update their dependency specs to point to the secure patch or alternative package, resolving exposure for thousands of downstream projects at once.

Communications: Play 15 (MoLR release publication).

---

## 7. Successor Maintainers

Akrites can help a project's community find a successor, but it never selects, appoints, or approves one (Policy Part I §3).

* **Solicited Search**: Akrites conducts targeted outreach to distros, dependent projects, foundations, and known past contributors. Akrites **never broadcasts** `"critical unmaintained package"` publicly, as this creates an attacker targeting list.
* **Vetting is for the community to decide**: Akrites may share the checks it recommends (Reference Threat: `xz` / CVE-2024-3094) — identity verification, contribution history, signed commit enforcement, and staged co-maintenance before full handoff — but the project's community, registry, or foundation decides who takes over.
* Record any outreach in the [Stewardship records](../templates/stewardship-records.md) project status notice.

---

## 8. The 12-Month Operational Donation and Wind-Down

A MoLR engagement is an operational donation of **up to 12 months**, counted from the first last-resort security release (Policy Part II §6).

1. **Record the start and end dates** in the MoLR decision record when the first release ships.
2. **Each new CVE still needs its own approval** during the engagement (Policy Part II §5.1, criterion 6).
3. **Give notice before the end.** Tell downstream parties and distributions of the planned freeze date well before month 12, and point them to any successor or alternative.
4. **Freeze at the end.** Freeze the artifact: published, signed, immutable, and marked `"no further fixes"`. **Never unpublish, delete, or yank** a security release, as doing so breaks downstream builds and causes supply-chain incidents.
5. **After the freeze,** new vulnerabilities in the package are handled with advisories, VEX, and mitigations only.

---

## 9. When the Maintainer Returns

Any activity by the maintainer's verified identity ends the engagement immediately (Policy Part I §5).

1. **Stop** all release work on the Akrites artifact.
2. **Hand over** the patch PRs, test artifacts, and advisory context, with no conditions.
3. **Redirect** users to the maintainer's releases through the advisory, OSV, and VEX records. If the maintainer asks, mark the Akrites release deprecated; keep historical releases and advisories published.
4. **Record** the end date and reason in the MoLR decision record.

---

## 10. Templates

- [Contact attempt log](../templates/Contact_attempt_log.md) — both clocks, every attempt (§1)
- [Maintainer non-fix record](<../templates/Maintainer non-fix record .md>) — deliberate non-fix (§2)
- [MoLR decision record](<../templates/MoLR decision record .md>) — one per CVE (§3, §8, §9)
- [Stewardship records](../templates/stewardship-records.md) — successor outreach (§7)

---

## Appendix A: One-Page Lifecycle & Decision Flow

```
DISCLOSURE CLOCK (Severity-adjustable; T0+15bd default decision point)
T0 ──▶ T0+3bd (Widen) ──▶ T0+7bd (Ecosystem) ──▶ T0+10bd (Coordinators) ──▶ T0+15bd (Decision)
                                                                                  │
  ┌───────────────────────────────────────────────────────────────────────────────┴──────────────┐
  │                                                                                              │
  ▼                                                                                              ▼
Track A: Upstream Assistance                                                   Track B: Last-Resort Action
├── Capacity Gap ──▶ Assist in place & build patch                              ├── Requires 90-Day Silence Floor
├── Disagreement ──▶ Technical exchange ──▶ Verbatim rationale                  ├── Signed Entry Test (Policy §5.1)
├── Non-Fix ──▶ Advisory + VEX + source patch (EOL branch: may enter Track B)   ├── Governing Board Approval & Recusal
└── Unresponsive ──▶ Intermediate maintainer migration                         ├── Patch Series on Pinned Commit
                                                                                └── Up to 12 months, then freeze
```

---

## Open items

- **Capacity cap:** the maximum number of concurrent MoLR engagements (Policy Part II §5.1, criterion 5).
- **Criticality threshold:** the published metric and threshold (Policy Part II §5.1, criterion 2).
- **Akrites namespace per ecosystem** (npm, PyPI, Maven Central, crates.io, and others) for MoLR artifacts (§4).
- **Per-engagement signing keys:** generation, storage, and retirement (§5).
- **Notice period** before the 12-month freeze (§8).
- **Repeat engagements:** whether a package may have a second MoLR engagement after a freeze, and who approves it.
