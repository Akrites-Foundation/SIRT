Project status notice / steward call (template)

*Per §7.1 of the MoLR Guidelines. **Internal, solicited distribution only** — there is no public variant. A public "critical, unmaintained, seeking steward" call is a targeting list for adversaries and a recruiting funnel for the persona §7.3 exists to screen out.*

**Distribution rules — check before sending:**
- [ ] TLP:AMBER+STRICT to the case circle. Never TLP:CLEAR while a fix is pre-PD.
- [ ] Sent only to named, solicited channels: distros carrying the package, dependent projects, foundations/funders, Akrites members, known contributors from the project's history.
- [ ] Does **not** state "critical + unmaintained + unpatched" in combination — in any artifact, at any time.
- [ ] Candidates are solicited, not self-nominated. Self-selection into an abandoned high-value project is the attack vector.
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
