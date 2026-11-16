# Better skill creator

Create and maintain simple agent skills using the opinionated rules in
[SKILL.md](SKILL.md). Adopt them as written or adapt them to your workflow.

Agent skills grow long and drift from what the agent really does. This skill
keeps authoring instructions short, checks them through real use, and documents
installation and recovery. It stays separate from the bundled skill-creator so
each can be maintained independently. It has no scripts and no eval harness:
a person checks the output of real requests against
[verification.md](verification.md).

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
DO_NOT_TRACK=1 npx skills add https://github.com/asabirov/better-skill-creator-skill/tree/v0.1.4 --skill better-skill-creator --agent claude-code codex --global
```

`DO_NOT_TRACK=1` turns off [skills CLI telemetry](https://github.com/vercel-labs/skills#telemetry).
If your configuration already manages this skill, update it there instead of
installing another copy.

| Dependency | Why |
| --- | --- |
| Node.js and npm | `npx skills` runs the installer |
| Git | The installer fetches the tagged release |
| An agent that supports the [Agent Skills format](https://agentskills.io/specification) | The agent loads `SKILL.md` |
| GitHub access | The skill delivers changes through branches, PRs and releases |

The version source is `metadata.version` in [SKILL.md](SKILL.md). To update
or roll back, record the tag you have now, then run the install command again
with the selected release tag. Do not assume that `skills update` follows tags.
This repo releases by hand: update the install line above when creating the
release tag. Remove the skill with:

```sh
DO_NOT_TRACK=1 npx skills remove better-skill-creator --agent claude-code codex --global
```

After any change, check discovery in a fresh agent session.

## Use

Start a new agent session and call the skill directly: use
`$better-skill-creator` in Codex or `/better-skill-creator` in Claude Code.
Then ask it to create, edit, simplify or audit a skill that you own.
For example:

> Use better-skill-creator to draft a release-notes skill. Group changes by user impact and include migration steps only when needed. Don't publish or install it.

## Verify

From a source checkout, this read-only discovery command should find one
skill, `better-skill-creator`:

```sh
DO_NOT_TRACK=1 npx skills add . --list
```

This checks discovery only; the behavioral trials below check the output.

Make the request of [Use](#use). Confirm that the agent reads this installation's `SKILL.md`. Then evaluate
the draft with [verification.md](verification.md). Also make an authoring
request without naming the skill and check which skill loads, because other
creator skills may compete for the request. Change that overlap only
intentionally; never edit another skill's files.

## Maintenance and license

Maintenance timing, versioning, and the required readable `CHANGELOG.md` format
are defined in [SKILL.md](SKILL.md), including a worked entry example.
Record audits as issues in this repository; the skill does not schedule itself
or store run state. This repository is licensed under the [MIT License](LICENSE).
