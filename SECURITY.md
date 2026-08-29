# Security Policy - DRAFT v.0.1

The Akrites Security Incident Response Team (**Akrites SIRT**) coordinates the
disclosure of security vulnerabilities affecting Akrites-maintained
code and configurations in this repository. Thank you for helping
keep our users safe.

<!-- Our full **Coordinated Vulnerability Disclosure (CVD) Policy** — including our
lifecycle, embargo handling, and timelines — is published at:
**https://sirt.akrites.dev/security/policy** -->

## Scope and supported versions

This policy applies to security vulnerabilities in code and configurations maintained by Akrites in this repository.

Support and remediation decisions depend on the affected upstream project, the versions maintained in this repository, and the practical availability of a fix. Please report suspected vulnerabilities even if you are unsure whether the affected version is currently supported.
## Reporting a vulnerability

**Please do not open a public issue, pull request, or discussion for a security
problem.** Use one of the private channels below.

### Preferred — GitHub private vulnerability reporting

Use the **"Report a vulnerability"** button on this repository's **Security**
tab, use it to submit your report privately. This allows us to
collaborate on a draft advisory and, where appropriate, develop a patch privately.

If the button is not available, use the email reporting channel below.

### Alternative — encrypted email

If GitHub reporting is unavailable, email
**[SIRT@Akrites.dev](mailto:SIRT@Akrites.dev)**. The address supports transport
encryption (MTA-STS / STARTTLS); for end-to-end protection you may use our
OpenPGP key linked from the policy page. We would rather receive your report
than have you blocked by encryption — when in doubt, send it.

### What to include

- Affected project, component, and version(s)
- Environment (OS, architecture, platform, configuration)
- Reproduction steps; proof-of-concept or screenshots if available
- Impact and how the issue could be exploited
- Any embargo/disclosure timing you would like us to honor
- Whether AI/LLM tooling materially helped find or analyze the issue — a
  report developed with public AI tooling must be treated as not having an
  embargo available ([AI-Use Disclosure Policy](docs/ai-use-disclosure.md);
  [Embargo Handling Guidance](docs/Embargo%20Handling%20Guidance.md))
- Whether and how you wish to be credited

Reports may be made anonymously, but we then cannot send you status updates.

## What to expect

| Stage           | Commitment                                                      |
| --------------- | --------------------------------------------------------------- |
| Acknowledgement | Within **2 business days**                                      |
| Initial triage  | Initial assessment within **10 business days**                  |
| Communication   | Ongoing status updates through remediation                      |
| Confidentiality | Phased TLP per our CVD policy: **TLP:RED** at intake, **TLP:AMBER+STRICT** during remediation, **TLP:CLEAR** at public disclosure |
| Credit          | Finder credited by default; anonymity honored on request        |
| Disclosure      | Coordinated; default planning target is PD within **30 days** of a validated report, deferring to the upstream project's own disclosure policy; extension beyond 30 days requires explicit rationale |

## Our process at a glance

We follow a nine-phase lifecycle:

```
Discover → Deduplicate & Triage → Validate → Coordination → Patch → Test → Document → Distribute → Disclose
```

Case details remain private (phased TLP, need-to-know) through the embargo; the
patch and full advisory are released together at Public Disclosure. The process
itself is open and reviewable — see the policy linked above.

## Safe harbor

Good-faith research conducted in line with our policy is authorized; we will not
pursue or support legal action for such reports. This is not a bug bounty and
confers no expectation of payment. Do not access more data than necessary, do
not degrade service for others, and do not disclose before the agreed date.

<!-- _Full policy: https://sirt.akrites.dev/security/policy_ -->
