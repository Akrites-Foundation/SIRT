# Akrites SIRT — Linux Kernel Upstream Engagement Guidelines

**Owner:** Akrites SIRT
**Status:** Draft for SIRT review
**Tracking:** [Akrites-Foundation/SIRT #36](https://github.com/Akrites-Foundation/SIRT/issues/36)
**Audience:** SIRT coordinators and WG engineers who engage Linux kernel maintainers
**Companion docs:** [Upstream Engagement Guidelines](upstream-engagement-guidelines.md),
[Embargo Handling Guidance](Embargo%20Handling%20Guidance.md),
[Engineer Read-in One-Pager](Akrites_ReadIn_Engineer_OnePager.md),
[SIRT Communications Playbook](sirt-communications-playbook.md)

## Purpose

How the SIRT works with Linux kernel maintainers: prepare a useful report,
contribute a fix, agree disclosure, and follow the fix through to release.
This companion to the general upstream engagement guidelines covers four areas:

1. **Reporting and first contact** — evidence, recipients, and technical follow-up.
2. **Confidentiality and disclosure** — release timing, distribution coordination, and CVEs.
3. **Patches and review** — authorship, tool assistance, and validation.
4. **Stable delivery** — backports, released versions, and case follow-through.

The maintainer leads the technical decision and upstream release. The SIRT
coordinator manages contact, disclosure, and confidential delivery; WG engineers
prepare the evidence, test fixes, and support review through the agreed channel
(see the [WG operating rules](Working_Group_Governance_and_Operations.md)).

---

## Section 1 — Reporting and first contact

### 1.1 Bring a report maintainers can use

Use the [kernel threat model](https://docs.kernel.org/process/threat-model.html)
and [reporting guide](https://docs.kernel.org/admin-guide/reporting-issues.html)
to establish scope and prepare the technical evidence.

- **Establish the security impact.** Identify the attacker's initial privileges,
  the affected resource, and the boundary crossed under realistic production
  conditions. Account for namespace scope, configuration, and required access.
- **Identify the responsible upstream.** Confirm the issue in maintained upstream
  code. Route vendor-only changes and out-of-tree modules to their maintainers.
  Ordinary bugs follow the reporting guide; uncertain security cases can go to
  private triage. Hardware-origin cases follow the separate
  [embargoed hardware process](https://docs.kernel.org/process/embargoed-hardware-issues.html).
- **Provide a complete report.** Include the exact upstream version or commit,
  observed failure, source reproducer or reproducible steps, and triggering
  conditions. Give relevant traces, configuration, privileges, hardware, local
  modifications, and taint status. Separate confirmed affected versions from
  suspected ranges and reference existing reports or fixes.
- **Offer a tested fix where available.** Include the cause, proposed correction,
  before/after results, available mitigations, and outstanding validation. Assign
  an engineer who can answer review questions and run follow-up tests.

Follow the kernel's
[AI Coding Assistants](https://github.com/torvalds/linux/blob/master/Documentation/process/coding-assistants.rst),
[Tool-Generated Content](https://github.com/torvalds/linux/blob/master/Documentation/process/generated-content.rst),
and [AI reporting rules](https://docs.kernel.org/process/security-bugs.html#responsible-use-of-ai-to-find-bugs).

- **Validate the finding and fix.** Record the mainline revision, verify the issue,
  identify the introducing commit, and check the fix. AI-discovered security
  reports require a thoroughly tested reproducer and tested proposed fix.
  Complete the required build and checkpatch checks and state outstanding work.

### 1.2 Reach the right maintainers

Follow the security policy's
[contact selection](https://docs.kernel.org/process/security-bugs.html#identifying-contacts)
and [reporting requirements](https://docs.kernel.org/process/security-bugs.html#sending-the-report).
Use the affected code's `MAINTAINERS` entries and `scripts/get_maintainer.pl` to
identify the responsible maintainers. Private reports go to individual
maintainers; public lists stay off the recipient list.

- **Apply the security-team CC rule.** With two or fewer report recipients,
  always also Cc: `security@kernel.org`. For larger teams, copy it on your first
  few reports or when seeking specific help, including a week without a response.
  Experienced reporters can send routine reports to larger teams directly.
- **Keep reports focused.** Send separate issues to their respective maintainers.
  Combine closely related issues only when the same maintainers handle them and
  one commit is expected to fix them together.
- **Resolve routing through the security team.** Contact `security@kernel.org`
  when ownership is unclear or coordination needs help.

- **Follow the reporting route.** The security policy treats AI-assisted
  discoveries as public. Keep reproducers private and offer them on request.
  Address public patches to maintainers and relevant lists; address reports and
  reproducers to maintainers, applying the security-team CC rule in §1.2.

### 1.3 Keep technical discussion moving

Send concise plain-text reports and follow the kernel's
[email requirements](https://docs.kernel.org/process/email-clients.html).
The coordinator agrees encrypted delivery with upstream for private patches and
reproducers, as required by SIRT's handling rules, and names the engineer
responsible for technical follow-up. Keep case artifacts in the approved
environment until delivery is arranged.

---

## Section 2 — Confidentiality and disclosure

### 2.1 Agree release timing and permissions

Under the kernel's
[disclosure policy](https://docs.kernel.org/process/security-bugs.html#disclosure-and-embargoed-information),
public-bug fixes are released immediately. For undisclosed issues, a reporter or
affected party may request deferral for QA and rollout: up to **seven calendar
days from the start of the release process after a robust fix exists**, or
exceptionally **fourteen** where the parties agree that the bug's criticality
requires more time.

The security team cannot enter NDAs. Private reports, discussions, exploits, and
reporter identities remain confidential indefinitely after fix publication unless
the reporter permits disclosure. Obtain permission for each intended publication.

The coordinator records the release trigger or date, participants, and publication
permissions, keeps the finder informed, and aligns SIRT's advisory with upstream
release.

### 2.2 Coordinate with distributions in the right order

Follow the kernel's
[coordination rules](https://docs.kernel.org/process/security-bugs.html#coordination-with-other-groups)
and the [distribution-list policy](https://oss-security.openwall.org/wiki/mailing-lists/distros).

- **Coordinate the kernel fix first.** Involve the kernel security team before
  distribution coordination. Following
  [SIRT's agreement with upstream](https://github.com/Akrites-Foundation/SIRT/issues/37),
  contact `linux-distros` **only after the fix is included in a publicly released
  kernel version**. Record the released version and fix commit.
- **Plan for the distribution deadline.** The list's embargo starts with the
  initial post and lasts at most fourteen days. Before posting, agree the public
  disclosure date and the work distributions will complete within that interval.
  The coordinator owns the required public follow-up.
- **Use the appropriate list.** Public issues go to `oss-security`. Use
  `linux-distros` for information that still qualifies for private handling under
  its policy. After the fix is merged, continue distribution work without copying
  the kernel security team.
- **Prepare material for public follow-up.** Obtain permission for the report
  material shared with distributions and its eventual disclosure. Keep private
  kernel correspondence subject to the reporter's permissions.

### 2.3 Coordinate CVE assignment

Follow the kernel's [CVE policy](https://docs.kernel.org/process/cve.html).

- **Use the kernel assignment process.** CVEs are assigned automatically after
  fixes enter stable trees. Contact `cve@kernel.org` for a missed assignment or
  to request a reserved identifier before resolution. Send vulnerability reports
  through the security reporting channel; reporting and fixing can proceed
  before an identifier is assigned.
- **Respect assignment scope.** The kernel CVE team covers supported Stable/LTS
  versions. Distribution-only code and distribution-maintained EOL branches go
  to the distribution. Handle disputes or modifications through the relevant
  subsystem maintainers and assess applicability to affected deployments.

---

## Section 3 — Patches and review

### 3.1 Fit the subsystem's workflow

Follow [Submitting patches](https://github.com/torvalds/linux/blob/master/Documentation/process/submitting-patches.rst)
and the [subsystem instructions](https://docs.kernel.org/process/maintainer-handbooks.html).

- **Agree the target tree.** Supply the base revision and prerequisites. Keep
  patches focused, independently reviewable, and buildable throughout the series.
- **Explain the change.** Describe impact, cause, and correction. Follow subsystem
  subject conventions and include the introducing commit in `Fixes:`. Use
  `Closes:` for public reports and `Link:` for relevant public discussion.

### 3.2 Preserve authorship and disclose assistance

- **Preserve authorship and consent.** Check licensing and DCO obligations.
  Each `Co-developed-by:` entry must be followed immediately by that coauthor's
  `Signed-off-by:`. Obtain permission for credit and review tags. The limited
  implicit-consent exceptions for `Cc:`, `Reported-by:`, and `Suggested-by:`
  depend on prior public kernel identity use; reports and suggestions must also
  have been public. Obtain consent before naming private reporters.
- **Disclose meaningful assistance.** In the cover letter or changelog, identify
  the tools used, the content they contributed to, and how the result was
  verified. Include material assistance with discovery, tests, code, commit
  messages, or translation. Routine spelling, completion, formatting, and
  mechanical edits fall outside this requirement.
- **A human owns the submission.** The submitter reviews and understands the
  contribution, supplies their own `Signed-off-by:`, and sends it. Complete the
  policy's recipient and mail-client review before sending, then remove that
  temporary section from the report.

### 3.3 Follow through on review

- **Use patch email conventions.** Submit inline plain-text patches with intact
  formatting and threading. Arrange confidential transport under §1.3.
  Check explicit recipients and addresses extracted from trailers against the agreed disclosure scope.
- **Stay with the review.** Address feedback, provide complete revisions with
  changelogs, and retain review/test tags while they remain applicable. Allow at
  least a week before following up on ordinary public review. Private security
  coordination follows the agreed case schedule.

### 3.4 Validate with the maintainer

Use the [submission checklist](https://docs.kernel.org/process/submit-checklist.html)
to select coverage with the maintainer. Record exact tested revisions, reproduction
results before and after the fix, relevant subsystem tests, configuration and
architecture coverage, build diagnostics, and unresolved findings. Identify gaps
that need maintainer or hardware-owner assistance.

Use approved test systems and private CI, logs, and artifacts while the case is
confidential. Include affected interfaces and documentation in the review.

---

## Section 4 — Stable delivery and follow-through

### 4.1 Arrange stable backports

Under the [stable kernel rules](https://docs.kernel.org/process/stable-kernel-rules.html),
the fix or an equivalent must already be in mainline for stable inclusion and meet
the stable eligibility requirements. Coordinate security fixes with the security
team as well as stable maintainers.

Mark public mainline fixes with `Cc: stable@vger.kernel.org`. For unpublished
vulnerabilities, use `Cc: stable@kernel.org`: this non-delivering address keeps
the stable trailer from adding a public recipient. Send private material to the
actual recipients agreed with the security team.

Request stable selection for eligible mainline fixes that were missed. For
adapted backports, provide the upstream commit ID, target series, prerequisites,
differences, and target-tree test results. Ensure the fix or an equivalent is
applicable, submitted, or already present in every newer supported stable tree.
Arrange private stable delivery with the security team.

### 4.2 Confirm release and close the loop

- **Confirm delivery.** Track mainline and stable integration through release,
  recording exact commits and released versions. Publish the agreed advisory
  material and retain confidential case records and attribution preferences.

---

## Case Checklist

Record pending items with an owner and next action; mark non-applicable items explicitly.

**Before upstream engagement**

* [ ] Reproduction evidence and upstream revision recorded; technical follow-up owner named.
* [ ] Maintainers, recipients, security-team CC, and delivery channel confirmed.

**Before sending a patch**

* [ ] Patch tested; authorship, sign-offs, and tool-assistance disclosure checked.
* [ ] Patch email format, threading, and actual recipients checked.

**Before public follow-up / closure**

* [ ] Release timing, publication permissions, and distribution notification order checked.
* [ ] Released versions and current stable backport and CVE status recorded.
