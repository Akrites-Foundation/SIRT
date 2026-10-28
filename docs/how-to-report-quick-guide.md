# How to Report a Vulnerability to Akrites SIRT - DRAFT v0.2

A short guide for security researchers and users (we call you a **Finder**) who
have found a potential security issue in an open source project. Thank
you — reporting it is a real favor to the project and its users.

Full policy: [Akrites CVD Policy](Akrites_CVD_Policy.md) 

## 1. Please report privately — not in public

Do **not** open a public issue, pull request, or public discussion. Furthermore, do **not** run proof-of-concept tests or stage proposed fixes on public CI/CD runners (e.g., public GitHub Actions) or public repository forks before the agreed disclosure date. Per our disclosure policy, public CI output and unencrypted public commits constitute public disclosure and put users at risk.

## 2. Pick a channel

- **Preferred — GitHub private vulnerability reporting to Akrites.** Open
  https://github.com/Akrites-Foundation/SIRT/security/advisories/new. This keeps
  everything private and lets us add you to the draft advisory so you can stay
  involved. (Reporting on the affected project's own Security tab reaches that
  project's maintainers, not Akrites.)
- **Alternative — email.** Write to **SIRT@Akrites.dev**. The address supports
  transport encryption (MTA-STS / STARTTLS). Hold any proof-of-concept until a
  secure channel is established (GitHub private reporting counts as one). If
  encryption is a barrier, send the description anyway — we'd rather have the report.

Anonymous reporting opens with public intake (see CVD Policy §12); anonymous reporters can't receive status updates.

## 3. Tell us what you found

The more of the following you can answer, the faster we can validate and fix it
(see the intake template for a fill-in version):

- **What** the problem is, and the **impact** if exploited.
- **Which project/package/component** and which **versions** you believe are
  affected.
- **How to reproduce** it — steps, plus any software/hardware requirements.
- **Proof of concept** (share only over the secure channel).
- **Root cause** if you can identify it (and the relevant source lines / when it
  was introduced).
- A **severity** estimate ([CVSS v4.0 or v3.1](https://www.first.org/cvss/)) and a
  [**CWE**](https://cwe.mitre.org/) category, if you can. We may revise these —
  it's a conversation, not a grade.
- Whether it's **being exploited** in the wild.
- Any **suggested fix or mitigation** (patches are very welcome).
- Any **time constraints** (conference deadline, your own disclosure policy).
- **Credit preferences** How you (and your organization) would like to be acknowledged in the security advisory (e.g., full name, handle, anonymous, or organization name/link; see [Acknowledgements & Attribution Guidance](acknowledgements-and-attribution.md)).
- **AI assistance disclosure** Whether any part of the vulnerability analysis, code analysis, or proof-of-concept was generated using AI tools, in accordance with [AI and LLM Use Disclosure Policy](ai-use-disclosure.md), and whether the tooling was a public hosted service or private/confidential (public tooling means no embargo is available).
- Whether you've **shared this with anyone else**, and when/how.
- Whether you're open to a **call** to walk us through it.

English is preferred. A partial report is fine — send what you have.

## 4. What happens next

- We **acknowledge** your report within **2 business days**.
- We **triage and validate** and send an initial assessment within
  **10 business days**: confirmed vulnerability, non-security bug, or expected
  behavior (with our reasoning — correct us if we got it wrong).
- We treat your report as confidential — **TLP:RED** at intake, then shared under **TLP:AMBER+STRICT** only with those fixing it — until the agreed public disclosure date.
- We keep an **open dialogue**, share status, and coordinate the disclosure date with you. We propose a **15-business-day** upstream embargo and target public disclosure within 17 (Low/Medium), 21 (High) or 24 (Critical) business days of your report, always deferring to the affected project's own policy.
- We **credit** you by default under the name or handle you reported with, unless you ask to stay anonymous (see [Acknowledgements & Attribution Guidance](acknowledgements-and-attribution.md)).

## 5. Safe harbor

If you make a good-faith effort to follow this policy, we consider your research
authorized and will not pursue or support legal action over your report. This is
not a bug bounty and there's no expectation of payment. Please act in good
faith: access only the minimum data needed to demonstrate the issue, don't
degrade service for others, and don't disclose before the agreed date.

## 6. If you can't reach us, or we go quiet

Please give us a chance to respond and keep communicating. If you believe the
process has stalled, you can re-send to
**SIRT@Akrites.dev** noting your tracking ID. If a
vulnerability is being actively exploited, tell us immediately so we can
accelerate.

_Questions about this guide: SIRT@Akrites.dev_
