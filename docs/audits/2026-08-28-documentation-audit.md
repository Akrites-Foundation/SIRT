# Akrites SIRT Documentation Audit — 2026-08-28

**Owner:** Akrites SIRT (Director)
**Status:** DRAFT v0.1 — findings final; decision register pending Director selections (§6), then TOC/Board review where flagged
**Audience:** Governing Board, TOC, SIRT staff and coordinators, WG members, upstream maintainers, prospective Finders
**Scope:** Every tracked document in this repository at snapshot [`ca62393`](https://github.com/Akrites-Foundation/SIRT/tree/ca6239341deea1d87f0a90283c114210815606ab) (2026-08-28) — root policy files, `docs/`, `templates/` — with the open issues and PRs read as in-flight context
**Companion docs:** [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md), [`sirt-communications-playbook.md`](../sirt-communications-playbook.md), [`CONTRIBUTING-glossary.md`](../CONTRIBUTING-glossary.md)
**Tracking:** PR #67

> Spelling standard: **Akrites** (Akrites Foundation, Akrites SIRT). "OSS-SIRT" is a synonym.
> This audit is written to the standard the Communications Playbook sets for outbound messages: as if read back publicly, quoted by a maintainer, or produced in a postmortem. It is a blameless review of documents, never of people.

---

## 1. Executive summary

**The verdict.** In under eight weeks this repository went from empty to a 39-file, ≈42,000-word documentation corpus covering the full coordinated-disclosure lifecycle, with an upstream stance — "we contribute, we don't impose" — that most established SIRTs never manage to write down. That drafting velocity is the headline achievement, and the debt this audit catalogs is its expected by-product: documents drafted days apart answer the same questions differently, and no ratification pass has yet reconciled them. This audit is the scheduled consolidation step — a blameless review of documents, not a verdict on the people who wrote them.

**The headline risk.** The documents a Finder reads first contradict the policy they summarize: a 90-day embargo default the CVD policy retired for 30 (POL-1), four contact addresses across four domains (FND-7), and a canonical policy host that doesn't respond (FND-2). The front door is the least reliable part of the house. (Codes like POL-1 are stable finding IDs — the key is in §2.)

**The five most expensive findings** (detail in §4; all 76 in Appendix A):

1. **OPS-7** — the playbook's maintainer-of-last-resort play is fully actionable while its own appendix lists that authority as undecided; operators cannot tell which plays are live.
2. **POL-1** — the retired 90-day default sits in the two most public artifacts, and both stalled intake PRs (#7, #8) would propagate it.
3. **POL-11** — public-AI use forfeits a Finder's embargo, and the entry checklist dropped exactly the field that would warn them.
4. **ROL-11** — read-in consent runs through a file that does not exist; a compliant read-in is currently impossible.
5. **FND-6** — the safe-harbor pledge names no legal entity; nobody identifiable stands behind it.

**Three asks of the Board.** Section 6.3 carries seven Board-level questions in full; these three block other work and lead that docket:

1. Name the legal entity behind the safe-harbor pledge (Q-20; FND-6) — every finder-facing promise inherits its credibility from this one.
2. Adopt one document-status scheme and a ratification path, then ratify the core policy set (Q-21; ROL-9, INT-5) — today nothing in the corpus is ratified, and nothing could be.
3. Put governance around maintainer-facing records — the "Security Card" — before any schema ships (Q-22; TON-1): it is the largest tone risk toward the maintainers the SIRT exists to serve.

The remaining four, no less real but not blocking other sections: the escalation map (Q-16), ratifying the disclosure break-classification matrix (Q-17), metrics-program design (Q-18), and infrastructure funding (Q-19).

**Scorecard** — the baseline the next audit measures against. The four severity columns sum to 76; *finder-facing* is an orthogonal tag counted within them, not a fifth severity:

| Theme | Blocker | Major | Moderate | Minor | …of which finder-facing |
|---|---|---|---|---|---|
| Finder experience (FND) | 6 | 4 | 0 | 0 | 10 |
| Policy coherence (POL) | 5 | 8 | 1 | 0 | 5 |
| Roles & authority (ROL) | 2 | 10 | 2 | 0 | 0 |
| Operating procedures (OPS) | 2 | 6 | 2 | 0 | 0 |
| Document integrity (INT) | 1 | 6 | 3 | 1 | 1 |
| Metrics & instrumentation (MET) | 1 | 3 | 2 | 0 | 1 |
| Upstream-facing tone (TON) | 1 | 3 | 1 | 0 | 0 |
| Conventions & hygiene (HYG) | 0 | 1 | 3 | 2 | 1 |
| **Total (76)** | **18** | **41** | **14** | **3** | **18** |

**What ships with this audit.** Eleven single-concern fix PRs carrying only mechanical corrections and propagations of decisions already recorded in the CVD policy's change history; a decision register (§6) grouped by decider, with the Director's selections recorded 2026-08-29 — three follow-up PRs (#80, #81, #82) propagate the Director-decidable ones, while the §6.2/§6.3 selections await Governing Board ratification; and a ready-to-paste issue draft for every untracked gap (§5). Nothing judgment-shaped was changed outside those recorded selections, and the only issue filed is the infrastructure wiring issue (#79), filed at the Director's direction during the selection pass.

## 2. How to use this audit

**By role.** Board members: read §1, then the Board-decidable questions in §6.3 — twenty minutes total. The Director: §5–§7 are the working sections; §6 is structured for a selection pass. SIRT operators and coordinators: §4 (especially the operations and policy-coherence themes) and Appendix A are your punch list. The SRE / metrics owner: §4.6 and the MET rows. Upstream maintainers: §1 and §4.7 — the tone review leads with what the corpus already does well. New SIRT staff: this document reads linearly; the census in §3 doubles as a map of what exists.

**Finding IDs** are stable and cross-referenced, never repeated: `FND` finder experience · `POL` policy coherence · `ROL` roles & authority · `OPS` operating procedures · `INT` document integrity · `MET` metrics & instrumentation · `TON` upstream-facing tone · `HYG` conventions & hygiene. Decision-register items are `Q-NN`; missing-artifact rows are `GAP-NN`.

**Severity** uses words, not codes, to avoid colliding with any future incident-severity vocabulary:

| Severity | Meaning |
|---|---|
| **Blocker** | A reader following this text takes a materially wrong or trust-damaging action |
| **Major** | Two operators following this text in a live case reach different decisions |
| **Moderate** | Confusing or wrong, but a careful reader can work around it |
| **Minor** | Polish; no behavioral consequence |

An orthogonal **finder-facing** flag marks findings visible to an external reporter before or during their first contact — these carry outsized trust cost regardless of severity.

## 3. Corpus census

Neutral inventory at snapshot `ca62393` (2026-08-28). No findings in this section.

| Area | Files | Markdown words |
|---|---|---|
| Repository root | 6 (4 markdown + `security.txt` + `LICENSE`) | 6,873 |
| `docs/` | 16 markdown + 1 SVG + `presentations/` (2 PDFs + index) | 30,761 |
| `templates/` | 13 (10 markdown + 2 CSV + 1 OSV JSON) | 4,368 |
| **Total** | **39 tracked files** | **≈42,000** |

Ten largest documents:

| Document | Words |
|---|---|
| [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) | 5,828 |
| [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) | 4,170 |
| [`Maintainer_of_Last_Resort_Guidelines.md`](../Maintainer_of_Last_Resort_Guidelines.md) | 3,629 |
| [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) | 2,643 |
| [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) | 2,310 |
| [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) | 2,154 |
| [`what-counts-as-public-disclosure.md`](../what-counts-as-public-disclosure.md) | 2,136 |
| [`Akrites_CVD_Guide.md`](../Akrites_CVD_Guide.md) | 2,077 |
| [`Akrites_SIRT_CVD_Glossary.md`](../Akrites_SIRT_CVD_Glossary.md) | 1,973 |
| [`acknowledgements-and-attribution.md`](../acknowledgements-and-attribution.md) | 1,655 |

**Document-status values in use** (as printed in front matter): `DRAFT v0.4`, `DRAFT 0.2`, `DRAFT v.0.1`, `Draft for TOC / Board review`, `Proposal / Draft for review`, and no status header at all (5 documents). No document in the corpus carries a ratified or approved status.

**Activity shape.** 218 commits on `main` since the repository began; a single primary contributor authored 96% of them, with outside contributions arriving mainly as pull requests. At snapshot time: 11 open issues, 5 open pull requests (the in-flight set §4 and §5 cross-reference), and a merge queue with a one-approval rule protecting `main`.

**In-flight at snapshot** (ages as of 2026-08-28): PR #7 (Finder how-to-report guide, open 51 days), PR #8 (operator intake runbook, open 51 days), PR #60 (prioritization policy, 8 days), PR #61 (severity methodology, 8 days), PR #62 (Maintainer-of-Last-Resort v0.2 rewrite, draft, approved, actively iterating). Issues #22, #23, #43 are done-but-open; #26 and #32 have artifacts waiting in the PRs above; #35, #36, #41, #42, #48 are stalled without artifacts; #63 is fresh.

## 4. Findings by theme

Twenty-four headline findings below; all 76 are in Appendix A, keyed by the same IDs. Each finding ends with exactly one action: **Mechanical** (remediated in the fix train accompanying this audit), **Decision** (a §6 register question), **New artifact** (a §5 gap row), or **Deferred** (a file an open PR is already rewriting). Severity was set by the persona reviews and could only be lowered, never raised, by cross-examination (§10).

### 4.1 Finder experience (FND) — 10 findings: 6 Blocker, 4 Major, all finder-facing

*Written to the Finder holding an unreported vulnerability — the reader with the least context and the most options to walk away.*

**FND-1 (Blocker, finder-facing) — The front door offers no way to report.** The README's Quick Start links the docs tree, the templates tree, and the issue tracker — but not the security policy; the only channel that mentions vulnerabilities at all is a Slack link labeled "NOT FOR REPORTING VULNERABILITIES", with no statement of what *is* for reporting. `SECURITY.md` exists eleven lines away in the same directory and nothing links to it — while the SIRT's own embargo guidance tells staff that a project's `SECURITY.md` is the first place to check. *Evidence:* [`README.md`](../../README.md) lines 51, 54–56; [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) line 40 ("Check, in order: a `SECURITY.md` / security policy page in the project repo"). *Action:* Mechanical — fix train (README reporting path; index entries).

**FND-2 (Blocker, finder-facing) — The canonical policy pointers are commented out, and every cited host is dead.** `SECURITY.md`'s only links to the full CVD policy are two HTML comments — invisible to every reader — and both point at a legacy host; `security.txt` wraps its Policy, Canonical, and Encryption fields in the same invisible comments. Meanwhile none of the four policy hosts the corpus cites responded to a liveness probe on the snapshot date, including the canonical `sirt.akrites.dev` (§9.4). A Finder cannot reach the policy the summary defers to; the adjacent promise of an OpenPGP key "linked from the policy page" therefore dangles too (FND-3). *Evidence:* [`SECURITY.md`](../../SECURITY.md) lines 8–10, 79; [`security.txt`](../../security.txt); §9.4 liveness table; [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) line 6. *Action:* Decision — Q-19 (stand up or re-point the canonical host; uncommenting ships in the train only as far as the recorded host name inside the comments).

**FND-4 (Blocker, finder-facing) — Who may report today is undisclosed at the entry point.** `SECURITY.md` invites everyone ("Please report suspected vulnerabilities even if you are unsure"), while the CVD policy phases intake by reporter class and rollout stage ("rollout phase — see Section 12"). A Finder outside the currently active class follows the front door in good faith and lands in an intake that isn't accepting their report — the audit could not determine from the public corpus which class is active now. *Evidence:* [`SECURITY.md`](../../SECURITY.md) lines 14–16; [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) line 144 and §12. *Action:* Decision — Q-14.

**FND-6 (Blocker, finder-facing) — Safe harbor is promised by no one in particular.** The safe-harbor pledge ("we will not pursue or support legal action") names no legal entity, and the CVD policy is explicit that the SIRT is "not the Owner of the affected code" in most cases — so the party most likely to feel harmed by good-faith research is precisely the one the pledge cannot bind. A Finder's lawyer reads this paragraph and finds nobody standing behind it. *Evidence:* [`SECURITY.md`](../../SECURITY.md) lines 72–77; [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) lines 170–171. *Action:* Decision — Q-20.

**FND-7 (Blocker, finder-facing) — Four contact addresses on four domains, three of them wrong.** Live, finder-facing artifacts disagree on where to write: the canonical `SIRT@Akrites.dev` (13 references), a wrong-TLD `sirt@akrites.org` in the WG guide's operational mailtos, a legacy `security@oss-sirt.linuxfoundation.org` as the acknowledgement template's fallback *for anonymous finders* — the one audience that gets no second chance to be corrected — and the OSV advisory template's contact block. *Evidence:* §9.4 contact census; [`Akrites_WorkingGroup_Operating_Guide.md`](../Akrites_WorkingGroup_Operating_Guide.md) lines 37, 60; [`acknowledgement-template.md`](../../templates/acknowledgement-template.md) line 105. *Action:* Mechanical — fix train (recorded-decision propagation: the CVD v0.4 change history consolidates contact to `SIRT@Akrites.dev`).

Also in this theme: **FND-3** PGP key promised, none exists (Blocker, ff → Q-19); **FND-8** `security.txt` breaks RFC 9116 with HTML comments (Major, ff — train); **FND-9** no recourse if the SIRT goes silent (Major, ff → Q-16); **FND-10** response-time promises no metric instruments (Major, ff → §4.6); **FND-11** anonymous-finder fallback address is legacy (Major, ff — train).

### 4.2 Policy coherence (POL) — 14 findings: 5 Blocker, 8 Major, 1 Moderate

*Written to the Director and the TOC — the readers who own reconciliation.*

**POL-1 (Blocker, finder-facing) — The two most public artifacts state a 90-day embargo default the policy retired, and two open PRs are about to propagate it.** `SECURITY.md` promises "PD within **90 days**" and the Finder notification template says "up to 90 days", while the CVD policy, the glossary, the Read-in Tier Policy, and the Embargo Handling Guidance all record 30 days — the CVD v0.4 change history (2026-08-24) explicitly "aligned 30-day embargo default". The same superseded number sits in both stalled intake PRs (#7, #8), so merging them as-is would land the drift twice more (GAP-01, GAP-02). A Finder plans disclosure around a number three times the real default. *Evidence:* [`SECURITY.md`](../../SECURITY.md) line 58; [`notification-templates.md`](../../templates/notification-templates.md) line 90; [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) lines 327, 510; [`Akrites_SIRT_CVD_Glossary.md`](../Akrites_SIRT_CVD_Glossary.md) line 38; PR #7 / PR #8 diffs (as of 2026-08-28). *Action:* Mechanical — fix train (recorded-decision propagation), plus the GAP-01/02 pre-merge review asks.

**POL-2b (Blocker) — Two documents ratified on the same day carry two different TLP models for the same case material.** The CVD policy (v0.4, 2026-08-24) sets an unconditional phase model — TLP:RED at intake, TLP:AMBER+STRICT during patch development. The Read-in Tier Policy (v0.2, same day) gates Tier-1 TLP by severity: "TLP:RED for CRITICAL and HIGH; TLP:AMBER+STRICT for Medium and Low." An operator classifying a High-severity case's patch material gets RED from one document and AMBER+STRICT from the other, with neither citing the other. *Evidence:* [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) lines 303–307, 510; [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) lines 23, 126. *Action:* Decision — Q-08.

**POL-8 (Blocker) — Read-in Gate 3 literally excludes the Finder.** The gate admits "a known, vetted engineer from a member organization or designated upstream security team engineer" — a Tier-0 Finder from outside the membership satisfies neither clause, so a strict reading bars the person who brought the case from the case. Operators will resolve this differently under pressure. *Evidence:* [`SIRT Read-in Guidelines.md`](../SIRT%20Read-in%20Guidelines.md) line 15. *Action:* Decision — Q-15.

**POL-11 (Blocker, finder-facing) — Using a public AI tool forfeits your embargo, and the entry documents never tell you.** The embargo guidance is unambiguous: "A report developed with public LLM tooling must be treated as NOT having an embargo available." The CVD policy's intake checklist accordingly asks "Whether and how you used AI or LLM tooling". But `SECURITY.md`'s "What to include" — a structurally parallel copy of that checklist — dropped exactly this field, so the Finder most likely to have triaged with a public chatbot learns the consequence only after it is irreversible. *Evidence:* [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) line 73; [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) lines 136–140; [`SECURITY.md`](../../SECURITY.md) lines 38–45. *Action:* Decision — Q-04 (where the warning surfaces; the checklist-parity edit ships with it).

**POL-13 (Blocker) — Three clocks tick against one unresponsive maintainer, in different units.** The MoLR contact ladder runs on business days (attempts at T0+5, +10, +15), the embargo default runs on 30 *calendar* days, and the actively-exploited policy targets "actionable guidance within 7 days" — an operator running all three against the same silent project cannot tell which deadline binds, and the business-vs-calendar mix means the ladder alone can consume most of the embargo window. PR #62 rewrites the MoLR document but does not reconcile the units. *Evidence:* [`Maintainer_of_Last_Resort_Guidelines.md`](../Maintainer_of_Last_Resort_Guidelines.md) lines 46–48; [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) line 23; [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) line 354. *Action:* Decision — Q-10.

Also in this theme: **POL-2a** `SECURITY.md` flat TLP:RED vs the phased model (Major, ff — train); **POL-3a** `SECURITY.md` lifecycle omits Deduplicate (Major, ff — train); **POL-3b** the glossary's three-stage pipeline vs the CVD policy's four stages, one of at least seven lifecycle framings (Major → Q-10); **POL-4** embargo-clock start: "a validated report" vs "validated and ownership is assigned", the latter citing a phase name no lifecycle model contains (Major → Q-10); **POL-5** extension approver: TIER v0.2 records maintainer-final while the CVD policy wants "explicit rationale and TOC awareness" (Moderate → Q-09); **POL-6** read-in lead times 1–30 vs 7–14 working days vs "open" (Major → Q-11); **POL-7** the intake template holds both intake contracts at once — "We accept and triage every report" and a six-★ completeness gate (Major, ff → Q-14); **POL-9** dispute apex: CVD ends technical disputes at the TOC, TIER routes breach sanctions to the Board — complementary, but no document says so (Major → Q-16); **POL-12** "Owner" — the CVD policy's central role — has no glossary entry (Major → glossary sweep, §7).

### 4.3 Roles & authority (ROL) — 14 findings: 2 Blocker, 10 Major, 2 Moderate

*Written to the Director: every row here is a decision right the corpus assigns two ways, or to nobody.*

**ROL-1 (Blocker) — Who can invoke Maintainer-of-Last-Resort is answered six ways across five documents.** "Only with SIRT+WG approval" (Read-in Tier Policy); "with TOC approval and time-bounding" (Embargo Handling); "only with oversight approval" (CVD Guide); "the group/TOC has approved" (Play 15); "requires TOC approval" (glossary); "{WG} → {TOC/Board decision}" (Play 15's record line). This is the corpus's single most consequential authority — publishing a patch or fork over a maintainer's silence — and PR #62's rewrite covers only its own document, leaving all seven external sightings of the old vocabulary in place (ROL-14, GAP-27). One mitigating reading: the Tier Policy's line sits in a read-in-access exception list and may govern access rather than execution. *Evidence:* [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) line 91; [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) line 122; [`Akrites_CVD_Guide.md`](../Akrites_CVD_Guide.md) line 126; [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) lines 656, 695; [`Akrites_SIRT_CVD_Glossary.md`](../Akrites_SIRT_CVD_Glossary.md) line 43. *Action:* Decision — Q-06, coordinated with PR #62 review.

**ROL-11 (Blocker) — The read-in consent mechanism points at a file that does not exist.** The case read-in notice makes acceptance contingent on "adding your name via a PR to the Knowers_File.md for this working group" — no `Knowers_File.md` exists anywhere in the repository, the term "Knower" has no glossary entry, and the same notice offers a second, competing acceptance path (reply-to-email). As written, a case lead cannot complete a compliant read-in, in the workflow where hesitation costs embargo days. *Evidence:* [`Akrites_Case_ReadIn_Notice_Template.md`](../../templates/Akrites_Case_ReadIn_Notice_Template.md) lines 17, 97; [`SIRT Read-in Guidelines.md`](../SIRT%20Read-in%20Guidelines.md) line 102. *Action:* Decision — Q-11, with GAP-16 as the artifact half.

**ROL-9 (Major) — Nothing in the corpus has ever been ratified, and no document says who could ratify it.** Five draft-status idioms and five headerless documents (§3), zero "Ratified" or "Approved" statuses, and no stated amendment or ratification procedure — while individual documents queue their own open items "for TOC / Board review" with no defined path for that review to conclude. The public-disclosure doc even lists ratifying its own break matrix as an open item. *Evidence:* §3 status census; [`what-counts-as-public-disclosure.md`](../what-counts-as-public-disclosure.md) line 273; [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) lines 904–911. *Action:* Decision — Q-21.

Also in this theme: **ROL-2** the case-runner role carries five different titles, none defined (Major → Q-01); **ROL-3** "WG Lead" holds real authority in one document while the WG guide's role is a "Chair" who is "not a manager" (Major → Q-02); **ROL-4** read-in approver of record conflicts between tables (Major → Q-11); **ROL-5** accept/reject shorthand lacks the cross-reference that resolves it (Moderate — wave-2); **ROL-6** who publishes the advisory, from whose account, is stated nowhere (Major → Q-03); **ROL-7** the public metrics cut has no named approver (Major → Q-18); **ROL-8** access-suspension actor unclear between SIRT and case lead (Major → Q-16); **ROL-10** "Premier Member" gates emergency read-ins yet is defined nowhere — in tension with the Tier Policy's own sector-neutral, equal-access principle (Major → Q-12); **ROL-12** a "stewardship panel" approves MoLR steps in PR #62's draft but is chartered nowhere, and #62's own decision-record template offers no panel field (Major → Q-06, GAP-27 review ask); **ROL-13** CoC-committee ↔ SIRT revocation bridge missing (Moderate — wave-2); **ROL-14** MoLR/fork vocabulary: seven sightings in five documents outside PR #62's file set go stale the day it merges (Major — wave-2 sweep, GAP-27).

### 4.4 Operating procedures (OPS) — 10 findings: 2 Blocker, 6 Major, 2 Moderate

*Written to the operator running a live case at 09:00 with these documents open.*

**OPS-7 (Blocker) — The playbook instructs operators to act on an approval its own appendix says doesn't exist yet.** Play 15 is a fully actionable MoLR publication notice — audience, channel, TLP, fill-in template — while the same document's Appendix B still lists "Decide **MoLR/fork** authority and triggers (Play 15)" as an open item for the TOC/Board. The same appendix asks to "Confirm the **default embargo window**" that the CVD policy's v0.4 change history had already recorded as decided four days earlier. An operator cannot tell which parts of the playbook are live. *Evidence:* [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) lines 654–679, 908, 911; [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) line 510. *Action:* Decision — Q-06 resolves the substance; the stale appendix rows are annotated in §5 (GAP-06).

**OPS-3 (Blocker) — The templates directory tells you nothing it contains.** Its index is one sentence ("Template files that the OSS-SIRT leverages as part of their daily operations.") naming none of its thirteen files; ten of thirteen templates — including the case read-in notice an operator needs mid-incident — are linked from nowhere in the repository. Operators discover templates by directory listing or not at all. *Evidence:* [`templates/readme.md`](../../templates/readme.md) line 1; §9.1 orphan table. *Action:* Mechanical — fix train (the index links the seven stable templates and names the five under rewrite in PR #62, deferring their links until it lands).

**OPS-2 (Moderate) — The severity document two policies link to is empty parentheses.** The Read-in Tier Policy cites "[Akrites SIRT Severity Guidelines]()" and "[Akrites SIRT Severity Scale]()" — two names, both with literally empty link targets. The TLP consequence is contained (the policy self-defines its CVSS thresholds inline), but the promised companion RACI and the naming split remain, and PR #61 — the in-flight severity methodology — edits no existing file, so it cannot repair these links on merge; it also retires the "High" label the Tier Policy's TLP threshold is keyed to (MET-7). *Evidence:* [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) lines 23, 30, 58; PR #61 file list (as of 2026-08-28). *Action:* New artifact — GAP-13, coordinated with PR #61 review.

Also in this theme: **OPS-1** "SIREN" fires in the disclosure procedure and is defined nowhere, including the glossary (Major — no decision needed: every use treats SIREN as an existing channel; the Director defines it in a wave-2 glossary entry); **OPS-4** the four named tools (Spyglass, Watchful Eye, Open Door, Rolodex) exist only as glossary concepts — no access path, no owner (Major → GAP-32); **OPS-5** the only onboarding checklist lives inside a welcome-email template at line 856 of a 923-line playbook (Major — wave-2 extraction, GAP-33); **OPS-6** the README roster names one working contact; Team Lead is TBD and two roster sections are empty (Major → GAP-20); **OPS-8** two drifted copies of the acknowledgement email, template vs playbook (Major — wave-2); **OPS-9** MoLR retains "adapt org names" localization boilerplate (Moderate — deferred, PR #62); **OPS-10** the read-in log CSV covers two of the guidelines' three gates, and its example row gives two people the same one-seat title (Major — wave-2, Q-01).

### 4.5 Document integrity (INT) — 11 findings: 1 Blocker, 6 Major, 3 Moderate, 1 Minor

*Written to whoever edits next: these are load-bearing references that don't hold.*

**INT-1 (Major) — Six shipped documents ground themselves in companion documents that do not exist.** The Embargo Handling Guidance "extends the confidentiality principles in *Akrites: The SIRT*" — no such document exists under any name; coordinators are told to use "the steward-engagement taxonomy to make this call" — none exists; the playbook's header names "OSS-SIRT Process (High Level)" and an MVSR as companions — neither exists. Authority chains that end in phantom citations make every derived rule unverifiable. *Evidence:* [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) line 9; [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) line 129; [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) line 6; §5.3 rows GAP-09 through GAP-16. *Action:* New artifact — §5.3 (each phantom has a gap row and an issue draft).

**INT-5 (Major) — Five status idioms, five headerless documents, and a stray-period version string.** Document statuses read `DRAFT v0.4`, `DRAFT 0.2`, `DRAFT v.0.1`, `Draft for TOC / Board review`, and `Proposal / Draft for review`; five documents carry no status at all. Nothing distinguishes a draft awaiting ratification from a draft in active drafting — which is how a fully actionable playbook and a still-open appendix ended up in the same file (OPS-7). *Evidence:* §3 status census; front matter of the ten largest documents. *Action:* Decision — Q-21 (one status scheme, one ratification path).

Also in this theme: **INT-2** MoLR cites Appendices B–E that don't exist while five unlinked templates carry the content (Major — deferred, PR #62); **INT-3** nine broken or degraded links (Major, partly finder-facing — train; full list §9.3); **INT-4** glossary drift both directions: five defined-but-unused terms, roughly twenty used-but-undefined including "Clearinghouse" (22 uses, defined only in CVD prose) (Major — wave-2 glossary task rides the Q-01, Q-02, and Q-10 selections); **INT-6** the One-Pager's read-in rule states its own negation — "never loop anyone in yourself or with explicit acknowledgement" is missing *without* (Blocker — train, obvious-intent restore, flagged for close review); **INT-7** the AI-use disclosure's filled example lists two contradictory Finder lines (Moderate — train deletes the stray line; the operative template above it is correct); **INT-8** the acknowledgements policy's controlled vocabulary is all placeholder rows (Major → register via Q-13 batch); **INT-9** LICENSE says Apache-2.0, MoLR claims CC-BY-4.0 for "Akrites materials" (Moderate — deferred, PR #62 carries the line; flag at review); **INT-10** "(template attached)" with nothing attached (Moderate — wave-2); **INT-11** MoLR names a "Global Board" that exists in no governance document (Minor — deferred, PR #62 removes it; confirm at merge).

### 4.6 Metrics & instrumentation (MET) — 6 findings: 1 Blocker, 3 Major, 2 Moderate

*Written to the SRE asked to build the dashboard this quarter.*

**MET-1 (Blocker) — Zero of the eleven starter metrics can be implemented as written.** No metric in the set has a numerator, denominator, unit, window, or start/stop event; the corpus offers three incompatible lifecycle models and no statement of which one carries timestamps (POL-3b), and no case-lifecycle data store is named anywhere (the two CSVs in `templates/` feed nothing). The metrics document's own open-items list — cadence, severity weighting, public-cut approver — is the honest tell that this is a direction document, not a specification; nothing downstream treats it that way. *Evidence:* [`Akrites_SIRT_Metrics.md`](../Akrites_SIRT_Metrics.md) (the starter set; open items at lines 104–108); [`Akrites_CVD_Guide.md`](../Akrites_CVD_Guide.md) line 106 ("capture metrics", no pointer). *Action:* New artifact — GAP-30 (definitions), GAP-31 (data store); the approver and weighting halves are Decision — Q-18.

**MET-7 (Major, finder-facing) — The severity vocabulary is about to fork in public.** The corpus scores Critical/High/Medium/Low (CVSS-native; the Tier Policy keys its TLP:RED threshold to "the HIGH level"), while in-flight PR #61 retires "High" for "Important" at the same CVSS band — advisory labels Finders and downstream users will read. If #61 merges as drafted, the Tier Policy's TLP routing references a label that no longer exists. The decision currently lives only inside a PR body. *Evidence:* [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) lines 30, 58; PR #61 diff lines 104–119 (as of 2026-08-28); [`Akrites_SIRT_Metrics.md`](../Akrites_SIRT_Metrics.md) line 106. *Action:* Decision — Q-07, as a review condition on PR #61.

Also in this theme: **MET-2** no case-lifecycle data store exists or is named (Major → GAP-31); **MET-3** milestone dates carry no year, and "~Aug 15" passed silently with "~50 through the system by Oct 15" unowned (Major → Q-18); **MET-4** "tooling already supports this" claimed without evidence (Moderate → Q-18); **MET-5** no process document points at the metrics doc (Moderate — wave-2).

### 4.7 Upstream-facing tone (TON) — 5 findings: 1 Blocker, 3 Major, 1 Moderate

*Written with the upstream maintainer over our shoulder — the one audience whose continued goodwill this program depends on and can never compel.*

**TON-0 (baseline, not a defect).** The corpus's upstream stance is genuinely strong: "we contribute, we don't impose. The maintainer keeps final authority" opens the engagement guidelines; "A reachable maintainer's decision not to fix is a **legitimate exercise of their authority**" anchors the MoLR doc; "This is a consumer-protection measure, not a takeover" leads the fork notice. The findings below are deviations from a standard the corpus itself sets — quoted with their softening context, per the same fairness rule this audit asks of the documents. *Evidence:* [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) line 20; [`Maintainer_of_Last_Resort_Guidelines.md`](../Maintainer_of_Last_Resort_Guidelines.md) line 95; [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) line 668.

**TON-1 (Blocker) — Maintainers are behavior-scored by a record nobody governs.** The "Security Card" logs a project's — and by extension its maintainers' — security conduct ("log the break on the project Security Card"; attempt histories and "embargo/mishandling" notes feed it), it drives who gets pulled into future cases, and it has no owning document, no schema, no retention rule, and no appeal path. A maintainer who learns their non-response is being permanently scored, by a body they never joined, has every reason to disengage — the exact failure the engagement guidelines exist to prevent. The guidelines' own instinct ("confirm with human judgment") shows the fix's direction. *Evidence:* [`what-counts-as-public-disclosure.md`](../what-counts-as-public-disclosure.md) line 211; [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) lines 30, 175; [`Akrites_SIRT_CVD_Glossary.md`](../Akrites_SIRT_CVD_Glossary.md) line 132. *Action:* Decision — Q-22 (governance before schema; GAP-15 is the artifact half).

**TON-3 (Major) — Two documents promise the maintainer different final words on timing.** The engagement guidelines are unconditional — "we do **not** impose timelines" — while the disclosure procedure allows maintainer timing to be "overridden only to protect users after a confirmed public break." The override is defensibly narrow; the defect is that the unconditional promise and its exception live in different documents that never cite each other, so a maintainer discovers the exception mid-incident. *Evidence:* [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) lines 20, 74; [`what-counts-as-public-disclosure.md`](../what-counts-as-public-disclosure.md) lines 218–219. *Action:* Decision — Q-17 (ratify the exception and cross-reference it, or drop it).

Also in this theme: **TON-2** "Technical contribution is the price of admission" reads as gatekeeping when quoted alone — the glossary's definition ("meaningfully help… not merely observe") is the softer, better sentence (Major — wave-2 rewrite candidates ride Q-22 batch); **TON-4** MoLR "handover/handing back" phrasing risks reading as custody a maintainer never granted (Major — deferred, raised in PR #62's own review thread); **TON-5** co-finder attribution cutoff undefined, flagged as open by two documents (Moderate → Q-13, GAP-08).

### 4.8 Conventions & hygiene (HYG) — 6 findings: 1 Major, 3 Moderate, 2 Minor

*Written to whoever runs the next repo-wide sweep.*

**HYG-2 (Major, finder-facing) — The Code of Conduct's filename has two dots, so GitHub can't find it.** `Code_of_Conduct..md` defeats GitHub's community-health detection — the platform surface where contributors and Finders look first reports no code of conduct at all, and the playbook's welcome email links the doubled-dot path directly. *Evidence:* [`Code_of_Conduct..md`](../../Code_of_Conduct..md); [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) line 853. *Action:* Mechanical — fix train (rename plus all inbound links).

**HYG-1 (Moderate) — Thirty-nine files, five naming conventions, no owner for the choice.** The census is §9.2: snake_Case (11), kebab-case (9), spaces (7), trailing-space-before-`.md` (4), plus a double-dot filename, an `&`, a browser-download artifact name, and a README/readme case split. Two anomalies are renamed in the train; the convention itself is a one-line decision nobody has made. *Evidence:* §9.2 census. *Action:* Decision — Q-05.

Also in this theme: **HYG-3** the presentations index names neither PDF it fronts (Minor — annotated in §9.1); **HYG-4** stray `}` in the playbook welcome email (Minor — train, disclosed); **HYG-5** four trailing-space filenames plus an `&` (Moderate — deferred, PR #62 rewrites those files; §5 tracks); **HYG-7** the "Spelling standard: **Akrites**" banner appears in exactly seven documents — the two entry documents instead carried the variant names ("OSS-SIRT"; hyphenated "Akrites-SIRT") the banner exists to retire, and the variants never cross-reference (Moderate — the two entry-doc names are fixed in the train; banner placement is wave-2).

## 5. Missing & stalled artifacts

This section is a bidirectional momentum pass over the corpus and the tracker at snapshot time: artifacts the documents presuppose that nothing is building, artifacts already built that tracking never acknowledged, and work in flight that has quietly stopped moving. Four patterns organize the rows:

1. **The repository's three oldest contributions are its most stalled.** PR #7, PR #8, and the `add-security-insights` branch were all created on 2026-07-08 — the repository's first day — and have zero reviews and zero follow-up commits since, while documents shipped weeks later already cite the artifacts they would produce.
2. **Nine documents are cited as existing; none has been started.** Shipped documents reference an upstream-engagement Code of Conduct, a steward-engagement taxonomy, two OSS-SIRT foundation documents, an overview titled *Akrites: The SIRT*, severity guidelines, a read-in RACI, a "Security Card," a `Knowers_File.md`, and a `SECURITY-INSIGHTS.yml` — with no issue, PR, or draft behind any of them.
3. **Tracking alone isn't motion.** Five open issues have sat 9–35 days with no linked artifact activity, while three shipped documents' originating issues went quiet without closing — and the open items those documents *themselves* recorded have no successor tracking.
4. **Decisions have lapsed without a record.** Two GitHub Discussions raised decisions (meeting platform; account anonymization — the latter with a deadline that passed 2026-08-11) that as of the snapshot have no footprint in any tracked document or issue.

No issues were filed as part of this audit. Every untracked gap below carries a ready-to-paste draft in §5.7 — except the four decision-gated rows in §5.6, whose drafts follow the Director's §6 selections; filing is deliberately left to the Director and maintainers, who can batch, merge, or discard drafts as they see fit. Discussion-sourced rows cite the discussion with an as-of date; discussion threads were read live rather than frozen, unlike every file citation in this document (see §10).

### 5.1 In flight, waiting on review

The artifact exists — as an open PR — and needs review attention, not new work.

| ID | Artifact | Presupposed by | Momentum at snapshot (2026-08-28) | Next step |
|---|---|---|---|---|
| GAP-01 | Finder how-to-report guide (PR #7, adds `docs/how-to-report-quick-guide.md`) | The repo has no intake documentation on `main`; README offers no reporting path | Open 51 days, 0 reviews, no reviewer requested, empty PR body, no linked issue. The draft tells Finders a "default planning window is up to **90 days**" — the superseded default (§4, POL findings) — and reintroduces a legacy policy host and a legacy fallback contact (diff lines 13, 28) | Assign a reviewer; resolve the one open review comment; before merge, align naming, hosts, and contacts with `main`, and the embargo default with CVD policy v0.4 |
| GAP-02 | Operator intake runbook (PR #8, adds `docs/intake-runbook.md`) | [`acknowledgement-template.md`](../../templates/acknowledgement-template.md) line 10 already cites the runbook this PR would add | Open 51 days, 0 reviews, no reviewer requested, empty PR body, no linked issue. The draft repeats the superseded 90-day default ("Default planning window: up to 90 days") and points at the pre-migration organization in two links (diff lines 10, 12) | Assign a reviewer; same pre-merge alignments as GAP-01. The template's citation pointed at the wrong organization and a nonexistent path; the audit fix train repoints it at PR #8 as a proposal until this merges |
| GAP-03 | Report Prioritization Process (PR #60 ↔ issue #26) | Issue #26 (open since 2026-07-21); the PR's own document defers its severity input to issue #32 ("Align the severity input with the result of [issue #32]") | Open 8 days, 0 reviews. Review was requested from the SIRT Director — this audit's owner — on opening day; none has been posted. Issue #26 last updated 2026-08-12, before the PR existed | Post the requested review. #26 auto-closes on merge (closing keyword present) |
| GAP-04 | Severity Scoring Methodology (PR #61 ↔ issue #32) | Issue #32; the PR's own document defers to PR #60 ("Align with the Report Prioritization Process (PR #60) on how SSVC outcomes…") | Open 8 days, 0 reviews, no reviewer requested. PR body says "addresses #32" — not an auto-close keyword, so merging as-is leaves #32 open. Mutually deferring with PR #60: each document waits on the other | Assign a reviewer; add a real `Closes #32`; review the pair together to break the mutual deferral |

### 5.2 Shipped, but tracking never closed

The artifact landed; the issue stayed open, and in two cases the document's own recorded open items have no successor tracking.

| ID | Artifact | Presupposed by | Momentum at snapshot (2026-08-28) | Next step |
|---|---|---|---|---|
| GAP-05 | Issue #23 — what counts as public disclosure | [`what-counts-as-public-disclosure.md`](../what-counts-as-public-disclosure.md) self-declares "**Tracking:** #23" (line 5) | Doc landed 2026-08-19, refined 2026-08-24; issue untouched since 2026-08-19 — 9 days stale, silent even through the refinement | Close #23, or reopen scope if the exploit-consideration refinement wasn't what it asked |
| GAP-06 | Issue #43 — communications guidelines & templates | [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) (topic and date match; no self-citation) | Doc drafted 2026-08-17–18; issue silent since 2026-08-17 — 11 days stale. The doc still self-labels `Draft for TOC / Board review` with seven unresolved Appendix B items | Don't blind-close: re-scope #43 to the Appendix B ratification items (several are register questions in §6), or split them out |
| GAP-07 | Issue #22 — co-finder attribution process | [`acknowledgements-and-attribution.md`](../acknowledgements-and-attribution.md) §Co-finder handling (line 182) | Co-finder section landed 2026-08-13, enhanced 2026-08-20; issue silent since 2026-08-20 — 8 days stale | Close #22 for the process itself; its one residual decision is GAP-08, not a reason to hold #22 open |
| GAP-08 | Co-finder attribution **cutoff** (the concrete trigger) | [`acknowledgements-and-attribution.md`](../acknowledgements-and-attribution.md) lines 187, 259; independently repeated as an open item at [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) line 909 | The same undefined decision is flagged as an open item in two documents shipped five days apart; no issue owns it | Draft in §5.7; the value itself is a register question (§6) |

### 5.3 Cited as existing; nothing built

Each row is a named artifact that at least one shipped document treats as real — with zero issues, PRs, or drafts behind it. These are the audit's "phantom references."

| ID | Artifact | Presupposed by | Momentum at snapshot (2026-08-28) | Next step |
|---|---|---|---|---|
| GAP-09 | Upstream-engagement Code of Conduct (distinct from the contributor CoC) | [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) lines 53, 281; [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) line 914; [`Akrites_CVD_Guide.md`](../Akrites_CVD_Guide.md) line 118 — three docs | Cited by three shipped documents, one of which asks the Board to ratify it; no tracking anywhere | Draft in §5.7 |
| GAP-10 | Steward-engagement taxonomy | [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) lines 6, 129 (an active decision input: "the steward-engagement taxonomy to make this call"); [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) line 921 | Coordinators are instructed to consult a document that does not exist; no tracking | Draft in §5.7 |
| GAP-11 | OSS-SIRT Process (High Level) + OSS-SIRT MVSR | [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) lines 6, 921 — always cited as a pair | Named as companion documents by one doc; no tracking; treated here as one gap | Draft in §5.7 |
| GAP-12 | *Akrites: The SIRT* (overview / charter-level document) | [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) line 9 — the stated source of its confidentiality principles | Single but load-bearing citation; no file by this title exists; see also GAP-21 (a Technical Charter existed and was deleted on day one) | Draft in §5.7 (shared with GAP-21) |
| GAP-13 | Akrites SIRT Severity Guidelines / Severity Scale | [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) lines 23, 58 — both links have literally empty `()` targets (§9.3) | Empty since the doc shipped. PR #61 (GAP-04) drafts a *differently named* severity doc and adds only new files, so merging it cannot repair these links — and it retires the "High" label the Tier Policy's TLP threshold keys to (MET-7) | Coordinate with PR #61; draft in §5.7 covers the retarget decision |
| GAP-14 | RACI per read-in tier | [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) line 58; [`SIRT Read-in Guidelines.md`](../SIRT%20Read-in%20Guidelines.md) line 103 — both say "to be developed" | Both documents that would rely on it list it as their own known gap; no tracking | Draft in §5.7 |
| GAP-15 | "Security Card" owning template/schema | [`what-counts-as-public-disclosure.md`](../what-counts-as-public-disclosure.md) lines 211, 260; [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) lines 30, 42, 175; glossed but not owned at [`Akrites_SIRT_CVD_Glossary.md`](../Akrites_SIRT_CVD_Glossary.md) line 132 | Five operational citations treat it as a record a case lead can open and log to today; nothing exists under `templates/` | Draft in §5.7; governance of what it records is a register question (§6) |
| GAP-16 | `Knowers_File.md` (case read-in consent mechanism) | [`Akrites_Case_ReadIn_Notice_Template.md`](../../templates/Akrites_Case_ReadIn_Notice_Template.md) line 97 | The template's literal consent mechanism points at a file absent from the entire repository — as written, a case lead cannot complete a read-in | Draft in §5.7 |
| GAP-17 | `SECURITY-INSIGHTS.yml` | [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) lines 33, 194, and its own unchecked checklist item (line 258) | Drafted once on branch `add-security-insights` (2026-07-08, day one), never opened as a PR, now structurally incompatible with `main` — it would delete ~40 files that exist today | Draft in §5.7: extract just the YAML, rebase as a small PR |

### 5.4 Announced or chartered, then left unfilled

| ID | Artifact | Presupposed by | Momentum at snapshot (2026-08-28) | Next step |
|---|---|---|---|---|
| GAP-18 | Community meeting cadence & platform | [`README.md`](../../README.md) line 62 ("Community Meetings forthcoming"); GitHub Discussion #40 (as of 2026-08-28, unresolved) | README placeholder unchanged ≥14 days; the platform question sits in a discussion with no issue or doc change behind it | Draft in §5.7 |
| GAP-19 | Account-anonymization policy | GitHub Discussion #45 (as of 2026-08-28): decision deadline passed 2026-08-11 with no recorded decision | A corpus-wide search for "anonymiz" returns zero matches — the decision has no landing place even if made today | Draft in §5.7 |
| GAP-20 | OSS-SIRT Team Lead + Collaborators/Contributors roster | [`README.md`](../../README.md) lines 67, 69, 72 — "Team Lead (TBD)" and two empty roster sections | Unchanged since 2026-08-14. Self-flagged (the README says TBD outright), so lower weight than the phantom rows above | Draft in §5.7 |
| GAP-21 | Technical Charter | Repository history: `CHARTER.md` entered with the initial commit and was revised, reduced to placeholder text, and deleted the same day (2026-07-08; commits `822a211` → `b347588`) | No charter or mandate document has existed in the repository since day one; no issue tracks one. GAP-12's phantom overview citation may be the successor concept | Draft in §5.7 (shared with GAP-12): decide where the SIRT's mandate is chartered, then restore or point |

### 5.5 Tracked, but idle — and one forward risk

Existing issues cover these; filing anything new would duplicate. The gap is triage and ownership, not tracking.

| ID | Artifact | Presupposed by | Momentum at snapshot (2026-08-28) | Next step |
|---|---|---|---|---|
| GAP-22 | "Working Group about Working Groups" | Issue #35 only; zero corpus references to the concept | Open 35 days, untouched since creation | Triage: owner or close — no new issue |
| GAP-23 | WG archival process | Issue #41 only; zero corpus coverage | Open 30 days, untouched since creation | Triage: owner or close — no new issue |
| GAP-24 | Member retirement / withdrawal process | Issue #42 only; zero corpus coverage | Open 30 days, untouched since creation | Triage: owner or close — no new issue |
| GAP-25 | OWASP SAMM exploration | Issue #48 only; zero corpus coverage | Open 15 days, last touched 2026-08-19 | Comment on #48 confirming whether the deferral is still current — no new issue |
| GAP-26 | Upstream-maintainer-onboarding *group* (the undone half of issue #36) | Issue #36; the guidelines half shipped 2026-08-19 as [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) | Issue silent since the day the guidelines landed; the group it literally asks for has no artifact — the done half is masking the undone half | Split #36: close the guidelines half, keep group formation open — no new issue |
| GAP-27 | Post-MoLR-v0.2 alignment of five shipped docs (ROL-14) | PR #62's own description flags two ([`Akrites_SIRT_CVD_Glossary.md`](../Akrites_SIRT_CVD_Glossary.md), [`Akrites_CVD_Guide.md`](../Akrites_CVD_Guide.md)); this audit's sweep found the old MoLR/fork vocabulary at seven points in five documents — those two plus [`upstream-engagement-guidelines.md`](../upstream-engagement-guidelines.md) lines 162, 282, [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) lines 668, 911, and [`Embargo Handling Guidance.md`](../Embargo%20Handling%20Guidance.md) line 122 | Not yet a gap — it becomes one the day #62 merges, and nothing tracks it. (Small drift heads-up: the PR body cites the glossary text at line 41; at snapshot it sits at line 43) | Draft in §5.7; file it the day #62 merges |

### 5.6 Artifacts the findings call for

These rows derive from §4 findings rather than from any document's own citation — for each, no artifact, issue, or draft exists. The first four are decision-gated: their issue drafts are deliberately deferred to the post-selection pass, because drafting them now would presuppose the Director's §6 answer. GAP-32 and GAP-33 are decision-free and drafted in §5.7. *(Post-selection update, 2026-08-29: Q-19's selection turned GAP-28 and GAP-29 into issue #79, filed at the Director's direction; GAP-30 and GAP-31 follow ratification of Q-10 and Q-18.)*

| ID | Artifact | Presupposed by | Momentum at snapshot (2026-08-28) | Next step |
|---|---|---|---|---|
| GAP-28 | Published OpenPGP key (or a withdrawn promise) | [`SECURITY.md`](../../SECURITY.md) lines 34–35 and [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) line 120 promise a key "linked from the policy page"; `security.txt`'s Encryption field is commented out | No key or fingerprint exists anywhere in the repository (FND-3) | Q-19 selected 2026-08-29 — publish as written; tracked in issue #79 |
| GAP-29 | Reachable canonical policy host | [`coordinated-vulnerability-disclosure-policy.md`](../../coordinated-vulnerability-disclosure-policy.md) line 6 names `sirt.akrites.dev`; [`SECURITY.md`](../../SECURITY.md) lines 8–10, 79 and `security.txt` carry policy URLs | None of the four hosts the corpus cites responded to a liveness probe at snapshot (§9.4; FND-2) | Q-19 selected 2026-08-29 — stand up as written; tracked in issue #79 |
| GAP-30 | Per-metric definitions (numerator, denominator, unit, window, source events) | [`Akrites_SIRT_Metrics.md`](../Akrites_SIRT_Metrics.md) eleven-metric starter set; [`Akrites_CVD_Guide.md`](../Akrites_CVD_Guide.md) line 106 instructs "capture metrics" with nothing to point at | No definition prose exists for any metric (MET-1) | Gated on Q-10 + Q-18 — definitions must name the lifecycle model whose timestamps they read |
| GAP-31 | Case-lifecycle data store | The metrics doc's internal cut (queue depth, time-in-stage, cycle time, rework rate) presumes instrumented case states | No store is named anywhere; the two CSVs in `templates/` feed nothing (MET-2) | Gated with GAP-30 — the store and the definitions are one decision |
| GAP-32 | Tooling access & ownership doc (Spyglass, Watchful Eye, Open Door, Rolodex) | [`Akrites_SIRT_CVD_Glossary.md`](../Akrites_SIRT_CVD_Glossary.md) lines 127–134 define all four; [`sirt-communications-playbook.md`](../sirt-communications-playbook.md) line 846 points new operators at them "once provisioned" | No access path, owner, or owning document exists (OPS-4) | Draft in §5.7 |
| GAP-33 | Standalone operator-onboarding checklist | The only onboarding checklist sits inside the playbook's welcome-email template ([`sirt-communications-playbook.md`](../sirt-communications-playbook.md) Play 21; checklist at line 856) | Nothing outside a fill-in email template covers onboarding (OPS-5) | Draft in §5.7 |

### 5.7 Ready-to-paste issue drafts

Drafts for every untracked gap above except §5.6's decision-gated rows (GAP-30–GAP-31 follow ratification of the Q-10/Q-18 selections; GAP-28–GAP-29 became issue #79, filed at the Director's direction), in GAP order. Nothing below has been filed.

<details>
<summary><strong>GAP-08</strong> — Define the co-finder attribution cutoff (trigger/point in time)</summary>

**Title:** Define the co-finder attribution cutoff (trigger/point in time)

**Body:** `acknowledgements-and-attribution.md` ships co-finder credit rules but leaves the cutoff undefined: "Co-finders are honored up to the attribution cutoff — the point in the timeline after which additional independent reports are recorded but not added to the published advisory" (line 187), and lists it as an open item: "Set the concrete co-finder attribution cutoff trigger/point in time" (line 259). `sirt-communications-playbook.md` Appendix B independently repeats the same open item: "Define the co-finder attribution cutoff (referenced in Plays 7 and 13)" (line 909). Issue #22, which produced the doc, has no open successor tracking this decision. Pick a concrete trigger (e.g., patch-ready date, or the public-disclosure date) and update both docs.
</details>

<details>
<summary><strong>GAP-09</strong> — Draft the Akrites upstream-engagement Code of Conduct</summary>

**Title:** Draft the Akrites upstream-engagement Code of Conduct

**Body:** Three shipped docs presuppose a Code of Conduct for engaging upstream maintainers, distinct from the contributor Code of Conduct: `upstream-engagement-guidelines.md` says "Share the Akrites upstream-engagement CoC" (line 53) and "Ratify the Akrites upstream-engagement Code of Conduct referenced in 1.2" (line 281); `sirt-communications-playbook.md` Appendix B lists "Approve a distinct Code of Conduct for upstream engagement to accompany first-contact (Play 9)" (line 914); `Akrites_CVD_Guide.md` expects engagement "distinct from any general community code" (line 118). No such document exists and no issue tracks it. Draft and ratify it, then resolve the dangling internal citations.
</details>

<details>
<summary><strong>GAP-10</strong> — Create the steward-engagement taxonomy referenced by two guides</summary>

**Title:** Create the steward-engagement taxonomy referenced by two guides

**Body:** `upstream-engagement-guidelines.md` lists a "steward-engagement taxonomy" as a companion doc (line 6) and instructs coordinators to use "the steward-engagement taxonomy to make this call" when judging steward fit (line 129); `sirt-communications-playbook.md` Appendix C repeats it as a companion for Play 10 (line 921). No taxonomy document exists anywhere in the repo, and no issue tracks it. Without it, the steward-vetting instruction has nothing concrete to point coordinators at. Draft the taxonomy (e.g., by trust tier / org type / track record) and link it from both citing docs.
</details>

<details>
<summary><strong>GAP-11</strong> — Write OSS-SIRT Process (High Level) and OSS-SIRT MVSR</summary>

**Title:** Write OSS-SIRT Process (High Level) and OSS-SIRT MVSR

**Body:** `sirt-communications-playbook.md` names two foundational companion documents that exist nowhere in the repo: "OSS-SIRT Process (High Level), OSS-SIRT MVSR" in its header companion list (line 6), repeated in Appendix C (line 921). No issue or PR references either title. These read as the process-overview and minimum-viable-scope documents the playbook assumes exist. Scope, draft, and land both — or formally fold their content elsewhere and remove the citations. May split into two issues once scoped.
</details>

<details>
<summary><strong>GAP-12 / GAP-21</strong> — Decide where the SIRT's chartering document lives</summary>

**Title:** Decide where the SIRT's chartering document lives — and repoint the "Akrites: The SIRT" citation

**Body:** Two related gaps. (1) `Embargo Handling Guidance.md` grounds its confidentiality model on a document that doesn't exist under this title anywhere in the repo: it "extends the confidentiality principles in *Akrites: The SIRT*" (line 9). (2) Repository history shows a Technical Charter (`CHARTER.md`) was committed, revised twice, reduced to placeholder text, and deleted, all on 2026-07-08 (commits `822a211`, `a5d8b52`, `e0d9169`, `b347588`); no charter or mandate document has existed in the repo since. Decide whether the SIRT's mandate is chartered in this repository, in a foundation-level governance location, or on the website — then either restore a charter here or add a pointer to where it lives, and repoint or rewrite the Embargo Handling citation.
</details>

<details>
<summary><strong>GAP-13</strong> — Resolve the two empty Severity Guidelines/Scale links</summary>

**Title:** Resolve the two empty Severity Guidelines/Scale links in Read-in Tier Policy

**Body:** `Read-in Tier Policy.md` has two empty-target links to documents that don't exist under these names: "TLP classification follows case severity per [Akrites SIRT Severity Guidelines]()" (line 23) and severity "assessed using the [Akrites SIRT Severity Scale]()" (line 58). PR #61 (open, 0 reviews) drafts a differently named `Severity_Scoring_Methodology.md` for issue #32 — likely the intended target, but nothing wires these links to it and the names don't match. When #61 lands, retarget both links, or confirm a separate Guidelines/Scale doc is actually wanted.
</details>

<details>
<summary><strong>GAP-14</strong> — Develop the read-in tier RACI referenced by two policies</summary>

**Title:** Develop the read-in tier RACI referenced by two policies

**Body:** Two shipped docs defer to a RACI matrix that doesn't exist: `Read-in Tier Policy.md` says "A detailed RACI covering the specific actions each tier may take, and by whom, is to be developed as a companion to this policy" (line 58); `SIRT Read-in Guidelines.md` lists "RACI per tier — the specific actions each tier may take (to be developed)" among its own open items (line 103). No issue or PR tracks this; until it exists, who may do what at each read-in tier is undefined beyond general tier descriptions. Draft the RACI as a companion to both documents.
</details>

<details>
<summary><strong>GAP-15</strong> — Define the "Security Card" artifact referenced by three docs</summary>

**Title:** Define the "Security Card" artifact referenced by three docs

**Body:** Multiple shipped docs treat a per-project "Security Card" as an existing, actionable record — `what-counts-as-public-disclosure.md` says to "log the break on the project Security Card" (line 211) and shows it in a workflow diagram (line 260); `upstream-engagement-guidelines.md` says data "feeds the Security Card" (line 30) and cites it twice more (lines 42, 175). The Glossary only glosses the term (line 132). No template, schema, or owning doc exists. Create the Security Card template/schema — or a doc defining where it lives and who owns it — so these five citations resolve to something real. Note: what it may record about maintainers, and who governs that, is a separate open question in the 2026-08-28 audit's decision register.
</details>

<details>
<summary><strong>GAP-16</strong> — Create Knowers_File.md, the case-consent mechanism templates rely on</summary>

**Title:** Create Knowers_File.md, the case-consent mechanism templates rely on

**Body:** `Akrites_Case_ReadIn_Notice_Template.md` makes participation contingent on a file that doesn't exist anywhere in the repo: "adding your name via a PR to the Knowers_File.md for this working group" (line 97). This is the template's actual consent/acceptance mechanism, not a footnote — as written, a case lead following the template cannot complete a read-in. Either create a `Knowers_File.md` template (likely per-case or per-WG) and document where it lives, or replace the mechanism with one that already exists. Note the template also offers a second, competing acceptance mechanism (reply-to-email); pick one.
</details>

<details>
<summary><strong>GAP-17</strong> — Land SECURITY-INSIGHTS.yml, drafted once, orphaned since day one</summary>

**Title:** Land SECURITY-INSIGHTS.yml — drafted once, orphaned since day one

**Body:** `upstream-engagement-guidelines.md` expects a `SECURITY-INSIGHTS.yml` to exist (lines 33, 194, and its own unchecked checklist item "[ ] Add SECURITY-INSIGHTS.yml" at line 258), but the repo has none. A single-commit branch `add-security-insights` created the file on 2026-07-08 (the repo's first day) alongside a now-unrelated wholesale rewrite (it would delete ~40 files that exist on current `main`); it was never opened as a PR. Extract just the SECURITY-INSIGHTS.yml content from that branch, rebase it onto current `main` as its own small PR, and check off the guideline's checklist item.
</details>

<details>
<summary><strong>GAP-18</strong> — Establish a public SIRT community meeting cadence and platform</summary>

**Title:** Establish a public SIRT community meeting cadence and platform

**Body:** `README.md` has advertised a placeholder for at least two weeks: "Community Meetings forthcoming" (line 62), with no cadence, platform, or link ever added. GitHub Discussion #40 raised the meeting-agenda-platform question and it remains unresolved there (as of 2026-08-28), with no corresponding issue or doc change in this repo. Decide the platform and cadence, then replace the README placeholder with the real schedule and a link.
</details>

<details>
<summary><strong>GAP-19</strong> — Decide the account-anonymization policy</summary>

**Title:** Decide the account-anonymization policy — deadline lapsed with no record

**Body:** GitHub Discussion #45 set an account-anonymization decision deadline that expired 2026-08-11 with no recorded decision (as of 2026-08-28), and no corresponding issue was opened. A corpus-wide search for "anonymiz" across every doc in the repo returns zero matches — the decision currently has no footprint anywhere in tracked documentation, so even a delayed decision has nowhere to land once made. Carry the decision forward from the discussion into an issue, and identify which doc (likely `acknowledgements-and-attribution.md` or `ai-use-disclosure.md`) should record the resulting policy.
</details>

<details>
<summary><strong>GAP-20</strong> — Fill the OSS-SIRT Team Lead role; populate the roster sections</summary>

**Title:** Fill the OSS-SIRT Team Lead role; populate Collaborators/Contributors roster

**Body:** `README.md` lists "OSS-SIRT Team Lead (TBD)" (line 67) alongside two empty roster sections, "Project Collaborators" (line 69) and "Project Contributors" (line 72), unchanged since 2026-08-14. No issue tracks recruiting a Team Lead or populating either section. This is a self-flagged gap (the doc doesn't hide it) rather than a broken assumption, but it's a visible front-door placeholder on a public repo. Assign or recruit a Team Lead and populate both sections — or note in the README why they're intentionally deferred.
</details>

<details>
<summary><strong>GAP-27</strong> — Align five shipped documents with MoLR v0.2 once PR #62 merges</summary>

**Title:** Align five shipped documents with MoLR v0.2 (post-#62)

**Body:** PR #62's own description flags that merging it leaves two shipped docs carrying stale v0.1 framing: `Akrites_SIRT_CVD_Glossary.md` ("a WG stewards or forks an unmaintained project to ship a fix; requires TOC approval" — the PR body cites this at line 41; at the 2026-08-28 snapshot it sits at line 43) and `Akrites_CVD_Guide.md` ("a working group forks or stewards as a carefully bounded last resort," line 126). The 2026-08-28 audit's sweep (finding ROL-14) widens the set: the same v0.1 MoLR/fork vocabulary also sits at `upstream-engagement-guidelines.md` lines 162 and 282, `sirt-communications-playbook.md` lines 668 and 911, and `Embargo Handling Guidance.md` line 122 — seven sightings in five documents, none of them in #62's file set. No follow-up issue exists, so the misalignment would land silently on merge day. File this the day #62 merges and sweep all five docs to the v0.2 model. Two smaller things are cheaper to catch in #62's own review instead: the draft lets "a delegated stewardship panel" approve MoLR steps (diff line 487) while its decision-record template has no panel field (diff line 922), and the v0.1 "Global Board" reference (v0.1 line 18) should be confirmed gone at merge.
</details>

<details>
<summary><strong>GAP-32</strong> — Document access paths and owners for the four named SIRT tools</summary>

**Title:** Document access paths and owners for the four named SIRT tools

**Body:** The glossary defines four operational tools — Spyglass, Watchful Eye, Open Door, and Rolodex (`Akrites_SIRT_CVD_Glossary.md` lines 127–134) — and the playbook's welcome email points new operators at them "once provisioned" (`sirt-communications-playbook.md` line 846). No document says what any of them concretely is, where it lives, who owns it, or how access is requested and granted. Write the tooling doc: for each tool, its purpose, its location (or an explicit "private — ask the owner" pointer), its owner, and the access path. If a tool is aspirational rather than deployed, say so — operators currently cannot tell. Related finding: OPS-4 in the 2026-08-28 audit.
</details>

<details>
<summary><strong>GAP-33</strong> — Extract the operator onboarding checklist into a standalone doc</summary>

**Title:** Extract the operator onboarding checklist into a standalone doc

**Body:** The only onboarding checklist for new SIRT operators lives inside a fill-in email template — Play 21, the welcome email, of `sirt-communications-playbook.md` (play heading at line 802; the "Getting started this week" checklist at line 856 of a 923-line document). Someone joining the team can only find it by reading the whole playbook, and a checklist embedded in an email cannot grow independently of the email's tone and length. Extract it into a standalone onboarding doc under `docs/`, keep Play 21 pointing at it, and fold in the tooling-access paths once GAP-32's doc exists. Related finding: OPS-5 in the 2026-08-28 audit.
</details>

## 6. Decision register

This register consolidates the genuinely open questions the corpus cannot answer for its own readers into one place, with options and a recommendation for each, grouped by who is best placed to decide. It draws on the confirmed findings (§4, Appendix A), the missing-and-stalled inventory (§5), the persona and verification rounds described in §10, the corpus's own self-declared open-items lists, and the two dated decision records the corpus already carries (CVD policy v0.4 and Read-in Tier Policy v0.2, both 2026-08-24). A question appears here only if it is genuinely unresolved: a recorded decision that simply hasn't propagated everywhere yet is a documentation fix — most ship in the fix train accompanying this audit — not a decision, and is excluded (see the consolidation notes at the end of this section). Citations use the same compact `file:line` form as Appendix A.

Each question is assigned to a proposed decider using one rule: **Director-decidable** questions are operational or editorial calls inside existing, already-recorded policy; **TOC** questions are technical or process-policy calls, matching the split the CVD policy's own dispute-and-appeals section (§15) already draws for escalations; **Governing Board** questions are policy/legal, membership, or budget/infrastructure calls. The Director may reassign any question below to a different decider where operational reality warrants it.

Status on every question starts `Open — pending selection`, moves to `Selected by Director, <date>` once the Director (or the reassigned decider) picks an option, and to `Ratified by TOC/GB, <date>` once the relevant body formally ratifies it — substituting the actual ratifying body for whichever of TOC or GB applies.

**Selection pass, 2026-08-29.** All twenty-two questions below now carry a Director selection, recorded in each question's Status line. One structural note governs how to read them: **no Technical Oversight Committee is currently constituted.** Questions grouped under §6.2 keep the proposed-decider grouping as written at audit time, but their selections route to the Governing Board for ratification, and forward-looking text avoids new TOC references until a TOC exists (quotes from source documents are unchanged). §6.1 selections are final Director calls — the three Director-decidable selections with textual propagation ship as PRs #80 (role titles), #81 (the AI-tooling intake field), and #82 (the SIREN glossary entry) — while §6.2 and §6.3 selections are the Director's proposed direction pending Governing Board ratification, and deliberately ship no propagation until ratified.

### Summary

| Q-ID | Question | Proposed decider | Recommendation |
|---|---|---|---|
| Q-01 | Standard title for the individual running a case | Director | strong |
| Q-02 | Working-group leadership title: Chair/Co-Chair or WG Lead | Director | strong |
| Q-03 | Who is accountable for executing publication at Public Disclosure | Director | either-viable |
| Q-04 | Restore the AI-tooling warning at intake; verify or trust the self-disclosure | Director | strong on the warning; either-viable on verification |
| Q-05 | One filename convention for repository documents | Director | strong on picking one; either-viable on which |
| Q-06 | MoLR/fork/steward approval authority, and the undefined "Stewardship panel" | TOC | strong |
| Q-07 | Severity vocabulary, and the advisory-identifier scheme (AVID vs. OSS-SIRT ID) | TOC | either-viable |
| Q-08 | TLP during remediation: unconditional AMBER+STRICT, or severity-dependent RED | TOC | either-viable |
| Q-09 | Extension/deviation approval: TOC awareness, or TOC/Board approval | TOC | strong |
| Q-10 | Canonical lifecycle-phase list, and the embargo clock's exact trigger and units | TOC | either-viable |
| Q-11 | Read-in delegation, RACI, lead times, and the Knowers mechanism | TOC | either-viable |
| Q-12 | Remove or redefine the "Premier Member" emergency-read-in gate | TOC | strong |
| Q-13 | The co-finder attribution cutoff trigger | TOC | either-viable |
| Q-14 | Intake commitment (accept-everything vs. the six-item bar) and phase-advancement criteria | TOC | either-viable |
| Q-15 | Does read-in Gate 3 admit the Finder to their own case | TOC | strong |
| Q-16 | State the TOC-vs-Board escalation map — including the outsider's entry point — in one place | Governing Board | strong |
| Q-17 | Ratify the public-disclosure break-classification matrix and accelerate/hold authority | Governing Board | either-viable |
| Q-18 | Metrics program design: cadence, weighting, publication approval, headline metric | Governing Board | either-viable |
| Q-19 | Fund/launch the referenced public infrastructure and internal tool access | Governing Board | strong |
| Q-20 | Name the accountable legal entity for safe harbor and liability | Governing Board | either-viable |
| Q-21 | One document-status scheme and a ratification path | Governing Board | strong |
| Q-22 | Governance for the "Security Card" before any schema ships | Governing Board | strong |

### 6.1 Director-decidable

#### Q-01 — Standard title for the individual running a case

**Question:** What is the standard title for the individual who runs a case day-to-day?

**Why it blocks work:** The institutional function is ratified vocabulary, but the individual doing the work is named at least two different ways elsewhere, with no ratified individual title.

**Surfaces in:**
- `coordinated-vulnerability-disclosure-policy.md:171` — "neutral **clearinghouse and coordinator**" (institutional role, ratified)
- `docs/Read-in Tier Policy.md:108` — "**SIRT case lead**" (individual title, used in an escalation table)

**Options:**
- a) "SIRT case coordinator" — extends the CVD policy's own ratified institutional family of terms to the individual (per `coordinated-vulnerability-disclosure-policy.md:171`)
- b) "SIRT case lead" — matches the title already used in the read-in tier escalation table (per `docs/Read-in Tier Policy.md:108`)
- c) Keep both in circulation, and add a glossary entry stating they name the same role

**Recommendation:** (a), strong. The institutional vocabulary ("coordinator"/"clearinghouse") is already dated and ratified; extending the same family to the individual avoids introducing a fourth term into a corpus that already has two.

**If undecided:** New participants and external maintainers cannot tell whether "case lead," "coordinator," and "SIRT case lead" name one role or several, which complicates onboarding text and external-facing templates that use these terms interchangeably.

**Prior art:** CVD v0.4 (2026-08-24) ratifies the institutional terms; no decision on the individual title is recorded anywhere.

**Status:** Selected by Director, 2026-08-29 — (a): the individual running a case is titled "SIRT case coordinator." Propagated by PR #80.

#### Q-02 — Working-group leadership title

**Question:** Is the standard title for working-group leadership the Operating Guide's "Chair / Co-Chair" (long form "WG Chairperson") or the Tier Policy's "WG Lead"?

**Why it blocks work:** The document dedicated to working-group structure names leadership only in the Chair/Chairperson family; a governance escalation table elsewhere uses "WG Lead".

**Surfaces in:**
- `docs/Akrites_WorkingGroup_Operating_Guide.md:41` — "**Initial WG Chairperson** and if relevant, Co-Chair"
- `docs/Akrites_WorkingGroup_Operating_Guide.md:45` — "**Pick a Chair / Co-Chair** among yourselves to coordinate the WG"
- `docs/Read-in Tier Policy.md:108` — "may be performed by WG Lead in concurrence with other SIRT members"

**Options:**
- a) "Chair / Co-Chair" (long form "Chairperson"), per the Operating Guide
- b) "WG Lead," per Read-in Tier Policy's usage
- c) Treat as synonyms and record that explicitly wherever working-group roles are defined

**Recommendation:** (a), strong. The Operating Guide is the document specifically dedicated to working-group structure, and its usage is exclusive and repeated; the Tier Policy's "WG Lead" reads as incidental to a different table's purpose.

**If undecided:** Working-group documentation and read-in escalation language keep naming what looks like the same role two different ways, with no cross-reference telling a reader they are the same.

**Prior art:** None.

**Status:** Selected by Director, 2026-08-29 — (a): "Chair / Co-Chair" (long form "Chairperson"), per the Operating Guide. Propagated by PR #80.

#### Q-03 — Accountable role for executing Public Disclosure

**Question:** Who is accountable for actually executing publication at Public Disclosure — pressing publish, timing it, and owning the outcome if it slips?

**Why it blocks work:** Every description of this step is written in institutional voice, naming the organization but never a role or person responsible for the single most consequential action in the process.

**Surfaces in:**
- `coordinated-vulnerability-disclosure-policy.md:391` — "the Akrites SIRT publishes the advisory"
- `templates/notification-templates.md:189` — "Publish at PD. For GitHub projects, publishing the draft Security Advisory"

**Options:**
- a) Assign the case coordinator (per Q-01, once decided) as the default accountable actor for publication
- b) Create a separate, named "publisher" role distinct from the case coordinator
- c) Keep ownership institutional/collective, and document that as a deliberate choice rather than a gap

**Recommendation:** Either-viable. A dedicated accountable role and a documented collective-ownership model are both workable; nothing in the corpus leans toward one over the other.

**If undecided:** No single role can be asked why a disclosure published late or early, and accountability for the process's most consequential action stays diffuse by default rather than by design.

**Prior art:** None.

**Status:** Selected by Director, 2026-08-29 — (a): the SIRT case coordinator is the default accountable actor for executing publication. Propagated by PR #80.

#### Q-04 — The AI-tooling rule at intake: restore the warning, and verify or trust the disclosure

**Question:** The no-embargo rule for reports developed with public AI tooling is settled policy. Two operational questions around it are not: is the AI-tooling field — the one line that would tell a Finder the rule exists — restored to the entry checklist, and does the SIRT verify a Finder's self-disclosure or rely on it as purely self-reported?

**Why it blocks work:** The substantive rule is settled and converges across two policy documents, but `SECURITY.md`'s "What to include" checklist carries no AI-tooling item at all, and no compliance-checking mechanism is described anywhere.

**Surfaces in:**
- `docs/Embargo Handling Guidance.md:73` — "A report developed with public LLM tooling must be treated as NOT having an embargo available"
- `docs/Embargo Handling Guidance.md:76` — describes only Finder self-disclosure at intake, with no SIRT-side check
- `coordinated-vulnerability-disclosure-policy.md:324` — "This is why AI use is captured at intake"
- `SECURITY.md:38–45` — the six-item intake checklist, with no AI-tooling field

**Options:**
- a) Restore the AI-tooling field to `SECURITY.md`'s checklist with a one-line consequence warning, and accept self-disclosure alone, consistent with the program's good-faith framing elsewhere
- b) Restore the field, and add a lightweight technical or behavioral check at intake
- c) Restore the field, and spot-check after the fact, treating a misrepresentation as a safe-harbor violation

**Recommendation:** Strong on restoring the field — every option starts there, because the rule binds Finders whether or not the entry document lets them discover it. Either-viable on verification: a pure trust model and a lightweight check both fit the program's stated values, and the corpus does not lean either way.

**If undecided:** A Finder can forfeit their embargo by violating a rule the entry checklist never showed them, and the rule itself is only as strong as a Finder's willingness to disclose honestly, with no stated fallback for the cases where they don't.

**Prior art:** The underlying rule is settled (both documents agree on it); the missing warning is entry-document drift (POL-11), and the verification mechanism was never designed.

**Status:** Selected by Director, 2026-08-29 — (a): restore the AI-tooling field to SECURITY.md's checklist with a one-line consequence warning; self-disclosure is trusted as reported. Propagated by PR #81.

#### Q-05 — One filename convention for repository documents

**Question:** Which filename convention do repository documents adopt going forward?

**Why it blocks work:** Thirty-nine files follow at least five conventions, and each new document rolls the dice; the corpus's worst filename anomalies — a double-dot `.md` that hides the Code of Conduct from GitHub's detection, four templates with a trailing space before the extension — are the convention vacuum's direct products.

**Surfaces in:**
- §9.2 — the census: `snake_Case_With_Caps` (11), `kebab-case` (9), `Words with spaces.md` (7), trailing-space-before-extension (4), plus a double-dot filename, an `&`, and a `README`/`readme` case split
- `templates/Steward vetting & approval record .md` — a live template carrying both an `&` and a trailing space

**Options:**
- a) `kebab-case.md` — the convention the corpus's largest public-facing documents already use (the CVD policy, the communications playbook, the disclosure and engagement guidelines), and the only bucket that survives URL-encoding untouched
- b) `Snake_Case_With_Caps.md` — the numerically largest bucket today
- c) Leave the convention unset; rename only pathological names as they surface

