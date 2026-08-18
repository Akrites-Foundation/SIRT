# Akrites SIRT Communications Playbook

**Owner:** Akrites SIRT
**Status:** Draft for TOC / Board review
**Audience:** SIRT staff and coordinators; referenced by WGs and read-in participants
**Companion docs:** `acknowledgements-and-attribution.md`, `Embargo Handling Guidance.md`, OSS-SIRT Process (High Level), OSS-SIRT MVSR

> Spelling standard: **Akrites** (Akrites Foundation, Akrites SIRT). "OSS-SIRT" is a synonym.
> Every outbound message is written as if it may be read back publicly, quoted by a maintainer, or produced in a postmortem; with or without context.

---

## How to use this playbook

Part I sets the standards that apply to *every* Akrites communication. Part II gives
situation-specific templates. Templates use `{curly braces}` for fill-in fields and
`{optional | choices}` for pick-one phrasing. Always apply the Part I standards on top of any
template — the template is the skeleton, the principles are the muscle.

Each Part II play lists: **When to use**, **Audience**, **Channel & TLP**, **Template**, and
**Notes**.

---

# Part I — Communications Excellence Guidelines

## 1. Audience map

| Audience | Who | Default posture | Primary channels |
| --- | --- | --- | --- |
| **Members** | Akrites member orgs, WG participants | Trusted, need-to-know; least privilege | Member Slack, member mailing list, dashboard/API |
| **External security SMEs** | Read-in experts not on staff | Time-boxed, scoped to the case; spun down after | Case channel, case repo |
| **Upstream maintainers / developers** | Project owners receiving a report | Humble, human-to-human, "maintainer keeps authority" | PVR, security.txt contact, direct email (signed) |
| **Coordinators / clearinghouses** | CISA, ENISA, FIRST, national CERTs, trusted vendor programs | Peer coordinator; balanced, no single-government favoritism | Established coordinator channels, signed email |
| **General public** | Downstream consumers, press, ecosystem | Clear, accurate, machine-readable, no exploitation aid | Akrites website, GHSA/OSV, VEX feed, SIREN |

## 2. Core principles

1. **Confidentiality first and foremost.** Default to TLP:RED at intake. Share up a tier only
   with a reason and, where required, approval.
2. **Least privilege.** People are read into only what they need, for as long as they need it,
   then spun down.
3. **Human-to-human first.** Initial upstream and coordinator outreach is from a person, not an
   automated system, except where the project declares a preference for automation. Bias toward the same human coordinating a given relationship to reduce lead
   time. Move to automation only after a relationship is established.
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
| **TLP:RED** | Named individuals only. Case intake and pre-validation live here. No forwarding. |
| **TLP:AMBER** | Share within a specific trusted org, need-to-know. |
| **TLP:AMBER+STRICT** | Held case material (e.g., remediation in progress); do not share outside the case team. |
| **TLP:GREEN** | Community/peer sharing within the ecosystem, not public. |
| **TLP:CLEAR** | Public — only at/after PD. |

Every message carries an explicit TLP marking in its header or first line. When in doubt, mark
higher and ask. If message contains mixed levels, overall marking bears the most restrictive.

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
| Member awareness (no specifics) | Member mailing list / member Slack | AMBER / GREEN |
| Read-in SME coordination | Case channel (time-boxed) | RED / AMBER+STRICT |
| Upstream engagement | PVR / signed email / security.txt contact | RED → AMBER |
| Coordinator engagement | Established coordinator channel, signed email | AMBER |
| Public advisory | Website, GHSA, OSV→CVE/EUVD, VEX feed, SIREN | CLEAR |

**Hard rules:** no files or exploit code on Slack; no WG TLP:RED work conducted in general Slack;
encrypted file share only; no pre-disclosure to any single government.

---

# Part II — Situational Playbooks

## Incident lifecycle stages (reference)

Status plays below map to these stages:

`Received → Triaged/Deduplicated → Validated → Read-in/Tiering → Patch in development →
Maintainer engaged → Fix ready & date set → Public Disclosure → Postmortem`

---

## Play 1a — Intake acknowledgement: complete report

**When to use:** A report arrives with all required elements.
**Audience:** Finder.
**Channel & TLP:** Reply on the intake channel; TLP:RED.

Required elements (from "Let's Start Tomorrow" intake list): clear description of the software;
specifics of the finding; potential impact; PoC/PoV; proposed patch; unit test validating the fix;
tools & techniques used.

