# MoLR communications (templates)

*Used with the [MoLR Guidelines and Procedures](../docs/molr_guidelines_and_procedures.md). Every message is plain, specific, and says what the maintainer can do. Fill every `<placeholder>`; delete lines that don't apply. Log each send in the case issue.*

| ID | When | To |
| --- | --- | --- |
| [M1](#m1--engagement-notice) | Step 0, at least 14 days before Step 3 | Maintainer |
| [M2](#m2--fork-is-public) | Step 3 | Maintainer |
| [M3](#m3--your-options) | By month 9 | Maintainer |
| [M4](#m4--new-home) | When a new home is settled | Maintainer |
| [M5](#m5--freeze-notice) | At least 30 days before the end date | Maintainer, distributions, downstream |
| [M6](#m6--welcome-back) | Maintainer returns | Maintainer |
| [S1–S3](#sirt-disclosures-notices) | Step 0, Step 3, end of engagement | `#sirt-disclosures` (internal) |
| [B1](#b1--board-notice) | Step 1 | Governing Board |
| [README header](#readme-header) | Step 3 | Public, top of the MoLR repo |
| [Registry entries](#registry-entries) | Step 1 onward | Internal registry and public org page |

---

## Maintainer emails

Send from **SIRT@akrites.dev** to every address in the contact attempt log. Keep the subject line as written so replies thread.

### M1 — Engagement notice

```
Subject: [Akrites SIRT] Temporary security fixes for <project> <versions> — please read

Hi <maintainer name or handle>,

The Akrites SIRT plans to carry security fixes for <project> <affected versions>
for a limited time, starting no earlier than <date: at least 14 days from today>.
We are writing first so you can tell us if you'd rather we didn't, or if you'd
like to handle it yourself.

WHY
- <CVE-ID / advisory link>: <one-line description>. It affects <versions>,
  which <who depends on it: e.g. "is used by N downstream projects and shipped in X">.
- <Route 1> We tried to reach you <n> times between <first date> and <last date>:
  <list: date — channel — address>. We had no reply.
- <Route 2> On <date> you told us <versions> are end-of-life and won't be
  patched (<link>). The fix is in <supported versions>.
- We asked <distributions / downstream projects> to carry the fix. They declined.

WHAT WE WILL DO
- Create a separate, clearly labelled copy of <project> <versions> at
  github.com/akrites-molr/<project>-molr. Its README says it is not the
  official project and links to you.
- Carry security fixes only, for up to 12 months, staffed by an Akrites
  Member engineer (<GitHub handle>).
- Offer every patch back to you as a PR or patch file.
- At the end, the copy moves to a new home, comes back to you, or is frozen.

WHAT WE WILL NEVER DO
- Take your package name, publish under your name or namespace, or ask a
  registry to transfer anything to us.
- Choose your successor.
- Unpublish releases people rely on.

WHAT YOU CAN DO (any time, now or later)
- Take it back or fix it yourself: reply, or merge our patches. We stop and
  hand everything to you.
- Ask for help instead: we can arrange time-limited support in your own repo.
- Disagree: reply with your reasoning. We'll discuss it, and if we still
  publish, your words can appear verbatim in the advisory.
- Tell us not to copy your project: reply, or add a "do not fork" preference
  to your SECURITY.md. <If a critical-infrastructure override was recorded:
  "Because <reason>, the SIRT Director has decided to proceed despite your
  preference; you can still take the project back at any time.">
- Suggest who should take over: tell us who.

How this works, step by step:
https://github.com/Akrites-Foundation/SIRT/blob/main/docs/molr_guidelines_and_procedures.md

Reply to this email or write to SIRT@akrites.dev. You don't need to explain
any absence.

<name>, Akrites SIRT
```

### M2 — Fork is public

```
Subject: [Akrites SIRT] Temporary security fixes for <project> <versions> — now public

Hi <maintainer>,

As we wrote on <M1 date>, the Akrites SIRT has published security fixes for
<project> <versions>:

- Copy: https://github.com/akrites-molr/<project>-molr
- Release: <tag / release link>
- Advisory: <GHSA / CVE links>
- Patches offered to you: <PR or patch links on your project>

We will carry security fixes until <end date> at the latest. Everything in our
first message still applies: you can take it back, ask for help, or suggest a
new home at any time.

<name>, Akrites SIRT
```

### M3 — Your options

```
Subject: [Akrites SIRT] <project> <versions> — what happens after <end date>

Hi <maintainer>,

Our temporary security fixes for <project> <versions> end on <end date>.
Before then the copy needs a lasting home. The options are:

1. You take it back. We hand over every patch and archive our copy.
2. You take it back with help. An Akrites Member supports you for an agreed,
   limited time.
3. Someone else carries it. We transfer our copy to them. (Akrites doesn't
   choose or approve them; tell us if you have someone in mind.)

If nothing is settled by <end date>, we freeze our copy: it stays available,
marked "no further fixes".

Which would you prefer? Reply to this email or write to SIRT@akrites.dev.

<name>, Akrites SIRT
```

### M4 — New home

```
Subject: [Akrites SIRT] <project> <versions> — new home

Hi <maintainer>,

Our temporary security fixes for <project> <versions> have moved:

<Option 1> The copy now lives at <new URL>, maintained by <handle / org>. This
  was their request; Akrites did not appoint them.
<Option 2> Our patches are in your project (<links>). Our copy is archived and
  points users to your releases.
<Option 3> Our patches are in your project (<links>). <Handle> will help you
  with security fixes until <date>, as agreed on <date>. Our copy is archived.

Advisories now point to <new location>. Thank you.

<name>, Akrites SIRT
```

### M5 — Freeze notice

```
Subject: [Akrites SIRT] <project> <versions> — security fixes end on <date>

Hi <maintainer / distribution / project>,

The Akrites SIRT's temporary security fixes for <project> <versions> end on
<date>. No new home has been found. On that date we will:

- Archive https://github.com/akrites-molr/<project>-molr, marked "no further fixes".
- Keep every release and advisory published. Nothing will be removed.

After <date>, new vulnerabilities will get advisories and mitigations only.
Consider moving to <supported versions / alternatives>.

If you can carry the project instead, reply before <date> and we'll transfer it.

<name>, Akrites SIRT
```

### M6 — Welcome back

```
Subject: [Akrites SIRT] <project> — welcome back

Hi <maintainer>,

Thanks for getting back to us. We've stopped all release work on our copy of
<project>. Here is everything we did, with no conditions:

- Patches: <links>
- Tests: <links>
- Advisories: <links>

How would you like to continue?
1. Take it all back. We archive our copy and point users to your releases.
2. Take it back with help from an Akrites Member for an agreed, limited time.

If you'd like our release marked deprecated, tell us. It stays published so
nothing breaks, but it will point to yours.

<name>, Akrites SIRT
```

---

## `#sirt-disclosures` notices

Internal. Same format as our other disclosure notices.

### S1 — MoLR engagement starting (Step 0)

```
*Akrites SIRT Maintainer of Last Resort Notification*

MoLR engagement for AK-<reponame> *starting*.
- Project / versions: <project> <versions>
- Route: <unresponsive | end-of-life refusal>
- Case issue: <SIRT-private link>
- Maintainer notified (M1): <date>
- Fork public no earlier than: <date>
```

### S2 — MoLR public disclosure (Step 3)

```
*Akrites SIRT Maintainer of Last Resort Public Disclosure Notification*

Embargo for AK-<reponame> *has ended*.   <— or, if the advisory was already public: "MoLR fork for AK-<reponame> *is public*."
- Summary:
- CVE: <link>
- Advisory: <link>
- MoLR repo: https://github.com/akrites-molr/<project>-molr
- Engagement ends no later than: <date>
- Other Links:
```

### S3 — MoLR engagement ended

```
*Akrites SIRT Maintainer of Last Resort Notification*

MoLR engagement for AK-<reponame> *has ended*.
- Outcome: <moved to new owner | returned upstream | upstream + Member support | frozen | maintainer returned>
- New location: <link, or "archived">
- Case issue: <SIRT-private link>
```

---

## B1 — Board notice

```
Subject: [Akrites SIRT] New MoLR engagement: <project> <versions>

For information. The SIRT Director approved a Maintainer of Last Resort
engagement on <date>.

- Project / versions: <project> <versions>
- Why: <route, one line> — <CVE / advisory>
- Staffing: an Akrites Member has committed a named engineer and backup until <date>
- Conflicts recorded: <none | summary>
- Planned public date: <date>
- Case issue: <SIRT-private link>

<name>, SIRT Director
```

---

## README header

Top of every MoLR repository's README from Step 3.

```markdown
> [!IMPORTANT]
> **This is not the official <project>.** It is a temporary, security-fixes-only copy
> of <project> <versions>, maintained by the Akrites SIRT under its
> [Maintainer of Last Resort process](https://github.com/Akrites-Foundation/SIRT/blob/main/docs/molr_guidelines_and_procedures.md).
>
> - **Official project:** <upstream URL>
> - **Why this exists:** <advisory link>
> - **Security fixes until:** <end date> at the latest
> - **Maintained by:** <GitHub handles>
> - **Maintainer of <project>?** You can take this back at any time: SIRT@akrites.dev
>
> Issues are for patch regressions only. Every patch here is offered upstream.
```

On freeze, replace the first line with: `**Frozen on <date> — no further fixes.** Releases remain available.`

---

## Registry entries

**Internal registry** (`SIRT-private`, one row per engagement):

| Project | Versions | Route | Case issue | Staffing Member | Engineers | Status | Start | Planned end | Outcome |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `<project>` | `<versions>` | Unresponsive / EOL refusal | `<link>` | `<Member>` | `<handles>` | Preparing / Active / Moved / Returned / Frozen | `<date>` | `<date>` | |

**Public org page** (`akrites-molr/.github/profile/README.md`). Add a project only at Step 3. Never name the Member company, and never describe a project as unpatched.

| Project | Versions | Official project | Security fixes until | Status |
| --- | --- | --- | --- | --- |
| [`<project>-molr`](https://github.com/akrites-molr/<project>-molr) | `<versions>` | `<upstream link>` | `<end date>` | Active / Moved to `<link>` / Returned upstream / Frozen |
