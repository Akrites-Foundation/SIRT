# Akrites Working Group — Member Operating Guide

A Working Group (WG) is a small, self-organizing team of read-in members who analyze, test, and build patches and mitigations for vulnerabilities in upstream open source projects — privately, before public disclosure. This guide is meant to let you **assemble and run your WG with minimal help from the SIRT**. Reach out to the SIRT only for the few things listed in §6; everything else is yours to run.

---

## 1. Ground rules that never bend

Your WG operates under the same confidentiality rules as every case. Keep these front of mind:

- **Follow TLP.** Treat all case material as **TLP:AMBER+STRICT** (share only within your org, need-to-know) and finder/intake material as **TLP:RED** (your eyes only). When in doubt, treat it as TLP:RED and ask the SIRT.
- **Named parties only.** Discuss a case only with the people read into *that case*. If someone isn't read in, they don't exist as far as the case is concerned.
- **Work stays private.** Everything lives in your WG's private repo until the SIRT and maintainer coordinate taking it upstream at disclosure. Nothing goes to the public project, a public fork, or anywhere else beforehand.
- **No sensitive artifacts in chat.** Never put exploit code, PoCs, or patches in Slack. Those belong in the repo.
- **Keep it in the environment.** Don't copy case material to personal machines or accounts. Every action is logged.
- **Embargo breaks = removal from the program.** Report any suspected break to the SIRT immediately.

Detail lives in the *Read-In Tier Policy* and the *Case Read-In Notice*; this is just the reminder.

---

## 2. Set up your Working Group (once)

The SIRT provisions three private spaces for your WG: a **GitHub repository**, a **Slack channel**, and a **mailing list**. To get running:

1. **Pick a coordinator** among yourselves (rotating is fine). This is a point-of-contact role, not a manager: they keep the repo and read-in list tidy and act as the liaison to the SIRT.
2. **Agree how you'll work** — a working cadence (e.g., async in the repo plus a short weekly sync), and who tends to take which role (analysis, patch authoring, testing).
3. **Confirm everyone has access** — hardware-key 2FA is required for all three spaces.

That's the whole setup. You don't need SIRT sign-off to start working.

---

## 3. Adding people to your WG

Anyone who will analyze, patch, or test **must be read in first**. The rule is simple: **you nominate, the SIRT reads in.** Never add someone to the repo or channel yourself.

Before you nominate, apply the quick self-check:

- **Need-to-know** — does this case or WG genuinely require them?
- **Can contribute** — will they analyze/produce a patch, test it, or stage it?

If both are yes, send the SIRT the person's name, org, and which of those roles they'll perform. The SIRT verifies and grants access.

---

## 4. Sharing a vulnerability with the group

The private GitHub repo is how vulnerability data enters your WG for discussion and analysis. To bring a finding to the group:

1. **Dedupe first.** Search existing issues and run the SIRT dedupe check so you're not repeating work already in flight.
2. **Open a new issue** in the WG repo using the **Finding template** in the appendix. This is the record the group discusses and analyzes against.
3. **Attach sensitive artifacts to the repo, not Slack** — put PoCs, reproduction steps, and patch work in a private branch or issue attachment.
4. **Discuss in the issue thread or Slack channel** — keep the decision trail on the issue so anyone read in can follow it.

---

## 5. Work the vulnerability

A lightweight version of the case loop:

1. **Validate & dedupe** — confirm it's real and not already handled.
2. **Analyze** — characterize the flaw, affected versions, and impact; set a preliminary severity.
3. **Build the fix** — develop the patch and/or a mitigation in a private branch.
4. **Test** — verify the fix resolves the issue and introduces no regressions or new vulnerabilities.
5. **Propose the read-in list, embargo, and PD target** — together with the finder.
6. **Report to the SIRT** — hand off for the Vulnerability Disclosure Report and maintainer engagement.
7. **Support the hand-off** — the SIRT and maintainer take it upstream; you assist as needed.

**You do not contact the upstream maintainer directly.** The SIRT is the single front door to upstream. You prepare everything privately; the SIRT engages the project.

---

## 6. When to call the SIRT

Self-serve for the day-to-day. Bring in the SIRT for:

- Reading a new person into the WG or a case
- Dedupe or cross-WG questions (the same library touching another group)
- Requesting an embargo or disclosure-window extension
- A disputed finding, a rejected patch, or any disagreement you can't resolve
- Handing a case off for upstream engagement
- A suspected or actual embargo break — **immediately**

---

## 7. Hand-off checklist

Before you pass a case to the SIRT, confirm:

- [ ] Finding validated and deduped
- [ ] Patch and/or mitigation developed
- [ ] Fix tested — resolves the issue, no regressions
- [ ] Read-in list, embargo, and PD target proposed (with the finder)
- [ ] Finding issue complete and current

---

## Appendix — Vulnerability Finding template

*Paste this into a new issue in your WG's private repo. Do not include working exploit code inline — link to a private branch or attachment instead.*

```
## Summary
One or two sentences describing the vulnerability.

## Affected project / component
- Project:
- Component / module:
- Affected versions:
- Package / ecosystem:

## Type
CWE (if known):

## Preliminary severity
CVSS vector / score (best estimate):
Notes on real-world impact (e.g., critical for a specific vertical):

## Reproduction
Link to private branch / attachment with steps and PoC (do NOT paste exploit code here):

## Impact
What an attacker can achieve; scope and blast radius:

## Suspected fix approach
Patch idea, mitigation, or workaround under consideration:

## Finder & attribution
- Finder:
- Credit preference (named / anonymous):

## Handling
- TLP: (RED / AMBER+STRICT)
- Dedupe check done: (yes / no — link)
- Additional read-ins needed (role): (analyze-patch / test / stage)
```
