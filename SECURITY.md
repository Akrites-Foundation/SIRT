# Security Policy - v.1.0

The Akrites Security Incident Response Team (**Akrites SIRT**) coordinates the
disclosure of security vulnerabilities affecting Akrites-maintained
code and assists open source maintainers in resolving security findings. We welcome good-faith security research and reports from the community.

Our full **Coordinated Vulnerability Disclosure (CVD) Policy** — including our
lifecycle, embargo handling, and timelines — is published at [docs/Akrites_CVD_Policy.md](docs/Akrites_CVD_Policy.md) 

## Who this policy is for

This policy covers reports from the public. **Akrites member organizations should not use this process.** Member engineers report through the member intake process, available from their Akrites SIRT contact.

**Intake status:** Akrites is opening intake in stages (CVD Policy §12). Public reporting is planned to open by the end of 2026. Until then, reports received through the channel below may be deferred or handled manually.

## Scope and supported versions

This policy covers (1) security vulnerabilities in open source projects that you would like the Akrites SIRT to coordinate, and (2) vulnerabilities in code and configuration maintained by Akrites itself.

Support and remediation decisions depend on the affected upstream project, the versions maintained in this repository, and the practical availability of a fix. Please report suspected vulnerabilities even if you are unsure whether the affected version is currently supported.

## How to Report a Vulnerability

Please **do not** open public GitHub issues, pull requests, or public discussions for security vulnerabilities. Do not trigger public CI/CD pipelines or create public forks containing proof-of-concept exploit code prior to coordinated disclosure.

### Preferred Channel: GitHub Private Vulnerability Reporting
To report to the Akrites SIRT, open a private report on this repository: **Security** tab → **"Report a vulnerability"** (direct link: https://github.com/Akrites-Foundation/SIRT/security/advisories/new). This creates a private draft advisory where you can collaborate directly with the team. If the affected project has its own private vulnerability reporting, you may report to it directly instead — that report reaches the project's maintainers, not Akrites. If you would also like Akrites to coordinate, open a report here as well.

## What to Include in Your Report
To help us validate and reproduce the issue quickly, please include:
* **Target Details**: Affected project, package, component, and version(s).
* **Environment**: OS, architecture, platform, and relevant configuration.
* **Reproduction Steps**: Step-by-step instructions or proof-of-concept (PoC) code/screenshots. Share PoC material only over a private channel (GitHub private vulnerability reporting counts as one).
* **Impact**: Estimated severity, root cause (CWE) if known, and potential exploitation scenarios.
* **AI Assistance Disclosure**: State whether AI/LLM tooling was used during discovery, analysis, or PoC creation, and whether public or confidential tooling was used. A report developed with a public, hosted AI service is treated as having **no embargo available** (see our [AI and LLM Use Disclosure Policy](docs/ai-use-disclosure.md)).
* **Attribution Preferences**: How you (and your organization) would like to be credited — named, clearinghouse, or anonymous (we credit Finders by default).
* **Timing Constraints**: Any upcoming embargo timing, conference deadlines or publication windows we should be aware of.
* **Exploitation and exposure**: Whether you know of exploitation in the wild, and whether you have shared the issue with anyone else (who, when, how).
* **Suggested fix**: Any patch or mitigation you have — patches are very welcome.
* **Availability**: Whether you're open to a call to walk us through it. A partial report is fine; a fill-in [intake template](templates/vulnerability-report-intake-template.md) is available.

## What to Expect

| Stage           | Commitment                                                      |
| --------------- | --------------------------------------------------------------- |
| Acknowledgement | Receipt confirmed within **2 business days** |
| Initial triage  | Triage and validation status provided within **10 business days** |
| Communication   | Ongoing status updates through remediation |
| Confidentiality | Phased TLP per our CVD policy: **TLP:RED** at intake, **TLP:AMBER+STRICT** during remediation, **TLP:AMBER** for downstream staging, **TLP:CLEAR** at public disclosure |
| Credit          | Finder credited by default; anonymity honored on request |
| Disclosure      | Coordinated with maintainers and finders under a proposed **15-business-day** upstream embargo; target ≤ 17/21/24 business days from receipt for Low–Medium/High/Critical |

## If you can't reach us, or we go quiet
If you believe the process has stalled, add a comment to your private report, or email **SIRT@Akrites.dev** with your report link. If you disagree with how your report was handled, see the disputes and appeals path in [CVD Policy §15](docs/Akrites_CVD_Policy.md). If the vulnerability is being actively exploited, tell us immediately so we can accelerate.

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
* Do not publicly disclose vulnerability details before the agreed Public Disclosure date.
