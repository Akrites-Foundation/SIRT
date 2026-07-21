# Akrites SIRT & CVD Glossary

A shared vocabulary for the Akrites SIRT program and for Coordinated Vulnerability Disclosure (CVD) more broadly. Program-specific terms reflect current Akrites usage and may evolve as policies are ratified; for external standards, the linked source is authoritative.

Entries within each section are ordered alphabetically. See **[Contributing to the Glossary](./CONTRIBUTING-glossary.md)** to propose additions or changes.

---

## Program & governance

| Term | Definition |
|---|---|
| **Akrites** | The neutral, Linux Foundation–hosted Security Incident Response Team program coordinating vulnerability response across upstream open source projects. |
| **Front door** | The single, maintainer-facing intake path (the SIRT API) that consolidates reports so upstream projects aren't approached through many uncoordinated channels. |
| **Governing Board (GB)** | The program's governing body; owns policy- and legal-level decisions. |
| **PSIRT** | Product Security Incident Response Team — a vendor's or project's own product-security response function; Akrites coordinates with these. |
| **SIG** | Special Interest Group — a group formed around technology surrounding a WG's focus area. |
| **SIRT** | Security Incident Response Team — the Akrites staff and infrastructure that coordinate intake, disclosure, and upstream engagement. (The "Incident" mandate — coordinated response to large "celebrity" incidents — is planned to come online later.) |
| **TOC** | Technical Oversight Committee — sets technical direction and rules on cross-cutting and grey-area decisions. |
| **Working Group (WG)** | A small, private, self-organizing team of read-in members that analyzes, tests, and patches vulnerabilities in a specific domain. |

---

## Disclosure process & concepts

