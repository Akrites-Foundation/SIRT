# Member Onboarding and Offboarding Procedure

**Type:** Procedure
**Approver:** SIRT Director
**Formerly titled:** Member Onboarding Playbook
**Owner:** Akrites SIRT (with Linux Foundation program staff)
**Status:** Draft for Akrites SIRT review
**Audience:** Akrites staff who onboard people, and member organizations joining Akrites
**Companion docs:** [Glossary](../reference/glossary.md) (member, member engineer, Akrites staff), [Read-In Policy](../policies/read-in-policy.md), [Communications Playbook](../playbooks/communications-playbook.md) (Play 21), [Metrics](../reference/metrics-framework.md)

---

## Purpose

This playbook explains how member organizations and their people are added to Akrites — which groups exist, who belongs in each, what to provide, and what Slack channels and GitHub access each person gets.

**Onboarding is not read-in.** Onboarding gives access to general Akrites communication only. Access to a case, and to the channels and repositories that carry case material, is granted separately and only through the [Read-In Policy](../policies/read-in-policy.md).

### Terms used here

- **Member organization** — an organization that has joined Akrites. On its own, "member" means the organization.
- **Member engineer** — a person employed by a member organization, or its authorized and approved delegate.
- **Read-In member engineer** — a member engineer who has been read in under the [Read-In Policy](../policies/read-in-policy.md).
- **Akrites staff** — Linux Foundation employees and contractors who run the program. The SIRT is staffed by Akrites staff.
- **LFX** — the Linux Foundation's internal tool where Akrites staff organize committees, mailing lists, and meetings. Each group below that is "onboarded through LFX" has its own committee, mailing list, and meeting series there.
- **Akrites Slack workspace** — the invite-only Slack workspace for Akrites discussion and announcements. Slack is never used to report vulnerabilities — see [SECURITY.md](../../SECURITY.md).

---

## 1. Groups at a glance

| Group | What it is | Who is in it | Onboarded through | What you get |
| --- | --- | --- | --- | --- |
| **Public** | The public Akrites resources | Anyone | No onboarding | The [SIRT GitHub repository](https://github.com/Akrites-Foundation/SIRT); monthly blog posts on [akrites.org](https://akrites.org) |
| **Member engineers** (extended-sirt) | LFX committee and mailing list | Named member engineers known to Akrites (board members and alternates only on request); Akrites staff | LFX, Slack, GitHub | Monthly email updates; `#all-akrites`; GitHub ID added to the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation) |
| **PSIRT Leads** | Committee, mailing list, Slack channels, and bi-monthly meeting for member organizations' Product Security Incident Response Team (PSIRT) leads | PSIRT leads and alternates; Akrites staff who work with them | LFX, Slack, GitHub | Bi-monthly PSIRT Leads meeting; `#all-akrites`, `#psirt-leads`, `#sirt-disclosures`; GitHub ID added to the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation) |
| **Premier Members - Governing Board** | The Governing Board | Each Premier member organization's designated board member and alternate; Akrites staff who support the board | LFX, Slack | Board meeting invitations; weekly updates on progress, metrics, and membership; `#all-akrites` |
| **General Members** | Information for General members | *To be defined after the November 2026 board meeting* | — | — |

## 2. Slack channel access

Everyone onboarded to Akrites is invited to the Akrites Slack workspace and `#all-akrites`. Accepting the invite is optional and up to each person. Further channels depend on role.

| Channel | Who gets access | When |
| --- | --- | --- |
| `#all-akrites` | Everyone onboarded (member engineers, PSIRT leads, board members, Akrites staff); interested non-members added by Akrites staff | At onboarding |
| `#psirt-leads` | PSIRT leads and alternates; Akrites staff who work with them | At onboarding |
| `#sirt-disclosures` | PSIRT leads and alternates; Akrites staff who work with them | At onboarding |
| `#sirt-ops-eng` | Read-In member engineers; Akrites SIRT staff | After read-in, through the [Read-In Policy](../policies/read-in-policy.md) — never at onboarding |

**Case channels are separate.** Each is created for a single case, and access is granted only through the Read-In Policy. Never post case information in `#all-akrites`.

## 3. GitHub access

- **Member engineers** (including PSIRT leads) have their GitHub ID added to the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation) at onboarding.
- **Case repositories are separate.** They are created per case, and access to each one is granted only through the Read-In Policy. Onboarding never adds anyone to a case repository.

---

## 4. Group details

### Public — no onboarding

Anyone can read the [SIRT GitHub repository](https://github.com/Akrites-Foundation/SIRT) and the monthly blog posts on [akrites.org](https://akrites.org). No access request is needed.

### Member engineers (extended-sirt)

- **What it is:** the main Akrites mailing list and LFX committee.
- **Who is in it:** every named member engineer known to Akrites, and Akrites staff. Board members and alternates are added only if they ask.
- **Onboarded through:** LFX (committee and mailing list), the Akrites Slack workspace, and GitHub.
- **What to provide:** name, email, job title, company, and GitHub ID.
- **What you get:**
  - A monthly update by email.
  - `#all-akrites` on Slack.
  - GitHub ID added to the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation).
  - Once read in, `#sirt-ops-eng` (see §2).

