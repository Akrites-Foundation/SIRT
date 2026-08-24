# Akrites SIRT — Upstream Engagement Guidelines

**Owner:** Akrites SIRT
**Status:** Draft for TOC / Board review
**Audience:** SIRT coordinators and WG engineers who engage upstream projects
**Companion docs:** `sirt-communications-playbook.md` (Plays 9, 10, 15, 17), `acknowledgements-and-attribution.md`, `Embargo Handling Guidance.md`, steward-engagement taxonomy

> Spelling standard: **Akrites** (Akrites Foundation, Akrites SIRT). "OSS-SIRT" is a synonym.

## Purpose

How the SIRT approaches, works with, and — win or lose — *leaves behind* value for the open source
projects we disclose to. The goal is not just to land a fix; it's to strengthen the project's
security practices so the next issue is easier for everyone. Three sections:

1. **Best practices** for approaching and working with (responsive) maintainers.
2. **Tactics** for when a project is unresponsive.
3. **Leave-behind resources** — tools, training, and templates to hand maintainers.

Guiding stance throughout: **we contribute, we don't impose.** The maintainer keeps final authority
over their project, their fix, and their timing. We meet each community where it is.

---

## Section 1 — Best practices for engaging upstream maintainers

### 1.1 Do your homework before you knock (recon)

Before first contact, build a picture of the project's security posture and the right way in.
Automate this where possible (it feeds the "Security Card") but confirm with human judgment:

- **Reporting channel:** Is Private Vulnerability Reporting (PVR) enabled? Is there a
  `SECURITY.md`, a `security.txt`, or a `SECURITY-INSIGHTS.yml`? Run OpenSSF **Disclosure Check**
  to automate the hunt for the right disclosure path.
- **Who's in charge:** `OWNERS`/`CODEOWNERS`, `Stewards.md`, `Projects.md`, LFX maintainer
  listings, and member-sourced contacts. Solicit members for people who already know the project.
- **How they work:** license, whether a CLA is required (`CONTRIBUTING.md`), commit signing/sign-off
  expectations, test suite, local build steps, and code style.
- **Project state:** are issues and security fixes being actively addressed? (This distinguishes a
  slow-but-alive project from an unmaintained one — see Section 2.)
- **Reputation flags:** any history of mishandling reports or breaching embargoes (record on the
  Security Card).

### 1.2 First impressions are everything

- **A human makes first contact, not a bot.** Bias toward one consistent human coordinating each
  relationship to reduce lead time. Automation, if any, comes *after* a relationship exists.
