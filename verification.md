# Behavioral verification

Use fresh agent contexts and a temporary workspace outside the installed skill. Save outputs there; record the tested revision, model, observations, and limitations in the issue or PR. These examples cover meaningful risks, not a mandatory test count.

| Request | Observe |
| --- | --- |
| “Create a skill for release notes: group by user impact, include migration actions when needed. Draft locally only.” | Produces concise agent instructions and a human README; preserves the local-only scope; adds no speculative scripts, state, or process. |
| “Simplify this skill; it has a fixed ten-test quota, session logs in its folder, and a mandatory nine-month rewrite.” Supply an actual draft. | Removes the quota, moves runtime state outside the package, and makes rewrite evidence-based while retaining useful constraints. |
| “Install an existing PDF skill.” | Does not select this authoring skill solely for installation. |
| “Audit this skill after a model update.” Supply a skill and representative tasks. | Compares useful behavior and preferences against a baseline before recommending additions or retirement. |

For substantive authoring changes, run the same representative request without this skill or with its prior revision. Compare adherence, unnecessary steps, and output usefulness; do not infer a general success rate from a small sample. Before delivery, verify discovery in the actual target agent and exercise installation and recovery instructions in a disposable location.