**Recommendation:** Strong on picking one now; either-viable on which — though (a) is the bucket the finder-facing documents already live in. Renames themselves are cheap; every month without a convention adds files that will need renaming later, and inbound links that will break when they do.

**If undecided:** Every rename stays a one-off judgment call, four template filenames keep a trailing space no file browser shows, and the census in §9.2 keeps growing new buckets.

**Prior art:** None. The fix train renames the two worst anomalies (HYG-1); it deliberately does not pick the convention.

**Status:** Selected by Director, 2026-08-29 — (a): kebab-case.md for new and renamed files going forward; existing names are renamed opportunistically, not en masse.

### 6.2 TOC

#### Q-06 — MoLR/fork/steward approval authority, and the undefined "Stewardship panel"

**Question:** Who must approve a Maintainer-of-Last-Resort fork or a steward handoff, and what is the "Stewardship panel" offered as an alternative to the TOC in some of these documents?

**Why it blocks work:** Five documents state five different formulations of this authority, and "Stewardship panel" is never defined anywhere despite appearing as a named alternative in the merged guidelines, in a live template, and in the pending revision.

**Surfaces in:**
- `docs/Maintainer_of_Last_Resort_Guidelines.md:151` — "No unilateral SIRT forks"
- `docs/Maintainer_of_Last_Resort_Guidelines.md:212` — "The **TOC (or a delegated Stewardship panel) approves** the Steward" (the panel alternative is in the merged document today, not only in the pending revision)
- `docs/Akrites_SIRT_CVD_Glossary.md:43` — "requires TOC approval"
- `docs/Read-in Tier Policy.md:91` — "Only with SIRT+WG approval"
- `docs/sirt-communications-playbook.md:656` and `:911` — "the group/TOC has approved publishing a patch"; "Decide MoLR/fork authority and triggers"
- `templates/Steward vetting & approval record .md:10` — "TOC / panel approval"
- PR #62 diff line 487 (open, unmerged as of 2026-08-28) — "TOC, or a delegated stewardship panel, approves" — the rewrite keeps the panel option while rewording the clause

