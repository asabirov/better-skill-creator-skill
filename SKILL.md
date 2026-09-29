---
name: better-skill-creator
description: Create, edit, simplify, or audit an independently owned agent skill under the owner's rules. Use for changing or reviewing a skill the user owns. Not for installing a skill or for general agent policy.
metadata:
  version: "0.1.0"
---

# Better skill creator

Capture the owner's rules in as few words as possible, and check them by real use.

## Keep it simple

Keep each skill as simple as possible without losing its goal or must-keep rules. Let the model choose how to get there; add a step, script, or file only when needed, and say when to load it. To fix a failure, first try rewriting or removing existing text. Merge repeats; new rules must replace or merge with existing ones, or the PR must explain why they can't.

A skill holds reusable knowledge or preferences — not every lesson, policy, task history, or unneeded infrastructure. Before creating one, check if an existing skill covers this and who owns it, then edit that instead.

## Write it

- State a clear purpose and exclusion, with a name and description that don't overlap other skills. Match the frontmatter name to the skill's folder; the shared repo may add `-skill`.
- Lead with outcomes, must-keep rules, and decision criteria — skip steps unless order or precision matters, and skip advice the model knows. State each rule once, in one place across SKILL.md, README.md, and verification.md.
- `SKILL.md` holds agent instructions; `README.md` holds human usage, install, update, rollback, and removal steps. Use Mermaid only for a real decision, handoff, or set of states, never as a second rulebook.
- Treat the installed folder as read-only; keep logs, caches, and other output outside it. If the skill must remember something between runs, say what and where, and edit source through the repo's workflow.
- Prefer existing tools; add a dependency only when it's more reliable or saves more build-and-maintain work than doing it yourself, and say so. Don't depend on another skill's files or machine-specific paths.
- Exclude secrets and hard-coded user/install data from instructions, examples, tests, and commits: names, emails, machines, hosts, IPs, accounts, repositories. Use runtime settings, roles, or made-up examples; fixed interface names and documented tool defaults may stay. Instructions grant no permission; explain stopping and recovery from outside changes.

## Check data before delivery

Before delivery and during audits, author and reviewer each search the whole skill, including hidden and ignored files, for known owner aliases and deployment values: `rg -n --hidden --no-ignore -i -F -e "$candidate" -- "$skill_dir"` (non-empty runtime values). Read for unknown literals too; no matches isn't proof. Classify candidates, give borderline values kept a one-line reason, replace violations, and search again. Report coverage and findings without committing real data.

## Version and install it

On creation or audit, check visibility and release setup. Preserve existing versions, automation, and intentional package-version placeholders; start unversioned skills at `0.1.0`. Document one version source in the README, defaulting to quoted `metadata.version` in [Agent Skills frontmatter](https://agentskills.io/specification#metadata). Apply [SemVer](https://semver.org/spec/v2.0.0.html) to the skill contract: patch for fixes, minor for compatible capabilities, major for breaking activation, dependencies, output, or workflow. Extend automation to stamp/check that source; don't add a second process.

After authorized merge and release, the reviewed commit needs an immutable `vMAJOR.MINOR.PATCH` tag and matching GitHub release with concise change and migration notes. Verify the version source at that commit agrees with both; never move published tags. Unchanged released skills need no new release. Report missing authorization or release evidence instead of claiming delivery.

Keep each created or versioned skill's `CHANGELOG.md` readable by someone who has never seen the skill:

- Start the file with `# Changelog`. Give each release one heading: `## <version> — <YYYY-MM-DD>`, or `## <version> — Unreleased` until it is released.
- Under a heading, use only non-empty `### Added`, `### Changed`, `### Fixed` and `### Removed` groups. A first release opens with one plain sentence saying what the skill does and who uses it.
- Write each entry as two lines, addressing the reader as "you":

  ```md
  - **<Short name>.** <What is different for you now.> <Why it matters or what it prevents.>
    Action: <What you must do to get this change or keep things working, or "None.">
  ```

  `Action:` names a required step, not a usage tip. Use plain words, explain an unavoidable term in brackets, and leave out internal jargon, file paths and script names the reader would not run. Claim nothing the skill does not deliver.
- Test each entry: give it alone to a model with no other context and ask what changed and whether you must act. The answer should match the change.

Worked example, for an illustrative upload skill:

```md
## 0.2.0 — 2026-09-29

### Changed
- **Sign-in during setup.** You now sign in to GitHub once during setup instead of at your first upload. Uploads no longer stop halfway to ask for a password.
  Action: Run the setup command again after updating.

### Fixed
- **Large PDFs.** PDFs up to 10 MB now upload instead of timing out.
  Action: None.
```

For public repos, write one README install line for both agents using the actual repo, skill, and released tag. Don't run it over a skill already installed through the owner's managed configuration. Illustrative [skills CLI](https://github.com/vercel-labs/skills#readme) form ([ref parser](https://github.com/vercel-labs/skills/blob/main/src/source-parser.ts)):

```sh
DO_NOT_TRACK=1 npx skills add https://github.com/OWNER/REPO/tree/TAG --skill SKILL --agent claude-code codex --global
```

Explain the [telemetry opt-out](https://github.com/vercel-labs/skills#telemetry), Node/npm and Git prerequisites, and each skill's runtime needs. For updates or rollback, reinstall the chosen release; don't promise that `skills update` follows tags. Don't advertise an unreleased tag as installable.

Private repos need version/release details, not public installer docs. If a configuration repo pins the skill as a submodule, document that authenticated path; don't add pins automatically. Advance those pins through configuration PRs only to released tag commits, preserving the old SHA for rollback. Verify installed commits, not nearby tags.

## Verify the skill

Match how much you check to the stakes, not a fixed count. Unit-test only script code that always behaves the same way. Check instructions and model output with real requests: judge the result, confirm it fires when it should, and stays quiet on look-alikes. When a description changes, test a handful of likely phrasings, a few tries each, and note which ones route to the skill. Before the text claims it saves, enforces, or persists something, confirm the runtime can actually reach that mechanism. For a bigger change, compare against the old version or no skill, watching for extra actions, not just final output. Keep reusable checks with the skill; run artifacts outside the installed copy. See [verification.md](verification.md) for this skill's checks. Each PR reports word counts before and after; growth needs evidence that the added text changes behavior.

A draft or audit doesn't authorize publishing or installing it. The default delivery workflow is: claim the issue, open a PR, run the checks above, get an independent review answering “what here can be removed or merged?”, fix every finding, merge, release, install the released revision, then verify it in the target agent. If no other model can review, say so and use the best available. Use the owner's repository naming, visibility, and delivery conventions; the defaults are one private `<skill>-skill` repo per skill and the workflow above. After delivery, confirm the target agent finds and runs the expected revision — it isn't done until it works there.

## Maintain it

After each significant change, review the whole skill and look for anything to simplify, merge, or remove. Also review it after a model or tool change or an observed failure. Mark example output as illustrative, or regenerate it from a real run, before shipping. Base a rewrite on evidence, not elapsed time. Keep review dates and evidence in GitHub, outside the installed skill.
