# Better skill creator

Build simple agent skills under the owner's rules. The rules live in [SKILL.md](SKILL.md); change them only through this repo's issues and PRs.

This skill is separate from the bundled `skill-creator`, so each stays separately maintainable. It needs an agent that supports the [Agent Skills format](https://agentskills.io/specification), has no runtime packages or scripts, and needs Git and authenticated access to this private repo to install, plus GitHub access to deliver.

## Install

Clone it somewhere durable, into a folder named `better-skill-creator`; the commands below assume you're already there. Get the full commit SHA from the merged PR you want, and use it as `REVIEWED_COMMIT`.

```sh
git clone https://github.com/asabirov/better-skill-creator-skill.git better-skill-creator
git -C better-skill-creator checkout --detach REVIEWED_COMMIT
```

Link that checkout into your agent's skills folder. For Codex, with default settings:

```sh
mkdir -p "$HOME/.codex/skills"
ln -s "$PWD/better-skill-creator" "$HOME/.codex/skills/better-skill-creator"
```

For Claude Code, use `$HOME/.claude/skills/better-skill-creator` instead, or your configured skills folder. Check what's there before you change it; don't overwrite another install. A configuration repo can instead pin this repo at `skills/better-skill-creator` as a Git submodule and expose that checkout.

## Use and check it

Start a fresh agent session and call it directly — `$better-skill-creator` in Codex, `/better-skill-creator` in Claude Code. For example:

> Use better-skill-creator to create a skill for our internal release notes. Group changes by user impact and include migration steps only when needed. Keep it simple.

Confirm the agent reads this install's `SKILL.md`. Also try an authoring request without naming the skill, and see which one loads — other creator skills can compete for that, and only naming this one guarantees it. Change that overlap only on purpose, never by editing another skill's files.

Use the cases in [verification.md](verification.md) to judge the result. A file that loads fine isn't proof the output is good.

## Update, roll back, remove

Note the current revision: `git -C better-skill-creator rev-parse HEAD`. To update, fetch and check out the newly reviewed commit:

```sh
git -C better-skill-creator fetch origin
git -C better-skill-creator checkout --detach REVIEWED_COMMIT
```

To roll back, check out the SHA you noted earlier. For a submodule install, change the pin through the configuration repo's PR. Keep the installed checkout free of local edits, and re-check it in a fresh session after any change.

Before removing a symlink install, confirm it's really a symlink to this checkout, then unlink it. Keep the checkout until you no longer need it for recovery. Removing a submodule install also needs a PR in the configuration repo. Remove every place you exposed this skill to an agent.

Maintenance cadence and authoring rules live in [SKILL.md](SKILL.md). Record audits as issues in this repo — this skill doesn't schedule itself or keep its own run state.
