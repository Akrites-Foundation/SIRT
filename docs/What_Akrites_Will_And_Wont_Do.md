# What Akrites Will and Won't Do to Your Project

*A plain-language companion to the [Maintainer of Last Resort Guidelines](./Maintainer_of_Last_Resort_Guidelines.md). If the two ever disagree, the promises on this page win.*

You maintain an open source project. Someone found a security bug in it and Akrites is trying to reach you. This page says what happens next.

---

## What we're asking for

We want to hand you a finished security fix rather than a bug report: a written explanation of the problem, a working reproduction, a patch, and tests.

If you want us to, we'll also handle the CVE, write the advisory, notify the Linux distributions and downstream projects that ship your code, and agree a disclosure date with you. You review it and you release it. The credit is yours. If you're buried, we'll keep doing that work for as long as you'll have us, with no cap and no bill.

You are allowed to say no. "I'm not fixing this", "this version is end-of-life" and "I don't think this is a vulnerability" are all answers you're entitled to give about software you wrote.

If you tell us it isn't a vulnerability, or that it's just a bug, we treat that as the start of a conversation rather than the end of one. We'll send you the reproduction, the code path we think is reachable, and the deployment assumptions we made, and we'll ask what would change your mind. We'll take a call if you'd rather talk it through. **We might be the ones who are wrong**, and sometimes we are: you wrote the software and you know things about how it's used that we don't. If you convince us, we close the case, tell the reporter why, withdraw the CVE if one was reserved, and that's the end of it. No advisory, no write-up, no consolation prize.

If we still disagree after all that, we'll publish an advisory so your users know where they stand. You'll hear that from us first: what we think, why, and the date. We won't spring it on you, we won't argue with you in public, and we won't call your decision negligent. We also won't hold a publication date over you to get a fix out of you, because the deadline isn't a bargaining chip.

At that point we'll offer to print your reasoning in the advisory word for word. It's going to describe your decision either way, and you're better placed than we are to explain it: that the configuration has been documented as unsupported for years, that the affected code path needs a flag nobody sets, or that you just don't agree with our assessment. Write it however you like, put your name on it or don't, and we'll show you the finished advisory before it goes out. Say no to that too and we'll drop it.

---

## What we won't do

The first one matters most: we will not ask for your package name, and we will not accept it if it's offered. Not on npm, PyPI, Maven Central or anywhere else. Not through a registry's abandonment process, not through a dispute policy, and not through a quiet word with someone we know. That holds whether or not you ever answer us, and it holds in the cases where a registry's own rules would let us have it.

The rest follow from it. We won't publish to your namespace, so nothing we build can turn up as a new version of your package. We won't use your project's name or logo; whatever we publish is labelled as ours and points back at yours. We'll credit you in every advisory and every handoff. And if you come back, you get your project back, on the terms below.

---

## If we can't reach you

Maintainers go quiet for all sorts of reasons, and most of them are nobody's business: illness, a bereavement, a new job, a laptop that died on holiday.

So we won't call your project abandoned until it has been silent for **90 days**, across every channel we can find. That floor doesn't move for a critical bug, an exploited bug, or a downstream user shouting at us. Any sign of life resets it, including a commit, a comment, or a login the registry can confirm. Two people have to sign the finding and write down what they checked.

If you do go dark and a lot of software depends on yours, we may publish a last-resort security release: your code at a frozen commit, plus a short stack of security patches, built and signed by us under our own name, with a link back to you. Each patch matches one advisory, and we open each one as a pull request on your repository so it's waiting when you get back.

It stops there. We don't take feature requests, review pull requests, triage bugs or answer support questions, and we won't touch your API or promise anyone compatibility. Issues and PRs on our copy are switched off and point back to you. Somebody is running your code in production and is exposed today. That's the whole reason, and when it stops being true we stop.

---

## When you return to your project

If we couldn't reach you, Akrites has published a security release and an advisory for your project as described above. All of this under a separate name - we will not have taken over your project.

The existence of our security release of course indicates that your project was unreachable and unmaintained. So, when you finally find time again to work on your project and would like to let us know that you are back, any activity **by your GitHub identity** in your repository is sufficient.

There's no form, no appeal, and nobody here with the authority to say no. You don't have to explain where you were or justify anything, and we won't ask about your security practices, your release cadence or your tooling, because none of it is a condition of anything.

A great way to show that you are back is to review - and maybe eventually merge - the PRs with our patches we opened in your repository.

Once you are confirmed back, you get the patches with their advisory links, the test results, and the CVE records. You get no obligations with them. Keep what's useful and bin the rest.

If you'd rather like the release disappeared, say so and we'll mark it deprecated and point it at your own releases. We won't unpublish it unless a legal order requires it or the artifact itself is confirmed compromised. People are resolving against it, and pulling a package out from under them is a supply-chain incident of our own making. The advisories stay up too: the bug was real, and your users' history isn't ours to rewrite.

---

## Tell us in advance what you want

You shouldn't have to rely on our judgement about your project when you'd rather make the call yourself.

Pre-register what should happen if you ever go dark: whether a last-resort release is welcome, who we should talk to first, and who you'd want taking over. A note in your `SECURITY.md` and a record on our side is all it takes.

**If you tell us not to fork, we won't**, and no bug is critical enough to change that. We'll publish an advisory, help your users mitigate, and work with the projects that depend on you to move off.

It's free, it doesn't involve joining anything, and you can change your mind whenever you like.

---

## What we ask of you

Two things, and neither is obligatory.

Keep a working security contact: a `SECURITY.md`, a `security.txt`, or GitHub's private vulnerability reporting switched on. Most stalled cases are a missing address and nothing worse.

Reply once, even if the reply is "seen it, give me a month" or "I'm done with this project". A single acknowledgement takes everything in this document off the table, and you can take as long as you need afterwards.

---

## Where to reach us

The SIRT front door is the same address for everything: reporting a bug, telling us you're back, pre-registering your intent, or telling us you'd like us to leave you alone.

*Contact details to be filled in at publication.*

---

*Akrites is a consortium-funded security incident response team. We coordinate vulnerability disclosure into open source projects, and now and then we ship a fix ourselves when nobody else will. We aren't trying to acquire your project. The rules we work under, including the ones that constrain us, are public in the [Maintainer of Last Resort Guidelines](./Maintainer_of_Last_Resort_Guidelines.md).*
