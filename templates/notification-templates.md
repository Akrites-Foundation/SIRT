# Akrites SIRT Notification Templates

Pre-written messages for each communication point in the
[CVD Policy](../docs/Akrites_CVD_Policy.md) lifecycle.
Replace every `{{PLACEHOLDER}}` before sending. Pre-disclosure material follows
the phased TLP model in CVD Policy §8: **TLP:RED** at intake (Finder and SIRT),
**TLP:AMBER+STRICT** during verification and remediation (read-in Tiers 1, 1.5
and 2), **TLP:AMBER** for downstream staging (Tiers 3 and 3.5), and
**TLP:CLEAR** at Public Disclosure.

Every embargoed notification and public advisory carries an **AI use** block
stating, for both the Finder and the Akrites SIRT, whether and how AI/LLM tooling was
used. The wording, capability vocabulary, and rules are defined in the
[AI and LLM Use Disclosure Policy](../docs/ai-use-disclosure.md).

Quick map of which template to use when:

| Lifecycle phase            | Template                          | Audience            |
| -------------------------- | --------------------------------- | ------------------- |
| Discover / intake          | 1. Acknowledgement                | Finder              |
| Triage / Validate          | 2. Triage assessment              | Finder              |
| Coordination → Distribute  | 3. Embargoed notification         | Read-in providers   |
| Disclose                   | 4. Public disclosure advisory     | Public              |
| (any, on early leak)       | 5. Embargo-break notice           | Read-in + public    |

---

## 1. Acknowledgement (Discover / intake)

> Send within **2 business days** of receipt. If the report came via GitHub
> private vulnerability reporting, reply on the advisory thread instead of email.
> Include the AI-tooling paragraph only when the Finder indicated (or it is
> unclear whether) AI tooling was used; drop it otherwise.
> If the report has no reply address, keep a copy in the case record to show acknowledgement was attempted.

```
Subject: [Akrites SIRT] Received your report — {{TRACKING_ID}}

Hello {{FINDER_NAME}},

Thank you for reporting this to the Akrites SIRT. We've received your report and
assigned it the tracking ID {{TRACKING_ID}}. A team member is reviewing it now.

What happens next:
  - We'll triage and validate the report and send you an initial assessment
    within 10 business days.
  - We'll keep you updated as we work toward a fix and a coordinated
    disclosure date.

We are treating the details you sent as confidential (TLP:RED) and will not
share them outside the people needed to resolve the issue. As the case moves
forward, access widens only as far as our policy allows, and nothing is public
until the Public Disclosure date.

On AI tooling: we noted your report of {{AI usage / no AI usage}}. We publish a
short, capability-level note of any AI/LLM use — yours and ours — in the final
advisory. One thing to flag: material put through a public, hosted AI service is
not confidential, so a report developed that way is treated as having no
embargo available and is handled on an accelerated basis. If you used AI tooling and can tell us whether it was a public service
or a private/confidential one, that helps us plan the timeline correctly.

Please continue this conversation on {{CHANNEL: this email thread / the GitHub
advisory}}. If anything material changes on your end (for example, you observe
exploitation in the wild, or you intend to publish), please tell us right away.

Our coordinated disclosure policy:
https://github.com/Akrites-Foundation/SIRT/blob/main/docs/Akrites_CVD_Policy.md

Thank you,
Akrites SIRT
SIRT@Akrites.dev
```

---

## 2. Triage assessment (Triage / Validate)

> Use the branch that matches your determination. State your reasoning so the
> Finder can correct you if the original report was misunderstood.

**2a — Confirmed vulnerability**

