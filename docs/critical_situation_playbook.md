# Akrites SIRT — Critical Situation (Crit-Sit) Playbook

**Owner:** Akrites SIRT
**Status:** Draft for Akrites SIRT review
**Audience:** SIRT Director, SIRT case coordinators, and Working Group members working a declared Crit-Sit
**Companion docs:** [CVD Policy](Akrites_CVD_Policy.md) (§8 embargo and TLP, §9 actively exploited vulnerabilities, §15 escalation), [Read-In Policy](Akrites-Read-In-Policy.md), [Intake Runbook](intake-runbook.md), [Communications Playbook](sirt-communications-playbook.md), [What Counts as Public Disclosure](what-counts-as-public-disclosure.md), [Maintainer of Last Resort Policy](Maintainer_of_Last_Resort_Policy.md)

---

## Purpose

This playbook defines the standard **Akrites Critical Situation (Crit-Sit)** incident response process. A Crit-Sit is a case serious enough that the SIRT stops handling it as routine coordinated disclosure and runs it as an incident — a named Incident Commander, fixed roles, a dedicated bridge, and a set status cadence.

A Crit-Sit is a **mode of the existing CVD lifecycle, not a separate process.** The CVD Policy, Read-In Policy, and MoLR Policy apply in full. This playbook adds only what changes during a Crit-Sit and points to the existing documents for everything else. Cases that are not declared a Crit-Sit follow the [Intake Runbook](intake-runbook.md) with the severity targets in CVD Policy §8.

---

## 1. Crit-Sit declaration and escalation

| Item | Crit-Sit |
| --- | --- |
| **Trigger criteria** | Confirmed active exploitation in the wild (CVD Policy §9); a supply-chain compromise — malicious release, compromised maintainer account or signing key (MoLR Policy Part II §4, *Suspect / Compromised*); a critical vulnerability that has broken, or is about to break, embargo with broad exposure (What Counts as Public Disclosure §5); or a critical vulnerability spanning many projects or vendors that needs one synchronized response. |
| **Declared by** | The **SIRT Director**, who also declares it closed. |
| **TLP handling** | Phased, per CVD Policy §8: **TLP:RED** at intake, **TLP:AMBER+STRICT** for remediation (Tiers 1, 1.5, 2), **TLP:AMBER** for downstream staging (Tiers 3, 3.5), **TLP:CLEAR** at Public Disclosure. |
| **Response timing** | Declaration as soon as a trigger is confirmed; actionable guidance to defenders within **7 days** of confirmed exploitation (CVD Policy §9). See §3. |
| **Read-in and escalation** | The SIRT case coordinator (as Incident Commander) approves every read-in under the Read-In Policy. The Director escalates to the Governing Board through Comms Play 19. |

**Not a Crit-Sit on its own:** a high severity score, or an unmaintained project, without one of the triggers above. An unmaintained project *with* a trigger is a Crit-Sit, and the MoLR Policy still governs any last-resort release.

Anyone working a case may ask the Director to consider a declaration. The Intake Runbook's "Escalate to the Akrites SIRT Director when…" triggers are the usual path.

---

## 2. Roles

| Role | Who | Responsibilities |
| --- | --- | --- |
| **SIRT Director** | SIRT Director | Declares and closes the Crit-Sit; decides high-impact timing calls; escalates to the Governing Board (CVD Policy §15). |
| **Incident Commander (IC)** | The SIRT case coordinator for the case | Runs the operational flow; owns the timeline and status cadence; **approves all read-ins** (Read-In Policy §6). |
| **Remediation Lead** | The upstream maintainer (Tier 1.5) or a Tier 1 WG analyst / patch author | Leads drafting and testing of the fix, privately. The maintainer keeps authority over the fix and release except where CVD Policy §9 requires acceleration. |
| **Scribe** | A SIRT staff member named by the IC | Keeps the [case read-in log](../templates/Akrites_ReadIn_Log_CASE.csv), Read-In Notice acknowledgements, the case timeline, and the current TLP state. Records read-ins; does **not** approve them. |
| **Comms Lead** | A SIRT staff member named by the IC | Runs communication with the Finder, upstream maintainers, and pre-notification partners using the Communications Playbook and the [notification templates](../templates/notification-templates.md). |