**Template**

```
Subject: [Akrites SIRT] Report received — {tracking-id} (TLP:RED)

Hi {Finder},

Thank you — we've received your report on {component/project} and it's now tracked as
{tracking-id}. Your submission included everything we need to move quickly: description,
impact, PoC, a proposed patch, and a validating test.

What happens next:
1. Deduplication and validation against work already in flight.
2. Routing to the appropriate working group / SME as needed.
3. We'll confirm the coordination path and expected next update by {date}.

Two quick questions so we handle this the way you want:
- How would you like to be acknowledged at disclosure? (see Play 7)
- Any customer/constraint-driven timing needs we should know about now?

We'll hold everything TLP:RED until we agree otherwise. You can reach the case team at
{case-contact}.

— Akrites SIRT
```

**Notes:** Kick off the SLA acknowledgement clock here. Do not confirm it *is* a valid
vulnerability yet — say validation is underway.

---

## Play 1b — Intake acknowledgement: report needs more data

**When to use:** A report is missing required elements or is unclear.
**Audience:** Finder.
**Channel & TLP:** Reply on intake channel; TLP:RED.

**Template**

```
Subject: [Akrites SIRT] Report received — need a few details — {tracking-id} (TLP:RED)

Hi {Finder},

Thanks for this — it's tracked as {tracking-id}. To validate and route it efficiently, could
you add the following? The more complete the packet, the faster we can help:

- [ ] {e.g., affected versions tested / confirmed}
- [ ] {e.g., PoC or a failing unit test that demonstrates the issue}
- [ ] {e.g., proposed patch or mitigation, if you have one}
- [ ] {e.g., tools & techniques used, including any AI assistance}
- [ ] {e.g., purl / exact package identifier}

If it's easier, here's our reporting guide: {link}. No rush to be perfect — send what you have
and we'll iterate. We'll pause the clock on our side until we hear back, and hold everything
TLP:RED.

— Akrites SIRT
```

**Notes:** Frame missing items as "help us help you," never as gatekeeping. Point to the report
best-practices guide. If AI assistance is indicated, remind that specific model/harness details
stay internal.

---

## Play 2 — Lifecycle status updates to stakeholders

**When to use:** At each stage transition, or on a regular cadence for long-running cases.
**Audience:** Varies by stage (see table). Tailor detail to the audience's need-to-know.
**Channel & TLP:** Case channel / dashboard for read-in parties; member list (high-level) for
members; TLP scales down only at PD.

| Stage | Finder | Read-in WG/SME | Maintainer | Members (high-level) | Coordinators |
| --- | --- | --- | --- | --- | --- |
| Triaged/Deduped | ✔ status + dup note | ✔ | — | — | — |
| Validated | ✔ | ✔ | (engaged next) | — | if they reported |
| Patch in dev | ✔ | ✔ | ✔ (proposed patch) | — | — |
| Fix ready & date set | ✔ | ✔ | ✔ | ✔ (heads-up, no specifics) | ✔ |
| Public Disclosure | ✔ | ✔ | ✔ | ✔ | ✔ |
| Postmortem | ✔ (optional) | ✔ | optional | aggregate only | optional |

**Generic status template (adapt per audience)**

```
Subject: [Akrites SIRT] {tracking-id} status — {stage} ({TLP:__})

Case: {tracking-id} — {component}
Current stage: {stage}
Since last update: {what changed}
Blocking / needed: {none | what we're waiting on}
Next milestone: {what} by {date}
Your action: {none | specific ask}

Questions to {case-contact}.
— Akrites SIRT
```

**Notes:** Give status honestly, including "no change, still waiting on {X}." For members, use the
high-level variant in Play 4 — never leak case specifics into member-wide updates before PD.
A per-member dashboard/API view is preferred over broadcast for read-in parties who want to match
against their own tracking.

---

## Play 3 — Status updates to read-in Finders

**When to use:** Keeping a Finder who is read into the case informed through the lifecycle.
**Audience:** The Finder (and co-finders individually).
**Channel & TLP:** Case channel; TLP:RED / AMBER+STRICT.

**Template**