```
Subject: [Akrites SIRT] {{TRACKING_ID}} — confirmed, proceeding to remediation

Hello {{FINDER_NAME}},

We've reproduced the issue and confirmed it is a security vulnerability in
{{PROJECT}} {{AFFECTED_VERSIONS}}. Thank you — this is a real finding.

Next steps:
  - We are opening a private advisory and {{developing a fix before hand-off to
    the upstream maintainers (High / Critical) / handing the finding to the
    upstream maintainers to develop a fix (Low / Medium)}}.
  - We will request a CVE ID via {{CNA}}.
  - The upstream disclosure period starts on {{UPSTREAM_START_DATE}}. Our
    default is 15 business days from that date, unless {{PROJECT}}'s own
    disclosure policy sets a different timeline, which we follow.
  - Proposed Public Disclosure target: {{PD_DATE}} (our target from receipt is
    {{≤ 17 / ≤ 21 / ≤ 24}} business days for {{Low–Medium / High / Critical}}
    severity; we aim to disclose as soon as a fix can ship). Let us know if
    this timing works for you.

Credit: by default we credit you under the name or handle you reported with.
You can instead choose (a) named — your name and, if you wish, your
organization; (b) clearinghouse — your organization only; or (c) anonymous —
no Finder credit. Let us know before {{PD_DATE}} if you'd like something other
than the default.

AI use: the final advisory will include a short, capability-level note of any
AI/LLM tooling used — both yours and ours. Please confirm whether AI assisted
your work and, if so, at which step (e.g., discovery, analysis, patch, testing).
If you'd like specific tool/model names published, tell us which; otherwise we
publish the capability only.

Would you like to be added as a collaborator on the private fix so you can
review it before release?

Akrites SIRT
```

**2b — Not a vulnerability (bug / feature request / works-as-intended)**

```
Subject: [Akrites SIRT] {{TRACKING_ID}} — assessment

Hello {{FINDER_NAME}},

Thank you for the report. After review, we've assessed this as
{{a non-security bug / expected behavior / a feature request}} rather than a
security vulnerability, because {{SPECIFIC_REASONING}}.

{{If a bug:}} Could you please refile this as a regular issue at {{LINK}}?
{{If a feature request:}} If you'd like to see this behavior change, a feature
request at {{LINK}} is the best path.

If we've misunderstood any part of your report, please reply — we're happy to
take another look.

Akrites SIRT
```

---

## 3. Embargoed notification (Coordination → Distribute)

