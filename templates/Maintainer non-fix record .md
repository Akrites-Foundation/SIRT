# Maintainer non-fix record (template)

*Per [MoLR Policy](../docs/Maintainer_of_Last_Resort_Policy.md) Part I §2 and Part II §4 (Deliberate Non-Fix).*

```
Case ID / CVE:
Maintainer's first response (verbatim quote + link):
Date / source:

STEP 1 -- Technical disagreement on the merits (Part I §2). Complete before anything below.
  Nature of the disagreement: [ ] Threat model  [ ] Reachability  [ ] Severity / exploitability
                              [ ] Is-it-a-vulnerability-at-all  [ ] n/a, no dispute raised
  What we sent them (repro, reachability trace, versions/flags, affected configs):
  What they told us (their threat model, deployment reality, why the path is unreachable):
  Live conversation offered (date) / held (date):
  Asked "what would change your mind", answer:
  Second opinion from outside the case team (name / date / conclusion):
  Outcome:
    [ ] They persuaded us -> close as not-a-vulnerability or plain bug. STOP HERE.
          Finder informed (date):
          CVE withdrawn / rejected / never reserved:
    [ ] We persuaded them -> return to Track A (Part II §1.2), offer help shipping the fix. STOP HERE.
    [ ] Disagreement held after a genuine attempt -> continue below.
    [ ] No dispute was raised; maintainer directly declined (EOL / feature-complete) -> continue below.
  Maintainer told of our intent to publish, with reasoning and date, before any third party (date):

STEP 2 -- Non-fix classification (Part II §1.1, condition 2). Reachable via either "continue below" outcome above.
Type: [ ] Formal EOL  [ ] Feature-complete  [ ] WONTFIX-on-merits
Maintainer's final position (verbatim quote + link):
Stated rationale:

Verbatim rationale in the advisory (Part I §2):
  Offer made (date / channel):
  [ ] Declined (record only; do not re-ask)  [ ] Accepted
  Statement as it will be published (reproduce exactly; do not trim or paraphrase):

  Attribution: [ ] Named maintainer  [ ] Project / team  [ ] Unattributed
  Maintainer approved the final advisory wording in place (date):
  SIRT assessment published beside the statement rather than around it: [ ] Y

Downstream footprint (distros, registries, SBOM prevalence):
Decision: [ ] Advisory + VEX only  [ ] + downstream mitigation  [ ] Escalate to Track B MoLR (Part II §5)
VEX fix_status set to:
Approver / date:
```
