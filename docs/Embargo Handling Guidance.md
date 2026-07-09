# Akrites SIRT — Embargo Handling Guidance

**Status:** Proposal / Draft for review

**Applies to:** All vulnerability cases handled by the OSS-SIRT (Intake → Synchronized Disclosure)
**Relationship to existing docs:** Extends the *OSS-SIRT Process (High Level)* Coordination phase and the confidentiality principles in *Akrites: The SIRT*. Informed by the FIRST *Guidelines and Practices for Multi-Party Vulnerability Coordination and Disclosure*.

---

## 1. Purpose

This document sets out how the SIRT proposes, negotiates, and manages the embargo period — the window during which a validated vulnerability is kept confidential among read-in parties so a fix can be developed, tested, and staged before public disclosure (PD).

It exists to give the SIRT a predictable, defensible default while making one thing unambiguous: **the upstream project's own security policy and disclosure timelines take precedence over the SIRT's default whenever the two differ.** The SIRT coordinates and de-noises; it does not override maintainer authority over their own releases.

## 2. Core principle: the default is a starting point, not the rule

The SIRT operates a **default embargo of 30 calendar days** from the point a finding is validated and ownership is assigned (end of the *Deduplicate & validate* phase). This gives a consistent planning baseline for Finders, members, and downstream stakeholders when no other timeline applies.

**The default yields to the upstream project in every case where the project has its own policy.** The order of precedence the SIRT follows is:

1. **A published upstream security/disclosure policy** for the affected project. If the project states an embargo length, a maximum, a fixed cadence, or a "fix-ready-then-disclose" rule, that governs.
2. **A coordinating list or hub the project routes through** (e.g., the Linux kernel security team, the Openwall `linux-distros` list). Where an issue must flow through one of these, its rules cap the embargo regardless of the SIRT default — see §5.
3. **A timeline negotiated with the maintainer** for this specific case, where no published policy exists.
4. **The SIRT 30-day default**, used only when none of the above applies (typically an unmaintained or policy-less project).

Practically: the case owner records which of these four applies at the start of Coordination and sets the PD date accordingly. If the applicable upstream timeline is *shorter* than 30 days, the SIRT uses the shorter one. If a project explicitly permits *longer* (rare, and mostly for cross-vendor hardware/microarchitectural issues), the SIRT may follow it with TOC awareness.

### Why 30 days as the default (and why it flexes down so often)

A single fixed number is easy to communicate and lets members and downstream consumers plan. Thirty days is comfortably inside the broadly accepted industry norm — the 90-day convention popularized by coordinator practice (e.g., CERT/CC's ~45-day guidance and Project Zero's 90-day model) sits at the outer edge; most active open source projects move considerably faster than that. Because the fastest-moving, highest-impact projects (see §5) run embargoes measured in **days, not weeks**, the SIRT will in practice spend far more time shortening the default than extending it. The default mainly matters for projects that have *no* policy at all.

## 3. Guidance for the reader

> When you open a case, do not assume the 30-day default applies. **Look up the upstream project's security policy first.** Check, in order: a `SECURITY.md` / security policy page in the project repo; a `/security` or "slash security" page and a `security@` contact; the project's advisory or announce channels; and whether the project routes security issues through a known coordinating list (kernel security team, `linux-distros`, a distro PSIRT). Set the PD date to match whatever you find. Use 30 days only when you have confirmed there is nothing to defer to.

## 4. What Finders need to know before reporting to the SIRT

The embargo is set by the disclosure environment of the *affected project*, not by the Finder's preference. Finders reporting to the SIRT should understand and plan for the following.

### 4.1 The SIRT follows the upstream project's or list's disclosure requirements

When a report is shared with the SIRT, we will **always attempt to follow the affected upstream project's (or coordinating list's) disclosure requirements.** That governing timeline may be **shorter or longer than the window the Finder would prefer**:

- It is often **shorter** than a Finder might expect — the Linux kernel works to ~7 days from fix-ready, `linux-distros` caps at 14, and OpenSSL prenotifies for ~7 (see §5). A Finder hoping for a longer runway to prepare a write-up or conference talk should not count on it.
- It can occasionally be **longer** — for example, cross-vendor hardware/microarchitectural issues sometimes carry multi-month embargoes.

**Finders should plan accordingly.** By reporting to the SIRT, a Finder accepts that the disclosure timeline will be aligned to the project/list rules and the maintainer's authority, and may not match the Finder's own desired schedule. Where a Finder has a hard constraint (e.g., a planned publication date), raise it at intake so the SIRT can factor it into negotiation — but the project's requirements and maintainer approval remain controlling.

### 4.2 Others may be researching the same project — duplicate findings happen

