# Changelog

## 0.1.4 — Unreleased

### Changed

- **Shorter dependency lists.** Your dependency list now holds only external tools, libraries, and skills, and the formats and paths your skill defines belong with the steps that use them.

## 0.1.3 — 2026-10-03

### Changed

- **Independent skills.** The skill now asks you to state what your skill needs as an input or outcome instead of naming, calling, or requiring another skill, or a tool or service its purpose doesn't need, and its audits flag each violation.

- **A word budget for skill edits.** The skill now holds each change to 40 words of growth in its main instruction file unless you show the extra words change what the agent does, and asks you to cut any added sentence that doesn't stop a mistake.

## 0.1.2 — 2026-09-30

### Changed

- **Shorter changelog entries.** Changelog entries are now a bold name and one short sentence, with an `Action:` line only when you must act.

- **README tag tracks the release.** The skill now requires updating a public skill's README install line in the same step that creates its release tag.

## 0.1.1 — 2026-09-30

### Added

- **Public install.** You can install, update, roll back, and remove the skill with one `npx skills` command pinned to a release tag, instead of cloning it and linking it into your agent's skills folder by hand.

## 0.1.0 — 2026-09-29

This skill creates, edits, simplifies, and audits an independently owned agent skill under the owner's rules, for the person changing or reviewing a skill they own.

### Added

- **Simplicity check.** The skill keeps every rule stated once and merges repeats instead of piling on new text, so your skill stays as short as it can be without losing its goal or must-keep rules.

- **Structure rules for writing a skill.** The skill puts agent instructions in `SKILL.md` and human install and recovery steps in `README.md`, and checks the frontmatter name and description against other skills, so you get a skill that reads clearly and doesn't compete with one that already covers the same ground.

- **Search for hidden owner data.** Before delivery, the skill searches the whole skill, including hidden and ignored files, for known owner names, emails, hosts, and other deployment values, so real personal or machine-specific data doesn't ship inside instructions, examples, or tests.

- **Versioning and release preparation.** The skill applies Semantic Versioning to the skill's contract and, once authorized, prepares a matching immutable tag and GitHub release, so a version number always reflects what actually changed.

- **Readable changelog format.** The skill writes each changelog entry as a short bold name plus what changed and why it matters, checked by handing the entry alone to a model with no other context, so anyone who has never seen the skill can tell what changed and whether they must act.

- **Behavioral verification.** The skill tests the skill's instructions against real requests — confirming it fires when it should and stays quiet on look-alikes — instead of trusting that the file merely loads, so you know the skill works before it ships.
