# Akrites Case Read-In Notice — TEMPLATE

> **How to use.** The SIRT case lead completes the fields in `{{…}}` and the read-in list in §2, then sends this to the person being read in (email, the case mailing list, or as the pinned first message in the case Slack channel and GitHub repo). Delete this instruction block before sending.

---

**You are being read into a restricted vulnerability case.** You have passed verification confirming you have expertise relevant to this disclosure and that you are able to contribute.  Please read this notice in full before taking any action. Your continued participation confirms your agreement to the terms below.

*Please reply to this message, acknowledging receipt of this email so that your provisioning to the team resources listed below can be completed.  Please also include your GitHub ID so you can be added to any associated private repositories this group will be using.*

| Field | Detail |
|---|---|
| **Case ID** | {{CASE_ID}} |
| **Read-in recipient** | {{NAME}} |
| **Sponsoring organization** | {{ORG}} |
| **Your role in this case** | {{ROLE — SIRT ·KNOWER · analyze / produce patch · test patch · stage patch}} |
| **Your tier** | {{TIER 0/1/2/3}} |
| **Read-in date** | {{DATE}} |
| **Embargo / public disclosure target** | {{PD_DATE}} |
| **Access expires** | At public disclosure or case close |
| **SIRT case lead (your point of contact)** | {{LEAD_NAME}} — {{LEAD_CONTACT}} |

**What this case concerns (brief, need-to-know only):** 
{{ONE_LINE_SCOPE}}

---

## 1. Data classification — Traffic Light Protocol (TLP)

This case is governed by the **FIRST Traffic Light Protocol (TLP 2.0)**. Every piece of case information carries a TLP label that tells you exactly how far you may share it. **When in doubt, treat information as TLP:RED and ask the SIRT case lead.**

| Label | What it means for you |
|---|---|
| **TLP:RED** | For **your eyes only**. Do not share with anyone — including others inside your own organization — unless the SIRT reads them in. Most intake and finder material is TLP:RED. |
| **TLP:AMBER+STRICT** | Share **only within your organization**, strictly on a need-to-know basis. **Not** with clients, partners, or any third party. This is the default for case and remediation material. |

TLP:GREEN and TLP:CLEAR do **not** apply to this case until after public disclosure. If any item is unmarked, treat it as TLP:AMBER+STRICT at minimum. The authoritative definitions are published by FIRST at first.org.

---

## 2. Who you may communicate with

You are authorized to discuss this case **only** with the named individuals on the read-in list below. This applies regardless of a person's seniority, role, or security clearance — **if they are not on this list, they are not read in.** Do not confirm, hint at, or reference the existence of this case to anyone outside it.

| Name | Organization | Role / Tier |
|---|---|---|
| {{NAME_1}} | {{ORG_1}} | {{ROLE_1}} |
| {{NAME_2}} | {{ORG_2}} | {{ROLE_2}} |
| {{NAME_3}} | {{ORG_3}} | {{ROLE_3}} |
| *(add rows as needed)* | | |

---

## 3. Requesting additional read-ins

If you believe another person is needed — for example, an additional expert to analyze, test, or stage the fix — **request it from the SIRT case lead. Do not loop anyone in yourself.** In your request, state: who, why they are needed, and which sanctioned role they will perform (analyze/patch, test, or stage). The SIRT verifies eligibility, reads the person in, and adds them to the list in §2. Only the SIRT grants access.

---

## 4. Communications channels

Use **only** the dedicated, case-specific channels below. Do not discuss this case on general Slack, personal email, shared ticketing systems, or any channel not listed here.

- **Private Slack channel — {{#SLACK_CHANNEL}}**
  Coordination and discussion only. **Do not upload exploit code, proof-of-concept, patches, or sensitive files here.** Those belong in the case repository.

- **Dedicated case mailing list — {{MAILING_LIST}}**
  For formal notices and announcements. Signed and encrypted email is encouraged.

- **Private GitHub repository — {{GITHUB_REPO}}**
  Where analysis, patch development, and testing happen. All work stays in this private repository and is **not** pushed to the public project, a public fork, or anywhere else until the SIRT and maintainer coordinate moving it upstream at disclosure. Nothing about this case becomes public before the disclosure date.

Access to all three requires hardware-key two-factor authentication.

---

## 5. Handling rules

- Keep all case material **inside the provided environment**. Do not copy it to personal machines, personal accounts, or other systems.
- No forwarding, screenshots, printouts, or re-sharing outside the read-in list.
- No use of case data to inform trading, disclosure to customers, or any purpose beyond resolving this case.
- Every action in the environment is logged for chain-of-custody.

---

## 6. Embargo & disclosure

- **Nothing** about this case is public until the disclosure date in the header. This includes the fix, the finding, and the fact that a case exists.
- If you learn of a **suspected or actual embargo break**, notify the SIRT case lead **immediately** — the SIRT coordinates all breach response.
- An embargo break results in **removal from the program.**
- Your access **expires automatically** at public disclosure or case close.

---

## 7. Acknowledgment

By adding your name via a PR to the Knowers_File.md for this working group, you are agreeing to participate in this case, and you confirm that you:

1. Understand and will apply the **TLP handling** rules in §1.
2. Will communicate about this case **only with the named parties** in §2, via the **channels** in §4.
3. Will route any **additional read-in requests through the SIRT** (§3).
4. Will comply with the **embargo** and report any suspected break (§6).

*Questions about this notice go to the SIRT case lead listed in the header — not to anyone outside the read-in list.*