**Options:**
- a) TOC approval only, no panel option (per the Maintainer-of-Last-Resort guidelines' own "no unilateral forks" rule and the glossary)
- b) TOC approval, or a delegated "Stewardship panel" left otherwise undefined — the position the merged guidelines (§7.4), the steward-vetting template, and the pending pull request all currently hold
- c) SIRT+WG approval, with no TOC role (per Read-in Tier Policy)
- d) Full TOC approval for standard cases, with a fast path of the SIRT lead plus one non-recused TOC member for lower-stakes cases — proposed in the same pending pull request (PR #62 diff line 923: "SIRT lead ___ + non-recused TOC member")

**Recommendation:** Toward (a) or (d), strong. Five of the six sources converge on a TOC role; the lone SIRT+WG-only position sits inside what reads as a read-in-access exception list rather than a dedicated treatment of fork/steward authority. The part most needing a decision is whether "Stewardship panel" is a real, separately-constituted body — in which case it needs a charter — or should be dropped from all three places it appears.

**If undecided:** An unmaintained project's fork-of-last-resort, or a steward handoff, can point to a different named approver depending which document a reader opens — including the document currently being revised to address exactly this.

**Prior art:** None recorded; the corpus's own communications playbook lists this as open from a prior in-person meeting.

**Status:** Selected by Director, 2026-08-29 — as amended by the Director: approval sits with the SIRT plus the Governing Board for now — no TOC is currently constituted — to be iteratively refined with each case; the "Stewardship panel" is dropped unless separately chartered. Awaiting Governing Board ratification.

#### Q-07 — Severity vocabulary and advisory-identifier scheme

**Question:** Is the ratified severity scale CRITICAL/HIGH/MEDIUM/LOW, or the Critical/Important/Moderate/Low scale that is already in live use elsewhere and separately proposed for formal adoption? And is the advisory identifier "AVID," or an OSS-SIRT-prefixed OSV-style ID?

**Why it blocks work:** The alternate severity vocabulary already appears in a merged, non-draft document — not only in the pending proposal that would formalize it — and the two named advisory-identifier concepts have never been reconciled with each other.

**Surfaces in:**
- `docs/upstream-engagement-guidelines.md:88` — "Prioritize **Critical/Important** findings for first engagement"
- `docs/Akrites_SIRT_CVD_Glossary.md:127` — AVID defined as "Akrites' disclosure record/advisory concept"
- `templates/advisory.osv.json:3` — `"id": "OSS-SIRT-0000-0000"`

**Options:**
- Severity scale: a) keep the recorded CRITICAL/HIGH/MEDIUM/LOW scale and correct the live outlier usage to match it, or b) adopt Critical/Important/Moderate/Low as PR #61 proposes, for closer alignment with major downstream severity vocabularies, and sweep the corpus to match
- Identifier: c) standardize on one scheme — either the OSS-SIRT-prefixed IDs already in the advisory template or the glossary's "AVID" — and retire the other to a defined synonym