> Sent to read-in providers/downstreams on the embargo list. Timing and TLP
> follow the recipient's read-in tier
> ([Read-In Policy §4](../docs/Akrites-Read-In-Policy.md#4-the-tiers-at-a-glance)):
>
> | Recipient | Tier | TLP | Lead time before PD |
> | --- | --- | --- | --- |
> | Distribution partners / maintainer pre-disclosure rings | 2 | **AMBER+STRICT** | Working figure 7–14 days |
> | Second-order distributors (registries, CDNs, downstream distributions) | 3 | **AMBER** | Working figure 7–14 days; the minimum consistent with a safe rollout |
> | International coordinators / strategic partners | 3.5 | **AMBER** | At most 24 hours |
>
> The 7–14 day figure is still a working figure (Read-In Policy Appendix A,
> item 1) and must fit inside the case's PD target. Avoid releasing into
> weekends/holidays; prefer Mon–Wed disclosure.

```
Subject: [TLP:{{AMBER+STRICT / AMBER}}][EMBARGO until {{PD_DATE}}] {{CVE_ID}} in {{PROJECT}}

CONFIDENTIAL — TLP:{{AMBER+STRICT / AMBER}}.
{{AMBER+STRICT: Share only within your organization, on a need-to-know basis —
not with clients, partners, or any third party.}}
{{AMBER: Share only within your organization and with its clients, on a
need-to-know basis — no onward sharing to other organizations.}}
Public disclosure is embargoed until {{PD_DATE}} {{TIME + TZ}}.

Summary
  - Identifier: {{CVE_ID}}
  - Project/component: {{PROJECT}} / {{COMPONENT}}
  - Affected versions: {{AFFECTED_VERSIONS}}
  - Fixed versions: {{FIXED_VERSIONS}}
  - Weakness (root cause): {{CWE_ID}} — {{CWE_NAME}}
  - Severity: {{CVSS_V4_SCORE}} ({{CVSS_V4_VECTOR}})
    [legacy: CVSS v3.1 {{CVSS_V31_SCORE}}]
  - Reporter credit: {{CREDIT or "withheld at reporter request"}}

Description
{{Plain-language description of the issue and impact. Where helpful, note the
affected code path and the configurations/settings in which a deployment is or
is NOT affected, so providers can judge their own exposure.}}

AI use
  - Finder: {{No AI tooling was used. / AI-assisted {phase(s)}. Tools: {names,
    if the Finder consented}.}}
  - Coordinator (Akrites SIRT): {{No AI tooling was used. / AI-assisted {phase(s)},
    under human review.}}

Mitigation / work-around
{{Available work-around, or "none — patch required."}}

Patch availability
{{How and where the patch will be made available at PD, e.g., release tag,
package version, advisory link.}}

What we ask of you
  - Prepare your update so you can ship promptly at public disclosure.
  - Keep this information within its TLP:{{AMBER+STRICT / AMBER}} limits until
    {{PD_DATE}}.
  - Reply to this thread with any patch problems or qualification issues —
    someone on the Akrites SIRT is monitoring for replies.

Public disclosure date: {{PD_DATE}} {{TIME + TZ}}

Akrites SIRT
SIRT@Akrites.dev
```

---

## 4. Public disclosure advisory (Disclose)

> Publish at PD — the SIRT case coordinator is accountable for executing
> publication. For GitHub projects, publishing the draft Security Advisory
> populates the Security tab; also announce to {{security-announce list}} and,
> for high-impact issues, the general community channel. Include the CVE ID and
> link the OSV record. Structure follows a standard advisory template: title,
> summary, identifiers, impact/status, mitigation, acknowledgement, AI use,
> references, revision history. The **AI use** block is required on every
> advisory — include both lines, and use the negative form ("No AI tooling was
> used.") where that applies.

```
Title: {{CVE_ID}}: {{SHORT_DESCRIPTIVE_TITLE}} in {{PROJECT}}

Summary
{{1–3 sentence plain-language summary of the vulnerability and its impact.}}

Identifiers
  - CVE: {{CVE_ID}}
  - GHSA: {{GHSA_ID}}
  - OSV: {{OSV_LINK}}
  - Weakness: {{CWE_ID}} — {{CWE_NAME}}

Severity
  - CVSS v4.0: {{SCORE}} ({{VECTOR}})
  - CVSS v3.1 (legacy): {{SCORE}} ({{VECTOR}})

Affected and fixed versions
  - Affected: {{AFFECTED_VERSIONS}}
  - Fixed in: {{FIXED_VERSIONS}}

Impact
{{What an attacker can do, under what conditions, and who is affected. Note any
configurations that are not affected.}}

Remediation
  - Upgrade to {{FIXED_VERSIONS}}.
  - {{Work-around, if any, for users who cannot upgrade immediately.}}

Acknowledgements
{{Reported by {{CREDIT}}. / Reported privately to the Akrites SIRT.}}
Thanks to all who assisted with validation and remediation.

AI use
  - Finder: {{No AI tooling was used. / AI-assisted {phase(s) — e.g., discovery,
    patch development}. Tools: {names — only if the Finder consented}.}}
  - Coordinator (Akrites SIRT): {{No AI tooling was used. / AI-assisted {phase(s) —
    e.g., triage, advisory drafting}, under human review.}}

References
  - Advisory: {{ADVISORY_URL}}
  - Patch / release: {{RELEASE_URL}}
  - AI-use disclosure policy: https://github.com/Akrites-Foundation/SIRT/blob/main/docs/ai-use-disclosure.md
  - {{Additional links}}

Revision history
  - {{DATE}}: Initial publication.
```

---

## 5. Embargo-break notice (early leak contingency)

> Use if the issue is published or exploited before PD. Disclosure may be
> accelerated; publish whatever helps Consumers protect themselves even without
> a complete fix. If exploitation in the wild is confirmed, the target is
> actionable guidance within **7 days** of confirmation
> ([CVD Policy §9](../docs/Akrites_CVD_Policy.md#9-actively-exploited-vulnerabilities)).
> This notice is public (TLP:CLEAR) and, like every advisory, carries the AI use
> block.

```
Subject: [TLP:CLEAR][Akrites SIRT] {{CVE_ID}} in {{PROJECT}} — disclosure accelerated

The Akrites SIRT is aware that information about {{CVE_ID}} in {{PROJECT}} has become
public ahead of the planned disclosure. To help users protect themselves, we
are sharing the following now:

  - Affected versions: {{AFFECTED_VERSIONS}}
  - Status: {{patch available at {{LINK}} / patch in progress, ETA {{DATE}}}}
  - Interim mitigation: {{WORK-AROUND, or specific configurations that reduce
    exposure}}

AI use
  - Finder: {{No AI tooling was used. / AI-assisted {phase(s)}.}}
  - Coordinator (Akrites SIRT): {{No AI tooling was used. / AI-assisted {phase(s)},
    under human review.}}

We will update this advisory as remediation becomes available:
{{ADVISORY_URL}}

Akrites SIRT
SIRT@Akrites.dev
```