One person may hold more than one role in a small Crit-Sit, but the IC and the Scribe should be different people.

---

## 3. Timing

A Crit-Sit uses the commitments the SIRT already makes; it adds no new public SLAs.

| Step | Target | Source |
| --- | --- | --- |
| Automated intake and deduplication | Within 2 hours of receipt | CVD Policy §5 |
| Crit-Sit declaration | As soon as a trigger is confirmed | This playbook |
| Emergency read-in of an essential SME | Same day; temporary access lapses at 72 hours unless prerequisites are complete | Read-In Policy §3.1 |
| Actionable guidance (fix, mitigation, or workaround) | Within **7 days** of confirmed exploitation | CVD Policy §9 |
| Internal status updates | At least once per business day, or as the IC sets | This playbook |
| Read-out notice to all read-in parties | At Public Disclosure | This playbook (§4, Phase 4) |
| Read-in channels archived; material reclassified TLP:CLEAR | Within 72 hours of PD | Intake Runbook step 9 |
| Post-incident review | Scheduled within 72 hours of PD | This playbook; Comms Play 18 |

Where exploitation is not confirmed, the case keeps its CVD Policy §8 severity target (≤ 24 business days for Critical) and the IC drives toward the earliest safe date. A shorter timeline set by the project or a coordinating list always governs (CVD Policy §9).

---

## 4. Crit-Sit phases

The phases map to the nine-phase CVD lifecycle used in the Intake Runbook.

### Phase 1 — Declaration, deduplication & read-in control
*Lifecycle: Discover, Deduplicate & Triage. Timing: as soon as a trigger is confirmed.*

1. **Intake & dedupe.** Take in the finding (from a member, scanner, or external Finder) and merge duplicate reports into one canonical case ID (Intake Runbook step 2).
2. **Declare the Crit-Sit.** The SIRT Director records the declaration in the case record — case ID, trigger, time (UTC), and Incident Commander. Case material is **TLP:RED** at this stage (CVD Policy §8).
3. **Enforce read-in.**
   1. Restrict the case channel, bridge, and private advisory workspace to people on the case's read-in list. Being in the same company, WG, or Slack workspace is not being read in.
   2. Every participant accepts the [Case Read-In Notice](../templates/Akrites_Case_ReadIn_Notice_Template.md) before access is enabled, and the Scribe records it in the case read-in log.
4. **Mobilize core roles** (§2) and send the **Crit-Sit declaration** (Template A) to everyone already read in.

### Phase 2 — Triage, isolation & CVD window
*Lifecycle: Validate, Coordination.*

1. **Assess impact & score.** CVSS v4.0 (v3.1 for legacy comparison), exploitability (EPSS, CISA KEV), and dependency reach.
2. **Isolate the code environment.** Work only in private GitHub Security Advisories or the private case repository. **No public commits, pull requests, branches, or CI runs** — these are public disclosure (What Counts as Public Disclosure §3.1).
3. **Set the disclosure window.** Agree the PD date with the upstream maintainer, who decides except where CVD Policy §9 requires acceleration, and tell the Finder in writing when the upstream period starts (CVD Policy §7). For confirmed exploitation, actionable guidance is due within 7 days; otherwise the CVD Policy §8 severity target applies.
4. **Determine the maintainer track.** If the project is unmaintained or unresponsive, start the MoLR Policy contact ladder and continue Track A — advisory, mitigation, and downstream routing. A Crit-Sit does **not** shorten the 90-day abandonment floor, does not remove the need for Governing Board approval of a last-resort release, and never puts Akrites into the original project's namespace (MoLR Policy Part I §3–§4).

### Phase 3 — Siloed patch development & selective read-in
*Lifecycle: Patch, Test.*

