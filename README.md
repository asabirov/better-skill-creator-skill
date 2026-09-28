# Better skill creator

Build simple agent skills under the owner's rules. The rules live in [SKILL.md](SKILL.md); change them only through this repo's issues and PRs.

This skill is separate from the bundled `skill-creator`, so each stays separately maintainable. It needs an agent that supports the [Agent Skills format](https://agentskills.io/specification), has no runtime packages or scripts, and needs Git and authenticated access to this private repo to install, plus GitHub access to deliver.

## Install

The version source is `metadata.version` in [SKILL.md](SKILL.md). The first release is pending; these instructions apply once its matching tag and GitHub release exist.

Use the authenticated configuration checkout that manages this private skill at `skills/better-skill-creator`. From that checkout, initialize its recorded pin:

```sh
git submodule update --init -- skills/better-skill-creator
git -C skills/better-skill-creator rev-parse HEAD
```

Confirm the pin is exactly the selected release's commit. Preserve the existing agent links; if a link is missing, expose this submodule in the agent's configured skills folder under `better-skill-creator`. For Codex with default settings, from that checkout’s root:

```sh
mkdir -p "$HOME/.codex/skills"
ln -s "$PWD/skills/better-skill-creator" "$HOME/.codex/skills/better-skill-creator"
```

For Claude Code, use `$HOME/.claude/skills/better-skill-creator` instead, or your configured skills folder. Check what's there before you change it; don't overwrite another install.

## Use and check it

Start a fresh agent session and call it directly — `$better-skill-creator` in Codex, `/better-skill-creator` in Claude Code. For example:

> Use better-skill-creator to create a skill for our internal release notes. Group changes by user impact and include migration steps only when needed. Keep it simple.

Confirm the agent reads this install's `SKILL.md`. Also try an authoring request without naming the skill, and see which one loads — other creator skills can compete for that, and only naming this one guarantees it. Change that overlap only on purpose, never by editing another skill's files.

Use the cases in [verification.md](verification.md) to judge the result. A file that loads fine isn't proof the output is good.

## Update, roll back, remove

Record the current SHA with `git -C skills/better-skill-creator rev-parse HEAD`. Advance the pin through a configuration-repository PR only to a reviewed GitHub release. Replace `RELEASE_TAG` below with that release's tag, and confirm its version agrees with `SKILL.md` at the selected commit:

```sh
git -C skills/better-skill-creator fetch origin --tags
git -C skills/better-skill-creator checkout --detach RELEASE_TAG
git -C skills/better-skill-creator rev-parse HEAD
```

To roll back, restore the previous SHA through a configuration-repository PR, preserving any pin hold so reconciliation doesn't undo the rollback. Keep the installed checkout free of local edits, and re-check it in a fresh session after any change.

To remove it, confirm each agent link points to this submodule before unlinking it. Remove the submodule through a configuration-repository PR; retain the previous pin for recovery.

Maintenance cadence and authoring rules live in [SKILL.md](SKILL.md). Record audits as issues in this repo — this skill doesn't schedule itself or keep its own run state.
