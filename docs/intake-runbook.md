# Akrites SIRT Intake Runbook (one page) - DRAFT v0.3

Step-by-step actions for the responder on duty, keyed to the nine-phase
lifecycle in the [Akrites CVD Policy](Akrites_CVD_Policy.md).
Templates referenced below are in [`templates/notification-templates.md`](../templates/notification-templates.md). Default handling for pre-disclosure material follows the phased TLP table in CVD Policy §8 (TLP:RED at intake).

```
Discover → Deduplicate & Triage → Validate → Coordination → Patch → Test → Document → Distribute → Disclose
```

### 1. Discover — intake & acknowledge  ⏱ ack within 2 business days
- Confirm the channel: **GitHub private vulnerability reporting** (preferred) or
  `SIRT@Akrites.dev`. If it arrived the "wrong" way (public
  issue, wrong list), move it private and continue — don't penalize the Finder.
- Assign a tracking ID; record reporter, date, project, claimed versions.
- Send **Template 1 (Acknowledgement)**. Set the report to TLP:RED.

### 2. Deduplicate & Triage — is it new, and is it a security issue?
- Check for duplicates against cases in flight; if duplicate, merge and send Play 13 (co-finder).
- Compare against prior risk assessments, threat models, and bug bars.
- Decide: vulnerability / non-security bug / feature request / works-as-intended.
- Send **Template 2a or 2b**. If not a vulnerability, explain reasoning and close.

### 3. Validate — confirm & reproduce
- Reproduce the issue; confirm affected versions and impact.
- Open a **private** GitHub Security Advisory; add the Finder as collaborator if
  they wish to stay involved. Engage the Owner and any needed maintainers.
- **AI Tooling Guardrail:** Put case artifacts, PoCs, and code only through confidential, access-controlled AI tooling (self-hosted, enterprise with contractual no-training/confidentiality terms, or the SIRT environment) — never public AI services ([AI-use policy](ai-use-disclosure.md)). Record the Finder's AI use and classify embargo eligibility.

### 4. Coordination — embargo & disclosure date
- Identify read-in **Collaborators** (need-to-know only); formally read them in following the [Read-In Policy](Akrites-Read-In-Policy.md) and log each acceptance of the Read-In Notice.
- Decide whether an embargo is required; agree the **Public Disclosure (PD)** date with the Finder. Proposed upstream embargo: 15 business days (total target time to PD: **≤ 17 bd** Low/Med, **≤ 21 bd** High, **≤ 24 bd** Critical).
- Prepare the **leak contingency** (Template 5): what to tell Consumers if
  details surface early.

### 5. Patch — develop the fix privately
- Develop and test the fix on a private branch / temporary private fork so the
  fix isn't visible before users can apply it. Create a patch or work-around
  that addresses the **root cause (CWE)**.
- **Avoid Public Leakage:** Do NOT trigger public CI/CD pipelines (e.g., public GitHub Actions runners) or commit to public branches, as public build logs and commits constitute a public disclosure ([What counts as public disclosure](what-counts-as-public-disclosure.md)).

### 6. Test — verify
- Run regression, smoke, and relevant tests; confirm the issue is resolved with
  no new regressions. Prepare (but do not cut) the release.

### 7. Document — advisory & identifiers
- Request a **CVE ID** via the Akrites SIRT CNA (MITRE is CNA of last resort).
- Capture: affected/fixed versions, CWE, **CVSS v4.0** score (v3.1 for legacy
  comparison), Consumer actions, and patch location.
- Draft the advisory (**Template 4**) and a machine-readable **OSV** record.

### 8. Distribute — stage for simultaneous availability
- Stage patch + documentation so all Consumers get the fix at PD.
- If an embargo list applies, send **Template 3 (Embargoed notification)** to
  read-in providers, typically **1–30 working days** before PD. Monitor replies
  for qualification problems. Prefer a **Tue-Thu** PD; avoid holidays.

### 9. Disclose — go public  ⏱ on the PD date
- Publish the GitHub Security Advisory (populates the Security tab), cut the
  release, and publish **Template 4** to release notes / security-announce; for
  high-impact issues, the general community channel too.
- Reference the CVE ID; link the OSV record. Flip private patch branches public.
- Credit the Finder and participating maintainers following the [Acknowledgements & Attribution Guidance](acknowledgements-and-attribution.md). Reclassify case material to TLP:CLEAR and archive read-in coordination channels within 72 hours.

---

**If the embargo breaks at any point:** stop, notify the read-in group, and
publish **Template 5** with whatever guidance helps Consumers protect
themselves — even before a full fix is ready. Then resume from the current
phase on an accelerated timeline.

**Escalate to the Akrites SIRT Director when:** active exploitation in the wild, the
Finder intends to publish early, the issue spans multiple projects/vendors
(multi-party coordination), or a PD date is at risk of slipping.


