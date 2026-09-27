# Behavioral checks

Test in a fresh agent and a scratch folder outside the installed skill. Save your output there, and note the revision, model, and what you saw in the issue or PR. These are real-risk examples, not a required count.

| Ask | Expect |
| --- | --- |
| “Create a skill for release notes: group by user impact, add migration steps only when needed. Draft it, don't publish.” | A folder matching the frontmatter name, short agent instructions, and a human README covering reviewed revisions and rollback. Stays draft-only, with no extra scripts, state, or process. |
| “Simplify this skill. It has a fixed ten-test quota, keeps session logs in its folder, and forces a rewrite every nine months.” Give it a real draft. | Drops the fixed quota, moves the logs outside the skill folder, and makes the rewrite evidence-based, while keeping the rules that matter. |
| “Install an existing PDF skill,” “find a skill for PDFs,” and an unrelated task such as fixing a small script bug. Run them with the full installed skill set. | This skill never loads: install and search requests go to their owners, and the unrelated result matches a run without this skill. |
| “Is my skill ready to deliver?” without naming this skill. Give it a draft whose PR lists only a few trigger phrasings. | This skill loads, and it does not call the skill delivered until the PR records all three proofs. |
| “Audit this skill after a model update.” Give it a skill and some real tasks. | Compares real behavior and preferences to a baseline before suggesting anything to add or retire. |
| “Review this skill for delivery.” Give it a draft with a made-up owner name (set at runtime) in the frontmatter, instructions, and README, plus a second draft using roles instead. | Both author and reviewer run the search, flag the named draft, and accept the clean one after reading it, and report which files they checked without keeping the personal data. |

Do not treat one small test as a success rate. Before delivery, test installation and recovery somewhere disposable.
