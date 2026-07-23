# You're Read Into a Vulnerability Case — Start Here

You've been tapped to help resolve a confidential vulnerability under embargo. Thank you. This one-pager is everything you need to operate correctly. The single idea behind all of it: **reduce harm, and keep this secret until the fix is ready.** When unsure, stop and ask the SIRT case lead.

## Confidentiality — non-negotiable

- **Follow TLP.** Treat case material as **TLP:AMBER+STRICT** — share only *within your organization, need-to-know*, never with clients or third parties. Some material is **TLP:RED** — *your eyes only*, not even your own manager or teammates. Under TLP:RED, "my org" does **not** mean "anyone at my org." When in doubt, treat it as TLP:RED and ask.
- **Named parties only.** Discuss the case only with the people on the read-in list. If someone else needs to help, ask the SIRT to read them in — **never loop anyone in yourself.**
- **No signaling.** Do nothing in public that hints the issue exists: no telltale commits, branches, issues, PRs, mailing-list questions, blog/social posts, or conference teasers. Most leaks are accidental.
- **Keep it contained.** Work only inside the provided environment (repo, channel). No copying to personal machines or accounts. **No exploit code, PoCs, or sensitive files in chat** — those live in the case repo.

## How to conduct yourself

- **Stay in scope.** Work only the assigned finding. If you spot something new or adjacent, **report it — don't chase it.**
- **Don't test where you shouldn't.** Never reproduce or test the vulnerability against production, or any system you don't own or aren't authorized to test. Use the provided test environment.
- **Use the front door.** Don't contact the upstream maintainer, other vendors, or the finder directly — the SIRT coordinates all outside contact.
- **Match the pace.** This is a coordinated timeline. Don't get ahead of the group, and if you can't meet a date, say so **early**.
- **Assume good faith.** Treat maintainers, finders, and peers with respect, even when things move slowly.

## Tell the SIRT immediately if…

- You see any sign the vulnerability is being **exploited in the wild**.
- You notice a **leak**, or evidence **someone else found it independently**.
- You're **contacted out-of-band** about it (journalist, researcher, government, another vendor) — don't engage; route it to the SIRT.
- You **made a mistake** or think the embargo may be at risk. Reporting early is always better than staying quiet — this is blameless.

## Easy to overlook

- **Personal OPSEC.** You may be targeted *because* you're read in. Watch for phishing and social engineering, lock your screen, and don't discuss the case where you can be overheard.
- **Material non-public information.** Vulnerability details can be MNPI — do not trade on them or pass them to anyone who might.
- **Conflicts of interest.** Tell the SIRT if you have one (e.g., you maintain the affected project or have a competitive tie).
- **At case close.** Delete local copies and stop work. Your access ends at public disclosure.

## Your case contacts

- **SIRT case lead:** {{NAME}} — {{CONTACT}}
- **Slack channel:** {{#CHANNEL}}  ·  **Mailing list:** {{LIST}}  ·  **Repo:** {{REPO}}

---

*Questions go to the SIRT case lead — never to anyone outside the read-in list. Aligned with established coordinated-disclosure practice: the CERT/CC Guide to Coordinated Vulnerability Disclosure, FIRST's TLP and multi-party coordination guidance, and ISO/IEC 29147 & 30111.*
