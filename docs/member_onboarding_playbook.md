# Akrites — Member Onboarding Playbook

**Owner:** Akrites SIRT (with Linux Foundation program staff)
**Status:** Draft for Akrites SIRT review
**Audience:** Akrites staff who onboard people, and member organizations joining Akrites
**Companion docs:** [Glossary](Akrites_SIRT_CVD_Glossary.md) (member, member engineer, WG member, Akrites staff), [Read-In Policy](Akrites-Read-In-Policy.md), [Working Group Governance and Operations](Working_Group_Governance_and_Operations.md), [Communications Playbook](sirt-communications-playbook.md) (Play 21), [Metrics](Akrites_SIRT_Metrics.md)

---

## Purpose

This playbook explains how member organizations and their people are added to Akrites groups — which groups exist, who belongs in each, what to provide, and what each group gives access to.

**Onboarding is not read-in.** Joining any group below gives access to general Akrites communication only. Access to a case, or to a Working Group that handles case material, is granted separately and only through the [Read-In Policy](Akrites-Read-In-Policy.md).

### Terms used here

- **Member organization** — an organization that has joined Akrites. On its own, "member" means the organization.
- **Member engineer** — a person employed by a member organization, or its authorized and approved delegate.
- **Akrites staff** — Linux Foundation employees and contractors who run the program. The SIRT is staffed by Akrites staff.
- **LFX** — the Linux Foundation's internal tool where Akrites staff organize committees, mailing lists, and meetings. Each group below that is "onboarded through LFX" has its own committee, mailing list, and meeting series there.
- **Akrites Slack workspace** — the invite-only Slack workspace for Akrites discussion and announcements. General channels (such as `#all-akrites`) are joined at onboarding. **Case channels are separate:** each is created for a single case, and access is granted only through the [Read-In Policy](Akrites-Read-In-Policy.md). Slack is never used to report vulnerabilities — see [SECURITY.md](../SECURITY.md).

---

## 1. Groups at a glance

