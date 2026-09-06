# Better skill creator

Create and maintain simple agent skills under the owner's rules. The authoring standard lives in [SKILL.md](SKILL.md); change it through this repository's issues and pull requests.

This is an independent skill named `better-skill-creator`, so bundled `skill-creator` files remain separately maintainable. It requires an agent supporting the [Agent Skills format](https://agentskills.io/specification). There are no runtime packages or scripts. Git and authenticated access to this private repository are needed to install; GitHub access is needed for delivery work.

## Install

Clone into a durable location with the folder name `better-skill-creator`. The commands below use the current directory; choose that location before running them. Obtain the reviewed commit from the merged PR you want to install and replace `REVIEWED_COMMIT` with its full SHA.

```sh
git clone https://github.com/asabirov/better-skill-creator-skill.git better-skill-creator
git -C better-skill-creator checkout --detach REVIEWED_COMMIT
```

Link that checkout into your agent's skill directory. For Codex with its default configuration:

```sh
mkdir -p "$HOME/.codex/skills"
ln -s "$PWD/better-skill-creator" "$HOME/.codex/skills/better-skill-creator"
```

For Claude Code, use `$HOME/.claude/skills/better-skill-creator` instead. Respect a custom skill directory if configured. Inspect an existing destination before changing it; do not overwrite another installation. Configuration repositories can instead consume this repository at `skills/better-skill-creator` as a pinned Git submodule and expose that checkout.

## Use and verify

Start a fresh agent session and explicitly invoke `$better-skill-creator` in Codex or `/better-skill-creator` in Claude Code. For example:

> Use better-skill-creator to create a skill for our internal release notes. Group changes by user impact and include migration actions only when needed. Keep it simple.

Confirm the agent reads this installation's `SKILL.md`. Also try an ordinary authoring request without naming it and inspect which skill loads. Other creator skills can compete for discovery; explicit invocation selects this one. Adjust overlapping exposure only deliberately, without editing vendor files.

Use the scenarios in [verification.md](verification.md) to assess behavior. A valid file or successful load alone does not prove useful output.

## Update, rollback, remove

Record the current revision with `git -C better-skill-creator rev-parse HEAD`. Fetch updates, then detach at the newly reviewed commit:

```sh
git -C better-skill-creator fetch origin
git -C better-skill-creator checkout --detach REVIEWED_COMMIT
```

Rollback by checking out the recorded previous SHA. For submodule installations, update or revert the pin through the configuration repository's PR workflow. Keep the installed checkout free of local edits, and verify again in a fresh session.

To remove a symlink installation, first confirm it is a symlink to this checkout, then unlink that skill entry. Retain the checkout until recovery is no longer needed. Removing a managed submodule also requires a configuration PR. Remove all agent exposure entries you installed.

Maintenance cadence and authoring requirements are defined in [SKILL.md](SKILL.md). Record audits in repository issues; this skill does not schedule itself or store execution state.