A Finder should assume they are **not the only party looking at a given project.** With AI-assisted research now cheap and widespread, it is common for multiple independent researchers to discover the **same or similar vulnerabilities** at around the same time. Deduplication is a core SIRT function (the *Deduplicate & validate* phase).

When the SIRT becomes aware that two or more reports cover the same or overlapping issue:

- We will **inform the affected reporters of the situation** (without exposing another Finder's confidential details beyond what is needed to convey that a duplicate exists).
- Finders should understand that a **parallel discloser is outside the SIRT's control.** Some other Finder may choose to **disclose to the project directly or through a separate Coordinator**, on their own timeline.
- As a result, **an embargo may already be in effect** (set by another party's earlier report) that the SIRT and the later Finder must work within — or, conversely, **an embargo may no longer be an option at all** if another party has already gone public or set an imminent public date. In that case the SIRT shifts to accelerated coordination and consumer-protection guidance rather than a fresh embargo window.

The practical takeaway for Finders: report early and let the SIRT coordinate, but do not assume exclusivity over a finding or full control of its disclosure timing.

### 4.3 Public AI / LLM tools do not provide confidentiality — assume NO embargo

Finders using AI tools — **especially public, hosted large language models (LLMs)** — to discover, analyze, or write up vulnerabilities must understand that **these tools are not private and do not guarantee confidentiality.** Prompts and pasted material submitted to a public LLM service may be retained, logged, used for training, reviewed by the provider, or otherwise exposed outside the Finder's control.

Accordingly:

- **A report developed with public LLM tooling must be treated as NOT having an embargo available.** Confidentiality cannot be claimed over material that has already been exposed to a public, non-confidential service. The SIRT cannot restore an embargo to information that has already left a trusted boundary.
- Such reports will generally be handled on an **accelerated / assume-exposed basis**: the SIRT prioritizes getting a fix and consumer-protection guidance out quickly rather than negotiating a private window that the input material may have already undermined.
- Finders who need to preserve the *option* of an embargo should conduct sensitive analysis using **private, confidential tooling** — self-hosted or enterprise models with contractual confidentiality and no-training guarantees, or the SIRT's own hardened, access-controlled analysis environment — and should **not** paste vulnerability details, proof-of-concept code, or affected-code excerpts into public LLM services.
- If a Finder is unsure whether their tooling qualifies as confidential, they should disclose that at intake so the SIRT can classify the report's embargo eligibility correctly.

This aligns with the Akrites first principle that an undisclosed vulnerability in a widely deployed package is, in effect, a weapon: confidentiality is only meaningful if it was actually maintained end-to-end, including in the tools used to find the issue.

## 5. Worked examples from key upstream projects

These illustrate how much real embargo windows vary, and why deferring to the project is the rule rather than the exception. Timelines below reflect the projects' published policies as of mid-2026; **always re-check the live policy, as these change.**

### Linux kernel (`security@kernel.org`)

The kernel security team treats its list as a fix-development channel, not a disclosure channel, and runs one of the tightest timelines in the ecosystem. Once a robust fix exists, publication of the fix may be deferred only at the reporter's or an affected party's request for **up to 7 calendar days from the start of the release process, extendable to 14 days only exceptionally** where criticality justifies it. The only accepted reason for deferral is QA and large-scale rollout logistics. The team does not assign CVEs or sign NDAs, and considers "get the bug fixed" its sole interest.

**SIRT implication:** for kernel issues, the 30-day default is irrelevant — the SIRT works to the 7-day (max 14-day) window and notifies the kernel security team **first**, before any distros or public list.

### Openwall `linux-distros` and `oss-security` lists

Where a kernel or broader OSS issue needs distribution vendors prepared before PD, coordination flows through the private `linux-distros` list, with public disclosure on `oss-security`. Key rules:

- **Maximum embargo is 14 days. Do not ask for longer.** Windows shorter than 7 days are preferred; the reasonable minimum is 1 day, and a few hours can be acceptable in extreme cases.
- For **Linux kernel** issues specifically, you must notify the **kernel security team first, wait for the fix, and only then** notify `linux-distros` or `oss-security`.
- The reporter **must** post publicly on `oss-security` within 14 days of contacting the list, **whether or not a patch is ready.** So don't engage `linux-distros` until a patch exists.
- Everything sent to `(linux-)distros` becomes public at disclosure — post nothing that can't eventually be public.
- Vendors generally prefer to publish updates Tuesday–Thursday (the historical policy allowed stretching a window to ~19 days only to land disclosure on a Monday/Tuesday when reported late in the week).

**SIRT implication:** these lists hard-cap the embargo well below the SIRT default. For any multi-distro Linux issue, plan to the ≤14-day `linux-distros` clock and treat the kernel-first ordering as mandatory.

### OpenSSL

OpenSSL's stated principle is that **embargoes should be measured in days and weeks, not months or years.** It categorizes issues LOW / MODERATE / HIGH / CRITICAL. For HIGH and CRITICAL issues it prenotifies certain organizations and distributions with details and patches, and aims to keep issues private for **no longer than about a month**, with a **prenotification window of 7 days or less**. Severity assessments can and do change during the embargo (e.g., a CRITICAL later downgraded to HIGH after prenotification testing).

**SIRT implication:** a ~7-day prenotification and a keep-it-short posture; the SIRT's role is to support that cadence, not lengthen it. The 30-day default is roughly OpenSSL's *outer* bound, not its norm.

### Fixed-cadence projects (illustrative)

Some projects run scheduled release trains rather than per-issue embargoes — e.g., short fixed windows tied to a CVE issuance (72 hours is used by some projects), or quarterly critical-patch cadences with a ~5-day advance pre-release notice used by large vendors. Where a project has a cadence, the SIRT aligns the PD to the next appropriate release window rather than imposing its own date.

## 6. Operating rules for the SIRT

1. **Determine the governing timeline at the start of Coordination** and record it in the case (which of the four precedence tiers in §2 applies, and the source URL/policy it came from).
2. **Set PD to the shortest applicable timeline.** When multiple parties/components are involved with different windows, the tightest binding constraint (e.g., a `linux-distros` 14-day cap, or a project that has already committed to a date) governs the synchronized window.
3. **Maintainer authority is final.** The SIRT proposes and negotiates; the maintainer approves or revises the PD date for their project. The SIRT does not extend an embargo past what the project or a coordinating list permits.
4. **Prepare for embargo break from day one.** Per the FIRST guidance and the Coordination phase of the SIRT process, hold ready an interim advisory and consumer-protection guidance so that if the embargo leaks or an in-the-wild exploit appears, the SIRT can move immediately to accelerated or full disclosure. Recent kernel cases (multiple 2026 embargo collapses driven by AI-accelerated independent discovery) show this is now a routine contingency, not an edge case.
5. **TLP throughout.** The embargo is enforced technically and procedurally via TLP 2.0 (TLP:RED at intake, TLP:AMBER+STRICT for case/patch material) and least-privilege read-in, consistent with the Akrites confidentiality framework.
6. **Set Finder expectations at intake.** Confirm the Finder understands the timeline is governed by the project/list (§4.1), that duplicate reports may exist and alter the window (§4.2), and classify the report's **embargo eligibility** based on the tooling used — reports developed with public LLMs are treated as having **no embargo available** (§4.3).
7. **Handle duplicates transparently.** When deduplication surfaces overlapping reports, inform the affected reporters that a duplicate exists (without leaking another Finder's confidential detail), and account for any embargo already set — or foreclosed — by a parallel discloser or Coordinator.
8. **Unmaintained / unresponsive projects.** Where no policy and no responsive maintainer exist, the 30-day default applies as the working clock. If the project remains unresponsive, escalate per the intake process (new steward, or — with TOC approval and time-bounding — a hardened fork / full disclosure), with advisories and CVEs issued through the Linux Foundation's CNA authority.
9. **Document deviations.** Any embargo longer than 30 days (only expected for cross-vendor hardware/microarchitectural issues) requires explicit rationale and TOC awareness.

## 7. Summary table

| Source of timeline | Typical embargo | SIRT action |
|---|---|---|
| Linux kernel security team | ≤7 days from fix ready (14 exceptional) | Notify kernel team first; work to their window |
| Openwall `linux-distros` / `oss-security` | ≤14 days (7 preferred); must go public in 14 | Kernel-first ordering; engage only with patch in hand |
| OpenSSL | ~7-day prenotify; ≤~1 month total | Support short prenotification cadence |
| Fixed-cadence projects | Project-defined (e.g., 72h, quarterly) | Align PD to project's release window |
| Project with a published policy (general) | As published | Defer to it |
| No policy / unmaintained project | **30 days (SIRT default)** | Use default; escalate if unresponsive |
| Finder's preferred window | N/A — does not govern | Align to project/list; Finder plans accordingly (§4.1) |
| Duplicate / parallel disclosure | Set (or foreclosed) by another party | Inform both reporters; work within any existing embargo (§4.2) |
| Report developed with public LLM tooling | **None — assume exposed** | Handle on accelerated / assume-exposed basis (§4.3) |

---

*This is a draft proposal for review by the SIRT and TOC. Referenced upstream policies are summarized from their published sources and are subject to change; verify the live policy for each project when handling a case.*
