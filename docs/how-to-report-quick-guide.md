# How to Report a Vulnerability to Akrites OSS-SIRT - DRAFT v0.1

A short guide for security researchers and users (we call you a **Finder**) who
have found a potential security issue in a project OSS-SIRT coordinates. Thank
you — reporting it is a real favor to the project and its users.

Full policy: https://sirt.linuxfoundation.org/security/policy

## 1. Please report privately — not in public

Do **not** open a public issue, pull request, or public discussion. Furthermore, do **not** run proof-of-concept tests or stage proposed fixes on public CI/CD runners (e.g., public GitHub Actions) or public repository forks before the agreed disclosure date. Per our disclosure policy, public CI output and unencrypted public commits constitute public disclosure and put users at risk.

## 2. Pick a channel

- **Preferred — GitHub private vulnerability reporting.** On the affected
  repository, go to the **Security** tab and choose **"Report a vulnerability."**
  This keeps everything private and lets us add you to the draft advisory so you
  can stay involved.
- **Alternative — encrypted email.** Write to
  **security@oss-sirt.linuxfoundation.org**. The address supports transport
  encryption (MTA-STS / STARTTLS); for end-to-end protection you can use our
  OpenPGP key linked from the policy page. Hold any proof-of-concept until a
  secure channel is established. If encryption is a barrier, send it anyway —
  we'd rather have the report.

You may report **anonymously**, but then we can't send you status updates.

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
- **Credit preferences** How you (and your organization) would like to be acknowledged in the security advisory (e.g., full name, handle, anonymous, or organization name/link; see `docs/acknowledgements-and-attribution.md`).
- **AI assistance disclosure** Whether any part of the vulnerability analysis, code analysis, or proof-of-concept was generated using AI tools, in accordance with `docs/ai-use-disclosure.md`.
- Whether you've **shared this with anyone else**, and when/how.
- Whether you're open to a **call** to walk us through it.

English is preferred. A partial report is fine — send what you have.

## 4. What happens next

- We **acknowledge** your report within **2 business days**.
- We **triage and validate** and send an initial assessment within
  **10 business days**: confirmed vulnerability, non-security bug, or expected
  behavior (with our reasoning — correct us if we got it wrong).
- We treat your report as confidential (**TLP:RED**) and keep details among a
  need-to-know group until the agreed public disclosure date.
- We keep an **open dialogue**, share status, and coordinate the disclosure date
  with you. Our default planning window is up to **90 days**; we aim to disclose
  as soon as a fix can ship.
- We **credit** you in the final security advisory according to your requested preferences, following our standard format in `docs/acknowledgements-and-attribution.md`.

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