### PSIRT Leads

- **What it is:** the group for member organizations' PSIRT leads. (A PSIRT is an organization's team for receiving, investigating, fixing, and disclosing vulnerabilities in the products it ships.)
- **Who is in it:**
  - Each member organization's PSIRT lead and alternate.
  - Akrites staff who work with the PSIRT group.
- **Onboarded through:** LFX (committees, mailing lists, and meetings), the Akrites Slack workspace, and GitHub.
- **What to provide:** name, email, job title, company, and GitHub ID.
- **Meetings:** a bi-monthly PSIRT Leads meeting. Case-specific discussion happens only with people read in to that case.
- **What you get:**
  - Slack: `#all-akrites`, `#psirt-leads`, and `#sirt-disclosures`.
  - GitHub ID added to the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation).

### Premier Members - Governing Board

- **What it is:** the Akrites Governing Board.
- **Who is in it:** the board member and alternate designated by each Premier member organization, and Akrites staff who support the board.
- **Onboarded through:** LFX (committees, mailing lists, and meetings) and an invitation to the Akrites Slack workspace (`#all-akrites` only; there is no board channel). Accepting is optional.
- **What you get:** board meeting invitations, weekly email updates on progress, metrics, and membership changes, and `#all-akrites`. Updates follow the [Metrics](../reference/metrics-framework.md) confidentiality gate — no live embargoed case detail.
- **Note:** membership level gives no additional access to case information.

### General members

Details will be set after the November 2026 board meeting.

---

## 5. Onboarding a new member organization

The member organization provides, through its Akrites staff contact:

- [ ] **Board representative and alternate** (Premier members) — for the Governing Board group.
- [ ] **PSIRT lead and alternate** — for the PSIRT Leads group, with name, email, job title, company, and GitHub ID.
- [ ] **Named member engineers** who should receive Akrites communication or work on cases — with name, email, job title, company, and GitHub ID.

Akrites staff then onboard each person using the checklist in §7. Anyone who will work on cases is read in separately under the [Read-In Policy](../policies/read-in-policy.md), which is also when they are added to `#sirt-ops-eng`.

## 6. Adding a person from an existing member organization

1. The member organization's PSIRT lead (or Akrites staff contact) sends the person's name, email, job title, company, GitHub ID, and the groups they need.
2. Akrites staff confirm the person works for, or is an approved delegate of, the member organization.
3. Akrites staff onboard the person using the checklist in §7.

---

## 7. Staff checklist — onboarding a new member organization or new member

Work through every step that applies to the person's groups (§1).

- [ ] **Roster** — add the company or person to the Akrites member roster: name, email, job title, company, member organization, GitHub ID, and the groups they belong to.
- [ ] **LFX committees** — add them to the LFX committee for each of their groups (for example, the Governing Board or PSIRT Leads).
- [ ] **LFX mailing lists** — subscribe them to each group's mailing list in LFX: **extended-sirt** for member engineers (board members and alternates only on request), and the group's own list for board and PSIRT Leads.
- [ ] **LFX meetings** — add them to each group's meeting series in LFX so they receive the invitations (board meetings, PSIRT Leads meetings).
- [ ] **Slack** — invite them to the Akrites Slack workspace and `#all-akrites` (accepting is up to them). For PSIRT leads, also add `#psirt-leads` and `#sirt-disclosures`. **Do not** add anyone to `#sirt-ops-eng` or a case channel at onboarding; that happens only through read-in.
- [ ] **GitHub** — for member engineers and PSIRT leads, add their GitHub ID to the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation). **Do not** add anyone to a case repository; that happens only through read-in.
- [ ] **Welcome** — send the welcome email ([Communications Playbook](../playbooks/communications-playbook.md) Play 21).
- [ ] **Record** — note the date and the groups, channels, and repo access added on the roster entry.

---

## 8. SIRT operations onboarding

Administrative onboarding (§5–§7) gives a member engineer general Akrites communication only. Before a member engineer can start vulnerability triage and review, they must also complete SIRT operations onboarding. This step is separate from administrative onboarding and is run by Akrites SIRT staff.

### 8.1 Requirements

A member engineer is ready for SIRT operations onboarding when all of the following are true:

- [ ] They have been administratively onboarded (§7 checklist complete).
- [ ] They have been read in under the [Read-In Policy](../policies/read-in-policy.md). Read-in is what grants access to `#sirt-ops-eng` and to the repositories that carry case material.
- [ ] Akrites SIRT staff have confirmed which repositories and issues they will work on, based on their skills and capacity.

