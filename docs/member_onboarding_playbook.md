# Akrites — Member Onboarding Playbook

**Owner:** Akrites SIRT (with Linux Foundation program staff)
**Status:** Draft for Akrites SIRT review
**Audience:** Akrites staff who onboard people, and member organizations joining Akrites
**Companion docs:** [Glossary](Akrites_SIRT_CVD_Glossary.md) (member, member engineer, Akrites staff), [Read-In Policy](Akrites-Read-In-Policy.md), [Communications Playbook](sirt-communications-playbook.md) (Play 21), [Metrics](Akrites_SIRT_Metrics.md)

---

## Purpose

This playbook explains how member organizations and their people are added to Akrites — which groups exist, who belongs in each, what to provide, and what Slack channels and GitHub access each person gets.

**Onboarding is not read-in.** Onboarding gives access to general Akrites communication only. Access to a case, and to the channels and repositories that carry case material, is granted separately and only through the [Read-In Policy](Akrites-Read-In-Policy.md).

### Terms used here

- **Member organization** — an organization that has joined Akrites. On its own, "member" means the organization.
- **Member engineer** — a person employed by a member organization, or its authorized and approved delegate.
- **Read-In member engineer** — a member engineer who has been read in under the [Read-In Policy](Akrites-Read-In-Policy.md).
- **Akrites staff** — Linux Foundation employees and contractors who run the program. The SIRT is staffed by Akrites staff.
- **LFX** — the Linux Foundation's internal tool where Akrites staff organize committees, mailing lists, and meetings. Each group below that is "onboarded through LFX" has its own committee, mailing list, and meeting series there.
- **Akrites Slack workspace** — the invite-only Slack workspace for Akrites discussion and announcements. Slack is never used to report vulnerabilities — see [SECURITY.md](../SECURITY.md).

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
| `#sirt-ops-eng` | Read-In member engineers; Akrites SIRT staff | After read-in, through the [Read-In Policy](Akrites-Read-In-Policy.md) — never at onboarding |

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
- **What you get:** board meeting invitations, weekly email updates on progress, metrics, and membership changes, and `#all-akrites`. Updates follow the [Metrics](Akrites_SIRT_Metrics.md) confidentiality gate — no live embargoed case detail.
- **Note:** membership level gives no additional access to case information.

### General members

Details will be set after the November 2026 board meeting.

---

## 5. Onboarding a new member organization

The member organization provides, through its Akrites staff contact:

- [ ] **Board representative and alternate** (Premier members) — for the Governing Board group.
- [ ] **PSIRT lead and alternate** — for the PSIRT Leads group, with name, email, job title, company, and GitHub ID.
- [ ] **Named member engineers** who should receive Akrites communication or work on cases — with name, email, job title, company, and GitHub ID.

Akrites staff then onboard each person using the checklist in §7. Anyone who will work on cases is read in separately under the [Read-In Policy](Akrites-Read-In-Policy.md), which is also when they are added to `#sirt-ops-eng`.

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
- [ ] **Welcome** — send the welcome email ([Communications Playbook](sirt-communications-playbook.md) Play 21).
- [ ] **Record** — note the date and the groups, channels, and repo access added on the roster entry.

---

## 8. Offboarding

- **A person leaves a member organization:** the member organization tells Akrites staff, who reverse the §7 checklist — remove the person from the roster's active list, LFX committees, mailing lists, and meetings, member-only Slack channels (`#psirt-leads`, `#sirt-disclosures`, `#sirt-ops-eng`, and the workspace if they have no other reason to be there), and the [Akrites-Foundation GitHub organization](https://github.com/Akrites-Foundation). Any case access ends immediately (Read-In Policy §8, departure from the sponsoring organization).
- **A read-in ends:** when a member engineer is no longer read in, Akrites staff remove them from `#sirt-ops-eng`.
- **A member organization leaves Akrites:** Akrites staff do the same for all of its people in member-only groups. Ongoing cases they are read in to are handled case by case by the SIRT case coordinator.
- **Periodic review:** Akrites staff check the roster, LFX lists, Slack channels, and GitHub access against current membership at least once a year.
- **#all-akrites is open to guests,** so leaving a member organization does not remove someone from it. Staff remove them only if they are leaving the Slack workspace; otherwise they may leave the channel themselves.

---

## 9. Open items

- Define the General member group after the November 2026 board meeting.
- Set how long onboarding details (name, email, title, GitHub ID) are kept after someone leaves — part of the wider data-retention question for the Governing Board.
