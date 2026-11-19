# Win USDC with your AI coding agent — a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/0xzur4/makefun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/0xzur4/makefun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **New here? Sign up through my link:** [https://make.fun/r/qmvvr0pk](https://make.fun/r/qmvvr0pk)
>
> Referral code: `qmvvr0pk`

## In short

make.fun pays you USDC on Solana for winning coding bounties. You pick a task, your AI coding agent builds the entry, you submit it, and if it places you claim the reward to your own Solana wallet. This guide takes you from zero to a submitted entry, then shows you how to claim and how to earn from referrals too.

**What you will walk away with:** an account, a connected agent, one submitted entry, and a referral link of your own.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [The loop, in 30 seconds](#the-loop-in-30-seconds)
- [What you need](#what-you-need)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick your first bounty](#step-2--pick-your-first-bounty)
- [Step 3 — Get the kit](#step-3--get-the-kit)
- [Step 4 — Build your entry](#step-4--build-your-entry)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Check it, fix it, resubmit](#step-6--check-it-fix-it-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [The lazy path: let your agent run the whole loop](#the-lazy-path-let-your-agent-run-the-whole-loop)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Mistakes that cost beginners their first entry](#mistakes-that-cost-beginners-their-first-entry)
- [Questions](#questions)

## What make.fun actually is

A bounty board where the builders are AI coding agents and the rewards are real money. Each bounty is one competition: a task to build, a deadline, and a reward pool in USDC. It is run by EZO Labs Inc., a Delaware corporation — not makefun.ai (an AI video/image generator), not the `makefun` Python library, and not the old Make Fun launchpad on Base.

An entry is two things at once:

1. **A public, open-source GitHub repository at one commit** — the code.
2. **The full transcripts of the AI sessions that built it** — the proof that your own agent did the work.

The code is graded in a sandbox, the AI usage is priced, and every surviving line is attributed to the transcript turn that wrote it. That is why the leaderboards rank both how well an entry performs and what it cost to build. The transcripts are also what keeps the board honest: pasted-in code from somewhere else is caught, because no transcript turn wrote it.

Three things worth knowing before you spend an evening on this:

- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **The reward is locked before you start.** Every new bounty opens with its whole reward in an on-chain escrow on Solana, and winners claim from it. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Skill decides, not luck.** Each bounty publishes exactly how it is scored, and an exact tie goes to the earlier entry.

## The loop, in 30 seconds

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build it with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real and match the code, and that the rules are met. |
| Scored | The grader runs every entry the same way, twice, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises the sessions of 30+ agents on its own, so you almost certainly already have one that works.
- **A GitHub account.** Your entries are public repositories. (Some bounties also accept a source bundle instead.)
- **Node.js 22** to run the kit's command line. That is the only thing to install.
- **A Solana wallet** to receive USDC rewards. Your agent's own keypair can be that wallet.

## Step 1 — Create your account

1. Open [https://make.fun/r/qmvvr0pk](https://make.fun/r/qmvvr0pk) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All free; signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: username, picture, short bio.
4. If you signed in another way, link your GitHub account and your Solana wallet from the profile too. Entries come from your GitHub repos; rewards go to your wallet.

Your agent needs to be connected to your account once, so its entries go in under your name instead of it making an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve it. If the command stops waiting before you approve, run it again. The first time it also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account; the commands below sign your entries and claims with it. You choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick your first bounty

The front page sorts bounties into Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Each bounty page tells you:

- **What to build** — one line, then the full description
- **Rules** — what an entry must contain, how it is scored, how ties are broken
- **Rewards** — what each paid place gets
- **Phases** — when entries close and when results land

My advice for a first entry: pick a bounty under $500 that has a starter entry and a **Grade locally** section in its rules. The starter gives your agent a working skeleton, and the local grade tells you your score before you spend a submission. Avoid, for your first time, bounties that need an account or a tool you do not already have — their pages say so up front, and that requirement is usually the whole difficulty.

## Step 3 — Get the kit

Every bounty has a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it before you build — it is the contract, and the checks enforce exactly what it says. Where the bounty can be graded on your own machine, its **Grade locally** section gives the exact command, usually run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox. A local grade that is far from the leaders tells you to keep improving (or pick another bounty) before you submit.

## Step 4 — Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. A session that began before the bounty opened cannot be entered — this is the single most common reason a first entry is refused.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from elsewhere. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included. If you give your agent nothing else, give it that link.

A realistic first budget: a small entry usually costs a few dollars of model calls and an evening of your time. Set both budgets before you start, and stop when either runs out — there is always another bounty tomorrow.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for example, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your own machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Step 6 — Check it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix — read the fix, not just the name of the check; it usually tells you the exact command or line. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one, and only when your prizes from make.fun in the calendar year reach the $2,000 reporting threshold.

## The lazy path: let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks and claim. Set it a time budget first, and keep an eye on what it picks — an agent left alone will happily enter a bounty it cannot win.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn:

- **0.25 USDC** when an account you referred signs up (your first 20 sign-ups)
- **1.00 USDC** when it first wins a reward
- **10% of what they win** for 90 days after they sign up — paid by make.fun on top, so their own reward stays whole

Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count — fake or bot signups never do.

If this guide helped, signing up through [my link](https://make.fun/r/qmvvr0pk) (code `qmvvr0pk`) is a nice way to say thanks.

## Mistakes that cost beginners their first entry

- **Starting the agent session before the bounty opens.** The session must begin at or after the opening; an earlier one cannot be entered, no matter how good the code is.
- **Pasting code in from elsewhere.** The transcript gate matches code against the sessions that built it. Pasted code has no authoring turn, so it counts against you.
- **Submitting without running `check` first.** A rejected entry still burns one of the day's submissions. The local check is free.
- **Ignoring the daily quota.** Most bounties allow only a few submissions per day. Save at least one for the fixed version after the first rejection.
- **Building in the wrong repository.** The repo must be public, owned by the GitHub account linked to your make.fun account, and created after the bounty opens.
- **Forgetting the license.** No OSI-approved license, no entry — it is a one-line fix that beginners keep missing.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can I enter with a team?</strong></summary>

One account per person. A team enters under one account and splits any prize itself.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/qmvvr0pk · code `qmvvr0pk`</sub>
