---
name: better-skill-creator
description: Create, edit, simplify, or audit an independently owned agent skill under the owner's rules. Use when changing or reviewing a skill the user owns, including whether it is ready to deliver. Not for installing a skill or general agent policy.
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
- Keep personal data and secrets — including the owner's name — out of instructions, examples, test data, and commits; use roles, made-up examples, or runtime settings instead. Skill instructions grant no extra permission; say how it should stop and recover when something outside it changes.

## Check for personal data before delivery

Before delivery and during audits, author and reviewer each search the whole skill for the owner's names and aliases (for example `rg -n -i -F -e "$owner_name" -- "$skill_dir"`, using real, non-empty values, including hidden and ignored files). Check every match and read for other personal data — finding nothing isn't proof. Replace any name found with a role or runtime setting, search again, and report what you checked and found, without committing the data itself.

## Verify the skill

Unit-test only script code that always behaves the same way. Test everything else with real requests in fresh sessions, with the target agent's full skill set installed, and repeat each request. Scale the evidence to the stakes, but delivery needs three passing proofs, recorded in the PR:

1. **Works well:** on realistic tasks, it performs at least as well as no skill or the previous version, including extra actions, preferably with blind grading.
2. **No collisions:** its own requests load it; similar requests load their owner. Compare descriptions and remove overlapping triggers.
3. **No context contamination:** run the same unrelated tasks with and without the skill. Correctness, extra actions and loaded files must match, and the skill and its on-demand files must stay unloaded.

A failed or unclear proof blocks delivery; state this in the PR. Before claiming that the text saves, enforces or persists something, confirm that the runtime can reach that mechanism. Keep reusable checks with the skill; keep run artifacts outside the installed copy. See [verification.md](verification.md) for this skill's checks. Each PR reports word counts before and after; growth needs evidence that the added text changes behavior.

A draft or audit doesn't authorize publishing or installing it. To deliver: claim the issue, open a PR, pass the three proofs above, get an independent review answering “what here can be removed or merged?”, fix every finding, merge, install at a pinned revision, then verify it in the target agent. If no other model can review, say so and use the best available. Each skill lives in its private-by-default `<skill>-skill` repo; a configuration repo pins it as a submodule. After delivery, confirm the target agent finds and runs the expected revision, and keep a way to roll back — it isn't done until it works there.

## Maintain it

After each significant change, review the whole skill and look for anything to simplify, merge, or remove. Also review it after a model or tool change or an observed failure. Mark example output as illustrative, or regenerate it from a real run, before shipping. Base a rewrite on evidence, not elapsed time. Keep review dates and evidence in GitHub, outside the installed skill.