```
Subject: [Akrites SIRT] {tracking-id} — update for you ({TLP:__})

Hi {Finder},

Where things stand on {tracking-id} ({component}):
- Validation: {done / in progress}
- Fix: {alpha patch available for your review | in development | finalized}
- Upstream: {not yet engaged | engaged {date} | maintainer reviewing}
- Disclosure: {target date TBD | proposed {date}, pending maintainer}

For your review/test: {link to case repo, if a patch is ready}
Decisions we need from you: {read-in list input | embargo preference | PD date preference |
acknowledgement preference}

You'll hear from us at the next milestone or by {date}, whichever comes first.
— Akrites SIRT
```

**Notes:** Finders help determine read-in list, embargo, tiering, and desired PD date — surface
those decisions explicitly. Offer the alpha patch for review/test when available. Respect that the
maintainer sets the final PD and fix.

---

## Play 4 — High-level member notice (pre-PD, no specifics)

**When to use:** Giving members situational awareness before PD without disclosing the vuln.
**Audience:** Members (broad) or a WG.
**Channel & TLP:** Member mailing list / member Slack; TLP:AMBER or GREEN.

**Template**

```
Subject: [Akrites SIRT] Heads-up: coordinated case in progress ({TLP:AMBER})

Members,

We are coordinating a security issue affecting {broad category — e.g., "a widely used
serialization library" / "a component in the {ecosystem} space"}. We are not sharing specifics
prior to public disclosure.

What we can say now:
- Severity band: {e.g., High} (subject to change)
- General area: {category, not the component}
- Status: fix {in development | staged}; coordinated disclosure targeted around {timeframe, not
  exact date}.
- Action for you today: {none required | ensure your security contact is current | watch for the
  member notice at PD}.

If you believe you have unique exposure or can assist (SME/tiered role) and need to be read in,
contact {case-contact} — read-in is need-to-know and requires validation.

— Akrites SIRT
```

**Notes:** No component name, version, PoC, or patch details. Give a severity *band* and *category*
only. This is the correct place to invite self-identification for read-in without revealing the
target. Members receive a special notice again at PD (Play 5 companion).

---

## Play 5 — Public disclosure announcement

**When to use:** The issue goes fully public (fix available, identifier assigned).
**Audience:** General public + members (member notice in parallel).
**Channel & TLP:** Website, GHSA, OSV (→ CVE-LIST/EUVD), CSAF VEX feed, SIREN; TLP:CLEAR.

**Template (advisory body)**

```
{Component} — {short title} ({CVE-ID})

Summary: {1–2 sentences: what it is, who is affected, what to do}.

Affected versions: {precise, tested ranges}
Fixed in: {version(s)} / Fixed commit: {hash}
Severity: {CVSS vector string} ({band}). {If applicable: deviation notice — our assessment
differs from the maintainer's; see below.}

Impact: {common impact, not weakness jargon where possible}
Mitigations / workarounds: {deployable steps, if any}
Detection / IOCs: {indicators — default to IOCs, not PoC}

Coordination: This issue was coordinated to disclosure by the Akrites SIRT.
{Acknowledgements block — insert the chosen scenario from acknowledgements-and-attribution.md}

Timeline: {optional — first report date; key milestones}
References: {GHSA, OSV, CVE, project advisory, patch}
```

**Notes:** Publish machine-readable data (CSAF VEX, OSV) alongside human-readable. Do **not** publish
PoC/exploit code; prefer IOCs. Attribute coordination to the Akrites SIRT / Akrites Foundation.
Fire the parallel member notice and, if relevant, the SIREN alert simultaneously.

---

## Play 6 — Embargo break handling

**When to use:** An embargo is broken (leak, premature publication, third-party disclosure).
**Audience:** Internal SIRT first; then case team, maintainer, coordinators, and — if warranted —
accelerated public notice.
**Channel & TLP:** Start on the case channel; TLP:RED until a public decision is made.

**Core rule from prior discussion:** In the event of an embargo breach, the **SIRT coordinates the
response**, based on what was broken and how. Any member who discovers a break **must notify the
SIRT immediately**.

**Step 1 — internal flash (case team)**

```
Subject: [Akrites SIRT] EMBARGO BREAK — {tracking-id} (TLP:RED)

We have a confirmed/suspected embargo break on {tracking-id}.
- What leaked: {scope — full details? partial? existence only?}
- Where / how: {channel, link, timestamp}
- Confirmed by: {who}, at {time}
- Exposure assessment: {who can now see what}

SIRT is coordinating. Do not respond publicly or independently. Hold for direction.
Next: assess whether to accelerate disclosure. Decision owner: {name}. By: {time}.
```

