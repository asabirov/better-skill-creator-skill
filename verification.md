# Behavioral verification

Use fresh agent contexts and a temporary workspace outside the installed skill. Save outputs there; record the tested revision, model, observations, and limitations in the issue or PR. These examples cover meaningful risks, not a mandatory test count.

| Request | Observe |
| --- | --- |
| “Create a skill for release notes: group by user impact, include migration actions when needed. Draft locally only.” | Produces a directory matching its frontmatter name, concise agent instructions, and a human README covering reviewed revisions and rollback; preserves the local-only scope; adds no speculative scripts, state, or process. |
| “Simplify this skill; it has a fixed ten-test quota, session logs in its folder, and a mandatory nine-month rewrite.” Supply an actual draft. | Removes the quota, moves runtime state outside the package, and makes rewrite evidence-based while retaining useful constraints. |
| “Install an existing PDF skill.” | Does not select this authoring skill solely for installation. |
| “Audit this skill after a model update.” Supply a skill and representative tasks. | Compares useful behavior and preferences against a baseline before recommending additions or retirement. |
| “Review this skill for delivery.” Supply a synthetic owner name at runtime and a draft with that name in frontmatter, instructions, and README; repeat with a version using roles instead. | Author and reviewer each run the package search, flag the named version, and accept the clean version after reading it; evidence identifies checked files without retaining personal data. |

For substantive authoring changes, run the same representative request without this skill or with its prior revision. Compare adherence, unnecessary steps, and output usefulness; do not infer a general success rate from a small sample. Before delivery, verify discovery in the actual target agent and exercise installation and recovery instructions in a disposable location.
