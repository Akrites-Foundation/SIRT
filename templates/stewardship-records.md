# Stewardship records (template)

*Per [MoLR Policy](../docs/Maintainer_of_Last_Resort_Policy.md) Part III §1. Use §1 when searching for a steward, and §2 to vet and approve a candidate.*

---

## 1. Project status notice / steward call

***Internal, solicited distribution only** — there is no public variant. A public "critical, unmaintained, seeking steward" call hands adversaries a targeting list, and it reaches self-selected strangers rather than candidates with a checkable history.*

**Distribution rules — check before sending:**
- [ ] TLP:AMBER+STRICT to the case circle. Never TLP:CLEAR while a fix is pre-PD.
- [ ] Sent only to named, solicited channels: distros carrying the package, dependent projects, foundations/funders, Akrites members, known contributors from the project's history.
- [ ] Does **not** state "critical + unmaintained + unpatched" in combination — in any artifact, at any time. Any one of the three is publishable on its own; together they name a high-value target, confirm nobody is watching it, and confirm the hole is still open. State status and steward criteria; say nothing about exposure.
- [ ] Approach candidates first rather than waiting for volunteers. A self-nomination is welcome and is not disqualifying; it carries no prior standing to check against, so route it through the same vetting in §2 with no shortcuts.
- [ ] Declared intent (Part I §6) checked first — a registered nomination is contacted before any other candidate; a registered "do not fork" ends the case at advisory + VEX + downstream routing (Part III §3).

```
TLP: AMBER+STRICT
Project: <name> — Status: <unresponsive | abandoned | EOL | WONTFIX>
Declared intent on file (Part I §6): <none | preference recorded>
Summary of situation and contact history:
Dependency footprint (dependents, distros, member SBOM prevalence):
Last-resort security release (if any): <Akrites-controlled namespace, term, CVEs covered>
   NOTE: no namespace transfer is sought or accepted, now or at handoff (Part I §3).
We are seeking a Steward. Criteria and vetting: <Part III §1>. Approval: <Governing Board or designated MoLR subcommittee>.
Recipients (named, solicited):
Expressions of interest to: <contact> by <deadline>.
```

---

## 2. Steward vetting & approval record

```
Candidate (identity verified Y/N, method):
Contribution history / references checked:
Continuity/bus-factor assessment:
Suspicious-persona check (abandonment-exploitation / xz pattern) — findings:
Integrity onboarding: [ ] signed commits [ ] signed releases [ ] hardware keys [ ] 2-person [ ] protected branches
Staged co-maintenance ramp (duration):
Approval — Governing Board, or MoLR subcommittee designated in writing (names / date):
Handoff completed: [ ] repo [ ] signing authority rotated to steward's keys (SIRT keys never shared)
   [ ] patch series + per-patch advisory mapping [ ] open upstream PRs [ ] test artifacts
   [ ] advisory/CVE context [ ] successor pointers (Part III §3) updated [ ] notices published
NOTE: no namespace is transferred — Akrites holds none (Part I §3). A steward who intends to
   pursue the original name does so independently and has been told so in writing: [ ] confirmed
Conflicts declared / recusals (Part II §5.2):
```
