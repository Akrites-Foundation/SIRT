# Akrites SIRT Metrics

**Status:** Draft — for Akrites SIRT review
**Owner:** Policy/Process work stream (CRob)
**Scope:** A lean starter set of metrics, measurable in the near term and tied to the 30/60/90 goals. A fuller "north-star" catalog can follow in a later phase.

---

## Purpose

Give each audience the view it needs — the internal team, the Board and members, and the public — from **one dataset, measured once and cut three ways.** We define each metric a single time from what the pipeline (akrites.dev, Spyglass) can emit, then filter and aggregate by audience rather than running three separate measurement efforts. The audiences differ in *granularity and sensitivity*, not in the underlying data.

## What these metrics lead with

By agreement, the headline metrics prove, in priority order:

1. **Remediation outcomes & impact** — did we get real fixes shipped and help people remediate?
2. **Coverage & ecosystem trust** — how much of the ecosystem we support, and how maintainers experience us.
3. **Throughput & speed** — supporting evidence, never the headline.
4. **Efficiency & resourcing** — lightest weight; mainly for internal planning and board resourcing.

## Guiding principles

- **Outcomes over volume.** We do not reward raw report counts, which invite low-quality floods.
- **Speed is never shown alone.** Any time-to-fix figure appears next to a quality figure (regressions introduced), so it is never read as "just go faster."
- **A confidentiality gate on every external metric.** Before a metric is shown to the Board or the public we ask: *does this leak embargoed information, identify a member, or create a target?* If yes, it stays internal or is aggregated and delayed.
- **Leading + lagging pairs.** Health indicators (queue age, capacity) sit alongside results (fixes shipped, disclosures) so the Board sees both.
- **Measure what we can now; phase the rest.** The starter set favors metrics the tooling can produce soon.

---

## The starter metric set

Audience key: **I** = internal team · **B** = Board/members · **P** = public. Public rows are always an aggregated or qualitative form.

| Metric | Proves | Audience | Measurable | 30/60/90 tie |
|---|---|---|---|---|
| Coordinated disclosures completed | Outcome | I · B · P | Now (as cases flow) | Oct 15: ~50 through the system |
| Upstream fixes merged (count & % of cases) | Outcome | I · B · P | Near | Oct 15: successful upstream patch |
| Downstream remediation cases enabled | Impact | I · B · P* | Near | Oct 15: ≥1 downstream case |
| Projects & maintainers supported | Coverage | I · B · P | Now | Ongoing |
| Active WGs / projects under watch | Coverage | I · B | Now–near | Aug 15: WGs stood up |
| Maintainer experience & testimonials | Trust | B · P* | Near (qualitative) | Oct 15: blog stories |
| Reports processed & dedup rate (%) | Throughput | I · B | Now | Sept 15: dedup counts/% |
| Median time: report → fix *(shown with regressions)* | Speed + quality | I · B · P* | Near | Sept 15: patches in pipeline |
| Regressions introduced by our patches (goal: 0) | Quality guardrail | I · B · P* | Near | Oct 15: no-regression goal |
| Embargo integrity (% clean / incident count) | Integrity guardrail | I · B · P* | Now | Ongoing |
| Automation ratio; capacity vs. demand | Efficiency/resourcing | I · B | Near | Ongoing (lightest weight) |
| Acknowledgement within 2 business days (% of reports) | Commitment (SECURITY.md) | I · B · P | Now | Ongoing |
| Initial assessment within 10 business days (%) | Commitment (SECURITY.md) | I · B · P | Now | Ongoing |
| PD within severity target (≤ 17/21/24 bd) (%) | Commitment (CVD Policy §5) | I · B · P* | Near | Ongoing |
| Actionable guidance within 7 days of confirmed exploitation (%) | Commitment (CVD Policy §9) | I · B · P* | Near | Ongoing |
| Appeals acknowledged within 3 bd / resolved within 10 bd (%) | Commitment (CVD Policy §15) | I · B | Now | Ongoing |
| Known-affected consumers on a fixed version at 30 / 90 days post-PD | Outcome (MoLR Policy Part IV §2) | I · B | Later | — |
| MoLR engagements (count) — **rising = failure signal** | Counter-metric (MoLR Policy Part IV §2) | I · B | Now | Ongoing |

\* Public sees an aggregated or qualitative form only.


### Metric definitions

Every time-based metric is measured in **business days** unless stated, from the case record. A case counts once, in the period its stop event falls.

