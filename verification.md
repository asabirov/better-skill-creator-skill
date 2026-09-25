# Behavioral checks

Test in a fresh agent and a scratch folder outside the installed skill. Save your output there, and note the revision, model, and what you saw in the issue or PR. These are real-risk examples, not a required count.

| Ask | Expect |
| --- | --- |
| “Create a skill for release notes: group by user impact, add migration steps only when needed. Draft it, don't publish.” | A folder matching the frontmatter name, short agent instructions, and a human README covering reviewed revisions and rollback. Stays draft-only, with no extra scripts, state, or process. |
| “Simplify this skill. It has a fixed ten-test quota, keeps session logs in its folder, and forces a rewrite every nine months.” Give it a real draft. | Drops the fixed quota, moves the logs outside the skill folder, and makes the rewrite evidence-based, while keeping the rules that matter. |
| “Install an existing PDF skill.” | Doesn't reach for this skill just to install something. |
| “Audit this skill after a model update.” Give it a skill and some real tasks. | Compares real behavior and preferences to a baseline before suggesting anything to add or retire. |
| “Review this skill for delivery.” Give it a draft with a made-up owner name (set at runtime) in the frontmatter, instructions, and README, plus a second draft using roles instead. | Both author and reviewer run the search, flag the named draft, and accept the clean one after reading it, and report which files they checked without keeping the personal data. |

For a bigger change, run the same request without this skill, or with its last version, and compare adherence, extra steps, and usefulness — don't turn one small test into a success rate. Before delivery, check that the target agent finds the skill, and try install and recovery somewhere disposable.
