# Akrites SIRT Report Prioritization Process

**Status:** Draft v0.1 — for review by the SIRT Policy/Process subgroup  
**Owner:** Akrites SIRT Policy/Process subgroup  
**Scope:** Ordering validated vulnerability reports and assigning response capacity

---

## Purpose

This process gives the Akrites SIRT a consistent, explainable way to decide **what should be worked
next** when more than one vulnerability report needs attention.

Prioritization is not severity scoring and is not a judgment about the value of a Finder. It is an
operational decision that combines the vulnerability's potential impact, the available exploit
evidence, attacker prerequisites, affected scope, coordination constraints, and queue age.

Every queue position should have an auditable answer to: **Why is this case being worked now?**

## Guiding principles

- **Reduce harm first.** Active exploitation, imminent public exposure, and credible high-impact
  attack paths receive the fastest response.
- **Report source selects the validation path, not the priority.** Trusted and complete reports may
  require less validation effort, but member affiliation or reporter identity does not make a
  vulnerability more important.
- **Severity, exploit state, and priority remain separate.** Severity describes the vulnerability;
  exploit state describes the evidence; priority describes what the SIRT should do next.
- **No opaque composite score.** The SIRT records the factors and the reason for the selected band
  rather than hiding unlike signals inside one number.
- **Missing information is not low risk.** An incomplete report moves to `NEEDS-INFO`; it is not
  silently treated as low severity or left to starve.
- **Deduplicate conservatively.** Merge case handling only when reports share the same root cause
  and expected fix. Preserve every source report and co-Finder attribution.
- **Reassess as evidence changes.** Priority is a current operational judgment, not a permanent
  property of a vulnerability.
- **Respect confidentiality.** Queue views and rationale must not expose embargoed details beyond
  the case's authorized read-in group.

## Relationship to other SIRT decisions

The SIRT makes four related but distinct decisions:

| Decision | Question | Output |
|---|---|---|
| Validation | Is the report reproducible, in scope, and sufficiently evidenced? | Validation state and evidence gaps |
| Severity | How serious is the vulnerability under the documented assumptions? | SIRT severity assessment and vector |
| Exploit state | What evidence exists that the vulnerability can or is being exploited? | Active, demonstrated, PoC, theoretical, or unknown |
| Priority | What response pace and queue position does this case need now? | Response band, owner, next action, and due date |

The severity methodology is defined separately. This process consumes its result without replacing
it.

Use a controlled exploit-state vocabulary:

- **Active:** exploitation has been observed against real targets.
- **Demonstrated:** the attack has been independently executed against an affected target with the
  claimed impact.
- **PoC:** exploit code or reproduction material exists but has not yet been independently
  validated by the SIRT.
- **Theoretical:** the attack path is reasoned from the code or design without a working PoC.
- **Unknown:** available evidence does not support a classification.

## Prioritization flow

Apply these steps in order:

1. **Acknowledge and protect the report.** Apply the appropriate confidentiality handling and record
   any indication that the issue is already public or actively exploited.
2. **Check for duplicates.** Compare stable identity fields and the technical root cause. Link
   possible matches for human review; do not auto-merge uncertain cases.
3. **Validate or identify gaps.** Confirm the affected project and version, reproduction, impact,
   and scope as far as the available evidence permits.
4. **Record severity and exploit state separately.** Preserve assumptions, confidence, and unknowns.
5. **Assign the highest applicable response band.** Use the definitions below.
6. **Order cases within the band.** Apply the tie-break factors in order and record the rationale.
7. **Assign an owner and next action.** A band without ownership and a dated next action is not an
   operational decision.
8. **Reassess on every material change.** Promote or demote the case with a dated reason.

## Response bands

The highest applicable band wins. Report source is never a band criterion.

### `INCIDENT`

Use when immediate coordination is required to reduce current or imminent harm.

Typical triggers:

- confirmed or strongly credible active exploitation;
- the vulnerability is already publicly actionable before a fix is available;
- an embargo has broken or sensitive technical detail is credibly exposed;
- a credible attack can cause severe, widespread harm with low attacker prerequisites;
- a hard external deadline makes delay materially more dangerous.

Operational expectation:

- notify the SIRT lead or on-call path immediately;
- assign a case owner and establish the next coordination action the same business day;
- reassess at least daily while incident conditions remain.

### `URGENT`

Use for confirmed vulnerabilities that are not current incidents but need accelerated staffing.

Typical triggers:

- high or critical technical impact with demonstrated exploitability or a working PoC;
- low attacker prerequisites or a broadly reachable vulnerable path;
- substantial affected scope or critical ecosystem dependency;
- a maintainer release window or coordinated disclosure deadline requires prompt action;
- delay would materially increase likely consumer harm.

Operational expectation:

- assign an owner within one business day;
- establish a dated validation, maintainer-engagement, or remediation action;
- reassess whenever exploit, scope, or coordination evidence changes.

### `STANDARD`

Use for confirmed, actionable vulnerabilities without incident or urgent-response signals.

Typical cases:

