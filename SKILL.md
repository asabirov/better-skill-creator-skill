---
name: better-skill-creator
description: Create, edit, simplify, or audit independently owned agent skills under the owner's authoring rules. Use when the user wants their own skill, changes to its instructions, or a skill maintenance review. Not for merely installing an existing skill or changing general agent policy.
---

# Better skill creator

Create and maintain independently owned skills that encode the owner's requirements with minimal instructions and dependencies, verified through realistic use.

## Simplicity and boundaries

Keep the skill as simple as possible while preserving its intended outcome and essential constraints. Let the model choose how to achieve the goal. Add steps, scripts, supporting files, or dependencies only when they solve a demonstrated problem. Ask what can be removed without weakening results.

A skill is for reusable knowledge or preferences that improve relevant behavior. It is not a home for every lesson, general agent policy, task history, or speculative infrastructure. Inspect existing skills and ownership before creating another; prefer a focused edit when it belongs to an existing skill.

## Authoring rules

- State a concise purpose and likely exclusions. Give the skill a distinct name and a precise activation description that differentiates it from overlapping skills. Match frontmatter `name` to the containing skill directory; the remote repository may use the `-skill` suffix.
- Write outcomes, essential constraints, and useful decision criteria first. Specify exact steps only when sequence or precision matters. Omit generic advice the model already knows. Keep each requirement in one authoritative place.
- Use `SKILL.md` with standard `name` and `description` frontmatter for agent instructions, and `README.md` for human usage, installation and updates at a reviewed revision, rollback, and removal. Add supporting files only when needed; explain when to load each reference. Use Mermaid when it clarifies meaningful decisions, handoffs, or states, without creating a second requirements document.
- Treat the installed skill directory as read-only during execution. Put logs, caches, progress, and temporary output outside it. Declare any necessary external persistent state and its location. Source edits belong in the repository workflow.
- Prefer available tools and minimal dependencies. Add a dependency when its reliability or avoided implementation and maintenance cost justifies it; declare it explicitly. Avoid dependencies on another skill's internal files or machine-specific paths.
- Keep personal data and secrets out of instructions, examples, fixtures, and committed results. Use synthetic examples and runtime configuration. Skill instructions grant no extra permissions; define stopping and recovery behavior where external changes make it necessary.

## Verification and delivery

Scale verification to the behavior and risk, without test quotas or assertions that merely match wording. Check realistic outcomes, intended activation, and nearby requests that should not activate the skill. For substantive changes, compare behavior with the prior version or without the skill; inspect unnecessary actions as well as final output. Keep reusable checks with the skill, and run artifacts outside the installed package. See [verification.md](verification.md) when verifying this authoring skill.

Respect the requested scope: a local draft or audit does not authorize publication or installation. For delivery, each skill has its own private-by-default `<skill>-skill` repository. Claim the issue before editing. Deliver through issue → PR → behavioral checks → independent review → merge → pinned install → target verification. Resolve findings before merging. If another model is unavailable, disclose it and use the strongest available independent review. Configuration repositories consume pinned submodules. Verify the installed revision and discovery in the target agent; preserve a rollback path. Completion means the intended outcome works there.

## Maintenance

Audit every three months and after relevant model or tool changes or observed failures. Prefer removal and simplification backed by behavior checks. Every nine months, reassess from first principles whether to retain, simplify, rewrite, merge, or retire the skill. Recommend a rewrite when evidence supports it, not solely because time passed. Keep review dates and evidence in GitHub, outside the installed package.