| Metric | Start event | Stop event | Notes / exclusions |
|---|---|---|---|
| Acknowledgement within 2 bd | Report received on any intake channel | Acknowledgement (Notification Template 1) sent | Denominator: reports with a reply channel |
| Initial assessment within 10 bd | Report received | Triage assessment (Template 2a/2b) sent | — |
| PD within severity target | Report received | Public Disclosure (advisory published) | Severity band = the band assigned at enrichment. Cases on a longer timeline under the upstream project's own policy (CVD Policy §8) and accelerated cases (§9) are reported separately, not as misses. There is no "clock pause." |
| Median time: report → fix | Report received | Fixed release or merged upstream fix publicly available | "Fix availability" in the public cut means the same stop event |
| Actionable guidance after exploitation | Active exploitation confirmed | Guidance or mitigation published | Target 7 calendar days (CVD Policy §9) |
| Embargo integrity | — | — | % of cases reaching PD with no embargo break, as classified in [What Counts as Public Disclosure](what-counts-as-public-disclosure.md) §5 |
| Upstream fixes merged | — | Fix merged upstream | % = merged ÷ coordinated disclosures completed in the period |
| Downstream remediation enabled; automation ratio | — | — | *To be defined before first Board report* |

---

## The three cuts

### Internal / operational — "run the machine"
The full-resolution, real-time view for the SIRT team: intake volume and sources, dedup rate, queue depth and backlog age, time-in-stage across the workflow, cycle time, WG capacity and active cases, rework and rejected-patch rates, regressions introduced, and embargo near-misses and extension requests. This tier may include live and case-identifying detail because it stays with SIRT staff.

### Board / members — "value & health"
An aggregated **monthly written summary**: disclosures completed, upstream fixes merged, downstream remediation enabled (weighted by severity label — Critical / High / Medium / Low, per the [Severity Scoring Guidelines](severity_scoring_guidelines.md)), coverage, median time-to-fix trend (with regressions), automation ratio, embargo integrity, risk posture (aging embargoes, unmaintained-project exposure, MoLR cases), and capacity vs. demand. No live embargoed detail; no individual member identification beyond a member's own data.

### Public — "trust, aggregate, safe"
Kept deliberately simple and credible — five numbers plus stories. The SIRT Director approves each period's public cut against the confidentiality gate.

1. Vulnerabilities coordinated to disclosure (period total)
2. Upstream fixes shipped
3. Projects / maintainers supported
4. Median time from report to fix availability, shown with regressions introduced by our patches
5. % of coordinations completed with no embargo incident

…accompanied by maintainer testimonials and ecosystem success stories. **Excluded from the public tier:** anything live or embargoed, member identities, per-project unfixed counts, throughput internals, efficiency figures, and any SBOM detail.

---

## Member SBOM coverage — opt-in, private to the member

Members reasonably want to know "is the SIRT watching the components I depend on?" — but a member's dependency footprint is sensitive and can become a target. Therefore:

- SBOM coverage is **not** a shared Board or cross-member metric.
- It is **opt-in**: a member chooses whether to have their coverage tracked at all.
- For members who opt in, coverage is shown **only in their own private dashboard** (the Spyglass portfolio brief) — visible to that member and to SIRT staff, and to no other member.

This preserves the member-value signal without exposing anyone's dependency map.

---

## Guardrails summary

- **Anti-gaming:** outcomes weighted above volume; speed always paired with quality; no metric tied to a reward that would incentivize low-quality reports or corner-cutting.
- **Confidentiality gate:** applied to every Board and public metric; public metrics are lagging and aggregated.
- **Data minimization:** the public tier is the smallest credible set; member-identifying data is opt-in and private.

---

## Phasing (tied to 30/60/90)

- **2026-08-15 — internal counters** (intake, dedup rate, disclosures, projects supported, active WGs, embargo integrity): {met / partly met / not met — note}.
- **2026-09-15 — throughput and cycle-time views**: {status}.
- **2026-10-15 — outcome headlines and first public cut** (~50 disclosures, upstream fixes merged, ≥1 downstream case): {status}.
- **Next milestone:** {date} — {what}, owner {name}.

---

## Decisions (2026-11-10)

Decided by the SIRT Director under the document approval rules (decision D2):

- **Cadence and format:** the Board / member view is a monthly written summary. Weekly Board emails cover progress and membership and link to it.
- **Severity weighting:** impact metrics are weighted by the severity label (Critical / High / Medium / Low) from the [Severity Scoring Guidelines](severity_scoring_guidelines.md). EPSS is not used, because embargoed cases have no EPSS value.
- **Public cut:** the SIRT Director approves each period's public cut against the confidentiality gate.
- **Data store owner:** the SIRT Director owns the case-lifecycle data store these metrics are computed from.
