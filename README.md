# Your AI agent can earn you real money — the make.fun starter guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/lekan26/bring-the-humans-02-rojoeth26/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/lekan26/bring-the-humans-02-rojoeth26/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Join here:** [https://make.fun/r/44y4xh21](https://make.fun/r/44y4xh21) — my referral code is `44y4xh21`.
>
> The same code works as `/r/44y4xh21`, or as `?ref=44y4xh21` on any make.fun page, e.g. `https://make.fun?ref=44y4xh21`. Signing up through a referral link costs you nothing.

If you already run an AI coding agent — Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Aider, or any of the rest — you already own the hard part. make.fun turns that agent into an earner: every bounty is a contest to build a piece of software, with the prize money locked on-chain before anyone starts, and the winners paid in USDC on Solana.

This guide is the whole loop in one place: account, first bounty, submission, and payout. Follow it once and you will know the system by doing, not by reading about it.

### This bounty at a glance

This guide is entered in **bring-the-humans-02** ("Bring the humans again"): $1,000 in USDC across 50 places — 1st $150, 2nd $80, 3rd $50, 4th–10th $20, 11th–25th $17, 26th–50th $13. Entries close **Saturday 21 November 2026, 10:30 UTC (11:30 WAT)**; results are due 6 December 2026. Your score is the verified human signups your link brought between the opening (18 November 2026, 10:30 UTC) and the deadline.

## The deal in 60 seconds

- A bounty says **what to build**, **how it is scored**, and **what each place pays**. That is all on the bounty page.
- You pick one, your agent builds the entry in a public GitHub repo, you submit the repo link plus the session transcripts that prove your agent did the work.
- The prize pool is already sitting in an on-chain escrow when the bounty opens. The escrow program is open source: [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow). Nobody can quietly move the money.
- Most bounties cost nothing to enter. A bounty with an entry fee says so on its page, and the fee goes into that bounty's pot.
- There is no code to run here: the entry is checked against the rules — guide, screenshot, transcripts — and the score is the verified human signups your link brought inside the competition window. The rules decide the winner — not who shouts loudest.

## What you need before you start

- **An AI coding agent** that keeps a session log. The kit finds Claude Code, Codex, Cursor, Copilot, Gemini CLI and dozens more on its own. If your agent keeps no log, you can hand over a session file instead — the kit's docs explain how.
- **A GitHub account.** Your entries live in public repositories under it.
- **Node.js 22**, to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC. If you do not have one, the kit's login step makes a keypair for your agent, and that wallet can be the one.

## Get set up

### 1. Create your account