| Group | What it is | Who is in it | Onboarded through | What you get |
| --- | --- | --- | --- | --- |
| **Public** | The public Akrites resources | Anyone | No onboarding | The [SIRT GitHub repository](https://github.com/Akrites-Foundation/SIRT); monthly blog posts on [akrites.org](https://akrites.org) |
| **extended-sirt** | Committee and Mailing list in LFX | Named member engineers known to Akrites (board members and alternates only on request); Akrites staff | LFX | Monthly email updates; invitations to public Working Group meetings |
| **PSIRT Leads** | Committee, mailing list, Slack channel, and bi-monthly meeting for member organizations' Product Security Incident Response Team (PSIRT) leads | PSIRT leads and alternates; Akrites staff who work with them | Slack, LFX, GitHub | Bi-monthly PSIRT Leads meeting; access to designated repositories and Slack channels. Case discussion requires read-in. |
| **Premier Members - Governing Board** | The Governing Board | Each Premier member organization's designated board member and alternate; Akrites staff who support the board | LFX | Board meeting invitations; weekly updates on progress, metrics, and membership |
| **General Members** | Information for General members | *To be defined after the November 2026 board meeting* | — | — |
| **#all-akrites** | Slack channel | Named member engineers known to Akrites; interested non-members added by Akrites staff | Slack | General announcements and news. **No** Working Group meeting access |

---

## 2. Group details

### Public — no onboarding

Anyone can read the [SIRT GitHub repository](https://github.com/Akrites-Foundation/SIRT) and the monthly blog posts on [akrites.org](https://akrites.org). No access request is needed.

### extended-sirt

- **What it is:** the main Akrites mailing list and LFX committee.
- **Who is in it:** every named member engineer known to Akrites, and Akrites staff. Board members and alternates are added only if they ask.
- **Onboarded through:** LFX (committee and mailing list).
- **What you get:**
  - A monthly update by email.
  - Invitations to **public** Working Group meetings — Enablement or Practice WGs that handle no embargoed material ([WG Governance](Working_Group_Governance_and_Operations.md) §10). Private WGs, which hold case material, require WG membership through the Read-In Policy.

### PSIRT Leads

- **What it is:** the group for member organizations' PSIRT leads. (A PSIRT is an organization's team for receiving, investigating, fixing, and disclosing vulnerabilities in the products it ships.)
- **Who is in it:**
  - Each member organization's PSIRT lead and alternate.
  - Akrites staff who work with the PSIRT group, including program staff helping set up Working Groups.
- **Onboarded through:** the Akrites Slack workspace, LFX (committees, mailing lists, and meetings), and GitHub (repository access).
- **What to provide:** name, email, job title, company, and GitHub ID.
- **Meetings:** a bi-monthly PSIRT Leads meeting. Case-specific discussion happens only with people read in to that case.
- **What you get:**
  - Access to these repositories: *to be confirmed.*
  - Access to these Slack channels: *to be confirmed.*
  - **Case repositories are separate.** They are created per case, and access to each one is granted only through the Read-In Policy.

### Premier Members - Governing Board

- **What it is:** the Akrites Governing Board.
- **Who is in it:** the board member and alternate designated by each Premier member organization, and Akrites staff who support the board.
- **Onboarded through:** LFX (committees, mailing lists, and meetings). There is no Slack channel for the board.
- **What you get:** board meeting invitations, and weekly email updates on progress, metrics, and membership changes. Updates follow the [Metrics](Akrites_SIRT_Metrics.md) confidentiality gate — no live embargoed case detail.
- **Note:** membership level gives no additional access to case information.

### General members

Details will be set after the November 2026 board meeting.

### #all-akrites

- **What it is:** the general Slack channel `#all-akrites`.
- **Who is in it:** named member engineers known to Akrites, and interested people from organizations that have not yet joined, added by Akrites staff.
- **Onboarded through:** the Akrites Slack workspace.
- **What you get:** general news and announcements. **No** access to Working Group meetings.
- **Note:** the channel was busiest before Akrites launched and is used less now. Never post case information here.

---

## 3. Onboarding a new member organization

The member organization provides, through its Akrites staff contact:

- [ ] **Board representative and alternate** (Premier members) — for the Governing Board group.
- [ ] **PSIRT lead and alternate** — for the PSIRT Leads group, with name, email, job title, company, and GitHub ID.
- [ ] **Named member engineers** who should receive Akrites communication, and engineers available to work on cases — for extended-sirt and #all-akrites. Case work follows the Working Group nomination path below.

Akrites staff then onboard each person using the checklist in §5, and point anyone who will work on vulnerabilities to the Working Group nomination path ([WG Governance](Working_Group_Governance_and_Operations.md) §11) — WG membership and case access follow the [Read-In Policy](Akrites-Read-In-Policy.md).

## 4. Adding a person from an existing member organization

1. The member organization's PSIRT lead (or Akrites staff contact) sends the person's name, email, job title, company, GitHub ID (if needed), and the groups they need.
2. Akrites staff confirm the person works for, or is an approved delegate of, the member organization.
3. Akrites staff onboard the person using the checklist in §5.

---

## 5. Staff checklist — on-boarding  a new member or one person

Work through every step that applies to the person's groups (§1).

- [ ] **Roster** — add the company or person to the Akrites member roster: name, email, job title, company, member organization, GitHub ID (if provided), and the groups they belong to.
- [ ] **LFX committees** — add them to the LFX committee for each of their groups (for example, the Governing Board or PSIRT Leads).
- [ ] **LFX mailing lists** — subscribe them to each group's mailing list in LFX: **extended-sirt** for member engineers (board members and alternates only on request), and the group's own list for board and PSIRT Leads.
- [ ] **LFX meetings** — add them to each group's meeting series in LFX so they receive the invitations (board meetings, public Working Group meetings).
- [ ] **Slack** — invite them to the Akrites Slack workspace (not for board-only members), then add them to the channels for their groups: `#all-akrites`, and the PSIRT Leads channels for PSIRT leads.
- [ ] **GitHub** — for the PSIRT Leads group, add their GitHub ID to the designated repositories or team. **Do not** add anyone to a case repository; that happens only through read-in.
- [ ] **Welcome** — send the welcome email ([Communications Playbook](sirt-communications-playbook.md) Play 21).
- [ ] **Record** — note the date and the groups added on the roster entry.

---

## 6. Offboarding

- **A person leaves a member organization:** the member organization tells Akrites staff, who reverse the §5 checklist — remove the person from the roster's active list, LFX committees, mailing lists, and meetings, specific Slack channels (and the workspace, if they have no other reason to be there), and GitHub repositories or teams. Any case or Working Group access ends immediately (Read-In Policy §8, departure from the sponsoring organization).
- **A member organization leaves Akrites:** Akrites staff do the same for all of its people in member-only groups. Ongoing cases they are read in to are handled case by case by the SIRT case coordinator.
- **Periodic review:** Akrites staff check the roster, LFX lists, Slack, and GitHub against current membership at least once a year.
- **#all-akrites is open to guests,** so leaving a member organization does not remove someone from it. Staff remove them only if they are leaving the Slack workspace; otherwise they may leave the channel themselves.

---

## 7. Open items

- List the repositories and Slack channels the PSIRT Leads group can access.
- Define the General member group after the November 2026 board meeting.
- Set how long onboarding details (name, email, title, GitHub ID) are kept after someone leaves — part of the wider data-retention question for the Governing Board.