**Recommendation:** Either-viable on the severity-scale choice — both scales have a live, reasoned constituency, and the alternate vocabulary is not a typo but a considered proposal. Strong on (c): pick one identifier scheme rather than carrying two names for what appears to be the same artifact.

**If undecided:** A severity label or an advisory ID means something different depending on which document produced it — exactly the kind of drift that downstream automated tooling cannot absorb silently.

**Prior art:** Read-in Tier Policy v0.2 (2026-08-24) records a severity-classification scale; live usage has since drifted from it in at least one merged document, and PR #61 would formalize the drift.

**Status:** Selected by Director, 2026-08-29 — scale (a): keep CRITICAL/HIGH/MEDIUM/LOW and correct outlier usage (PR #61 to be revised in review rather than adopted as-is); identifier (c): standardize on AVID and retire the OSS-SIRT-prefixed scheme to a defined synonym. Awaiting Governing Board ratification.

#### Q-08 — TLP classification during remediation

**Question:** During patch development, is the TLP label unconditionally AMBER+STRICT for every case, or severity-dependent (RED at CVSS 7.0 and above)?

**Why it blocks work:** Two policy documents, recorded the same day, state different rules for the same moment in the process, with no stated precedence between them.

**Surfaces in:**
- `coordinated-vulnerability-disclosure-policy.md:303–307` — phased TLP model: "TLP:RED at intake", "TLP:AMBER+STRICT during patch development", unconditionally
- `docs/Read-in Tier Policy.md:23` and `:30` — severity-dependent TLP tied to a CVSS 7.0 threshold

**Options:**
- a) CVD's unconditional phased model governs
- b) Read-in Tier Policy's severity-dependent model governs
- c) Merge into one severity-by-phase matrix that states both axes together

