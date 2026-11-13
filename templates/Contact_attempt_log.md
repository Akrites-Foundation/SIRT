# Contact attempt log (template)

*One log per case. Record every attempt to reach the upstream maintainer, as it happens. The log is what M1 quotes to the maintainer and what the MoLR case issue links to, so write it as if the maintainer will read it.*

*Timings come from the [MoLR Policy](../docs/Maintainer_of_Last_Resort_Policy.md#31-disclosure-clock-contact--escalation) (contact ladder) and [Part I §4](../docs/Maintainer_of_Last_Resort_Policy.md#4-90-day-silence-floor) (abandonment floor). This log doesn't restate them.*

```
Case ID:
Project / affected versions:
Advisory / CVE:
T0 (first attempt):
```

## Attempts

| # | Date | Channel | Address / handle | What we sent | Outcome |
| --- | --- | --- | --- | --- | --- |
| 1 | | `SECURITY.md` / PVR / security email | | Private report | No reply / bounced / read / replied |
| 2 | | Commit-history emails, registry contacts | | Re-send | |
| 3 | | Umbrella org, foundations, distro security teams | | Escalation | |
| 4 | | Coordinator (CERT/CC, VINCE, CNA-LR) | | Hand-off | |
| | | | | | |

**Outcome values:** `no reply` · `bounced` · `read, no reply` · `replied` (link the reply). Any reply moves the case back to normal coordination.

## Signs of life

Any commit, comment, release, or registry login after T0 restarts the abandonment floor. Record it here with the new start date.

| Date | Where | What | Floor restarts on |
| --- | --- | --- | --- |
| | | | |

## Carry the fix?

Who we asked to carry the fix (distributions, downstream projects, intermediate maintainers) and what they said.

| Date | Party | Answer |
| --- | --- | --- |
| | | |

## Summary for the case issue

```
Attempts: <n> between <first date> and <last date>
Abandonment floor reached: <date>   (or: n/a — end-of-life refusal, see non-fix record)
Third-party log used (Policy Part II §3.2): <no | yes, from <member>, attached>
Declined to carry the fix: <parties>
Logged by:
```