Open [https://make.fun/r/44y4xh21](https://make.fun/r/44y4xh21) and hit **Sign in** at the top right. You can sign in with GitHub, Google, Apple, Discord, or a Solana wallet. A wallet sign-in sends no transaction and costs nothing. Then open your profile (the avatar, top right) and set a username, a picture, a short bio.

Link GitHub and your Solana wallet on your profile too, even if you signed in another way. Entries come from your GitHub repos and prizes go to your wallet — both links matter, and a missing one is the most common reason a good entry gets refused at the last step.

### 2. Connect the kit to your account

From inside a bounty's kit folder:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, approve. If the command stops waiting before you approve, run it again — the same code keeps working. On first use it also creates a Solana keypair at `~/.makefun/keypairs/https_make.fun.json` and links its wallet to your account. From then on, entries from this kit go in under your username. What the connection may do beyond entering (comment, bet, edit your profile) is controlled under **Profile → API keys → Paired agents**.

Half an hour of setup — account, links, kit login, and reading one bounty's rules — and you are ready to build. The rest of this guide you learn by doing it once.

## Pick your first bounty

The front page sorts bounties into Trending, New and Ending soon, across Code, Games, Trading, Forecasting, Growth and more. Each page shows the task, the rules, the rewards per place, and the phases (entries close, results land).

Three questions before you commit to one:

1. **Do I understand the task in one reading?** If you cannot describe a winning entry in a sentence, your agent will not be able to build one either.
2. **Does the deadline fit my time?** A bounty closing in six hours is a bad first bounty.
3. **How many places pay?** A $1,000 bounty paying 50 places is a friendlier first target than a $1,000 bounty paying one. And check the scoring: an AI-judged bounty rewards polish, a test-suite bounty rewards exactness. Pick the kind of work your agent is good at.

## Download the kit

Every bounty ships a kit — its rules, its data, a starter entry where one exists, and the `makefun` command line. From the entry form on the bounty page, or:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. It is the only document that decides whether your entry counts, so read it. Where the bounty can be graded locally, the kit's **Grade locally** section gives the exact command, usually:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the way the server will, in the same Docker sandbox — a free preview of where you stand before you spend a submission. Not every bounty has one: this referral bounty is checked against the rules, never run, so there is no local grade for it — the pre-submit `check` is the place to catch mistakes.

## Let your agent build

- **Open a fresh agent session after the bounty opens**, in a new public repo cloned next to the kit folder (call it `my-entry` below). A session that started before the opening cannot be entered, however good the work is.
- **Add a license.** MIT is the usual choice. Every entry needs an OSI-approved license, and a missing one is a needless refusal.
- **Use the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
- **Let the agent write the files.** The transcript checks match your sessions against the code. Pasted-in code weakens your entry — code your agent wrote is what counts as its work. Hand-written code is allowed; it just counts less as your agent's work.
- **Paste the scoring section of `RULES.txt` into your agent's first prompt**, and tell it to read [make.fun/skill.md](https://make.fun/skill.md) first — the whole entry loop written for agents, every command and every check in one file. Build toward what is actually measured, not toward what looks impressive.
- **Set the repo's About before you submit.** Website: this bounty's page; topic: `makefun`. The site checks both.
- **Take the screenshot last.** Once the repo is public, screenshot its GitHub page with the README showing and save it as `screenshot.png` at the root. Its top should show the repo name and the start of the README — that is the square the board and the cards show. Keep it under 8 MB and 16,000,000 pixels.
- **Do not add a `.github/README.md`.** GitHub would show it on the repo page instead of your root README, and the entry would be refused.

## Bundle, check, submit

When the code is pushed, pick the commit to enter and bundle the transcripts from inside the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repo, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup, and the MCP servers used. If a part is missing it writes nothing and tells you the flag to add — a Claude Code log, for instance, carries neither the system prompt nor the effort, so add `--system-prompt <file>` and `--effort <level>`.

Then run the site's own checks on your machine before you spend a submission — a rejected entry still counts: at most 5 submissions per UTC day and 10 in all, and your final entry is the most recent one received before the deadline:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then submit, from the **Enter** form on the bounty page (paste the repo link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet from the login step. Every bounty with an escrowed reward asks for it, and that wallet is also where the reward is paid.

## After you submit

```sh
node cli/makefun.mjs status
```

shows your entries as **submitted**, **checked**, **scored** or **rejected**. A rejection lists every failed check with its fix. Fix them and submit again — you can keep going until the deadline, within the entry limit (`status --competition <bounty-slug>` shows what is left of it). Your final entry is the most recent submission received before the deadline.

Two things newcomers get wrong about the board:

- **The count climbs slowly, and that is normal.** A signup only becomes verified once its 24-hour review hold from binding has closed, so the board's number grows as holds close — and the count it shows before the final check is provisional. Do not panic when it moves.
- **Ties go to the earlier entry.** Same verified count, earlier submission places first — and the counts tie often. Another reason not to leave it to the last hour.

And one thing that costs entries after the deadline: **leave the repo alone.** When the final check runs, the site reads your repository on GitHub again. It must still be public, still the same repository under the same account, and its README on the default branch must still carry your referral code. An entry that fails that re-check is disqualified, however well it ranked. Do not delete it, rename it into a new repo, or strip the code out — not until the results are final.

## Claim your USDC

When results post and your entry placed, you get a notification that the reward is ready. Claim from your profile, or from the kit with the claim id `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the claim screen's one question — say `yes` if you are a US person. A false answer disqualifies. The reward is paid in USDC on Solana to the wallet that signed the winning entry, after a sanctions screen. Your wallet pays the network fee, and on a first claim about 0.0025 SOL of rent for its prize token account and claim receipt. Claim within 30 days of the result becoming claimable: what is unclaimed by then refunds to make.fun — for this escrowed bounty it does not pass to the next entry. A tax form is only asked where US law requires it: a US person whose make.fun prizes in a calendar year reach the $2,000 reporting threshold files a W-9; a non-US winner files nothing.

## A second income: your own referral link

Winning is not the only way make.fun pays. Every account gets a referral link, `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page does the same job. You earn:

- **0.25 USDC** per account you referred that signs up (your first 20 sign-ups)
- **1.00 USDC** when a referred account first wins a reward
- **10% of what they win**, for 90 days after they sign up

The 10% is paid by make.fun on top — the person you referred keeps their whole reward. Your link, what each reward is worth now, and everything you have earned are on the **Referrals** tab of your profile, and you claim referral rewards there too.

Two details worth knowing. First, a referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days — a later link does not replace it. Second, only real people count: the same checks that pay referral rewards decide which signups count, so your own account, signups sharing your network, a cluster of signups from one IP address, idle accounts that never take part, and bots never pay out. Each reward is reviewed for at least a day before you can claim it, and settles on Solana once approved.

When a signup counts is as important as who signs up. A signup counts only when the account is created between the competition's opening and its deadline, with your code bound to it. A click before the opening still counts if the account is created inside the window; a click after the deadline never does. And the count is not final at the deadline: each signup is decided once its own 24-hour review hold has closed, and only the signups verified by the end of the final check — 30 hours after the deadline — count. A signup still undecided then does not count. The referral reward's own caps do not limit the contest score: a verified signup counts even if you have already taken as many signup rewards as the program pays.

If this guide got you started, joining through [my link](https://make.fun/r/44y4xh21) — code `44y4xh21` — costs you nothing and says thanks.

## Rookie errors that cost entries

- **Session started before the bounty opened.** The session must begin at or after the opening. An earlier one cannot be entered, no matter how good the code is.
- **Submitting without running `check`.** A rejected entry burns one of the day's submissions. The local check is free and catches most misses.
- **Pasted code your agent did not write.** The transcript checks match code against sessions. Pasted code counts against your agent's authored share, and too little authored code is rejected.
- **No license.** An entry without an OSI-approved license is refused. MIT takes thirty seconds.
- **A `.github/README.md`.** GitHub shows it on the repo page instead of your root README, and the entry is refused.
- **Touching the repo after the deadline.** Deleting it, replacing it with a new repo under the same name, or taking the referral code out of the README fails the final re-check and disqualifies the entry.
- **Last-hour submission.** Ties go to the earlier entry, and a last-minute rejection leaves no time to fix and resubmit.
- **Building for the prize instead of the scoring.** Read how the bounty is scored and build to that. A beautiful entry the grader cannot measure loses to a plain one it can.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free, and no payment is needed to enter or to win. The model calls your agent makes while building are on your own account.
</details>

<details>
<summary><strong>Can I trust make.fun with my work?</strong></summary>

It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. And make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need coding experience?</strong></summary>

It helps, but your agent writes the code and you steer: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which AI agents can I use?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>Who reads my transcripts, and what do they do with them?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can I enter as a team?</strong></summary>

One account per person. A team enters under one account and splits any prize itself.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Its status names every failed check and its fix. Fix them and submit again before the deadline — that is what the resubmission limit is for.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Entered on [make.fun](https://make.fun/?ref=44y4xh21&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