**Recommendation:** Either-viable. Both were ratified the same day (2026-08-24) with no tiebreaker recorded between them; (c) is the more durable eventual shape but is itself a design decision, not a default.

**If undecided:** Read-in participants can receive different confidentiality obligations for the identical case, depending which document they were trained against.

**Prior art:** Both CVD v0.4 and Read-in Tier Policy v0.2 are dated, recorded decisions that simply disagree with each other.

**Status:** Selected by Director, 2026-08-29 — (a): the CVD policy's unconditional phased TLP model governs. Awaiting Governing Board ratification.

#### Q-09 — Extension/deviation approval authority

**Question:** Beyond the maintainer's final say on routine extension requests, is the TOC's or Board's role for embargoes longer than 30 days advance *awareness*, or affirmative *approval*?

**Why it blocks work:** The maintainer-final baseline is ratified and independently converges across three documents, but a fourth uses stronger "approve" language for long deviations than the other three's "awareness," and a fifth names a different decision-maker for ordinary extensions altogether.

**Surfaces in:**
- `docs/Read-in Tier Policy.md:74` — "the maintainer having the final authority"
- `coordinated-vulnerability-disclosure-policy.md:338–339` — "requires explicit rationale and TOC awareness"
- `docs/sirt-communications-playbook.md:591` — "TOC/Board approve significant deviations"
- `docs/Akrites_CVD_Guide.md:132` — extension requests go "through the Coordinator, who decides in consultation with the Finder and maintainer"

**Options:**
- a) Maintainer-final always; TOC/Board are informed, not a gate, even past 30 days
- b) Maintainer-final by default, but TOC/Board hold an affirmative approval gate for "significant" deviations specifically
- c) The Coordinator decides, in consultation with Finder and maintainer

**Recommendation:** (a), strong. It is the ratified position (Read-in Tier Policy v0.2) and independently converges with the Embargo Handling Guidance's operating rules and the CVD policy's own embargo section; the Practical Guide's Coordinator-decides framing is explicitly non-normative supplementary material, and the playbook's "approve" reads as a wording drift against its own source material rather than a considered alternative.

**If undecided:** A maintainer negotiating a long extension cannot tell whether TOC sign-off is a courtesy notice they owe, or a veto they need to secure in advance.

**Prior art:** Read-in Tier Policy v0.2 (2026-08-24) records maintainer-final authority as part of its ratified changes.

**Status:** Selected by Director, 2026-08-29 — (a): maintainer-final always; leadership is informed, never a gate — the Governing Board standing in while no TOC is constituted. Awaiting Governing Board ratification.

#### Q-10 — Canonical lifecycle-phase list and the embargo clock's trigger and units

**Question:** Which phase breakdown is canonical for describing the vulnerability lifecycle, precisely when does the embargo clock start, and are all of the corpus's clocks even using the same units?

**Why it blocks work:** Three documents describe the lifecycle using three non-matching phase lists (and the glossary carries a fourth, pipeline-shaped framing); the phase the Embargo Handling Guidance names as the clock trigger matches none of them verbatim; and the Maintainer-of-Last-Resort contact ladder counts in business days while the embargo and accelerated-disclosure clocks count in calendar days — the mix runs through the middle of a single table.

**Surfaces in:**
- `SECURITY.md:65` — "Discover → Triage → Validate → Coordination → Patch → Test → Document → Distribute → Disclose"
- `docs/Embargo Handling Guidance.md:23` — clock starts at the "end of the *Deduplicate & validate* phase" (a phase name no lifecycle model contains)
- `docs/Maintainer_of_Last_Resort_Guidelines.md:46–49` — contact attempts at T0+5/10/15 *business* days, then a decision point at "T0 + ~30 days" in the same table
- `coordinated-vulnerability-disclosure-policy.md:354` — accelerated track targets "actionable guidance within 7 days", calendar days
- `docs/Akrites_SIRT_CVD_Glossary.md:131` — "Pipeline: Dedup → Investigator → Fixer", vs. the CVD policy's own four-stage mapping at `coordinated-vulnerability-disclosure-policy.md:290–295`

**Options:**
- a) Adopt `SECURITY.md`'s public-facing nine-phase list as canonical, and align the Embargo Handling Guidance's trigger wording to it
- b) Adopt the Practical Guide's more detailed Phase 1–9 breakdown as canonical instead
- c) Write one harmonized phase list used everywhere, with a calendar-day convention stated once and inherited by every clock in the corpus

*Rider to (a) or (b):* the units mix is its own fix — state the calendar-vs-business-day convention once and have every clock inherit it. Picking a phase list alone leaves the POL-13 counting hazard live.

**Recommendation:** Either-viable on which existing list wins; (c) is the more durable fix but is a materially bigger lift than picking a winner among the existing lists.

**If undecided:** "When does the clock start" has a different literal answer depending which document a reader holds, and a Maintainer-of-Last-Resort case can be simultaneously on-track and off-track by two different counting conventions running at once.

**Prior art:** None directly. CVD v0.4's changelog describes harmonizing the nine-phase lifecycle with a four-stage pipeline, but the Embargo Handling Guidance's and Practical Guide's own phase names were not brought into that harmonization.

**Status:** Selected by Director, 2026-08-29 — (a) plus the rider: SECURITY.md's nine-phase list is canonical, the Embargo Handling Guidance's trigger wording aligns to it, and one calendar-vs-business-day convention is stated once and inherited by every clock. Awaiting Governing Board ratification.

#### Q-11 — Read-in delegation, RACI, lead times, and the Knowers mechanism

**Question:** Who is the approver of record for read-in decisions, what are the default lead times per tier, what is the RACI, may a maintainer veto a read-in, and how does adding someone to a working group's "Knowers" list actually work in practice?

**Why it blocks work:** The corpus's own read-in guidelines list all of these as unresolved, and the one concrete mechanism pointed to for expanding a "Knowers" list — adding a name to a "Knowers_File.md" by pull request — does not otherwise exist anywhere in the corpus.

**Surfaces in:**
- `docs/SIRT Read-in Guidelines.md:98–104` — "Open items to confirm with the TOC / Governing Board", listing approver of record, lead times, delegation rules, RACI, and antitrust documentation
- `templates/Akrites_Case_ReadIn_Notice_Template.md:97` — "adding your name via a PR to the Knowers_File.md for this working group"
- `docs/sirt-communications-playbook.md:910` — "Ratify the read-in delegation model and whether maintainers may veto read-ins"

**Options:**
- a) Formalize the Knowers_File.md mechanism as designed, and create the missing location for it
- b) Drop the Knowers_File.md idea, and track read-in membership through existing case-management tooling instead
- c) Leave lead times and RACI to case-by-case judgment rather than a fixed table, at least for now
- d) In addition to whichever of (a)–(c) is selected: name the approver of record — the natural default is the case-runner role Q-01 selects — and record whether a maintainer may veto a read-in on their own project. These are the two sub-questions in the source guidelines that none of the mechanics above settles

**Recommendation:** Either-viable among (a)–(c); (d) is needed under any of them — ROL-4 exists because the approver of record already differs between documents.

**If undecided:** A participant told to add their name to the Knowers_File.md has no working location to do it in, and no one can point to an approver of record for how long that process should take.

**Prior art:** None; self-declared open in the source document.

**Status:** Selected by Director, 2026-08-29 — (b) + (d): read-in membership is tracked in existing case-management tooling (no Knowers_File.md); the approver of record is the SIRT case coordinator (per Q-01); the maintainer-veto rule is to be recorded as part of the same fix. Awaiting Governing Board ratification.

#### Q-12 — "Premier Member" emergency-read-in gate

**Question:** Should the "Premier Member" sponsorship gate for emergency read-in be removed or redefined?

**Why it blocks work:** The gate directly contradicts a ratified, same-corpus principle that read-in access is never determined by membership tier.