- **Make Akrites verifiable.** Impersonation is a real risk (a maintainer once flagged a peer
  SIRT's GitHub account as bogus). List the official Akrites GitHub handle and contacts on the
  website and in `security.txt`; sign outreach with S/MIME or GPG; offer a verification link.
- **Maintainer-to-maintainer tone.** Humble, appreciative, concise. Acknowledge their time is
  scarce and that we're here to help, not to add burden or take over.
- **Lead with a Code of Conduct for engagement.** Share the Akrites upstream-engagement CoC
  (distinct from the Foundation's general CoC) so maintainers know exactly what to expect from us.

### 1.3 Deliver an excellent report

Quality of the packet directly sets the pace. Model the report on what maintainers actually want:

- **Fewest words that fully convey the issue.** "Here is a unit test that fails; here is a patch
  that makes it pass" is often the ideal shape.
- **A regression-test-style PoC** is widely preferred over a weaponized exploit. Default to IOCs,
  not exploitation aids.
- **Include:** clear software description, specific finding, potential impact, reproducer, a
  proposed patch, and a validating unit test. (Mirror the intake data elements.)
- **Fit their house style.** Patches that match the project's conventions get merged faster;
  collect style/build info during recon so fixes land cleanly.
- Reference Daniel Stenberg's guidance on excellent vulnerability reports as a shared standard.

### 1.4 Frame fixes as offers, not mandates

- Label contributions as an **"initial/proposed patch"** and explicitly invite the maintainer to
  refine or replace it.
- We do **not** impose timelines. The embargo/PD window is a guideline we negotiate (default 30
  days from owner confirmation), and we defer to upstream where they have their own process.
- Confirm the fix with the maintainer where possible rather than assuming; respect their final call
  on the fix and the disclosure date.

### 1.5 Handle AI-content sensitivities head-on

Some projects distrust or refuse AI-generated reports/patches, and high-volume AI output without
humans in the loop carries real credibility risk.

- **Keep a human in the loop and say so.** Attribute AI assistance by capability only; model +
  harness internals stay internal (see attribution doc).
- Respect **no-AI-content** policies. Have a short FAQ/Q&A ready for maintainers who are wary, and
  never bury a project in automated reports.
- Prioritize **Critical/Important** findings for first engagement to establish a positive track
  record before bringing lower-severity volume.

### 1.6 Prolific maintainers and special cases

- Maintainers who steward 1,000+ projects (e.g., kernel, curl, and other high-volume maintainers)
  need a tailored, low-friction path — coordinate batching and cadence with them directly rather
  than firing individual reports.
- Where a project has its **own mature CVD/CNA process**, defer to it; we add our perspective (and
  can record a deviation notice) without trying to take over.

### 1.7 Escalate needs, not just findings

If a project needs more than a fix — new maintainers, tooling, funding, governance help — route
that need to the group, foundation, or registry scoped to provide it (and flag candidates for the
OpenSSF Vanguard-style "deploy best practices" effort). Build the relationship, then keep it warm
with periodic, respectful check-ins.

---

## Section 2 — When the project is unresponsive

Silence is not one problem; it's several. Diagnose before you escalate, and keep every step
human-first and transparent about *why* we want to help.

### 2.1 First, are we even talking to the right person?

Before treating silence as unresponsiveness, re-check the contact path: PVR, `security.txt`,
`SECURITY.md`, `OWNERS`/`CODEOWNERS`, `Stewards.md`, LFX listings, and member contacts. Try a
second, verified channel. Confirm our outreach looks legitimate (signed, verifiable) — a maintainer
may be ignoring what looks like spam.

### 2.2 Classify the situation

| Category | What it looks like | Signals to check |
| --- | --- | --- |
| **Unmaintained** | Nothing is being touched at all | No commits/releases; issues untouched; no security fixes anywhere |
| **Unresponsive** | Silent to us, but active elsewhere | Other issues/PRs handled; security fixes landing; active in other channels |
| **Overwhelmed** | Afloat but nothing is a priority | Sporadic activity, backlog growth, solo maintainer signals |
| **Mature/Stable (false-dead)** | Slow by design; "nothing is broken" | Responds eventually; not accepting features; low but real activity |

Use LFX's continuous project-state validation and the steward-engagement taxonomy to make this call
consistently rather than by gut feel. Number of open issues alone is **not** a verdict.

### 2.3 The escalation ladder (timers, not tantrums)

Move deliberately, documenting each attempt. Timers are guidelines negotiated per case, not hard
automation:

1. **Polite re-contact** on the verified channel, restating that we've done the analysis and drafted
   a fix, and offering help (testing, resources, PVR enablement). Reference Play 10.
2. **Alternate channel / delegate.** Try a second contact or ask a member who knows the project to
   make a warm introduction.
3. **Offer to reduce their burden.** Label our work "initial/proposed patch," offer to help with
   testing, or connect them to scoped support (foundation/registry/steward candidates).
4. **State the fallback plainly.** If we still hear nothing by an agreed date, our process considers
   next steps to protect users — say so honestly and give them the chance to respond first.
5. **Publish to protect consumers** (see 2.4), only after documented failed attempts and the right
   approvals.

### 2.4 Getting a fix to users when upstream won't act

Order of preference (least intervention first — takeovers/forks demand real care):

1. **Maintainer fixes** based on our disclosure package. *(Always the goal.)*
2. **Akrites publishes a patch file / mitigation** so consumers can protect themselves, framed as an
   initial/proposed fix and inviting the maintainer back in at any time.
3. **WG steward/fork** — a time-bounded hardened fork, with **TOC/Board approval**, as a last
   resort.

Mechanics and cautions:

- If the repo is **active but unresponsive**, a public PR with the fix lets consumers benefit and
  invites the maintainer to merge.
- If the repo is **archived**, you can't PR — a public fork is required, which risks *looking* like
  we've adopted maintenance (feature requests, expectations). Treat forking as a deliberate group
  decision, not a reflex.
- **Stay out of binaries/builds** unless the group establishes trusted build infrastructure; default
  to source patches and mitigations. Don't create walled gardens.
- Align emergency-release handling with community norms (e.g., the Maven Central "care" / emergency
  release policy) rather than inventing our own where a standard exists.
- If a patch time exceeds the window, **share mitigations/workarounds** rather than slipping silently.

### 2.5 Always leave the door open

Every unresponsive-path action is framed as consumer protection, *not* a takeover. Explicitly invite
the maintainer to adopt, refine, or replace our work, and to reclaim their project at any time. Log
the full attempt history for the postmortem and the Security Card (including any embargo/mishandling
behavior for future reference).

---

## Section 3 — Leave-behind resources to strengthen the project

The disclosure is a moment of contact; the goal is to leave the project more secure than we found
it. Offer these as a menu, not a checklist to impose — pick what fits the project's maturity and
appetite. Links verified August 2026.

### 3.1 Make the project easy (and safe) to report to

- **Private Vulnerability Reporting (PVR)** — one-click private reporting on GitHub. Politely
  suggest enabling it. Docs: https://docs.github.com/en/code-security/how-tos/report-and-fix-vulnerabilities/report-privately
- **security.txt** — a standard `/.well-known/security.txt` so finders know where to send reports.
  Generator and spec: https://securitytxt.org/
- **SECURITY.md** — a clear security policy. Ready-made templates in the OpenSSF OSS Vulnerability
  Guide: https://github.com/ossf/oss-vulnerability-guide
- **SECURITY-INSIGHTS.yml** — machine-readable security metadata (contacts, policies, practices).
  Spec: https://github.com/ossf/security-insights-spec
- **OpenSSF Disclosure Check** — tool that discovers a project's disclosure mechanism; useful to
  hand maintainers so they can see (and fix) how discoverable their reporting path is:
  https://github.com/ossf/disclosure-check

### 3.2 Coordinated disclosure know-how

- **OpenSSF OSS Vulnerability Guide** — CVD guidance plus templates for security policies and
  disclosure notifications: https://github.com/ossf/oss-vulnerability-guide
- **OpenSSF Researcher Vulnerability Guide** — the reporter-side companion, useful context to share:
  https://github.com/ossf/oss-researcher-vulnerability-guide
- **OpenSSF Vulnerability Disclosures Working Group** — home for maturing CVD practice; a path to
  escalate project needs: https://github.com/ossf/wg-vulnerability-disclosures
- **"Do excellent vulnerability reports" (Daniel Stenberg / curl)** — a concise, maintainer-endorsed
  standard for what a good report looks like:
  https://daniel.haxx.se/blog/2026/06/29/do-excellent-vulnerability-reports/

### 3.3 Training (free, self-paced)

- **Developing Secure Software (LFD121)** — free OpenSSF/LF course, ~14–18 hrs, free certificate:
  https://training.linuxfoundation.org/training/developing-secure-software-lfd121/
- **OpenSSF training catalog:** https://openssf.org/training/courses/
- **OpenSSF Concise Guides & Best Practices WG** — short, practical guides for developers and
  maintainers: https://best.openssf.org/
- **Secure Software Development Fundamentals (course content, open):**
  https://github.com/ossf/secure-sw-dev-fundamentals

### 3.4 Measure and improve posture

- **OpenSSF Scorecard** — automated security-health checks with an actionable report:
  https://openssf.org/projects/scorecard/
- **OpenSSF Best Practices Badge** — passing/silver/gold criteria projects can work toward:
  https://www.bestpractices.dev/

### 3.5 Supply-chain hardening (for projects ready to go further)

- **SLSA** — graduated build-provenance levels (start at L1, target L3 for critical builds):
  https://slsa.dev/
- **Sigstore** (Cosign/Fulcio/Rekor) — keyless artifact and commit signing:
  https://www.sigstore.dev/
- Encourage commit signing / sign-off and SHA-pinned dependencies as low-cost first steps.

### 3.6 Testing & threat-modeling aids the SIRT can provide directly

- A **regression-test-style reproducer** delivered with the report (doubles as a permanent guard).
- Help fitting the **patch to the project's code style** and build.
- A **threat model** generated from the Akrites toolchain to help the project reason about risk
  (used internally to score findings; shareable as a leave-behind).
- A **CVSS vector** (not just a score) so the project can reason about severity in their context.

### 3.7 Akrites "Security Starter Kit" — suggested leave-behind bundle

A one-page handoff the coordinator can tailor per project. Suggested contents:

```
Akrites Security Starter Kit — {project}

Quick wins (this week):
[ ] Enable GitHub Private Vulnerability Reporting
[ ] Add a SECURITY.md (template attached)
[ ] Publish a security.txt

Next steps (this month):
[ ] Add SECURITY-INSIGHTS.yml
[ ] Run OpenSSF Scorecard and review the report
[ ] Adopt commit signing / sign-off

Grow over time:
[ ] Work toward an OpenSSF Best Practices Badge
[ ] Add build provenance (SLSA) and artifact signing (Sigstore)
[ ] Take LFD121 (free)

Who to call:
- Akrites SIRT coordinator: {name / verified contact}
- Escalation for maintainer needs (new maintainers, tooling, funding): {path}
```

---

## Appendix — cross-references & open items

**Companion plays:** upstream first-contact (Play 9), unresponsive/overwhelmed (Play 10),
MoLR/fork publication (Play 15), rejected patch (Play 17) — all in `sirt-communications-playbook.md`.

**Open items for TOC / Board:**

- Ratify the **Akrites upstream-engagement Code of Conduct** referenced in 1.2.
- Confirm **MoLR/fork authority and triggers** (Section 2.4) and the archived-project fork policy.
- Decide whether Akrites ever provides **binaries** or source/patches only (Section 2.4).
- Confirm the **default embargo window** and extension principle referenced in 1.4.
- Approve the **Security Starter Kit** contents and maintain the resource list as links evolve.

