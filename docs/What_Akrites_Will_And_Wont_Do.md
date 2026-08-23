# What Akrites Will and Won't Do to Your Project

*A plain-language companion to the [Maintainer of Last Resort Guidelines](./Maintainer_of_Last_Resort_Guidelines.md). If the two ever disagree, the promises on this page win.*

You maintain an open source project. Someone found a security bug in it, and Akrites is trying to reach you. This page sets out what we will and won't do.

---

## What we're asking for

We want to hand you a finished security fix.

Not a bug report. A written explanation of the problem, a working reproduction, a patch, and tests. If you want us to, we'll also handle the CVE, write the advisory, notify the Linux distributions and downstream projects that ship your code, and coordinate the disclosure date with you. You review, you decide, you release, and you get the credit.

If you're buried, we'll keep doing that work for as long as you want it. There's no cap and no bill.

**You are allowed to say no.** "I'm not fixing this," "this version is end-of-life," and "I disagree that this is a vulnerability" are all legitimate answers from the person who wrote the software. We'll publish an advisory so your users know where they stand, and we'll move on. We won't argue with you in public, and we won't describe your decision as negligence.

---

## Our hard promises

**We will never ask for or take your package name.** Not on npm, PyPI, Maven Central, crates.io, or anywhere else. Not through a registry's abandonment process, not through a dispute policy, not by asking a friendly contact. Even if a registry offered it to us, we would decline. This is unconditional, and it applies whether you answer us or not.

**We will never publish to your namespace.** Nothing we build will ever appear as a new version of your package.

**We will never use your project's name or logo.** Anything we publish is clearly ours, clearly labelled, and clearly points back at your project as the original.

**We will always credit you.** Your name stays on your work, through every advisory and every handoff.

**We will always hand back.** See below.

---

## If we can't reach you

Sometimes maintainers go quiet. Life happens: illness, a death in the family, a new job, a broken laptop, a country with bad connectivity, a long holiday.

**We will not call your project abandoned for at least 90 days of complete silence**, across every way we can find to contact you. That floor doesn't move, no matter how serious the bug is or how loudly anyone is complaining. Any sign of life anywhere, a commit or a release or a comment, resets it. Two people have to sign the finding, and they have to write down what they checked.

If you do go dark and the software is widely depended on, we may publish a **last-resort security release**.

**What we publish:** your code at a frozen commit, plus a small stack of security patches, built and signed by us, under our own name, with a link back to you. Each patch matches one advisory. We open every one of those patches as a pull request against your repository, so it's waiting for you when you get back.

**What we don't do:** accept feature requests, review or merge pull requests, triage bugs, or provide support. We add nothing, we change no API, and we make no promises about compatibility. Issues and PRs on our copy are turned off, with a pointer back to you.

We do this because someone is running your code in production and is currently exposed. We do it for as long as that's true and not one day longer.

---

## Getting your project back

**Email us. There is no other step.**

- You don't have to explain where you were.
- You don't have to justify anything.
- We won't ask about your security practices, your release cadence, or your tooling. Nothing is conditional on any of that.
- There is no appeal, no dispute process, and nobody at Akrites has the authority to say no.

We aim to complete handback within **14 days** of confirming it's you. That check exists to make sure you're you, and it evaluates nothing else.

You get the patches with their advisory links, the pull requests we already opened on your repo, the test results, and the CVE records. **You get no obligations.** Nothing transfers to you except the work, and you can throw away as much of it as you like.

**If you'd rather we took our release down entirely**, say so. We'll mark it deprecated and point it at your releases. We won't delete it from the registry. People are depending on it, and yanking a package that others resolve against breaks their builds, which is a supply-chain incident we're not going to cause. The security advisories stay published too, because the bug was real and your users' history shouldn't be rewritten.

---

## Tell us in advance what you want

You shouldn't have to trust our judgement about your project when you'd rather decide yourself.

You can **pre-register what should happen if you ever go dark**: whether a last-resort release is welcome or unwelcome, who we should contact before doing anything, and who you'd want to take over if you couldn't. A note in your `SECURITY.md` and a record on our side is all it takes.

**If you tell us not to fork, we won't.** Not under pressure, and not for a critical bug. We'll publish an advisory, help your users mitigate, and work with the projects that depend on you to move off.

This is free, it doesn't require joining anything, and you can change your mind at any time.

---

## What we ask of you

Nothing, really. But two things help a lot:

1. **A working security contact**: a `SECURITY.md`, a `security.txt`, or GitHub's private vulnerability reporting turned on. Most stalled cases come down to a missing address.
2. **A one-line reply**, even if it's "I've seen this, give me a month" or "I'm done with this project." A single acknowledgement takes the whole apparatus in this document off the table and puts us back to normal, and you can take as long as you need after that.

---

## Where to reach us

The SIRT front door is the same address for everything: reporting a bug, telling us you're back, pre-registering your intent, or telling us you'd like us to leave you alone.

*Contact details to be filled in at publication.*

---

*Akrites is a consortium-funded security incident response team. We coordinate vulnerability disclosure into open source projects and, rarely, ship a security fix ourselves when nobody else will. We are not trying to acquire your project. The full rules we operate under, including the parts that constrain us, are public in the [Maintainer of Last Resort Guidelines](./Maintainer_of_Last_Resort_Guidelines.md).*