**Surfaces in:**
- `docs/SIRT Read-in Guidelines.md:49` — emergency read-in requires sponsorship "by an active maintainer or Premier Member"
- `docs/Read-in Tier Policy.md:13` — read-in decisions are made "never by a member's industry, commercial standing, or membership tier"

**Options:**
- a) Remove the Premier Member sponsorship path entirely
- b) Keep a sponsorship path, but make it tier-neutral — any active maintainer or vetted member organization, not a named commercial tier
- c) Keep it as written, and treat the equal-access principle as not covering this specific emergency case

**Recommendation:** Toward (a) or (b), strong. "Premier Member" is not defined anywhere as an actual program tier, and the equal-access principle it conflicts with is unambiguous and was ratified after the guideline containing the gate.

**If undecided:** The corpus keeps a live, actionable procedure that its own ratified policy says should not exist.

**Prior art:** Read-in Tier Policy v0.2 (2026-08-24) ratifies the equal-access principle this gate conflicts with.

**Status:** Selected by Director, 2026-08-29 — (a): remove the Premier Member sponsorship path entirely. Awaiting Governing Board ratification.

#### Q-13 — Co-finder attribution cutoff

**Question:** What is the trigger point ("cutoff") after which a later reporter of the same issue is no longer credited as a co-finder?

**Why it blocks work:** Two documents name the need for this cutoff without ever proposing where it falls.

**Surfaces in:**
- `docs/acknowledgements-and-attribution.md:187` — "up to the attribution cutoff — the point in the timeline after which"
- `docs/sirt-communications-playbook.md:909` — "Define the co-finder attribution cutoff"

**Options:**
- a) First successful contact with the SIRT
- b) The point a case is formally opened and assigned
- c) The point read-in begins for the original finder's report

**Recommendation:** Either-viable. The corpus repeatedly names the need for a cutoff without proposing where to draw it, and each option has a reasonable operational case.

**If undecided:** Two people who report the same issue days apart cannot be told in advance whether both will be credited.

**Prior art:** None; self-declared open in two documents.

**Status:** Selected by Director, 2026-08-29 — (a): the attribution cutoff is first successful contact with the SIRT. Awaiting Governing Board ratification.

#### Q-14 — Intake commitment and phased-rollout advancement

**Question:** Does the SIRT accept and triage every report regardless of completeness, or does the six-item "SIRT-ready" bar function as a gate? And what moves intake from the member-reports phase to the clearinghouse phase, and then to the unsolicited/public phase?

**Why it blocks work:** The intake template states both an unconditional accept-everything promise and a completeness bar in the same short section, and the policy names a three-phase rollout sequence without stating what triggers advancing between phases.

**Surfaces in:**
- `templates/vulnerability-report-intake-template.md:13–16` — "We accept and triage every report … you do not need all of the following to report", immediately alongside a six-item completeness bar
- `coordinated-vulnerability-disclosure-policy.md` §12 — member reports first, clearinghouse reports next, unsolicited/public reports in the final phase

**Options:**
- a) The six-item bar is a target for Finders to aim for, not a gate — everything gets triaged regardless
- b) An incomplete report may be deferred until it meets the bar
- c) Set explicit, dated criteria for advancing each rollout phase, published wherever intake status is announced

**Recommendation:** Either-viable. Both intake postures are workable programs, and the corpus does not commit to either; the phase-advancement question additionally has no existing candidate answer at all.

**If undecided:** A Finder cannot tell whether an incomplete report will be worked or shelved, and no one can say when the next reporter class becomes eligible to report at all.

**Prior art:** None.

**Status:** Selected by Director, 2026-08-29 — (a) + (c): the six-item bar is a target, not a gate — every report is triaged; explicit, dated phase-advancement criteria are published wherever intake status is announced. Awaiting Governing Board ratification.

#### Q-15 — Does read-in Gate 3 admit the Finder to their own case?

**Question:** As written, can the person who reported a vulnerability pass the read-in gates for their own case — and if not, is that exclusion intended?

**Why it blocks work:** Gate 3's eligibility class is "a known, vetted engineer from a member organization or designated upstream security team engineer." A Tier-0 Finder from outside the membership satisfies neither clause, and the guidelines' own fallback line — non-qualifiers "are served at public disclosure (PD), not before" — would read the report's author out of their own case.

**Surfaces in:**
- `docs/SIRT Read-in Guidelines.md:15` — "**Gate 3 - Vetted Person** Is a known, vetted engineer from a member organization or designated upstream security team engineer"
- `docs/SIRT Read-in Guidelines.md:17` — "consumers are served at public disclosure (PD), not before"
- `docs/Read-in Tier Policy.md:13` — the equal-access principle ("never by a member's … membership tier") the member-organization key sits in tension with

**Options:**
- a) Amend Gate 3 to name the case's own Finder as qualifying explicitly
- b) Keep Gate 3 as the bar for *expanding* access, and state that the Finder's continued participation is not a read-in at all — they already hold the information; the gates govern who else learns it
- c) Deliberate exclusion — document that later-phase participation is for remediation actors only, and say so in the Finder-facing documents

**Recommendation:** Toward (a) or (b), strong that the exclusion become deliberate text rather than an accident of wording; either-viable between them. (b) is the smallest change that makes the model coherent.

**If undecided:** An operator applying the gate literally must refuse the report's own author continued access to the case they opened — likely to be read as bad faith by exactly the population the program depends on.

**Prior art:** None recorded.

**Status:** Selected by Director, 2026-08-29 — (b): the Finder's continued participation in their own case is not a read-in; the gates govern who else learns the information. Awaiting Governing Board ratification.

### 6.3 Governing Board

#### Q-16 — State the TOC-vs-Board escalation map — including the outsider's entry point — in one place

**Question:** Can the corpus state, in one place, the complete escalation map — which disputes go to the TOC, which go to the Governing Board for policy/legal reasons, which go to the Governing Board for membership/sanctions reasons, and where an external Finder or maintainer enters that ladder when their complaint is the SIRT's own silence?

**Why it blocks work:** Two distinct Governing-Board escalation triggers exist side by side in the corpus — policy/legal disputes, and embargo-breach sanctions up to program removal — and nothing states that these are two different tracks rather than a contradiction. Meanwhile the dispute ladder's first rung is "raise it with the case coordinator," which presumes a case and a channel: a Finder whose report has simply gone unanswered has neither, and `SECURITY.md`'s response-time promises name no fallback if they are missed.

**Surfaces in:**
- `coordinated-vulnerability-disclosure-policy.md:481–483` — the TOC's "determination is final for technical and process matters"; "Policy- or legal-level questions are referred to the Governing Board"
- `docs/Read-in Tier Policy.md:100` and `docs/Akrites_WorkingGroup_Operating_Guide.md:28` — identically, "escalated to the GB for considering permanent removal from the program"
- `SECURITY.md:53–54` — acknowledgement within 2 business days, initial assessment within 10, with no stated recourse if neither arrives (FND-9)

**Options:**
- a) State explicitly that these are two complementary tracks — technical/process to the TOC; policy/legal, and membership/sanctions, to the Board — add the entry point an outsider uses when the SIRT itself is unresponsive, and cross-reference the statement from each source document
- b) Fold breach-sanctions escalation into the same TOC-first ladder as technical disputes, with the Board only as a final policy/legal referral
- c) Leave the two tracks separately documented as they are today

**Recommendation:** (a), strong. The two triggers plausibly already coexist by design; the fix is mainly to say so in one place — and the outsider's entry point is one sentence in `SECURITY.md` once the map exists.

**If undecided:** A reader who encounters only one of the two Board triggers can reasonably conclude the other one is a drafting contradiction, and an outside Finder whose report has gone silent has no stated door to knock on.

**Prior art:** CVD v0.4 (2026-08-24) records the technical/process-vs-policy/legal split; the membership/sanctions trigger elsewhere was never explicitly reconciled with it.

**Status:** Selected by Director, 2026-08-29 — (a) as amended by the Director: one map, with every track terminating at the Governing Board — no TOC is currently constituted — including the outside Finder's entry point in SECURITY.md; forward-looking text drops TOC references until one exists. Awaiting Governing Board ratification.

#### Q-17 — Ratify the public-disclosure break-classification matrix

**Question:** Should the Board ratify a formal break-classification/decision matrix, confirm who holds accelerate/hold authority for a given case, and decide whether the first-report date is published alongside an advisory?

**Why it blocks work:** Individual-case accelerate/hold authority is already reasonably assigned in practice, but the formal matrix the source document itself calls for approving has not been ratified — and the "maintainer keeps final authority" principle stated unconditionally elsewhere is never reconciled against the disclosure procedure's scoped override once a break is confirmed public.

**Surfaces in:**
- `docs/what-counts-as-public-disclosure.md:273` — "Approve the break classification/decision matrix and who holds accelerate/hold authority"
- `docs/sirt-communications-playbook.md:912–913` — "Finalize disclosure definition … and whether first-report date is published"
- `docs/upstream-engagement-guidelines.md:74` — "We do **not** impose timelines. The embargo/PD window is a guideline we negotiate", unconditional — vs. `docs/what-counts-as-public-disclosure.md:218–219`, where maintainer timing can be overridden only to protect users after a confirmed public break

**Options:**
- a) Ratify the matrix as currently drafted in `what-counts-as-public-disclosure.md`
- b) Ratify a revised matrix that also states explicitly how it interacts with the general maintainer-final principle
- c) Publish first-report dates by default, with an opt-out
- d) Do not publish first-report dates by default, with an opt-in

**Recommendation:** Either-viable. This calls for the Board to choose specific matrix content and a publication default, not to resolve a conflict where the evidence already favors one side — though (b) would also close the override/maintainer-final seam (TON-3) in the same motion.

**If undecided:** The one document written specifically to answer "what counts as public disclosure" still has its own central decision matrix sitting unratified.

**Prior art:** None; self-declared open for Board approval in the source document.

**Status:** Selected by Director, 2026-08-29 — (b) + (c): ratify a revised matrix that states explicitly how it interacts with the maintainer-final principle, and publish first-report dates by default with an opt-out. Awaiting Governing Board ratification.

#### Q-18 — Metrics program design

**Question:** What is the reporting cadence and format, the severity-weighting methodology (CVSS, EPSS, or a blend), who approves the public cut of metrics against the confidentiality gate, and which metric is the headline figure?

**Why it blocks work:** All four are listed as open questions for the Board in the metrics document itself, and no data source named in that document points to a system of record for case-lifecycle data — the one process document that instructs anyone to capture metrics has nothing to point at.

**Surfaces in:**
- `docs/Akrites_SIRT_Metrics.md:103–108` — "Open questions for the Board", covering cadence/format, severity weighting, public-cut approval, and headline-metric selection
- `docs/Akrites_CVD_Guide.md:106` — the Coordinator is told to "capture metrics" with no reference to the metrics document or any data store

**Options:**
- a) Quarterly public cut, blended CVSS/EPSS weighting, TOC review before publication, mean-time-to-disclosure as the headline figure
- b) Decide each axis independently rather than as one package: (i) cadence and format, (ii) severity weighting — CVSS, EPSS, or a blend, (iii) who approves the public cut against the confidentiality gate, (iv) the headline figure. Each axis has a small option space once separated, and (iii) is the one that blocks publication
- c) Defer the whole program until the read-in and case-data questions elsewhere in this register are settled

**Recommendation:** Either-viable. This is a self-declared Board design question with several genuinely open axes, and no existing document leans toward a specific answer.

**If undecided:** No metrics program can credibly launch, since even its confidentiality gate — who is allowed to approve what gets published — has no named approver.

**Prior art:** None; self-declared open for the Board in the source document.

**Status:** Selected by Director, 2026-08-29 — (a), with Governing Board review in place of TOC review: quarterly public cut, blended CVSS/EPSS weighting, Board approval of the public cut against the confidentiality gate, mean-time-to-disclosure as the headline figure. Awaiting Governing Board ratification.

#### Q-19 — Fund and launch the referenced public infrastructure

**Question:** Will the Board fund and stand up the canonical public infrastructure the policy documents already reference, and specify access-provisioning for the internal tools they name?

**Why it blocks work:** No canonical host the corpus references responded to a liveness probe at snapshot time (2026-08-28; §9.4), the PGP key referenced in `security.txt` has never been published, and the onboarding template lists three named internal tools with a literal fill-in-the-blank placeholder in place of provisioning steps.

**Surfaces in:**
- `security.txt:10` — commented-out PGP key reference, never live
- `docs/sirt-communications-playbook.md:846` — "Tooling once provisioned:" followed by a placeholder listing three named tools with no provisioning steps
- `coordinated-vulnerability-disclosure-policy.md:417` — "the SIRT states the currently active intake modes at the Canonical URL"

**Options:**
- a) Fund and launch the referenced domains, and publish the PGP key as written
- b) Simplify the policy text to stop referencing infrastructure that isn't funded yet, until it is
- c) Both — descope the current promises now, and restore them as the real infrastructure ships

**Recommendation:** (a), strong. Nothing here is a design disagreement; every reference already specifies what should exist, and the gap is execution and budget, not decision-making.

**If undecided:** Even the currently-active intake phase — which class of reporter the SIRT accepts right now — is undiscoverable, since the policy points readers to a dead URL to find out.

**Prior art:** None; this is a funding/execution gap against infrastructure the corpus already specifies.

**Status:** Selected by Director, 2026-08-29 — (a): the referenced infrastructure already exists on the program side; issue #79 tracks standing it up (canonical host, OpenPGP key and fingerprint, security.txt fields). Awaiting Governing Board ratification.

#### Q-20 — Name the accountable legal entity

**Question:** What specific legal entity is accountable for the program's safe-harbor commitments and liability?

**Why it blocks work:** The program describes itself only as an informal group, and the safe-harbor language names no legal entity, while canonical references split between two different domains.

**Surfaces in:**
- `README.md:8` — "a group working within the Linux Foundation and broader open source ecosystem"
- `SECURITY.md:72–77` and `coordinated-vulnerability-disclosure-policy.md:455` (§14) — safe-harbor language naming no legal entity

**Options:**
- a) Name the Linux Foundation itself as the accountable entity
- b) Name a specific sub-entity or fund hosted by the Linux Foundation
- c) Commission a legal review to determine the right structure before naming one

**Recommendation:** Either-viable. This is a legal-structuring choice that needs counsel input the corpus itself cannot supply; no document leans toward a specific entity.

**If undecided:** A security researcher relying on the safe-harbor commitment cannot identify who is actually making that commitment to them.

**Prior art:** None.

**Status:** Selected by Director, 2026-08-29 — (a): name the Linux Foundation as the accountable entity. Awaiting Governing Board ratification.

#### Q-21 — One document-status scheme and a ratification path

**Question:** What status scheme do the corpus's documents carry, and what is the path by which a draft becomes ratified, in-force policy — who ratifies, by what procedure, recorded where?

**Why it blocks work:** Five status idioms circulate, five documents carry no status at all, and no document defines who ratifies or what "ratified" would even look like — while individual documents queue their own open items "for TOC / Board review" with no defined way for that review to conclude. Nothing in the corpus is ratified, and under the current scheme nothing could be.

**Surfaces in:**
- `coordinated-vulnerability-disclosure-policy.md:3` — "**Status:** Draft v0.4"
- `docs/Read-in Tier Policy.md:3` — "**Status:** Draft for Governing Board review"
- `docs/Embargo Handling Guidance.md:3` — "**Status:** Proposal / Draft for review"
- §3 — the status census (five idioms, five headerless files)
- `docs/what-counts-as-public-disclosure.md:273` — a document listing ratification of its own central matrix as an open item, with no path for that to happen

**Options:**
- a) Adopt one three-state scheme — Draft → TOC-ratified → Board-ratified (where policy/legal) — stamped in every document's front matter, with a one-page ratification procedure and a register of in-force versions
- b) Keep per-document statuses, but require every document to name its own approver and a review-by date
- c) Drive statuses from the standing decision register this section proposes: a document is "ratified" when the register records the ratifying selection

**Recommendation:** (a), strong. The corpus already writes dated changelogs recording real decisions (CVD v0.4, Read-in Tier Policy v0.2) — the machinery is half-built; what is missing is the named body, the state names, and the stamp. This is the one selection that makes every other ratification-shaped question in this register (Q-08, Q-17, and the register's own status idiom) executable.

**If undecided:** Every "Draft" stays draft forever, readers cannot distinguish binding policy from work in progress, and OPS-7-class failures — a fully actionable play whose authority is still listed as an open item — keep shipping.

**Prior art:** CVD v0.4 and Read-in Tier Policy v0.2 changelogs record dated, ratified-in-substance decisions; no scheme exists to mark the documents themselves as in force.

**Status:** Selected by Director, 2026-08-29 — (a), with the Governing Board as ratifying body while no TOC is constituted: a three-state scheme (Draft → Adopted by the Director → Ratified by the Governing Board) stamped in every document's front matter, one ratification procedure, and a register of in-force versions. Awaiting Governing Board ratification.

#### Q-22 — Governance for the "Security Card" before any schema ships

**Question:** Should the SIRT keep a "Security Card" — a standing record that scores projects' and, by extension, their maintainers' security conduct — and if so, under what governance: who owns it, who can read and write it, what triggers a flag, how long entries live, and what recourse the scored party has?

**Why it blocks work:** The card is live in three documents' instructions — log embargo breaks on it, feed attempt histories and "embargo/mishandling" notes into it, use it to decide who joins future cases — while no document owns it, defines its schema or retention, or gives the scored party any way to see or contest their record.

**Surfaces in:**
- `docs/upstream-engagement-guidelines.md:41–42` — "**Reputation flags:** any history of mishandling reports or breaching embargoes (record on the Security Card)"
- `docs/what-counts-as-public-disclosure.md:211–212` — "log the break on the project **Security Card** (including any upstream/partner mishandling for future risk weighting)"
- `docs/upstream-engagement-guidelines.md:175` — the full attempt history feeds "the postmortem and the Security Card"
- `docs/Akrites_SIRT_CVD_Glossary.md:132` — defined only as "A record of a project's or member's security posture and SME areas"

**Options:**
- a) Pause writes to reputation-flag fields until a Board-approved governance note ships — owner, access, flag criteria, retention, and a contest path — then resume under it
- b) Keep operational facts only (contact attempts, preferred channels, SME areas) and drop conduct scoring ("reputation flags") entirely
- c) Continue as-is, and accept the documented risk