**Step 2 — notify maintainer & coordinators**

```
Subject: [Akrites SIRT] {tracking-id} — disclosure timing may change (TLP:AMBER)

{Maintainer/Coordinator}, we've detected that information about {tracking-id} has been exposed
outside the agreed embargo. To protect users, we may need to bring the coordinated disclosure
forward. We'll finalize the fix/advisory as quickly as possible and coordinate the new timing
with you. Current proposal: {accelerate to {date/time}} / {publish now}. Your input by {time}?
```

**Step 3 — accelerated public notice (if warranted):** use Play 5, noting the fix/mitigation
status honestly even if not everything is final.

**Notes:** Match the response to the break — existence-only leaks may not warrant full acceleration;
full-detail leaks usually do. Capture the break in the postmortem (Play "Blameless postmortem").

---

## Play 7 — Asking a Finder how they want to be acknowledged

**When to use:** At intake and again before PD, to confirm attribution preference.
**Audience:** Finder (each co-finder individually).
**Channel & TLP:** Case/intake channel; TLP:RED.
**Companion:** `acknowledgements-and-attribution.md` (scenarios 1–3, controlled AI vocabulary).

**Template**

```
Subject: [Akrites SIRT] {tracking-id} — how would you like to be credited? (TLP:RED)

Hi {Finder},

When this is disclosed, how would you like to be acknowledged? Options:

1. Named — your name{, and organization if you wish}. You can also choose to list the
   tools/models used (from our published list); model/harness internals stay private either way.
2. Clearinghouse — credit {your organization / CERT} as the reporter, no individuals named.
3. Anonymous — no attribution; we credit the Akrites SIRT as coordinator only.

Please reply with 1, 2, or 3 (and the exact display name if 1 or 2). You can change your mind any
time before public disclosure. If we don't hear back before PD, we default to anonymous (option 3).

— Akrites SIRT
```

**Notes:** Preference is confirmed before PD and held TLP:RED until then. Honor declines fully;
WG-level credit may substitute for individuals where appropriate. Record the confirmation date.

---

## Play 8 — Requesting additional resources be read into a disclosure

**When to use:** The case needs an SME, WG, tiered partner, or the Finder/maintainer requests
someone be looped in.
**Audience:** Two directions — (a) the person/org to be read in; (b) approvers (SIRT/TOC as needed)
and the parties who must be informed (Finder, WG, maintainer).
**Channel & TLP:** Case channel; TLP:RED. Read-in is need-to-know, validated, and can be delegated
(e.g., a coordinator decides whom to loop in); the maintainer may weigh in on read-ins.

**8a — Read-in request/approval (internal)**

```
Subject: [Akrites SIRT] Read-in request — {tracking-id} (TLP:RED)

Requesting read-in for: {name / org / role}
Reason / expertise needed: {why they're essential now}
Scope of access: {what they'll see — full case? patch only? tier {n} material?}
Duration: {time-boxed to {milestone/date}, then spun down}
Requested by: {name}. Approver: {SIRT / TOC if tiered}. Informed parties: Finder{, WG}{, maintainer}.

Least-privilege check: is there a narrower scope that still works? {yes/no}
```

**8b — Invitation to the person being read in**

```
Subject: [Akrites SIRT] Invitation to a coordinated security case ({TLP:RED})

Hi {Name},

Your expertise in {area} is needed on a coordinated, embargoed security case. Before we share
details we need to confirm:
- You accept TLP:RED handling: named-recipient only, no forwarding, no PoC outside the case repo.
- Your access is scoped to {scope} and time-boxed until {date/milestone}.
- {Any org-vetting / hardware-2FA / access prerequisites}.

Reply to confirm and we'll provision access to {case repo/channel}. Access is revoked when the
work concludes.

— Akrites SIRT
```

**Notes:** Provisioning should be simple and as automated as possible, with clean spin-down. Log
every read-in. Respect delegation (a clearinghouse may choose its own read-ins) and the maintainer's
ability to weigh in.

---

# Part II (cont.) — Additional plays from prior discussions

These cover comms situations already raised in the F2F and collateral that weren't in the original
eight.

## Play 9 — Upstream first-contact / introduction ("maintainer to maintainer")

**When to use:** First outreach to a project about a coordinated report.
**Audience:** Maintainer(s).
**Channel & TLP:** PVR if enabled, else security.txt/SECURITY.md contact; signed email. TLP:RED→AMBER.

