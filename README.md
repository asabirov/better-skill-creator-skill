# Better skill creator

Create and maintain simple agent skills using the opinionated rules in
[SKILL.md](SKILL.md). Adopt them as written or adapt them to your workflow.

This skill keeps authoring instructions short, checks them through real use,
and documents installation and recovery. It stays separate from the bundled
skill-creator so each can be maintained independently.

## Design

Put agent rules in `SKILL.md` and human instructions here. Behavioral checks
evaluate the agent's output; a file loading successfully does not prove that
the skill works. This repository has no runtime packages or scripts.

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Rules for authoring, verification and delivery |
| [verification.md](verification.md) | Trial requests and expected behavior |
| [README.md](README.md) | Installation, use and recovery |

## Install, update, roll back, and remove

Install the tagged skill for Claude Code and Codex with:

```sh
DO_NOT_TRACK=1 npx skills add https://github.com/asabirov/better-skill-creator-skill/tree/v0.1.1 --skill better-skill-creator --agent claude-code codex --global
```

`DO_NOT_TRACK=1` turns off [skills CLI telemetry](https://github.com/vercel-labs/skills#telemetry).
The `npx skills` installer requires Node.js/npm and Git. The agent must support
the [Agent Skills format](https://agentskills.io/specification), and delivering
changes also requires GitHub access. If your configuration already manages
this skill, use the owner section below instead of installing another copy.

The version source is `metadata.version` in [SKILL.md](SKILL.md). To update
or roll back, record the tag you have now, then run the install command again
with the selected release tag. Do not assume that `skills update` follows tags.
This repo releases by hand: update the install line above when creating the
release tag. Remove the skill with:

```sh
DO_NOT_TRACK=1 npx skills remove better-skill-creator --agent claude-code codex --global
```

After any change, check discovery in a fresh agent session.

## Verify

From a source checkout, this read-only discovery command should find one
skill, `better-skill-creator`:

```sh
DO_NOT_TRACK=1 npx skills add . --list
```

This checks discovery only; the behavioral trials below check the output.

Start a new agent session and call the skill directly: use
`$better-skill-creator` in Codex or `/better-skill-creator` in Claude Code.
For example:

> Use better-skill-creator to draft a release-notes skill. Group changes by user impact and include migration steps only when needed. Don't publish or install it.

Confirm that the agent reads this installation's `SKILL.md`. Then evaluate
the draft with [verification.md](verification.md). Also make an authoring
request without naming the skill and check which skill loads, because other
creator skills may compete for the request. Change that overlap only
intentionally; never edit another skill's files.

## Owner section: managed installation

Public users can skip this section. It preserves the existing authenticated
configuration checkout and agent links.

Use the authenticated configuration checkout that manages this skill at `skills/better-skill-creator`. From that checkout, initialize its recorded pin:

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

### Update, roll back, remove a managed install

Record the current SHA with `git -C skills/better-skill-creator rev-parse HEAD`. Advance the pin through a configuration-repository PR only to a reviewed GitHub release. Replace `RELEASE_TAG` below with that release's tag, and confirm its version agrees with `SKILL.md` at the selected commit:

```sh
git -C skills/better-skill-creator fetch origin --tags
git -C skills/better-skill-creator checkout --detach RELEASE_TAG
git -C skills/better-skill-creator rev-parse HEAD
```

To roll back, restore the previous SHA through a configuration-repository PR, and make sure no automatic update moves the pin forward again. Keep the installed checkout free of local edits, and re-check it in a fresh session after any change.

To remove it, confirm each agent link points to this submodule before unlinking it. Remove the submodule through a configuration-repository PR; retain the previous pin for recovery.

## Maintenance and license

Maintenance timing, versioning, and the required readable `CHANGELOG.md` format
are defined in [SKILL.md](SKILL.md), including a worked entry example.
Record audits as issues in this repository; the skill does not schedule itself
or store run state. This repository is licensed under the [MIT License](LICENSE).
