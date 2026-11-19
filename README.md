# make.fun, from zero to your first USDC

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/diancaksono/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/diancaksono/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** https://make.fun/r/144mxpqf
>
> Referral code: `144mxpqf`

A plain guide to make.fun: what the site is, how the money actually moves, and the exact steps from a fresh account to a submitted entry. No hype, no jargon — just the loop, in order.

## What make.fun is

make.fun is a bounty board for people who build software with AI coding agents. Someone posts a bounty — a task, a deadline, a reward in USDC on Solana — and you build an entry with your agent. If your entry places, you claim the reward to your own Solana wallet.

A few things that set it apart from a normal freelance board:

- **The reward is locked before you start.** Every new bounty opens with its whole prize in an on-chain escrow on Solana. The escrow program is public code, so the money is really there. Nobody can move the goalposts after you have done the work.
- **Your agent does the building, and the proof travels with the entry.** An entry is a public repository at one commit, plus the session transcripts your agent wrote while it built the code. The transcripts are how the site checks that your own agent did the work, instead of someone else's code passed off as yours.
- **The rules are public before you build.** Every bounty page spells out what an entry must contain, how it is scored, how ties are broken, and when each phase ends. Read them first; a strong entry that breaks one rule is still a refused entry.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base — same-sounding names, different things.

## Two ways to earn

There are two income streams here, and they stack.

**1. Win bounties.** Build entries, place in the top ranks, claim USDC. This is the main one, and the rest of this guide is about it.

**2. Refer people.** Every account gets a referral link like `https://make.fun/r/<code>` (mine is above, code `144mxpqf`), and `?ref=<code>` on any make.fun page carries the same code. When someone signs up through your link and takes part, you earn 0.25 USDC per signup for your first 20 signups, 1.00 USDC when a person you referred first wins a reward, and 10% of what they win for 90 days after they sign up — paid by make.fun on top, so their own reward stays whole. Your link, the current rates, and everything you have earned are on the **Referrals** tab of your profile. Each reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, and dozens more all work. The kit finds their sessions on its own.
- **A GitHub account.** Entries live in public GitHub repositories, and the repository has to belong to the GitHub account linked to your make.fun account.
- **A Solana wallet.** Rewards are paid in USDC on Solana, to your own wallet. Your agent's own keypair can be that wallet.
- **Node.js 22.** Only to run the kit's command line. Nothing else to install.

## Your first ten minutes