- exploitation is theoretical, unknown, or requires significant prerequisites;
- impact or affected scope is limited;
- coordination can proceed through the normal SIRT lifecycle without increasing likely harm.

Operational expectation:

- assign ownership through normal capacity planning;
- record the next action no later than the initial-assessment target;
- apply queue-aging checks so older cases cannot be displaced indefinitely by new arrivals.

### `NEEDS-INFO`

Use when the SIRT cannot yet validate or prioritize the report because required evidence is missing.

Typical gaps:

- affected project, component, or version is unclear;
- reproduction steps or PoC evidence are insufficient;
- impact, attacker prerequisites, or affected scope cannot be determined;
- the report may be a duplicate but the root cause cannot yet be compared safely.

Operational expectation:

- send a specific evidence request rather than a generic rejection;
- identify the owner of the follow-up and the date for the next review;
- immediately re-enter prioritization when the missing evidence arrives;
- escalate aging cases for a human decision instead of treating silence as low risk.

`NEEDS-INFO` is a workflow state, not a severity label.

## Ordering within a band

When two cases share a band, compare these factors in order. Stop when one case has a clear,
documented reason to move first:

1. **Public exposure or active exploitation**
2. **Exploit evidence:** demonstrated attack before standalone PoC, before theoretical or unknown
3. **Technical impact and reversibility of harm**
4. **Attacker prerequisites, reachability, and required privileges**
5. **Affected scope and ecosystem criticality**
6. **Coordination constraint:** maintainer release window, embargo deadline, or dependency between cases
7. **Queue age and prior deferrals**

Pervasiveness or dependency count may inform affected scope, but does not override exploit evidence,
attacker prerequisites, or technical impact by itself.

If the factors remain materially equal, the older case moves first.

## Treatment of report source

Source affects how validation is performed:

- a trusted working group or security team may supply evidence that can be verified more quickly;
- an anonymous or first-time Finder may need additional reproduction and identity-independent
  validation;
- every source remains subject to technical verification;
- source affiliation must not override the response-band criteria.

For example, an anonymous public report with a reproducible unauthenticated remote-code-execution
PoC should outrank a complete member report describing a theoretical, low-impact issue.

## Duplicate and co-Finder handling

Deduplication happens before final queue placement.

- Treat reports as the same case only when they share the same underlying root cause and expected
  remediation.
- Keep near matches separate when uncertainty remains. Over-merging can hide a distinct
  vulnerability; under-merging creates visible extra work that can be corrected later.
- Preserve every source report, submission time, evidence contribution, and attribution preference.
- The coordinated case inherits the highest response band justified by any linked report's
  evidence.
- New duplicate reports can change exploit state, affected scope, confidence, or exposure status
  and therefore require reprioritization.

## Required case record

Each prioritized case records:

- validation state and unresolved evidence gaps;
- duplicate/canonical-case links and co-Finder records;
- SIRT severity assessment and its assumptions;
- exploit state and supporting evidence;
- response band and concise rationale;
- owner, next action, and due date;
- affected scope and known attacker prerequisites;
- coordination or disclosure deadline, if any;
- date last assessed and reason for the latest change;
- confidentiality/read-in restrictions.

Avoid including sensitive exploit detail in a general queue view. Link to the authorized case record
instead.

## Reassessment triggers

Re-run prioritization when:

- exploitation is observed, reproduced, or disproved;
- vulnerability details become public or an embargo may have broken;
- affected versions, reachability, impact, or prerequisites change;
- a maintainer confirms a release window or requests a different coordination timeline;
- missing evidence arrives;
- a duplicate or independent Finder adds material evidence;
- a case misses its next-action date or remains unowned;
- capacity changes would otherwise cause repeated deferral.

Do not lower a case's band merely because the SIRT lacks capacity. Record and escalate the capacity
gap.

## Escalation and disagreements

- Any participant may request reprioritization by providing new evidence or identifying an incorrect
  assumption.
- The SIRT lead resolves unresolved band disagreements and records the decision rationale.
- An unowned `INCIDENT`, a missed incident action, or a suspected embargo break is escalated
  immediately.
- Repeatedly deferred `STANDARD` and `NEEDS-INFO` cases receive an explicit aging review rather than
  remaining indefinitely open.

## Operational metrics

Use prioritization metrics to find process problems, not to reward volume:

- count and age of cases by band;
- time to owner and time to first material action;
- missed next-action dates;
- number and reason for promotions or demotions;
- aging and repeated deferrals;
- duplicate candidates, confirmed duplicates, and reversed merges;
- capacity versus demand by band.

Apply the SIRT metrics confidentiality gate before sharing any aggregated queue data outside the
authorized audience.

## Open decisions for ratification

- Confirm the response-band names and operational targets.
- Define the SIRT lead/on-call escalation path.
- Align the severity input with the result of
  [issue #32](https://github.com/Akrites-Foundation/SIRT/issues/32).
- Confirm the queue-aging review cadence.
- Decide which fields are visible in the general queue versus only in the read-in case record.

---

*This document implements the process tracked in
[issue #26](https://github.com/Akrites-Foundation/SIRT/issues/26). Propose changes through pull
requests and SIRT Policy/Process review.*
