# Security Policy - v.1.0

The Akrites Security Incident Response Team (**Akrites SIRT**) coordinates the
disclosure of security vulnerabilities affecting Akrites-maintained
code and assists open source maintainers in resolving security findings. We welcome good-faith security research and reports from the community.

Our full **Coordinated Vulnerability Disclosure (CVD) Policy** — including our
lifecycle, embargo handling, and timelines — is published at [docs/Akrites_CVD_Policy.md](docs/Akrites_CVD_Policy.md) 

## Scope and supported versions

This policy covers (1) security vulnerabilities in open source projects that you would like the Akrites SIRT to coordinate, and (2) vulnerabilities in code and configuration maintained by Akrites itself.

Support and remediation decisions depend on the affected upstream project, the versions maintained in this repository, and the practical availability of a fix. Please report suspected vulnerabilities even if you are unsure whether the affected version is currently supported.

## How to Report a Vulnerability

Please **do not** open public GitHub issues, pull requests, or public discussions for security vulnerabilities. Do not trigger public CI/CD pipelines or create public forks containing proof-of-concept exploit code prior to coordinated disclosure.

### Preferred Channel: GitHub Private Vulnerability Reporting
To report to the Akrites SIRT, open a private report on this repository: **Security** tab → **"Report a vulnerability"** (direct link: https://github.com/Akrites-Foundation/SIRT/security/advisories/new). This creates a private draft advisory where you can collaborate directly with the team. If the affected project has its own private vulnerability reporting, you may report to it directly instead — that report reaches the project's maintainers, not Akrites. Tell us at SIRT@Akrites.dev if you would also like Akrites to coordinate.

### Alternative Channel: Encrypted Email
If GitHub Private Vulnerability Reporting is unavailable, send your report to **SIRT@Akrites.dev**.
* The address supports transport encryption (MTA-STS / STARTTLS).
* End-to-end encryption: our OpenPGP key will be published at https://sirt.akrites.dev/.well-known/pgp-key.txt with its fingerprint in this file. Until then, use GitHub private vulnerability reporting for sensitive details.
* Anonymous reports will be accepted once public intake opens (see CVD Policy §12); anonymous reporters cannot receive status updates.

## What to Include in Your Report
To help us validate and reproduce the issue quickly, please include:
* **Target Details**: Affected project, package, component, and version(s).
* **Environment**: OS, architecture, platform, and relevant configuration.
* **Reproduction Steps**: Step-by-step instructions or proof-of-concept (PoC) code/screenshots.
* **Impact**: Estimated severity, root cause (CWE) if known, and potential exploitation scenarios.
* **AI Assistance Disclosure**: State whether AI/LLM tooling was used during discovery, analysis, or PoC creation, and whether public or confidential tooling was used.
* **Attribution Preferences**: How you (and your organization) would like to be credited — named, clearinghouse, or anonymous (we credit Finders by default).
* **Timing Constraints**: Any upcoming embargo timing, conference deadlines or publication windows we should be aware of.

## What to Expect (Public SLAs)

| Stage           | Commitment                                                      |
| --------------- | --------------------------------------------------------------- |
| Acknowledgement | Receipt confirmed within **2 business days** |
| Initial triage  | Triage and validation status provided within **10 business days** |
| Communication   | Ongoing status updates through remediation |
| Confidentiality | Phased TLP per our CVD policy: **TLP:RED** at intake, **TLP:AMBER+STRICT** during remediation, **TLP:AMBER** for downstream staging, **TLP:CLEAR** at public disclosure |
| Credit          | Finder credited by default; anonymity honored on request |
| Disclosure      | Coordinated with maintainers and finders under a proposed **15-business-day** upstream embargo; target ≤ 17/21/24 business days from receipt for Low–Medium/High/Critical |

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
This commitment is made by {"The Akrites Foundation, a Linux Foundation project"}

**Safe Harbor Requirements**:
* Do not access or modify more data than necessary to demonstrate the issue.
* Do not degrade, disrupt, or deny service to users.
* Do not publicly disclose vulnerability details before the agreed Coordinated Release Date.