**Template**

```
Subject: Coordinated security report for {project} — from the Akrites SIRT

Hi {Maintainer},

I'm {name}, a coordinator with the Akrites SIRT — a neutral, non-profit team that helps open
source projects turn vulnerability reports into trusted fixes. You keep full authority over your
project, the fix, and the timing; we're here to make this easier, not to impose anything.

We have a validated report affecting {project}. We've prepared a complete package: description,
impact, a reproducer, and an initial/proposed patch you're welcome to refine or replace. We'd
like to share it privately at your convenience.

You can verify this outreach at {akrites.dev/verify} and via our security.txt / GitHub handle
{@handle}. What's the best private channel for the details?

Thank you for maintaining {project}.
— {name}, Akrites SIRT
```

**Notes:** Human sends this, not a bot. Humble, few words, offer a *proposed* patch and invite
refinement. Provide a verification path. Bias critical/high issues to the front of the queue for
first engagement.

---

## Play 10 — Unresponsive / unmaintained / overwhelmed maintainer

**When to use:** Contact info exists but the project doesn't respond, or is unmaintained/overwhelmed.
**Audience:** Maintainer (escalating attempts), then internal/TOC for next steps.
**Channel & TLP:** Same as Play 9, escalating; TLP:RED.

**Escalating follow-up template**

```
Subject: Following up — coordinated security report for {project} (attempt {n})

Hi {Maintainer},

Following up on my {date} note about a security issue in {project}. We understand maintainer time
is scarce and we're not here to add burden — we've done the analysis and drafted a fix.

If it helps, we can: label our fix as an "initial/proposed patch" for you to review; help with
testing; or connect you with resources. If we don't hear back by {date}, our process asks us to
consider next steps to protect users (which may include publishing a patch/mitigation for
consumers). We strongly prefer your involvement.

You can verify us at {akrites.dev/verify}.
— {name}, Akrites SIRT
```

**Notes:** Distinguish **unmaintained** (nothing touched), **unresponsive** (silent but active
elsewhere), and **overwhelmed** (afloat, not prioritizing). Be transparent about *why* we want to
help and earn trust. MoLR / fork / publish-patch decisions are last-resort and require group/TOC
agreement (see Play 15). Preference order: maintainer fixes → Akrites publishes patch file → WG
stewards/forks.

---

## Play 11 — Coordinator / clearinghouse engagement (CISA, ENISA, FIRST, CERTs)

**When to use:** Coordinating with or receiving a report from a clearinghouse/coordinator.
**Audience:** The coordinator.
**Channel & TLP:** Established coordinator channel, signed email; TLP:AMBER.

**Template**

```
Subject: [Akrites SIRT] Coordination on {tracking-id} ({TLP:AMBER})

Hi {Coordinator},

{Acknowledging your report of {issue} | Reaching out to coordinate on {issue}}. Proposed handling:
- Roles: {who does what}
- Read-in: {who needs access; delegation is yours to decide on your side}
- Disclosure timing: proposed {date}, deferring to upstream where they have a process.
- Attribution: {per your preference — named clearinghouse or coordinator-only}.

Note on our principles: we don't pre-disclose to any single government — if we notify one, we
notify all comparable parties. {If relevant: CRA Article 14 considerations for ENISA reporting.}

What timing and channel work best on your side?
— Akrites SIRT
```

**Notes:** Stay balanced — no favoring one government/coordinator. Cite CRA Article 14 where ENISA
reporting is relevant. Defer to upstream process where one exists.

---

## Play 12 — Embargo extension request / negotiation