1. **Upstream-first remediation.** Develop and test the patch for the original project and offer it to its maintainer — no forks. Remediation material is **TLP:AMBER+STRICT**.
2. **Selective read-in expansion.** Read in only those the fix needs, at the lowest sufficient tier (Read-In Policy §4–§5): analysts and patch authors at Tier 1, the upstream maintainer at Tier 1.5, testers at Tier 2. The IC approves each read-in; use Emergency Read-In (Read-In Policy §3.1) when an essential SME cannot wait for full prerequisites.
3. **Pre-notification.** Stage the fix with distribution partners (Tiers 2–3) and notify international coordinators (Tier 3.5, at most 24 hours before PD) using Notification Template 3; staging material is **TLP:AMBER**. Critical-infrastructure requests follow Comms Play 16, and government and coordinator engagement follows Comms Play 11 — **no single-government pre-disclosure**. Members receive situational awareness only, without case specifics (Comms Play 4).
4. **Prepare for an embargo break.** Have Notification Template 5 ready; if a break happens, follow What Counts as Public Disclosure §5 and Comms Play 6.

### Phase 4 — Synchronized release, CVE/VEX & public disclosure
*Lifecycle: Document, Distribute, Disclose.*

1. **Validate the patch.** Run the build matrix and regression tests before release.
2. **Publish upstream.** At the PD time, the maintainer publishes the fix in their own project. Akrites never publishes into the original project's namespace.
3. **Issue identifiers & advisories.** Publish the advisory, CVE (through the authoritative CNA, CVD Policy §2), OSV record, and VEX status together (Notification Template 4).
4. **Read out.** Send the **read-out notice** (Template B) to everyone on the read-in list. Access ends at PD or case close (Read-In Policy §8), and case material is reclassified TLP:CLEAR within 72 hours.

### Phase 5 — Post-incident review & ecosystem follow-up
*Timing: review scheduled within 72 hours of PD.*

1. **Post-incident review.** Run a blameless review (Comms Play 18): did the embargo hold, did read-in stay least-privilege, and what slowed the fix.
2. **Downstream monitoring.** Track patch adoption and help distributions integrate the fix (the MoLR Policy headline metric: known-affected consumers on a fixed version at 30 and 90 days).
3. **Process refinement.** Feed lessons into intake, deduplication, and triage.
4. **Close.** The SIRT Director declares the Crit-Sit closed in the case record.

---

## 5. Templates

Read-in records use the existing [case read-in log](../templates/Akrites_ReadIn_Log_CASE.csv) — set **Emergency Read-In (72h)** to Y where Read-In Policy §3.1 was used — and read-in acknowledgements use the [Case Read-In Notice](../templates/Akrites_Case_ReadIn_Notice_Template.md). The two templates below are specific to a Crit-Sit.

### Template A — Crit-Sit declaration and status update

> Send to the case's read-in list only. Use TLP:RED while only Tier 0 is read in; once Tier 1–2 participants are read in, mark updates TLP:AMBER+STRICT.

```
Subject: [TLP:RED] Crit-Sit declared — {case-id} — {component}

TLP:RED — Private vulnerability information. Share only with the read-in list for {case-id}.

Crit-Sit declared: {date/time UTC} by {SIRT Director}
Incident Commander: {name}   Scribe: {name}   Comms Lead: {name}
Bridge / workspace: {private link — read-in list only}
Affected component: {package} {version range}

1. Severity & ecosystem risk: {trigger}; CVSS {score}; exploitation {status}; exposure {scope}.
2. Remediation status: {private patch status / test results / maintainer engagement}.
3. Timeline: actionable guidance due {date}; target PD {date/time UTC}.
4. Actions & owners: {list}.

Next status update: {date/time UTC}
```

### Template B — Read-out notice

> Send at Public Disclosure to everyone who was on the read-in list.

```
Subject: [TLP:CLEAR] Read-out — {case-id} — {component} disclosed

{case-id} was publicly disclosed at {date/time UTC}: {advisory link}.

- The embargo has ended. Public information about this issue is now TLP:CLEAR.
- Non-public case material you received keeps its original TLP label — do not republish it.
- Your access to the case workspace and channels ends now (Read-In Policy §8). Delete local copies.
- A blameless post-incident review is scheduled for {date}; you may be invited to contribute.

Thank you for your work on this case.
— {Incident Commander}, Akrites SIRT
```

---

## 6. Open items

- Whether Crit-Sit response needs round-the-clock on-call coverage, and the staffing to support it.
- Whether a Crit-Sit is reported publicly as such (for example, in the periodic metrics) after disclosure.
