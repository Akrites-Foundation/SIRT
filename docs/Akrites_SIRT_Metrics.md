# Akrites SIRT Metrics — Proposal

**Status:** Draft v0.1 — for review by the Governing Board and extended SIRT members
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
| Regressions introduced by our patches (goal: 0) | Quality guardrail | I · B | Near | Oct 15: no-regression goal |
| Embargo integrity (% clean / incident count) | Integrity guardrail | I · B · P* | Now | Ongoing |
| Automation ratio; capacity vs. demand | Efficiency/resourcing | I · B | Near | Ongoing (lightest weight) |

\* Public sees an aggregated or qualitative form only.

---

## The three cuts

### Internal / operational — "run the machine"
The full-resolution, real-time view for the SIRT team: intake volume and sources, dedup rate, queue depth and backlog age, time-in-stage across the workflow, cycle time, WG capacity and active cases, rework and rejected-patch rates, regressions introduced, and embargo near-misses and extension requests. This tier may include live and case-identifying detail because it stays with SIRT staff.

### Board / members — "value & health"
An aggregated, periodic view: disclosures completed, upstream fixes merged, downstream remediation enabled (severity-weighted), coverage, median time-to-fix trend (with regressions), automation ratio, embargo integrity, risk posture (aging embargoes, unmaintained-project exposure, MoLR cases), and capacity vs. demand. No live embargoed detail; no individual member identification beyond a member's own data.

### Public — "trust, aggregate, safe"
Kept deliberately simple and credible — five numbers plus stories:

1. Vulnerabilities coordinated to disclosure (period total)
2. Upstream fixes shipped
3. Projects / maintainers supported
4. Median time from report to fix availability
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

- **By ~Aug 15:** stand up the internal counters the tooling already supports — intake, dedup rate, disclosures, projects supported, active WGs, embargo integrity.
- **By ~Sept 15:** add throughput and cycle-time views — dedup counts/percentages, median time-to-fix (with regressions), patches-in-pipeline.
- **By ~Oct 15:** report the outcome and impact headlines — disclosures completed (~50 target), upstream fixes merged, ≥1 downstream remediation case — and publish the first public cut alongside the blog and maintainer testimonials.

---

## Open questions for the Board

- Reporting **cadence and format** for the Board/member cut (e.g., monthly summary vs. live dashboard).
- Whether **severity weighting** for impact metrics uses CVSS, EPSS, or a blended model.
- Who **approves the public cut** each period against the confidentiality gate.
- Any metric the Board wants elevated to a **headline** that isn't in this starter set.