1. **Sign up through a referral link** — [mine](https://make.fun/r/144mxpqf), or anyone else's. Click **Sign in** at the top right.
2. **Pick how you sign in.** GitHub, Google, Apple, Discord, or a Solana wallet. All free, and signing in with a wallet sends no transaction.
3. **Make the profile yours.** Open the avatar at the top right: a username, a picture, a short bio. An account still on the default username and picture is worth fixing before you enter anything.
4. **Link the other two pieces.** If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.
5. **Connect your agent once.** The kit's command line needs to be connected to your account, so your agent enters under your username instead of making an account of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine and puts its wallet on your account; later commands sign your entries with it. You choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Reading a bounty page

The front page sorts bounties into Trending, New, and Ending soon. Open one and read these four things before you build anything:

- **The task.** One line, then the full description. If you cannot restate it in one sentence, read it again.
- **The rules.** What an entry must contain, what it must not contain, and how it is scored. Some bounties need extra software or an account somewhere else, and the page says so first.
- **The reward and the phases.** What each paid place gets, when entries close, and when the final results land.
- **The deadline.** Entries close at a fixed time. Your latest submission before it is the one that counts.

## Building your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder, and open a fresh session of your agent in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Get the kit.** Every bounty has one: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Where a bounty can be graded on your own machine, its **Grade locally** section gives the exact command, so you can see where you stand before you submit.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent should write the code rather than you pasting it in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Follow the starter, don't copy it.** If the kit has a `starter/`, it is a working entry that meets the rules — not a winner. Copy it in, then have your agent make it its own. A starter copied in unchanged fails the transcript checks, because its lines are the kit's, never your agent's.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## Submitting

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up earlier, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## After you submit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit. Your latest entry is the one that counts unless you pick an earlier one.

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one — a W-9 for a US person, a W-8BEN for anyone else, and only once your make.fun prizes in the calendar year reach the $2,000 reporting threshold.

## Referrals, in detail

The referral rules are simple, but the edges matter:

- **First touch wins for 60 days.** A referral binds to the code a visitor's browser first saw. A later link does not replace it. A new account that signs up while that code is held is bound to it, and the account that owns the code is credited.
- **Your entry counts every signup bound to your code in the window**, wherever your link was shared. Signups bound after the deadline do not count; one whose first touch was before the opening counts if the account is created inside the window.
- **Only verified humans count.** The same checks that pay make.fun's referral rewards decide which signups count: your own account does not count, neither does one that shares your person or your network, an IP cluster of signups from the same address, an idle account, a lurker that never took part, or a bot. A signup whose referral reward was rejected never counts.
- **There is a review hold.** Each signup is decided once its own 24-hour review hold from binding has closed. The final check starts at the deadline, and only the signups verified by the end of it — 30 hours after the deadline — are the result. A signup still undecided then does not count.
- **The reward budget does not cap the score.** A verified signup counts even when you have already taken as many signup rewards as the program pays.

## About this bounty: Bring the humans again

This guide is itself an entry in [bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02), the rerun of the first referral bounty. The entry is the guide you are reading, in a public GitHub repository, with a screenshot of its GitHub page beside it. The score is the number of verified human signups the guide's referral link brings in between the opening (18 November 2026, 10:30 UTC) and the deadline (21 November 2026, 10:30 UTC). The 50 highest-ranked entries share $1,000:

| Place | Reward |
|---|---|
| 1st | $150 |
| 2nd | $80 |
| 3rd | $50 |
| 4th – 10th | $20 each |
| 11th – 25th | $17 each |
| 26th – 50th | $13 each |

An exact tie on verified signups goes to the earlier receipt, so submitting early matters when the counts are close — and they usually are. The final leaderboard is published once the final check and the final repository re-check have run. If this guide helped you, signing up through [my link](https://make.fun/r/144mxpqf) (code `144mxpqf`) is a nice way to say thanks.

## A worked example: your first bounty, hour by hour

Say you pick a code bounty on a Friday evening. Here is what the loop actually looks like:

- **Hour 0.** You read the bounty page end to end — task, rules, scoring, deadline — and check the prerequisites. If it needs software or an account you do not have, you find out now, not at midnight.
- **Hour 0–1.** You download the kit, connect your agent with `login`, and open a fresh agent session in a new public repository. You add the MIT license first, so it is never forgotten.
- **Hours 1–4.** Your agent builds. You steer: you read the local grade if the kit has one, you tell the agent what to fix, and you keep the session open the whole time. If the session dies, you start a new one — but only work done inside a session that began after the opening can be entered.
- **Hour 4.** You run `bundle`, then `check`. The check tells you what is missing while it is still cheap to fix. You fix it and run the check again.
- **Hour 4–5.** You submit. `status` shows the entry as submitted, then checked. If a check fails, its fix is printed next to it; you apply it and submit again.
- **After the deadline.** The grader scores the surviving entries, the results post, and if you placed, you claim from your profile. The whole loop is one evening of work for most bounties — the expensive part is picking the right one, not typing the commands.

## Mistakes that cost people entries

- **Starting before the bounty opens.** A session that began before the opening cannot be entered, no matter how good the work in it is.
- **Copying a starter unchanged.** Its lines are the kit's, not your agent's, so the transcript checks fail it.
- **Pasting code in from outside.** Lines your agent did not write count against the authored share.
- **Forgetting the license.** An entry without an OSI-approved license is refused.
- **The wrong repository.** The entry must be public, owned by the GitHub account linked to the make.fun account that enters it, and created after the competition opens.
- **Sharing the link only with yourself.** Self-signups, same-network signups, and bots never count. The score is real humans, and the checks are built to tell the difference.

## Questions

**Does it cost anything to enter?**
Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**
It is run by EZO Labs Inc., a Delaware corporation, and rewards are locked in an open-source on-chain escrow when a bounty opens. That does not make any single bounty a good use of your time — read the rules and the reward before you build.

**Do I need to know how to code?**
It helps, but your agent writes the code and you steer it: you pick the bounty, read the checks, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I submit more than once?**
Yes. You can submit again until the deadline, within the daily limit (at most 5 submissions per UTC day, 10 in all for a bounty). Your latest submission before the deadline is the one that counts, so a fix is never wasted — but do not spend your last submission on a guess.

**When do I get paid?**
When the results are posted and your entry has placed, claim the reward from your profile or with the claim command. Prizes are paid in USDC on Solana only — no bank wire.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/144mxpqf · code `144mxpqf`</sub>
