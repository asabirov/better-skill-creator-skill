# Behavioral checks

Run the proofs in SKILL.md, and record the revision, model and observations in the issue or PR. These are real-risk examples, not a required count.

| Ask | Expect |
| --- | --- |
| “Create a skill for release notes: group by user impact, add migration steps only when needed. Draft it, don't publish.” | A folder matching the frontmatter name, short agent instructions, and a human README covering reviewed revisions and rollback. Stays draft-only, with no extra scripts, state, or process. |
| “Simplify this skill. It has a fixed ten-test quota, keeps session logs in its folder, and forces a rewrite every nine months.” Give it a real draft. | Drops the fixed quota, moves the logs outside the skill folder, and makes the rewrite evidence-based, while keeping the rules that matter. |
| “Install an existing PDF skill,” “find a skill for PDFs,” “is PR 42 ready to merge?”, “tag and release this skill,” and an unrelated task such as fixing a small script bug. | Each skill request loads its intended owner, never this skill; loading no skill fails. The unrelated result matches a run without it. |
| “Is my skill ready to deliver?” without naming this skill. Give it one draft whose PR lists only a few trigger phrasings, and another whose PR has all three proofs but a failed routing or contamination result. | This skill loads and refuses delivery for both, naming each missing or failed proof. |
| “Audit this skill after a model update.” Give it a skill and some real tasks. | Compares real behavior and preferences to a baseline before suggesting anything to add or retire. |
| “Review this skill for delivery.” Give it a draft with a made-up owner name (set at runtime) in the frontmatter, instructions, and README, plus a second draft using roles instead. | Both author and reviewer run the search, flag the named draft, and accept the clean one after reading it, and report which files they checked without keeping the personal data. |

Do not treat one small test as a success rate. Before delivery, try installation and recovery somewhere disposable.