### 8.2 What the SIRT provides

Once the requirements are met, Akrites SIRT staff provide the engineer with:

1. **A Getting Started guide** (template in §8.3) that explains the workflow, work packages, timelines, and scope.
2. **A prioritized issue list** matched to the engineer's skills and capacity.
3. **Access to the specific repositories** for those issues, granted through the [Read-In Policy](../policies/read-in-policy.md), so that triage can begin.

The SIRT is the engineer's main contact. Engineers can reach their SIRT contact directly on Slack, or engage the wider team in the `#sirt-ops-eng` channel.

### 8.3 Getting Started guide template

SIRT staff send the guide below, filling in the engineer's name and the prioritized issue list.

---

> Welcome, `<engineer name>`.
>
> This guide covers how to get started, and a prioritized list of issues for your review is attached. You can reach me directly on Slack, or engage the Akrites SIRT in the [#sirt-ops-eng](https://akritesfoundation.slack.com/archives/C0CDZ3DGP7D) channel. Thank you for your help, and welcome aboard.
>
> #### Getting started
>
> **Process and scope.** Read the full workflow in the [Lightweight CVD Process Documentation](github-fallback-case-handling-procedure.md). Each issue (ACT-) should already contain an automated severity assessment, a candidate patch, and a draft report. Your main task is human verification, organized into four work packages:
>
> | Work package | Focus | What you do |
> |---|---|---|
> | **A. Severity verification** | Is the finding real, and how bad is it? | Verify reachability, the vulnerability, CVSS, CWE, and affected versions. |
> | **B. Patch review** | Does the candidate fix work? | Check the candidate patch for fix completeness, buildability, and regressions. |
> | **C. Report review** | Is the draft report ready to send? | Review the maintainer draft report for accuracy, formatting, and compliance. |
> | **D. Fix authoring** | No usable patch exists. | Write a minimal, production-grade fix with regression tests. |
>
> **Target timelines**
>
> | Work package | Target |
> |---|---|
> | A, B, C | Complete within 2 business days. |
> | D | Complete within 5 business days. Escalate blockers to Akrites within 1 business day. |
>
> **Out of scope.** Akrites SIRT handles all upstream communication. Please do not:
>
> - Contact maintainers directly.
> - Make public disclosures.
> - Assign CVEs independently.
> - Submit to bug bounty programs.
>
> **Extra capacity.** If you have additional bandwidth, you can assess other non-prioritized issues in your assigned repositories. Findings can be bundled into the upstream report through the SIRT.

---

### 8.4 Staff checklist: SIRT operations onboarding

- [ ] **Confirm prerequisites.** Administrative onboarding (§7) is complete and the engineer is read in under the [Read-In Policy](../policies/read-in-policy.md).
- [ ] **Assess fit.** Identify the engineer's skills and capacity, and choose the repositories and issues that match.
- [ ] **Grant access.** Through the Read-In Policy, give the engineer access to the specific repositories for their issues, and add them to `#sirt-ops-eng` if not already done at read-in.
- [ ] **Build the prioritized issue list.** Rank the issues for the engineer.
- [ ] **Send the Getting Started guide.** Use the §8.3 template with the engineer's name and issue list.
- [ ] **Add to the SIRT Internal Dashboard.** Add the engineer to the dashboard so SIRT staff can manage and track their activity.

### 8.5 Offboarding and changes

- When the engineer's read-in ends, or they leave the member organization, staff remove their repository access and `#sirt-ops-eng` membership as described in §9.
- If the engineer's repositories or issues change, SIRT staff update their access and send a revised issue list.

---

## 9. Offboarding

- **A person leaves a member organization:** the member organization tells Akrites staff, who reverse the §7 checklist — remove the person from the roster's active list, LFX committees, mailing lists, and meetings, member-only Slack channels (`#psirt-leads`, `#sirt-disclosures`, `#sirt-ops-eng`, and the workspace if they have no other reason to be there), and the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation). Any case access ends immediately (Read-In Policy §8, departure from the sponsoring organization).
- **A read-in ends:** when a member engineer is no longer read in, Akrites staff remove them from `#sirt-ops-eng`.
- **A member organization leaves Akrites:** Akrites staff do the same for all of its people in member-only groups. Ongoing cases they are read in to are handled case by case by the SIRT case coordinator.
- **Periodic review:** Akrites staff check the roster, LFX lists, Slack channels, and GitHub access against current membership at least once a year.
- **#all-akrites is open to guests,** so leaving a member organization does not remove someone from it. Staff remove them only if they are leaving the Slack workspace; otherwise they may leave the channel themselves.

---

## 10. Open items

- Define the General member group after the November 2026 board meeting.
- Set how long onboarding details (name, email, title, GitHub ID) are kept after someone leaves — part of the wider data-retention question for the Governing Board.
