---
name: MoLR case
about: One issue per Maintainer of Last Resort engagement. Open in SIRT-private only.
title: "[MoLR] <project> <versions>"
labels: ["molr"]
---

<!--
MoLR case issue template.
Source of truth: Akrites-Foundation/SIRT templates/. Copy into SIRT-private/.github/ISSUE_TEMPLATE/molr-case.md.
Never open this issue in a public repository: it names the staffing Member and pre-public details.
Steps follow docs/molr_guidelines_and_procedures.md. Tick boxes as you go; link evidence inline.
-->

## Case

- **Project / repo:** <!-- upstream URL -->
- **Affected versions:**
- **Route:** <!-- Unresponsive (past the abandonment floor) | End-of-life refusal -->
- **Advisory / CVE:** <!-- links -->
- **Case coordinator:** @

## Step 0 — Entry check

**Project health assessment**
- [ ] Last commit: <!-- date, link -->
- [ ] Last release: <!-- version, date -->
- [ ] Maintainer activity across repo, registry, email, social: <!-- summary -->
- [ ] `SECURITY.md` present? Security contact? <!-- Y/N, link -->
- [ ] License: <!-- SPDX ID --> — redistribution of modified code permitted? Obligations met?
- [ ] Dependents and criticality: <!-- dependents count, distros shipping it, member SBOM prevalence, or written justification -->

**Eligibility**
- [ ] Out of support: <!-- unresponsive since <date> (floor reached <date>) | EOL statement: link -->
- [ ] Outreach tried and failed: <!-- contact attempt log link, or non-fix record link -->
- [ ] Distributions and downstream projects asked to carry the fix, and declined: <!-- who, when -->
- [ ] Bounded patch series on a pinned commit is feasible: <!-- commit/tag -->
- [ ] Capacity slot free: <!-- open engagements / cap -->

**"Do not fork"**
- [ ] `SECURITY.md` and Akrites records checked: <!-- none | preference found: link -->
- [ ] If found: Director's critical-infrastructure override recorded below, and maintainer told before Step 1

**Staffing** *(internal — never published)*
- [ ] Member: <!-- company -->
- [ ] Engineer: @<!-- handle --> · Backup: @<!-- handle -->
- [ ] Both read in under the Read-In Policy: <!-- dates -->
- [ ] Written 12-month commitment: <!-- link to internal record -->
- [ ] Member's dependency on the package (conflict): <!-- none | summary --> — this Member does not approve or sign off its own releases

**Approval**
- [ ] SIRT Director approves: @<!-- handle -->, <!-- date -->
- [ ] Override (only if "do not fork" found): <!-- reason, or n/a -->

**Notices**
- [ ] M1 to maintainer (≥ 14 days before Step 3): <!-- date, addresses -->
- [ ] S1 in `#sirt-disclosures`: <!-- date -->

## Step 1 — Repo and staffing

- [ ] Private repo created: `akrites-molr/<project>-molr` from pinned commit <!-- sha -->
- [ ] Engineers added; branch protection, signed commits, two-person publish set up
- [ ] Internal registry entry added (status `Preparing`)
- [ ] B1 sent to the Board: <!-- date -->

## Step 2 — Fork patched

- [ ] Patch series applied: <!-- PR/commit links -->
- [ ] Upstream backlog triaged: security items carried <!-- links --> · hand-over list for next home <!-- link -->
- [ ] Release gates passed (integrity + correctness, two named reviewers, AI disclosure): <!-- reviewers, links -->
- [ ] GHSA on MoLR repo: <!-- link -->
- [ ] Advisory, OSV, VEX updated with pointer: <!-- links -->
- [ ] CVE requested if none existed: <!-- link or n/a -->

## Step 3 — Fork public

- [ ] Repo public with README header
- [ ] Signed source release tagged: <!-- link -->
- [ ] Registry publish: <!-- no | yes, under Akrites name: <name> -->
- [ ] Patches offered upstream: <!-- links -->
- [ ] Downstream routing (distros, intermediate maintainers): <!-- who -->
- [ ] Public org page updated
- [ ] Registry: `Active` · **Start:** <!-- date of first release --> · **Planned end:** <!-- start + 12 months -->
- [ ] M2 to maintainer · S2 in `#sirt-disclosures`: <!-- dates -->

## During the engagement

- [ ] M3 "Your options" sent by month 9: <!-- date -->
- Additional fixes (each approved by the SIRT Director):
  - <!-- date — advisory — approval -->
- Member changes / withdrawal: <!-- none | date, replacement or freeze -->

## Outcome

- [ ] **Option 1** — transferred on request to <!-- org/URL -->
- [ ] **Option 2** — patches back upstream, our repo archived
- [ ] **Option 3** — patches back upstream, repo archived, support agreement <!-- link, until date -->
- [ ] **Freeze** — M5 sent ≥ 30 days before <!-- date -->; repo archived, "no further fixes"
- [ ] **Maintainer returned** on <!-- date --> — chose Option 2 / 3; M6 sent

- [ ] M4 / M5 / M6 sent · S3 in `#sirt-disclosures`
- [ ] Advisories point to the final location
- [ ] Registry and public org page updated
- [ ] Issue closed
