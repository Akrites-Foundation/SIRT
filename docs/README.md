# Akrites SIRT Documentation

Documents are organized by what they are. Where two documents disagree, the one higher in this list governs.

| Type | What it is | Folder |
| --- | --- | --- |
| **Policy** | Binding rules, limits and commitments, and who decides. | [policies/](policies/) |
| **Process** | The end-to-end flow: phases, roles, hand-offs, and why. | [processes/](processes/) |
| **Procedure** | Numbered steps for a named role to run a recurring task. | [procedures/](procedures/) |
| **Playbook** | A response to a specific situation, with decision points. | [playbooks/](playbooks/) |
| **Guidelines** | How to apply judgment under a policy. | [guidelines/](guidelines/) |
| **Reference** | Look-up material: glossary, specification, framework, diagram. | [reference/](reference/) |

Titles follow `<Subject> <Type>`, and filenames follow `<subject>-<type>.md` in lowercase kebab-case. Every document's header block names its type, owner, approver and status.

## Policies
- [Security Policy — how to report a vulnerability](../SECURITY.md)
- [Coordinated Vulnerability Disclosure (CVD) Policy](policies/cvd-policy.md)
- [Read-In Policy](policies/read-in-policy.md)
- [Working Group Governance Policy](policies/wg-governance-policy.md)
- [Maintainer of Last Resort (MoLR) Policy](policies/molr-policy.md)
- [Attribution and AI-Use Disclosure Policy](policies/attribution-and-ai-use-disclosure-policy.md)
- [Code of Conduct](../Code_of_Conduct.md)

## Processes
- [CVD Process](processes/cvd-process.md)

## Procedures
- [Read-In Procedure](procedures/read-in-procedure.md)
- [Case Handling Procedure](procedures/case-handling-procedure.md)
- [GitHub Fallback Case Handling Procedure (temporary manual process)](procedures/github-fallback-case-handling-procedure.md)
- [Member Onboarding and Offboarding Procedure](procedures/member-onboarding-and-offboarding-procedure.md)
- [MoLR Procedure](procedures/molr-procedure.md)
- [Working Group Operating Procedure](procedures/wg-operating-procedure.md)

## Playbooks
- [Critical Situation (Crit-Sit) Playbook](playbooks/crit-sit-playbook.md)
- [Communications Playbook](playbooks/communications-playbook.md)
- [Embargo Break Playbook](playbooks/embargo-break-playbook.md)

## Guidelines
- [Embargo Handling Guidelines](guidelines/embargo-handling-guidelines.md)
- [Public Disclosure Guidelines](guidelines/public-disclosure-guidelines.md)
- [Communications Guidelines](guidelines/communications-guidelines.md)
- [Severity Scoring Guidelines](guidelines/severity-scoring-guidelines.md)
- [AI Operations Guidelines](guidelines/ai-operations-guidelines.md)
- [Upstream Engagement Guidelines](guidelines/upstream-engagement-guidelines.md)

## Reference
- [Glossary](reference/glossary.md) — includes how to contribute terms
- [Metrics Framework](reference/metrics-framework.md)
- [TAP Intake API Specification](reference/tap-intake-api-specification.md) (members)
- [Read-In Engineer Quick Reference](reference/read-in-engineer-quick-reference.md)
- [Read-In Process Diagram](reference/read-in-process-diagram.svg)

## Templates
- [Templates index](../templates/README.md)

## Presentations and audits
- [Public presentations](presentations/)
- [Documentation audits](audits/)

## Document status

**How documents are approved**

- **Governing Board** reviews and initially approves three policies: the CVD Policy, the Read-In Policy, and the MoLR Policy. After the Board has reviewed a policy once, later edits are not brought back for approval; the Board is informed of them.
- **Every other document** is reviewed by the Akrites SIRT and approved by the SIRT Director.
- **Templates** follow the status of the document they support.

**Status labels**

- `Draft — for Akrites SIRT review`
- `Approved by the SIRT Director — vX.Y, YYYY-MM-DD`
- `Draft — for Governing Board review`
- `Board-reviewed — vX.Y, YYYY-MM-DD (later edits reported to the Board)`