**Recommendation:** Toward (a) or (b), strong. The engagement guidelines' own instinct — "confirm with human judgment" — already points the direction: an ungoverned behavior score on maintainers is the single likeliest trust-breaker toward the exact audience those guidelines exist to protect. §1 asks the Board for this decision before any schema ships; GAP-15 (§5.3) is the artifact half, deliberately drafted as schema-last.

**If undecided:** A maintainer discovers the SIRT keeps permanent conduct scores on them, assembled by a body they never joined, with no stated criteria or appeal — and the corpus's "we contribute, we don't impose" posture reads as unearned exactly where it matters most.

**Prior art:** None. The glossary entry describes the record; nothing governs it.

**Status:** Selected by Director, 2026-08-29 — (b): keep operational facts only (contact attempts, preferred channels, SME areas); conduct scoring ("reputation flags") is dropped entirely. Awaiting Governing Board ratification.

### Consolidation notes

This register was built against roughly two dozen register-candidate threads carried forward from the confirmed findings, the persona reviews' "questions the documents can't answer," the momentum inventory, and the corpus's own open-items lists. Disposition of each:

- **Case-runner title** → Q-01. **WG leadership title** → Q-02. **Publish-at-PD ownership** → Q-03.
- **AI-use warning at intake** and **self-disclosure verification** → merged into Q-04 — both are "how the settled AI rule meets the Finder at intake" (POL-11 is the warning half).
- **Filename convention** (HYG-1, §9.2) → Q-05 — small, but genuinely unmade, and every month it stays open adds files that will need renaming later.
- **MoLR/fork authority** → Q-06, merged with the previously-separate "Stewardship panel" thread — both trace to the same document family and read as one authority-clarity gap, not two.
- **Severity vocabulary** and the **advisory-identifier scheme** (AVID vs. OSS-SIRT ID) → merged into Q-07 — both are machine-readable-vocabulary consistency questions with the same proposed decider.
- **TLP-during-remediation matrix** → Q-08. **Extension/deviation approval authority** → Q-09.
- **Embargo clock trigger**, **lifecycle-phase taxonomy**, and the **business-vs-calendar units mix** → merged into Q-10 — the clock trigger is, on inspection, inseparable from which phase list is canonical, since the trigger is defined as the end of a named phase.
- **Read-in delegation/RACI/lead times** and the **Knowers_File.md mechanism** → merged into Q-11 — both come from the same self-declared open-items list and describe one operational gap (how read-in access actually gets granted and tracked) from two angles.
- **Premier Member gate** → kept as its own item, Q-12, rather than folded into Q-11 — it has a clean, strong, dated-contradiction recommendation that a broader RACI bundle would dilute.
- **Co-finder attribution cutoff** → Q-13.
- **Intake completeness contract** and **phased-rollout advancement criteria** → merged into Q-14 — both concern how the intake program actually admits reports, one at the report level and one at the reporter-class level.
- **Read-in Gate 3 vs. the Finder** (POL-8) → kept as its own item, Q-15, rather than folded into the Q-11 bundle — it is a yes/no policy call on one sentence, not a RACI design.
- **Escalation-split clarity** → Q-16, merged with the "recourse when the SIRT goes silent" thread (FND-9) — no distinct recourse question survives independent of the escalation map itself; the outsider's entry point is one clause of that map.
- **Break-classification/decision-matrix ratification** → Q-17, merged with the narrower "who holds accelerate/hold authority" and "is the first-report date published" threads, and with the timing-override-vs-maintainer-final tension (TON-3) — all trace to the same source document and the same unratified matrix.
- **Metrics program design** → Q-18.
- **Canonical domain/infrastructure liveness** and **PGP key** → merged into Q-19, along with the internal tool-provisioning gap (Spyglass, Watchful Eye, Open Door, Security Card/Rolodex as *tools*) — all are "named but not stood up" infrastructure, funding-level rather than design-level. Governance of what the Security Card *records* is a separate policy call: Q-22.
- **Accountable legal entity** → Q-20, merged with a separate "organizational identity" framing of the same underlying Akrites/Linux Foundation relationship question.
- **Document-status scheme / ratification path** (ROL-9, INT-5) → Q-21.
- **Security Card governance** (TON-1) → Q-22.

**Excluded — already answered in the corpus** (confirmed during the verification rounds, §10):
- Any question on regulatory-disclosure override: the Read-in Tier Policy addresses the mechanism directly.
- Any question on "which embargo number applies": the 30-day default is recorded (CVD v0.4 changelog); where it hasn't propagated is a documentation-sweep item — the fix train carries it — not an open decision.
- Any question on "is the 30-day default ratified": it is, with a dated record; asking again would re-open a closed decision.
- The entry documents' organization-name variants ("OSS-SIRT", "Akrites-SIRT"): a copy-edit already answered by the CVD policy's own naming record; the train propagates it.
- A dispute-resolution-process/deviation-notice-format item in the playbook's open-items list: a propagation gap against the CVD policy's already-recorded §15 dispute process, not a fresh decision; the escalation-map half folds into Q-16.

**Found, but excluded to keep the register to its highest-value items:**
- The AI-use disclosure policy's own open items (vocabulary-ratification cadence, per-advisory publication scope, itemization granularity) — real, but narrower documentation-maturity questions inside an otherwise well-cross-referenced, substantively settled policy.
- The upstream-engagement guidelines' own open items (a distinct Code of Conduct for upstream engagement, binaries-in-scope, a "Security Starter Kit" approval) — self-admitted and real, but derivative of decisions already captured above.
- A "SIREN" alert mechanism is named repeatedly across the playbook and disclosure procedure and defined nowhere, including the glossary. Every usage treats it as an existing, working channel rather than a proposal under debate — a documentation gap, not a live decision. Treatment: the Director defines it in a wave-2 glossary entry (OPS-1), not a register question. Defined during the selection pass, 2026-08-29: SIREN is the OpenSSF's public threat-intelligence mailing list (announced May 2024; modeled on oss-security) — a post-disclosure channel for active threat activity affecting open source at large; PR #82 adds the glossary entry.

All citations above were checked directly against the pinned snapshot (or, for the two PR citations, against the PR diffs as frozen on 2026-08-28) before inclusion.

**After the selections:** this register is a point-in-time consolidation. Once selections are recorded, the natural follow-up is promoting it to a standing `docs/decision-register.md` that outlives this audit and becomes the place future "Open items" sections point instead of accumulating privately per document. That promotion is proposed as a follow-up, not part of this PR.

## 7. Recommended sequence

In the repository's own 30/60/90 idiom. Everything here is a §4 finding action, a §5 next step, or a §6 question — this section only orders them.

**Days 0–30 — stop the drift, unblock the queue** *(Director + any available reviewer)*

1. Merge the mechanical fix train accompanying this audit: eleven single-concern PRs (embargo-default and naming propagation, contact corrections, RFC 9116 syntax, broken links, typos, index completion, filename hygiene). Each opens from a branch named for its Appendix A action label (`fix/typos`, `fix/indexes`, …) and cites this audit's tracking PR — the front-matter **Tracking** line — so all eleven are listed there as linked references. Each is reviewable in minutes; none touches a file PR #62 is rewriting.
2. Clear the four stalled artifact PRs (GAP-01–GAP-04): review PRs #7 and #8 — 51 days old, and both need the 30-day default applied before merge so the drift doesn't land twice more — post the requested review on PR #60, give PR #61 a reviewer and a real closing keyword, and review the #60/#61 pair together to break their mutual deferral.
3. Walk the decision register: record Director selections for §6.1 and proposed directions for §6.2/§6.3. Selections whose propagation is textual ship as a second PR wave.
4. Do the tracker hygiene: close or re-scope the done-but-open issues (GAP-05–GAP-07), split #36 (GAP-26), and file whichever §5.7 drafts are worth carrying — batching or discarding drafts is an expected outcome, not a failure to act on the audit.

**Days 31–60 — ratify and harmonize** *(TOC / Board deciding, Director preparing)*