**When to use:** The fix needs more time than the default window (guideline: 30 days from owner
confirmation; CRob's stated personal preference is shorter, but 30 is the negotiating default).
**Audience:** Finder, maintainer, and any read-in parties affected by the date.
**Channel & TLP:** Case channel; TLP:AMBER+STRICT.

**Template**

```
Subject: [Akrites SIRT] {tracking-id} — proposing an adjusted disclosure date ({TLP:__})

The current target is {date}. {Maintainer/WG} needs additional time because {reason —
complexity, testing, release train}. We propose moving coordinated disclosure to {new date}.

This is a guideline, not a mandate — we defer to upstream. If mitigations exist, we can share
those on the original timeline while the full fix completes. Any objections or constraints
(customer obligations, tiered partners) by {date}?
```

**Notes:** Extensions are for "the greater good" and are negotiated, not imposed. If patch time
exceeds the window, share **mitigations/workarounds** rather than slipping silently. TOC/Board
approve significant deviations.

---

## Play 13 — Duplicate / co-finder notification

**When to use:** A report duplicates one already in flight, or multiple finders converge.
**Audience:** The reporting finder(s).
**Channel & TLP:** Case/intake channel; TLP:RED.

**Template**

```
Subject: [Akrites SIRT] {tracking-id} — related to work already underway ({TLP:RED})

Hi {Finder},

Thanks for this. Your report matches an issue we're already coordinating. That's genuinely useful —
it corroborates severity and reach. Here's what it means for you:
- Status: {the existing work is at {stage}}.
- Credit: you'll be honored as a co-finder if you wish (up to our attribution cutoff) — how would
  you like to be acknowledged? (see Play 7)
- We'll keep you posted at {the next milestone}.

Everything stays TLP:RED.
— Akrites SIRT
```

**Notes:** ~30% of reports may already be in flight/fixed — deduping is normal, not a rejection.
Honor co-finders up to the defined attribution cutoff. Provide status so dedupers can match their
own tracking.

---

## Play 14 — Dispute / disagreement (project says "not a vuln", or CNA-LR disputes)

**When to use:** The maintainer disputes the finding, or there's a scoring/validity disagreement.
**Audience:** Maintainer (and internally, SIRT/TOC).
**Channel & TLP:** Case channel; TLP:AMBER.

**Template**

```
Subject: [Akrites SIRT] {tracking-id} — reconciling our assessments ({TLP:AMBER})

Hi {Maintainer},

We hear that you {don't consider this a vulnerability | assess it differently}. We're not looking
to override your judgment or dispute your CVE. Here's our reasoning and evidence: {concise
technical basis}. 

If we still see it differently after your response, our options are to record a **deviation
notice** (our vector/description alongside yours, clearly attributed) rather than contest your
record. What are we missing, or how would you like to proceed?
— Akrites SIRT
```

**Notes:** We don't get into the business of disputing CVEs. A **deviation notice** (our score
vector + description, published in our system for members) is the mechanism when assessments differ.
Feeds the future dispute-resolution process (incl. CNA-LR scenarios).

---

## Play 15 — Maintainer-of-last-resort / patch or fork publication notice

**When to use:** Upstream can't/won't act and the group/TOC has approved publishing a patch or
stewarding/forking.
**Audience:** Public + members; maintainer informed as a courtesy if reachable.
**Channel & TLP:** Website/GH + advisory channels; TLP:CLEAR at publication.

**Template**

```
{Project} — coordinated fix published by the Akrites SIRT ({CVE-ID})

Because {project} is currently {unmaintained | unresponsive to coordinated outreach}, and to
protect downstream users, the Akrites SIRT is publishing {an initial/proposed patch | a
time-bounded hardened fork} for this issue after {n} coordinated attempts between {dates}.

This is a consumer-protection measure, not a takeover. We welcome the maintainer to adopt, refine,
or replace this fix at any time, and we will defer to upstream. {Steward/LTS invitation, if
applicable.}

Fix: {patch/commit/fork link}   Advisory: {refs}
```

**Notes:** Last resort only, with explicit group/TOC decision. Order of preference: maintainer fixes
→ publish patch file → WG steward/fork. Frame as "initial/proposed" and invite the maintainer back
in. Avoid implying ongoing maintenance you won't provide.

---

## Play 16 — Critical-infrastructure read-in requests

**When to use:** A critical-infra operator/sector needs to be read in before public knowledge.
**Audience:** Requesting party; decided via WG → TOC/Board.
**Channel & TLP:** Case channel; TLP:RED.

**Template**

```
Subject: [Akrites SIRT] Read-in request — critical infrastructure ({TLP:RED})

Sector/operator: {who}   Basis for need: {specific exposure / capability to act}
Requested by: {who}   Routed via: {WG} → {TOC/Board decision}

Reminder of principle: we do not pre-disclose to any single government. Read-ins are need-to-know,
validated, and time-boxed. Decision and rationale to be logged.
```

**Notes:** Default authority is the maintainer; otherwise the Board/TOC decides. "Learn to be
comfortable in the grey." Never convert a critical-infra read-in into single-government
pre-disclosure.

---

## Play 17 — Rejected / declined patch

**When to use:** The maintainer declines the proposed fix.
**Audience:** Finder, WG, internally.
**Channel & TLP:** Case channel; TLP:AMBER+STRICT.