**Register**

| Document | Type | Approver | Status |
| --- | --- | --- | --- |
| [CVD Policy](policies/cvd-policy.md) | Policy | Governing Board | Board-reviewed — v1.0, 2026-10-20 (later edits reported to the Board) |
| [Read-In Policy](policies/read-in-policy.md) | Policy | Governing Board | Draft — for Governing Board review |
| [Read-In Procedure](procedures/read-in-procedure.md) | Procedure | SIRT Director | Draft — for Akrites SIRT review |
| [Maintainer of Last Resort (MoLR) Policy](policies/molr-policy.md) | Policy | Governing Board | Draft — for Governing Board review |
| [MoLR Procedure](procedures/molr-procedure.md) | Procedure | SIRT Director | Draft — for Akrites SIRT review |
| [Security Policy](../SECURITY.md) | Policy | SIRT Director | Draft — for Akrites SIRT review |
| [Attribution and AI-Use Disclosure Policy](policies/attribution-and-ai-use-disclosure-policy.md) | Policy | SIRT Director | Draft — for Akrites SIRT review |
| [Case Handling Procedure](procedures/case-handling-procedure.md) | Procedure | SIRT Director | Draft — for Akrites SIRT review |
| [Critical Situation (Crit-Sit) Playbook](playbooks/crit-sit-playbook.md) | Playbook | SIRT Director | Draft — for Akrites SIRT review |
| [AI Operations Guidelines](guidelines/ai-operations-guidelines.md) | Guidelines | SIRT Director | Draft — for Akrites SIRT review |
| [Severity Scoring Guidelines](guidelines/severity-scoring-guidelines.md) | Guidelines | SIRT Director | Draft — for Akrites SIRT review |
| [Embargo Handling Guidelines](guidelines/embargo-handling-guidelines.md) | Guidelines | SIRT Director | Draft — for Akrites SIRT review |
| [GitHub Fallback Case Handling Procedure](procedures/github-fallback-case-handling-procedure.md) | Procedure | SIRT Director | Draft — for Akrites SIRT review |
| [Working Group Governance Policy](policies/wg-governance-policy.md) | Policy | SIRT Director | Draft — for Akrites SIRT review |
| [Working Group Operating Procedure](procedures/wg-operating-procedure.md) | Procedure | SIRT Director | Draft — for Akrites SIRT review |
| [Embargo Break Playbook](playbooks/embargo-break-playbook.md) | Playbook | SIRT Director | Draft — for Akrites SIRT review |
| [Communications Guidelines](guidelines/communications-guidelines.md) | Guidelines | SIRT Director | Draft — for Akrites SIRT review |
| [Read-In Engineer Quick Reference](reference/read-in-engineer-quick-reference.md) | Reference | SIRT Director | Draft — for Akrites SIRT review |
| [Metrics Framework](reference/metrics-framework.md) | Reference | SIRT Director | Draft — for Akrites SIRT review |
| [TAP Intake API Specification](reference/tap-intake-api-specification.md) | Reference | SIRT Director | Draft — for Akrites SIRT review |
| [CVD Process](processes/cvd-process.md) | Process | SIRT Director | Draft — for Akrites SIRT review |
| [Communications Playbook](playbooks/communications-playbook.md) | Playbook | SIRT Director | Draft — for Akrites SIRT review |
| [Upstream Engagement Guidelines](guidelines/upstream-engagement-guidelines.md) | Guidelines | SIRT Director | Draft — for Akrites SIRT review |
| [Public Disclosure Guidelines](guidelines/public-disclosure-guidelines.md) | Guidelines | SIRT Director | Draft — for Akrites SIRT review |
| [Glossary](reference/glossary.md) | Reference | SIRT Director | Draft — for Akrites SIRT review |
| [Member Onboarding and Offboarding Procedure](procedures/member-onboarding-and-offboarding-procedure.md) | Procedure | SIRT Director | Draft — for Akrites SIRT review |