| Term | Definition |
|---|---|
| **Alpha patch** | An early candidate fix shared with the WG and finder for review and testing before broader coordination. |
| **Blameless postmortem** | A no-fault review process used for hard cases such as a disputed finding, an unresponsive maintainer, or a rejected patch. |
| **CVD** | Coordinated Vulnerability Disclosure — the practice of privately reporting a flaw, coordinating a fix under embargo, and disclosing publicly in a synchronized way. |
| **Deviation notice** | A published record where Akrites' assessment (e.g., severity or root cause) differs from an existing public score — sharing the evidence rather than disputing the CNA. |
| **Embargo** | The agreed period of confidentiality before public disclosure, during which only read-in parties know of the issue. Akrites' working default is 30 days, deferring to the upstream project's own policy. |
| **Finder / Co-finder** | The party (or parties) who discovered and reported the vulnerability; co-finder rules govern shared attribution. |
| **IR** | Incident Response. |
| **Least privilege** | The principle that access is scoped to only what a role needs; members see only the WGs they belong to, and only SIRT staff have cross-cutting visibility. |
| **Mitigation / workaround** | A non-patch means of reducing risk (e.g., a configuration change or firewall rule) when no fix is yet available. |
| **MoLR (Maintainer of Last Resort)** | A carefully bounded arrangement in which a WG stewards or forks an unmaintained project to ship a fix; requires TOC approval. |
| **PD (Public Disclosure)** | The point at which a vulnerability and its fix become public. |
| **POC** | Proof of Concept - a controlled demonstration or set of instructions that proves a reported software flaw is real and exploitable, typically used by security teams to validate risks, reproduce issues, and test patches. [TechTarget](https://www.techtarget.com/searchsecurity/definition/proof-of-concept-PoC-exploit) |
| **POV** | Proof of Vulnerability - Proof of Vulnerability (PoV) is an executable test case, input, or script that definitively confirms a theoretical security flaw is real, reproducible, and exploitable in a specific environment. In the context of vulnerability response and management, it serves as concrete, hands-on evidence that an identified software weakness can be triggered to compromise a system's confidentiality, integrity, or availability. [arXiv](https://arxiv.org/html/2607.12316v1) |
| **Read-in** | Granting a named individual access to a specific case or WG after they clear the need-to-know and contribution gates. |
| **Steward / LTS** | A party that takes on long-term support or maintenance of a project; the preferred alternative to Akrites acting as MoLR. |
| **Synchronized disclosure** | Coordinating parties so the fix, advisory, and disclosure land together rather than piecemeal. |
| **Technical contribution ("price of admission")** | The requirement that read-in members meaningfully help analyze, patch, test, or stage a fix — not merely observe. |
| **Tier 0 / 1 / 2 / 3** | The read-in tiers: **0** reporter & maintainer; **1** SME patch authors/testers; **2** distribution partners / pre-disclosure rings; **3** second-order distributors (CDNs, registries) staging for rollout. |
| **Tiered disclosure** | Reading parties in across staged tiers (0–3), each later tier seeing less and being read in later. |
| **VDR (Vulnerability Disclosure Report)** | The package the SIRT prepares to drive maintainer engagement and disclosure. |

---

## Roles & parties

| Term | Definition |
|---|---|
| **CNA (CVE Numbering Authority)** | An organization authorized to assign CVE IDs within its scope. |
| **Consumer / end user** | The party who must act on a disclosure once public; served at public disclosure, not before. |
| **Distribution / staging party** | A downstream distributor (e.g., package registry, CDN) read in late to pre-stage a fix for rapid propagation (Tier 2/3). |
| **Maintainer** | The upstream owner of the affected project; retains final say on the fix and disclosure timing. |
| **SME** | Subject-Matter Expert — a member with domain expertise who analyzes, produces, or tests fixes (typically Tier 1). |

---

## Data handling & classification

| Term | Definition | Reference |
|---|---|---|
| **Need-to-know** | The requirement that a person genuinely requires the information to perform a role in the case. | — |
| **PVR (Private Vulnerability Reporting)** | A project's supported private channel for receiving vulnerability reports (e.g., GitHub's PVR feature). Akrites encourages projects to enable it. | — |
| **SBOM (Software Bill of Materials)** | A formal inventory of the components in a piece of software. | [cisa.gov/sbom](https://www.cisa.gov/sbom) |
| **TLP (Traffic Light Protocol)** | A standard set of labels governing how far information may be shared. | [first.org/tlp](https://www.first.org/tlp/) |
| **TLP:AMBER / AMBER+STRICT** | Limited sharing on a need-to-know basis within one's organization; **+STRICT** excludes clients and third parties. Akrites' default for case material. | [first.org/tlp](https://www.first.org/tlp/) |
| **TLP:RED** | For named recipients only — no onward sharing, including within one's own organization. | [first.org/tlp](https://www.first.org/tlp/) |

---

## Standards, identifiers, scores & formats

| Term | Definition | Reference |
|---|---|---|
| **CSAF (Common Security Advisory Framework)** | An OASIS standard for machine-readable security advisories (and VEX). | [OASIS](https://www.oasis-open.org/) |
| **CVE (Common Vulnerabilities and Exposures)** | The global catalog of unique identifiers for publicly known vulnerabilities; operated by MITRE, sponsored by CISA. | [cve.org](https://www.cve.org/) |
| **CVSS (Common Vulnerability Scoring System)** | An open framework for scoring vulnerability severity (0–10). Current version is 4.0 (Nov 2023); 3.1 remains in wide parallel use. | [first.org/cvss](https://www.first.org/cvss/) |
| **CWE (Common Weakness Enumeration)** | A community catalog of software and hardware weakness *types* (the class of flaw), distinct from a specific CVE instance. | [cwe.mitre.org](https://cwe.mitre.org/) |
| **EPSS (Exploit Prediction Scoring System)** | A model estimating the probability that a vulnerability will be exploited in the wild; complements CVSS for prioritization. | [first.org/epss](https://www.first.org/epss/) |
| **KEV (Known Exploited Vulnerabilities)** | CISA's catalog of vulnerabilities with confirmed active exploitation. | [cisa.gov/kev](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) |
| **OSV** | An open, distributed database and schema for vulnerabilities in open source. | [osv.dev](https://osv.dev/) |
| **VEX (Vulnerability Exploitability eXchange)** | A machine-readable statement of whether a product is actually affected by a given vulnerability; commonly expressed via CSAF. | [OASIS](https://www.oasis-open.org/) |

---

## Organizations & databases

| Term | Definition | Reference |
|---|---|---|
| **CISA** | U.S. Cybersecurity and Infrastructure Security Agency; sponsors CVE and publishes the KEV catalog. | [cisa.gov](https://www.cisa.gov/) |
| **ENISA** | European Union Agency for Cybersecurity; operates the CRA Single Reporting Platform. | [enisa.europa.eu](https://www.enisa.europa.eu/) |
| **FIRST** | Forum of Incident Response and Security Teams — maintains TLP, CVSS, and EPSS. | [first.org](https://www.first.org/) |
| **Linux Foundation (LF) / LFX** | The host foundation and its platform; LFX data-insights tooling supports the SIRT. | [linuxfoundation.org](https://www.linuxfoundation.org/) |
| **MITRE** | Operator of the CVE and CWE programs. | [cve.org](https://www.cve.org/) |
| **NVD (National Vulnerability Database)** | NIST's enriched database of CVEs with scoring and references. | [nvd.nist.gov](https://nvd.nist.gov/) |
| **OpenSSF** | Open Source Security Foundation (Linux Foundation); the community context for Akrites. | [openssf.org](https://openssf.org/) |

---

## Regulatory

| Term | Definition | Reference |
|---|---|---|
| **CRA (Cyber Resilience Act)** | EU Regulation (EU) 2024/2847. Entered into force 10 Dec 2024; **Article 14** vulnerability/incident reporting to ENISA and national CSIRTs applies from **11 Sept 2026** (24-hour early warning, 72-hour notification, 14-day final report), with full application from 11 Dec 2027. | [EU CRA summary](https://digital-strategy.ec.europa.eu/en/policies/cra-summary) |

---

## Akrites tooling

| Term | Definition |
|---|---|
| **akrites.dev** | The platform hosting the SIRT pipeline. |
| **AVID (Akrites Vulnerability Information Disclosure)** | Akrites' disclosure record/advisory concept. |
| **Open Door Policy Database** | The store of profiling and rules for how Akrites engages (and should engage) with each upstream project. |
| **OSSCRS** | An OpenSSF framework for calling models/harnesses in a standardized, benchmarkable way; referenced as a potential analysis tool. |
| **PE / NPE** | Person Entities and Non-Person Entities (e.g., automated agents); both are subject to read-in and access control. |
| **Pipeline: Dedup → Investigator → Fixer** | The core processing stages — deduplicate incoming reports, analyze/validate, and develop the fix. |
| **Security Card / Rolodex** | A record of a project's or member's security posture and SME areas, used to identify who to pull into a case. |
| **Spyglass** | A submitter console and API where a member can see the status of their own submissions and pull a portfolio brief to report internally. |
| **Watchful Eye** | The custodian console used by SIRT staff to debug, manage, and create or revoke access to working groups. |

---

*Maintained by the Akrites Policy/Process work stream. Propose additions or corrections via a pull request or the repo Discussions.*