**Template**

```
Subject: [Akrites SIRT] {tracking-id} — maintainer declined the proposed patch ({TLP:__})

The maintainer has declined our proposed patch because {reason}. Options on the table:
- Revise to match their code style / approach: {owner}
- Offer a mitigation/workaround for users while upstream develops their own fix
- If upstream won't fix and users are exposed: escalate to the MoLR discussion (Play 15) with
  TOC input

Finder/WG input by {date}?
```

**Notes:** Many maintainers prefer a regression-test-style PoC and patches that fit their style —
adapt rather than push. Keep it collaborative.

---

## Play 18 — Blameless postmortem / lessons learned

**When to use:** After resolution, especially for hard cases (breaches, disputes, unresponsive
upstreams).
**Audience:** Case team, WG; aggregate learnings to members/TOC.
**Channel & TLP:** Internal; shareable summary TLP:GREEN.

**Template**

```
Subject: [Akrites SIRT] Postmortem — {tracking-id} (blameless)

Timeline: {key dates}
What went well: {…}
What was hard / what broke: {…}  (blameless — focus on process, not people)
Process changes proposed: {…}
Reusable comms/templates to update: {…}
```

**Notes:** Explicitly blameless. Feed changes back into this playbook and the process docs.

---

## Play 19 — Internal escalation to TOC / Board

**When to use:** A decision exceeds SIRT authority (MoLR, major deviation, cross-sector timing,
policy gaps).
**Audience:** TOC / Governing Board.
**Channel & TLP:** Internal governance channel; TLP:RED.

**Template**

```
Subject: [Akrites SIRT] Decision needed — {topic} ({tracking-id}) (TLP:RED)

Decision required: {one sentence}
Context: {brief}
Options: {A / B / C with trade-offs}
SIRT recommendation: {…}
Deadline / why time-sensitive: {…}
```

**Notes:** Keep it decision-first. Log the outcome for chain-of-custody.

---

## Play 20 — Trend / periodic ecosystem report ("weird stuff" report)

**When to use:** Regular reporting of trends, notable/critical findings, and program stats.
**Audience:** TOC/Board and, in aggregate, the ecosystem.
**Channel & TLP:** Governance + public blog for the sanitized version; TLP varies (aggregate =
GREEN/CLEAR).

**Template**

```
Subject: [Akrites SIRT] {Quarter} trend report

Volume: {ingested / deduped / disclosed}
Notable trends: {classes of issues, ecosystems}
Critical findings (sanitized): {…}
Upstream engagement highlights: {responsive wins, tough cases}
Recognition: {top-collaborating projects/people, with consent}
Asks / recommendations to TOC-GB: {…}
```

**Notes:** Recognize great projects/people (top ~5%) with consent. Keep specifics sanitized until
public. This is also where general statistics promised to members are shared.

---
## Play 21 — General onboarding: reading an engineer into Akrites (welcome email)

**When to use:** First-time welcome for an engineer joining the Akrites effort — *not* tied to any
specific case. Orientation, resources, and expectations only. No case details.
**Audience:** Newly added member engineers / participants.
**Channel & TLP:** Signed email from a person; TLP:CLEAR/GREEN (contains no case material).

**Template**

