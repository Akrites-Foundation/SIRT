# Security Policy - v.1.0

The Akrites Security Incident Response Team (**Akrites SIRT**) coordinates the
disclosure of security vulnerabilities affecting Akrites-maintained
code and assists open source maintainers in resolving security findings. We welcome good-faith security research and reports from the community.

Our full **Coordinated Vulnerability Disclosure (CVD) Policy** — including our
lifecycle, embargo handling, and timelines — is published at:
**docs/Akrites_CVD_Policy.md** 

## Scope and supported versions

This policy applies to security vulnerabilities in code and configurations maintained by Akrites in this repository.

Support and remediation decisions depend on the affected upstream project, the versions maintained in this repository, and the practical availability of a fix. Please report suspected vulnerabilities even if you are unsure whether the affected version is currently supported.

## How to Report a Vulnerability

Please **do not** open public GitHub issues, pull requests, or public discussions for security vulnerabilities. Do not trigger public CI/CD pipelines or create public forks containing proof-of-concept exploit code prior to coordinated disclosure.

### Preferred Channel: GitHub Private Vulnerability Reporting
If reporting a vulnerability in a GitHub repository, go to the repository's **Security** tab and click **"Report a vulnerability"**. This creates a private draft advisory where you can collaborate directly with the team.

### Alternative Channel: Encrypted Email
If GitHub Private Vulnerability Reporting is unavailable, send your report to **SIRT@Akrites.dev**.
* The address supports transport encryption (MTA-STS / STARTTLS).
* For end-to-end protection, you may encrypt your message using our OpenPGP key published on [https://sirt.akrites.dev/security/policy](https://sirt.akrites.dev/security/policy).
* Anonymous reports are accepted, though we will be unable to send you status updates.

## What to Include in Your Report
To help us validate and reproduce the issue quickly, please include:
* **Target Details**: Affected project, package, component, and version(s).
* **Environment**: OS, architecture, platform, and relevant configuration.
* **Reproduction Steps**: Step-by-step instructions or proof-of-concept (PoC) code/screenshots.
* **Impact**: Estimated severity, root cause (CWE) if known, and potential exploitation scenarios.
* **AI Assistance Disclosure**: State whether AI/LLM tooling was used during discovery, analysis, or PoC creation, and whether public or confidential tooling was used.
* **Attribution Preferences**: How you (and your organization) would like to be credited in the public advisory (named, clearinghouse, or anonymous).
* **Timing Constraints**: Any upcoming embargo timing, conference deadlines or publication windows we should be aware of.
* **Credit**: If you wish to be credited and how.

## What to Expect (Public SLAs)

| Stage           | Commitment                                                      |
| --------------- | --------------------------------------------------------------- |
| Acknowledgement | Receipt confirmed within **2 business days**                                   |
| Initial triage  | Triage and validation status provided within **10 business days**                 |
| Communication   | Ongoing status updates through remediation                      |
| Confidentiality | Phased TLP per our CVD policy: **TLP:RED** at intake, **TLP:AMBER+STRICT** during remediation, **TLP:CLEAR** at public disclosure |
| Credit          | Finder credited by default; anonymity honored on request        |
| Disclosure      | Coordinated with maintainers and finders under a proposed **15-business-day** upstream embargo window |

## Our process at a glance
We follow a nine-phase lifecycle:

```
Discover → Deduplicate & Triage → Validate → Coordination → Patch → Test → Document → Distribute → Disclose
```

Case details remain private (phased TLP, need-to-know) through the embargo; the
patch and full advisory are released together at Public Disclosure. The process
itself is open and reviewable — see the policy linked above.

## Safe harbor
If you make a good-faith effort to comply with this policy during your research, we consider your research authorized, will work with you to resolve the issue, and will not pursue or support legal action related to your report. This is not a bug bounty program and confers no expectation of financial payment.

**Safe Harbor Requirements**:
* Do not access or modify more data than necessary to demonstrate the issue.
* Do not degrade, disrupt, or deny service to users.
* Do not publicly disclose vulnerability details before the agreed Coordinated Release Date.