5. Ratification pass over the §6.2/§6.3 questions — embargo window and extension authority, the TLP model, MoLR authority once PR #62 lands, read-in delegation — recording outcomes in the register and moving document statuses from the five current draft idioms toward a single ratified one.
6. Wave-2 propagation sweeps per selection: one role-vocabulary sweep (the case-runner title; WG Lead vs. Chair), one lifecycle-taxonomy unification (the CVD policy's harmonized model is the recorded candidate), one TLP-phrasing sweep, and one MoLR/fork-vocabulary sweep across the five documents PR #62 leaves stale (ROL-14).
7. Land the highest-leverage missing artifacts from §5.3: the read-in RACI (GAP-14) and the Knowers_File decision (GAP-16) unblock the read-in chain end to end; the severity links (GAP-13) resolve with PR #61.

**Days 61–90 — structure, so it doesn't recur** *(Director proposing, Board confirming)*

8. Review infrastructure: CODEOWNERS or an equivalent reviewer-routing norm, a second-reviewer norm for policy documents, issue and PR templates, and a CI link-and-format check so orphans and dead links cannot re-land silently. This is capacity work, not process criticism — the review queue's current shape is a one-primary-author bottleneck that structure, not effort, fixes.
9. Metrics foundations: adopt per-metric definitions (numerator, denominator, window, source event), name the case-lifecycle data store the definitions depend on, and record the public-cut approver.
10. Promote §6 to a standing `docs/decision-register.md`, and schedule the next audit against §1's scorecard as its baseline.

## 8. Appendix A — full findings register

All 76 confirmed findings: **18 Blocker · 41 Major · 14 Moderate · 3 Minor**, 18 of them finder-facing (**ff**). Five additional uncounted rows are kept for the record — three cross-references (FND-5, MET-6), one baseline (TON-0), one consistency note (INT-12), one checker annotation (HYG-6) — and one ID was retired: **POL-10** (the "undefined regulatory carve-out" candidate) was killed in cross-examination because [`Read-in Tier Policy.md`](../Read-in%20Tier%20Policy.md) lines 68 and 87 do define the mechanism; the ID is not reused.

Evidence cells use short document codes; line numbers refer to the snapshot. **SEC** `SECURITY.md` · **CVD** `coordinated-vulnerability-disclosure-policy.md` · **TIER** `docs/Read-in Tier Policy.md` · **READIN** `docs/SIRT Read-in Guidelines.md` · **EHG** `docs/Embargo Handling Guidance.md` · **UEG** `docs/upstream-engagement-guidelines.md` · **PD** `docs/what-counts-as-public-disclosure.md` · **PLAY** `docs/sirt-communications-playbook.md` · **GLOSS** `docs/Akrites_SIRT_CVD_Glossary.md` · **GUIDE** `docs/Akrites_CVD_Guide.md` · **METRICS** `docs/Akrites_SIRT_Metrics.md` · **MoLR** `docs/Maintainer_of_Last_Resort_Guidelines.md` · **WG** `docs/Akrites_WorkingGroup_Operating_Guide.md` · **ACK** `docs/acknowledgements-and-attribution.md` · **AIUSE** `docs/ai-use-disclosure.md` · **1PAGER** `docs/Akrites_ReadIn_Engineer_OnePager.md` · **NOTIF** `templates/notification-templates.md` · **ACK-T** `templates/acknowledgement-template.md` · **NOTICE** `templates/Akrites_Case_ReadIn_Notice_Template.md` · **INTAKE** `templates/vulnerability-report-intake-template.md`. Actions: **Train:** a fix-train PR accompanying this audit · **Q-…** a §6 register question · **GAP-…** a §5 row · **Deferred: PR #62** the file is being rewritten in flight · **Wave 2** ships after the register selections.

### A.1 Finder experience — 10 findings (6 Blocker, 4 Major; all ff)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| FND-1 | Blocker · ff | README offers no reporting path; `SECURITY.md` linked from nowhere | README:51, 54–56; EHG:40 | Train: fix/readme, fix/indexes | §4.1 |
| FND-2 | Blocker · ff | CVD-policy pointers HTML-commented at both entry files; every cited host unreachable | SEC:8–10, 79; `security.txt`; §9.4 | Q-19; GAP-29; train fixes the host inside the comments | §4.1 |
| FND-3 | Blocker · ff | OpenPGP key promised at the canonical URL; no key or fingerprint exists anywhere | SEC:34–35; CVD:120 | Q-19; GAP-28 | §4.1 |
| FND-4 | Blocker · ff | Phased intake rollout undisclosed at entry; active reporter class undeterminable | SEC:14–16; CVD:144 + §12 | Q-14 | §4.1 |
| FND-5 | — cross-ref | = POL-11 (AI-use embargo forfeiture invisible at entry) | — | — | §4.2 |
| FND-6 | Blocker · ff | Safe-harbor pledge names no legal entity; the SIRT is usually not the Owner | SEC:72–77; CVD:170–171 | Q-20 | §4.1 |
| FND-7 | Blocker · ff | Four contact addresses on four domains in live artifacts | §9.4; WG:37, 60; ACK-T:105 | Train: fix/wg-operating-guide, fix/acknowledgement-template, fix/advisory-template | §4.1 |
| FND-8 | Major · ff | `security.txt` wraps required fields in HTML comments, violating RFC 9116 | `security.txt` | Train: fix/security-txt | §4.1 |
| FND-9 | Major · ff | No recourse or escalation path if the SIRT goes silent on a report | SEC:53–54 (the promises with no fallback) | Q-16 | §4.1 |
| FND-10 | Major · ff | Response-time promises have no metric instrumenting them | SEC:53–54; METRICS | Q-18 | §4.1 |
| FND-11 | Major · ff | Anonymous-finder fallback contact is a legacy address | ACK-T:105 | Train: fix/acknowledgement-template | §4.1 |

### A.2 Policy coherence — 14 findings (5 Blocker, 8 Major, 1 Moderate; 5 ff)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| POL-1 | Blocker · ff | 90-day embargo default in the two most public artifacts; 30 is the recorded decision; PRs #7/#8 would propagate it | SEC:58; NOTIF:90; CVD:327, 510 | Train: fix/security-md, fix/notification-templates; GAP-01/02 review asks | §4.2 |
| POL-2a | Major · ff | `SECURITY.md` flat TLP:RED-until-disclosure vs the CVD policy's phased model | SEC:56; CVD:303–307 | Train: fix/security-md | §4.2 |
| POL-2b | Blocker | Same-day documents carry two TLP models: severity-gated (TIER) vs unconditional phases (CVD) | TIER:23, 126; CVD:303–307, 510 | Q-08 | §4.2 |
| POL-3a | Major · ff | `SECURITY.md` lifecycle omits the Deduplicate phase the CVD policy made explicit | SEC:65; CVD:510 | Train: fix/security-md | §4.2 |
| POL-3b | Major | Glossary's 3-stage pipeline vs the CVD policy's 4-stage mapping; ≥7 lifecycle framings corpus-wide | CVD:290–295; GLOSS | Q-10 | §4.2 |
| POL-4 | Major | Embargo clock starts at "a validated report" vs "validated and ownership is assigned"; the latter cites a phase no model contains | CVD:327; EHG:23 | Q-10 | §4.2 |
| POL-5 | Moderate | Extension approver: maintainer-final (TIER) vs "explicit rationale and TOC awareness" (CVD) | TIER:74; CVD:338–339 | Q-09 | §4.2 |
| POL-6 | Major | Read-in lead times: 1–30 working days vs 7–14 days vs "open" | NOTIF; READIN:100–104; TIER | Q-11 | §4.2 |
| POL-7 | Major · ff | Intake template carries both contracts: triage-every-report and a six-item completeness gate | INTAKE:13–16; CVD §4.3 + §5 | Q-14 | §4.2 |
| POL-8 | Blocker | Read-in Gate 3 wording excludes a Tier-0 Finder from their own case | READIN:15 | Q-15 | §4.2 |
| POL-9 | Major | Dispute apex: technical disputes end at the TOC, breach sanctions at the Board; the split is stated nowhere | CVD:473–483; TIER:96–100 | Q-16 | §4.2 |
| POL-11 | Blocker · ff | Public-AI use forfeits the embargo; the entry checklist dropped exactly that field | EHG:73; CVD:136–140; SEC:38–45 | Q-04 | §4.2 |
| POL-12 | Major | "Owner" — the CVD policy's central role — has no glossary entry | GLOSS (absent); CVD:51–54 | Wave 2 (glossary sweep, §7) | §4.2 |
| POL-13 | Blocker | Three clocks against one silent maintainer: 5/10/15 business days, 30 calendar days, 7-day exploited target | MoLR:46–48; EHG:23; CVD:354 | Q-10 | §4.2 |

### A.3 Roles & authority — 14 findings (2 Blocker, 10 Major, 2 Moderate)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| ROL-1 | Blocker | MoLR invocation authority answered six ways across five documents | TIER:91; EHG:122; GUIDE:126; PLAY:656, 695; GLOSS:43 | Q-06; PR #62 coordination | §4.3 |
| ROL-2 | Major | The case-runner role carries five titles, none defined | CVD:473, 477; TIER:23, 108 | Q-01 | §4.3 |
| ROL-3 | Major | "WG Lead" holds authority in TIER; the WG guide defines only a non-managing "Chair" | TIER:108; WG:45 | Q-02 | §4.3 |
| ROL-4 | Major | Read-in approver of record differs between documents | READIN:100–104; TIER:108 | Q-11 | §4.3 |
| ROL-5 | Moderate | The §7 accept/reject shorthand lacks the §6 cross-reference that resolves it | CVD:245 vs 170–183 | Wave 2 | §4.3 |
| ROL-6 | Major | Advisory publisher at disclosure (who, from which account) stated nowhere | no document (decision-rights pass, §10) | Q-03 | §4.3 |
| ROL-7 | Major | The public metrics cut has no named approver | METRICS:107 | Q-18 | §4.3 |
| ROL-8 | Major | Access-suspension actor unclear between the SIRT and the case lead | TIER:96–100 | Q-16 | §4.3 |
| ROL-9 | Major | No ratification body or procedure; nothing in the corpus is ratified | §3 census; PD:273 | Q-21 | §4.3 |
| ROL-10 | Major | "Premier Member" gates emergency read-ins; defined nowhere; tension with the equal-access principle | READIN:49; TIER:13 | Q-12 | §4.3 |
| ROL-11 | Blocker | Read-in consent points at a nonexistent `Knowers_File.md`; two competing acceptance paths | NOTICE:17, 97; READIN:102 | Q-11; GAP-16 | §4.3 |
| ROL-12 | Major | A "stewardship panel" approves MoLR steps; chartered nowhere; PR #62's own template omits it | PR #62 diff:487, 922 (as of 2026-08-28) | Q-06; GAP-27 review ask | §4.3 |
| ROL-13 | Moderate | CoC-committee ↔ SIRT access-revocation bridge missing | `Code_of_Conduct..md`; READIN | Wave 2 | §4.3 |
| ROL-14 | Major | MoLR/fork vocabulary at seven points in five documents goes stale the day PR #62 merges | GLOSS:43; UEG:162, 282; PLAY:668, 911; GUIDE:126; EHG:122 | Wave 2 sweep; GAP-27 | §4.3 |

### A.4 Operating procedures — 10 findings (2 Blocker, 6 Major, 2 Moderate)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| OPS-1 | Major | "SIREN" fires at the disclosure moment; defined nowhere, including the glossary | PLAY:35, 337; PD:133, 147, 209 | Director to define; wave-2 glossary entry (§6 consolidation notes) | §4.4 |
| OPS-2 | Moderate | Severity Guidelines/Scale links empty; naming split; promised RACI; PR #61 cannot repair them | TIER:23, 30, 58; PR #61 file list (as of 2026-08-28) | GAP-13; PR #61 review | §4.4 |
| OPS-3 | Blocker | The templates index names none of its thirteen files; ten are orphaned | `templates/readme.md`:1; §9.1 | Train: fix/indexes (7 linked; 5 named, deferred to #62) | §4.4 |
| OPS-4 | Major | Four named tools have no access path, owner, or owning document | GLOSS:127–134; PLAY:846 | GAP-32 | §4.4 |
| OPS-5 | Major | The only onboarding checklist sits inside a welcome-email template, line 856 of 923 | PLAY:838–860 | Wave 2; GAP-33 | §4.4 |
| OPS-6 | Major | Roster: one working contact; Team Lead TBD; two sections empty | README:62–73 | Train partial (link fix); GAP-20 | §4.4 |
| OPS-7 | Blocker | Play 15 is fully actionable while Appendix B lists its authority as undecided; the embargo row is also stale | PLAY:654–679, 908, 911; CVD:510 | Q-06; GAP-06 | §4.4 |
| OPS-8 | Major | Two drifted copies of the acknowledgement email | ACK-T; PLAY:831 | Wave 2 | §4.4 |
| OPS-9 | Moderate | MoLR retains "adapt org names" localization boilerplate | MoLR | Deferred: PR #62 | §4.4 |
| OPS-10 | Major | The read-in log CSV covers two of three gates; its example row gives two people one seat's title | `templates/Akrites_ReadIn_Log_CASE.csv` | Wave 2; Q-01 | §4.4 |

### A.5 Document integrity — 11 findings (1 Blocker, 6 Major, 3 Moderate, 1 Minor; 1 ff)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| INT-1 | Major | Six documents ground themselves in companion documents that do not exist | EHG:9; UEG:129; PLAY:6; §5.3 | GAP-09 through GAP-16 (drafts in §5.7) | §4.5 |
| INT-2 | Major | MoLR cites Appendices B–E that don't exist; the content sits in five unlinked templates | MoLR | Deferred: PR #62 | §4.5 |
| INT-3 | Major · ff (partial) | Nine broken or degraded links | §9.3 | Train: fix/link-corrections + per-document PRs | §4.5 |
| INT-4 | Major | Glossary drift: five defined-but-unused terms, ≈20 used-but-undefined | GLOSS | Wave 2 (glossary task) | §4.5 |
| INT-5 | Major | Five status idioms plus five headerless documents; no ratified state exists | §3 census | Q-21 | §4.5 |
| INT-6 | Blocker | The One-Pager's read-in rule states its own negation (a missing "without") | 1PAGER:8 | Train: fix/typos (flagged for close review) | §4.5 |
| INT-7 | Moderate | The AI-use filled example carries two contradictory Finder lines | AIUSE:106–107 | Train: fix/typos | §4.5 |
| INT-8 | Major | The acknowledgements controlled vocabulary is all placeholder rows | ACK:246 | Q-13 batch | §4.5 |
| INT-9 | Moderate | `LICENSE` is Apache-2.0; MoLR claims CC-BY-4.0 for "Akrites materials" | MoLR:236; `LICENSE` | Deferred: PR #62 (flag at review) | §4.5 |
| INT-10 | Moderate | "(template attached)" — nothing is attached | UEG:254 | Wave 2 | §4.5 |
| INT-11 | Minor | A "Global Board" appears in no governance document | MoLR:18 | Deferred: PR #62 removes it; confirm at merge | §4.5 |
| INT-12 | — note | Post-train, the glossary's 30-day embargo entry is consistent corpus-wide | GLOSS:38 | — | — |

### A.6 Metrics & instrumentation — 6 findings (1 Blocker, 3 Major, 2 Moderate; 1 ff)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| MET-1 | Blocker | Zero of the eleven starter metrics are implementable as written | METRICS; GUIDE:106 | GAP-30, GAP-31; Q-18 | §4.6 |
| MET-2 | Major | No case-lifecycle data store is named; the two CSVs feed nothing | METRICS; `templates/` CSVs | GAP-31 | §4.6 |
| MET-3 | Major | Milestones carry no year; "~Aug 15" lapsed silently; the Oct 15 target is unowned | METRICS | Q-18 | §4.6 |
| MET-4 | Moderate | "Tooling already supports this" asserted without evidence | METRICS | Q-18 | §4.6 |
| MET-5 | Moderate | No process document points at the metrics doc | GUIDE:106 | Wave 2 | §4.6 |
| MET-6 | — cross-ref | = ROL-7 (public-cut approver) | — | — | §4.3 |
| MET-7 | Major · ff | Severity vocabulary about to fork: "High" vs PR #61's "Important" at the same CVSS band | TIER:30, 58; PR #61 diff:104–119 (as of 2026-08-28); METRICS:106 | Q-07; PR #61 review condition | §4.6 |

### A.7 Upstream-facing tone — 5 findings (1 Blocker, 3 Major, 1 Moderate)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| TON-0 | — baseline | The upstream stance is strong and respectful; the rows below deviate from the corpus's own standard | UEG:20; MoLR:95; PLAY:668 | — | §4.7 |
| TON-1 | Blocker | The "Security Card" behavior-scores maintainers with no owner, schema, retention rule, or appeal | PD:211; UEG:30, 175; GLOSS:132 | Q-22; GAP-15 | §4.7 |
| TON-2 | Major | "Price of admission" reads as gatekeeping without its glossary softener | CVD:421; PLAY:831; GLOSS:50 | Wave 2 (rides the Q-22 batch) | §4.7 |
| TON-3 | Major | Unconditional "we don't impose timelines" vs a scoped timing override, never cross-referenced | UEG:20, 74; PD:218–219 | Q-17 | §4.7 |
| TON-4 | Major | MoLR "handover / handing back" implies custody a maintainer never granted | MoLR; PR #62 review thread | Deferred: PR #62 review | §4.7 |
| TON-5 | Moderate | The co-finder attribution cutoff is undefined; two documents flag it open | ACK:187, 259; PLAY:909 | Q-13; GAP-08 | §4.7 |

### A.8 Conventions & hygiene — 6 findings (1 Major, 3 Moderate, 2 Minor; 1 ff)

| ID | Severity | Finding | Evidence | Action | Discussed |
|---|---|---|---|---|---|
| HYG-1 | Moderate | Five filename conventions across 39 files; the convention choice is unowned | §9.2 | Q-05; train renames the two worst anomalies | §4.8 |
| HYG-2 | Major · ff | `Code_of_Conduct..md`'s double dot defeats GitHub's community-health detection | §9.2; PLAY:853 | Train: fix/filenames | §4.8 |
| HYG-3 | Minor | The presentations index names neither PDF it fronts | §9.1 | Annotated in §9.1 | §4.8 |
| HYG-4 | Minor | Stray `}` in the playbook welcome email | PLAY:853 | Train: fix/filenames (disclosed) | §4.8 |
| HYG-5 | Moderate | Four trailing-space filenames plus an `&` | §9.2 | Deferred: PR #62 (§9.2 tracks) | §4.8 |
| HYG-6 | — annotation | `CONTRIBUTING-glossary.md`:31 is quoted syntax, not a broken link (checker false positive) | §9.3 note | — | — |
| HYG-7 | Moderate | The spelling banner sits in exactly seven documents; both entry documents carried variant names instead | §3; README:1; SEC:3 | Train (the two names); Wave 2 (banner placement) | §4.8 |

## 9. Appendix B — mechanical inventories

Raw inventories backing Appendix A citations. Generated by scripts at snapshot `ca62393`; link targets checked 2026-08-28 (US Eastern).

### 9.1 Orphaned files

Files no markdown link in the repository points at (README exempt as the entry point). Nineteen of 39 tracked files are unreachable by link-following:

| File | Remediation |
|---|---|
| `SECURITY.md` | README link added — audit PR train |
| `security.txt` | — (machine-readable; consumed at its well-known path, not via links) |
| `LICENSE` | — (surfaced natively by GitHub) |
| `docs/readme.md` | README now points at it — audit PR train |
| `docs/Akrites_ReadIn_Flow.svg` | Indexed in `docs/readme.md` — audit PR train |
| `docs/presentations/readme.md` (and both PDFs) | Folder indexed from `docs/readme.md` — audit PR train; the folder's own one-line index still names neither PDF |
| `templates/readme.md` | README now points at it — audit PR train |
| `templates/acknowledgement-template.md` | Indexed in `templates/readme.md` — audit PR train |
| `templates/advisory.osv.json` | Indexed in `templates/readme.md` — audit PR train |
| `templates/Akrites_Case_ReadIn_Notice_Template.md` | Indexed in `templates/readme.md` — audit PR train |
| `templates/Akrites_ReadIn_Log_CASE.csv` | Indexed in `templates/readme.md` — audit PR train |
| `templates/Akrites_WG_Membership_Register.csv` | Indexed in `templates/readme.md` — audit PR train |
| `templates/Contact_attempt_log.md` | Deferred — file is rewritten by in-flight PR #62 |
| `templates/MoLR decision record .md` | Deferred — PR #62 |
| `templates/Maintainer non-fix record .md` | Deferred — PR #62 |
| `templates/Project status notice .md` | Deferred — PR #62 |
| `templates/Steward vetting & approval record .md` | Deferred — PR #62 |

### 9.2 Filename anomalies and naming conventions

Anomalies:

| File | Anomaly | Remediation |
|---|---|---|
| `Code_of_Conduct..md` | Double dot before extension; defeats GitHub's community-health Code-of-Conduct detection | Renamed — audit PR train |
| `docs/presentations/…the AI Vulnerability Era.pptx (1).pdf` | Browser download artifact (`.pptx (1).pdf`) in the name | Renamed — audit PR train |
| `templates/MoLR decision record .md` | Trailing space before `.md` | Deferred — PR #62 touches these files |
| `templates/Maintainer non-fix record .md` | Trailing space | Deferred — PR #62 |
| `templates/Project status notice .md` | Trailing space | Deferred — PR #62 |
| `templates/Steward vetting & approval record .md` | Trailing space, plus `&` in a filename | Deferred — PR #62 |

Convention census: the 39 filenames follow at least five conventions — `snake_Case_With_Caps` (11), `kebab-case` (9), `Words with spaces.md` (7), trailing-space-before-extension (4), plus the two anomalies above and an uppercase/lowercase `README`/`readme` split. A single convention choice is register item Q-05.

### 9.3 Broken and degraded links

| Location | Link | Problem | Remediation |
|---|---|---|---|
| `README.md:66` | `[Francis](u269c)` | Relative link to a bare username — 404s | Fixed — audit PR train |
| `SECURITY.md:33` | `[SIRT@Akrites.dev](sirt@akrites.dev)` | Missing `mailto:` — renders as a dead relative link | Fixed — audit PR train |
| `templates/notification-templates.md:4` | `./coordinated-…policy.md` | Policy lives at repo root; `./` from `templates/` 404s | Fixed — audit PR train |
| `templates/acknowledgement-template.md:10` | `github.com/ossf/SIRT/…` | Wrong organization (pre-migration home) | Fixed — audit PR train |
| `templates/acknowledgement-template.md:11` | `docs/intake-runbook.md` | Target does not exist on `main` (it is the file PR #8 proposes) | Fixed (retargeted) — audit PR train |
| `docs/Akrites_WorkingGroup_Operating_Guide.md:24` | `[URL: Read In Policy]` | Literal placeholder, never filled | Fixed — audit PR train |
| `templates/Akrites_Case_ReadIn_Notice_Template.md:5` | header link | Labeled as the read-in process; points at the engineer One-Pager | Fixed — audit PR train |
| `docs/Read-in Tier Policy.md:23` | `[Akrites SIRT Severity Guidelines]()` | Empty target — the severity document does not exist yet (PR #61 proposes it) | Register / in-flight PR #61 |
| `docs/Read-in Tier Policy.md:58` | `[Akrites SIRT Severity Scale]()` | Empty target — same missing document | Register / in-flight PR #61 |

Checker note: `docs/CONTRIBUTING-glossary.md:31` contains `[short-label](url)` and is flagged BROKEN by naive link checkers — it is quoted convention syntax inside an instruction, not a real link. No fix needed; recorded here so the next audit's tooling expects it.

### 9.4 Hosts, contacts, and liveness

Policy-URL hosts referenced across the corpus: `sirt.akrites.dev` (canonical per the CVD policy, line 6), `sirt.linuxfoundation.org` (9 references), `oss-sirt.linuxfoundation.org` (5), plus GitHub. Contact addresses: `SIRT@Akrites.dev` (canonical, 13 references), `sirt@akrites.org` (wrong TLD, 3), `security@oss-sirt.linuxfoundation.org` (legacy, 2), `conduct@akrites.org` (Code of Conduct contact, 2).

Liveness probe (2026-08-28, US Eastern): `sirt.akrites.dev`, `akrites.dev`, `sirt.linuxfoundation.org`, and `oss-sirt.linuxfoundation.org` all returned no response — none of the policy URLs the documents cite is currently reachable, including the canonical one. See register item Q-19.

## 10. Method, scope, and AI use

**Snapshot.** All findings cite repository state at commit `ca62393` (2026-08-28). Open issues and PRs were frozen the same day and are cited with as-of dates; anything merged later is out of scope. Two sourcing exceptions are labeled where they occur: GitHub Discussions (#40, #45 in §5.4) were read live on the snapshot date rather than frozen to disk, and where §5 quotes the text of an open PR (#7, #8, #60, #61 — drafts not yet on `main`), the quote was verified against that PR's frozen diff. Presentation PDFs were inventoried but not content-audited.

**Method.** Three grounding passes over the full corpus; seven persona reviews run independently against the raw documents (Governing Board member, SIRT Director, SIRT operator on two tabletop scenarios, SIRT SRE implementing the metrics, upstream maintainer reading only maintainer-facing material, external Finder starting from `security.txt`, and a new hire crawling only by links); four adversarial cross-examinations of those reviews plus a bidirectional momentum analysis of issues and PRs; mechanical scans (link graph, orphan detection, filename census, contact and URL census, RFC 9116 lint, host liveness probes); and synthesis with deduplication. Every quoted line in this audit was re-verified verbatim against the snapshot by script; severity reflects the highest confirmed assessment, and cross-examination could lower but never raise it.

**People rules applied throughout:** findings attach to artifacts, never to authors; review throughput is described as latency, not neglect; contributor concentration is stated as fact with a structural remedy, not a criticism; names appear only in §11, only in credit context.

**AI use** (per this repository's own [`ai-use-disclosure.md`](../ai-use-disclosure.md)):
  - Author: AI-assisted (documentation audit, drafting, and mechanical fixes; multiple coordinated AI agents), under human direction and review.
  - Accountability: SIRT Director (u269c)

**Limitations.** A one-day snapshot of a fast-moving corpus; PR #62 alone will invalidate several citations when it merges (those are marked in-flight rather than reported as defects). Private operational spaces exist and were deliberately neither examined nor cited; where a public document hands off to them, the audit says only that. Link checks reflect GitHub's rendered view; anchor-fragment behavior was spot-checked, not exhaustively verified. Tone findings are one careful reading, not a survey of actual maintainer sentiment.

## 11. Acknowledgements

This corpus is the product of a deliberate drafting sprint — roughly 42,000 words of policy brought from nothing to reviewable drafts in under three months, the large majority of it authored by CRob (SecurityCRob), whose velocity is the reason there is something substantive to audit at all. The consolidation debt this audit catalogs is the *expected* product of that phase, and several documents were diligent enough to record their own open questions — §6 consolidates the lists the authors themselves left as breadcrumbs.

Outside contributions sharpened the corpus at exactly the points this audit examines: the MoLR v0.2 rewrite and its review thread (scovetta, gkunz, and reviewers), the intake-documentation PRs and the service-level questions raised on them (kergon), and the prioritization and severity proposals awaiting review. The upstream foundations — FIRST's multi-party CVD guidelines, the CERT CVD guide, the OpenSSF vulnerability-disclosure guides — show through the corpus and are cited by it.

Corrections to this audit are welcome as issues or PRs against `docs/audits/`.