```
Subject: Welcome to Akrites — getting you set up

Hi {Name},

Welcome, and thank you for lending your time to Akrites. This note is your orientation — no
active case here, just what Akrites is, where the resources live, and how we work together.

What Akrites is
Akrites (the Akrites SIRT, also "OSS-SIRT") is a neutral, non-profit operational partner that
helps open source communities turn vulnerability reports into trusted fixes and actionable
security intelligence. We coordinate; maintainers keep final authority over their projects,
fixes, and disclosure timing. We contribute fixes — we don't impose process or tooling.

How we operate (the short version)
- Confidentiality first. We default to TLP:RED and share on a need-to-know basis (circles of
  trust / Traffic Light Protocol).
- Least privilege. You're read into only what you need, for as long as you need it.
- Human-to-human. Upstream and coordinator relationships start person-to-person; we meet
  communities where they are.
- Technical contribution is the price of admission — your expertise is exactly why you're here.
- Synchronized disclosure, coordinated through the SIRT as the single maintainer-facing front door.

Public resources (open to everyone)
- SIRT repository — policy, process, guidelines, and templates:
  https://github.com/Akrites-Foundation/SIRT
- {Website / pipeline}: {akrites.dev}
Start with the README and the docs/ folder — the CVD process, embargo guidance, and comms
templates all live there.

Member-only resources (please keep access within the community)
- Member Slack: https://akritesfoundation.slack.com/archives/C0BED9SLZ7W
  (plus working-group channels: #sirt and #<your-wg>)
- Member mailing list: {list address / signup}
- Working-group private mailing list(s): {as applicable to your WG}
- Tooling once provisioned: {Spyglass (your submissions & status), Watchful Eye (access console),
  Open Door Policy DB (upstream engagement info)}

A few ground rules
- Never post files, PoCs, or exploit code in Slack — use the designated case repo / encrypted
  file share. TLP:RED work does not happen in general Slack.
- Access requires {hardware-backed 2FA / your org's vetting}; we'll walk you through provisioning.
- We operate under the [Akrites Code of Conduct](https://github.com/Akrites-Foundation/SIRT/blob/main/Code_of_Conduct..md)}
and the Linux Foundation antitrust guidance applies to our meetings.

Getting started this week
1. Accept the Slack invite and say hello in #sirt.
2. Skim the SIRT repo (README + docs/).
3. {Confirm your working group / area of focus with {contact}.}
4. Reply with your preferred contact address and GitHub handle so we can finish provisioning.

Questions any time — just reply here or ping me in Slack.

Welcome aboard,
{Your name}
Akrites SIRT
```

**Notes:** Keep this free of any case specifics — it's orientation only, so it can be sent broadly
and reused. Confirm the correct member Slack channel/link and mailing-list addresses before sending;
verify tool names/access match what's live. Send from a person, and offer a verification path if the
recipient is new to Akrites. Pair with provisioning (2FA, repo access) rather than sending in
isolation.

---

# Appendix A — Play index

| # | Play | Primary audience |
| --- | --- | --- |
| 1a | Intake — complete report | Finder |
| 1b | Intake — needs more data | Finder |
| 2 | Lifecycle status updates | All stakeholders |
| 3 | Read-in Finder updates | Finder |
| 4 | High-level member notice (pre-PD) | Members |
| 5 | Public disclosure announcement | Public |
| 6 | Embargo break handling | Internal → all |
| 7 | Acknowledgement preference | Finder |
| 8 | Read-in resource request | SME / approvers |
| 9 | Upstream first-contact | Maintainer |
| 10 | Unresponsive / unmaintained / overwhelmed | Maintainer / TOC |
| 11 | Coordinator / clearinghouse | Coordinator |
| 12 | Embargo extension | Finder / maintainer |
| 13 | Duplicate / co-finder | Finder |
| 14 | Dispute / deviation notice | Maintainer |
| 15 | MoLR patch / fork publication | Public |
| 16 | Critical-infra read-in | Requestor / TOC |
| 17 | Rejected patch | Finder / WG |
| 18 | Blameless postmortem | Case team |
| 19 | Escalation to TOC / Board | Governance |
| 20 | Trend / periodic report | TOC / ecosystem |
| 21 | General onboarding / welcome | New member engineers |

# Appendix B — Open items for TOC / Board

These shape the templates above and are still open from the F2F:

- Confirm the **default embargo window** (30-day guideline) and the standard **extension** principle.
- Define the **co-finder attribution cutoff** (referenced in Plays 7 and 13).
- Ratify the **read-in delegation** model and whether maintainers may veto read-ins.
- Decide **MoLR/fork** authority and triggers (Play 15).
- Finalize **disclosure definition** (what counts as "public") and whether **first-report date** is
  published (Plays 2, 5).
- Approve a distinct **Code of Conduct for upstream engagement** to accompany first-contact (Play 9).
- Confirm the **dispute-resolution** process and the **deviation notice** format (Play 14).

# Appendix C — Companion documents

- `[acknowledgements-and-attribution.md](https://github.com/Akrites-Foundation/SIRT/blob/main/docs/acknowledgements-and-attribution.md)` — attribution scenarios + AI-disclosure vocabulary (Play 7).
- `[Embargo Handling Guidance.md](https://github.com/Akrites-Foundation/SIRT/blob/main/docs/Embargo%20Handling%20Guidance.md)` — embargo mechanics (Plays 6, 12).
- OSS-SIRT Process (High Level); OSS-SIRT MVSR; steward-engagement taxonomy (Play 10).

