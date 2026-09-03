# MoLR decision record (template)

*Per §6.2 of the MoLR Guidelines. One record per CVE — an open engagement on the same package does not pre-authorize a new fix.*

```
Case ID / CVE (this approval covers this CVE only):
Existing open MoLR engagement on this package? (Y/N — if Y, use fast path §6.2.1)
--
ENTRY TEST (§6.1 — all six must hold)
1. No willing rights-holder. Parties ASKED and DECLINED (name, date, response):
   [ ] maintainer (or §3.2 finding signed)  [ ] distros  [ ] downstream consumers
   [ ] dependent projects  [ ] existing successor project  [ ] foundation/funder
   [ ] intermediate maintainers (§8.4)
2. Criticality evidence (attach): OpenSSF Criticality Score ___ | distros carrying ___
   | direct dependents ___ | transitive dependents ___ | member SBOM prevalence ___
   Published threshold met? (Y/N)
3. License finding (SPDX ID, redistribution permitted Y/N, obligations), recorded before code touched:
4. Bounded patch series feasible? Pinned upstream commit/tag: ___ Bounded-effort estimate: ___
5. Capacity slot available? (open engagements ___ / published cap ___)
6. This CVE approved (not the package):
--
ARTIFACT
Publishing namespace (Akrites-controlled; original namespace prohibited §8.0):
Versioning scheme + per-registry sorting check (monotonic, never outranks a real upstream release):
Release gate owners (§6.4): upstream suite ___ | downstream suites selected ___
   | API-diff check ___ | reproducibility ___ | 2 named reviewers ___ | AI involvement disclosed (Y/N)
Upstream PRs to be opened at PD (§6.5) — repo/target:
Inbound channels closed (§6.3.2): [ ] issues [ ] PRs [ ] auto-close template deployed
--
TERM AND EXIT
Term (start / end / renewals used):
Retirement threshold status (§6.7): fixes shipped ___ / 3 · renewals used ___ / 2
Sunset triggers:
Steward-search plan + owner (§7.1 — solicited channels only, no broadcast):
--
GOVERNANCE
Security/provenance sign-off (required for 5.3c):
Conflicts declared / recusals (§6.2):
TOC approval (names / date)  [or interim approver + sunset date]:
Fast-path approval (§6.2.1): SIRT lead ___ + non-recused TOC member ___ / date:
```
