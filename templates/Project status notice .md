Project status notice / steward call (template)

*Per §7.1 of the MoLR Guidelines. **Internal, solicited distribution only** — there is no public variant. A public "critical, unmaintained, seeking steward" call hands adversaries a targeting list, and it reaches self-selected strangers rather than candidates with a checkable history.*

**Distribution rules — check before sending:**
- [ ] TLP:AMBER+STRICT to the case circle. Never TLP:CLEAR while a fix is pre-PD.
- [ ] Sent only to named, solicited channels: distros carrying the package, dependent projects, foundations/funders, Akrites members, known contributors from the project's history.
- [ ] Does **not** state "critical + unmaintained + unpatched" in combination — in any artifact, at any time. Any one of the three is publishable on its own; together they name a high-value target, confirm nobody is watching it, and confirm the hole is still open. State status and steward criteria; say nothing about exposure.
- [ ] Approach candidates first rather than waiting for volunteers. A self-nomination is welcome and is not disqualifying; it carries no prior standing to check against, so route it through the same §7.3 vetting with no shortcuts.
- [ ] Declared intent (§7.6) checked first — a registered nomination is contacted before any other candidate; a registered "do not fork" ends the case at advisory + VEX + §8 routing.

```
TLP: AMBER+STRICT
Project: <name> — Status: <unresponsive | abandoned | EOL | WONTFIX>
Declared intent on file (§7.6): <none | preference recorded>
Summary of situation and contact history:
Dependency footprint (dependents, distros, member SBOM prevalence):
Last-resort security release (if any): <Akrites-controlled namespace, term, CVEs covered>
   NOTE: no namespace transfer is sought or accepted, now or at handoff (§8.0).
We are seeking a Steward. Criteria: <§7.2>. Vetting and approval process: <§7.3–7.4>.
Recipients (named, solicited):
Expressions of interest to: <contact> by <deadline>.
```
