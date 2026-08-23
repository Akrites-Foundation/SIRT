# Maintainer non-fix record (template)

```
Case ID / CVE:
Maintainer position (verbatim quote + link):
Type: [ ] Formal EOL  [ ] Feature-complete  [ ] WONTFIX-on-merits
Stated rationale:
Date / source:

Technical disagreement resolved on the merits (§5.2.1) -- complete BEFORE the rest of this record:
  Nature of the disagreement: [ ] Threat model  [ ] Reachability  [ ] Severity / exploitability
                              [ ] Is-it-a-vulnerability-at-all  [ ] n/a, no dispute raised
  What we sent them (repro, reachability trace, versions/flags, affected configs):
  What they told us (their threat model, deployment reality, why the path is unreachable):
  Live conversation offered (date) / held (date):
  Asked "what would change your mind", answer:
  Second opinion from outside the case team (name / date / conclusion):
  Outcome: [ ] They persuaded us -> close as not-a-vulnerability or plain bug; STOP HERE
           [ ] We persuaded them -> return to §5.1, offer help shipping the fix; STOP HERE
           [ ] Disagreement held after genuine attempt -> continue this record
  If closed in our favour: Finder informed (date):  CVE withdrawn / rejected / never reserved:
  Maintainer told of our intent to publish, with reasoning and date, before any third party (date):

Verbatim rationale in the advisory (§5.2):
  Offer made (date / channel):
  [ ] Declined (record only; do not re-ask)  [ ] Accepted
  Statement as it will be published (reproduce exactly; do not trim or paraphrase):

  Attribution: [ ] Named maintainer  [ ] Project / team  [ ] Unattributed
  Maintainer approved the final advisory wording in place (date):
  SIRT assessment published alongside (not in place of) the statement: [ ] Y

Downstream footprint (distros, registries, SBOM prevalence):
Decision: [ ] Advisory + VEX only  [ ] + downstream mitigation  [ ] Escalate to §6 MoLR
VEX fix_status set to:
Approver / date:
```
