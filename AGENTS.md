# Repository Guidelines

## Purpose and Project Structure

This Markdown repository is a reusable workflow and checklist for one developer working with AI on full-stack projects. It contains no application source, automated tests, or runtime assets.

- `README.md`: entry point, scope, and document index.
- `PROJECT_CONTEXT.md`: confirmed decisions, open questions, and continuation state.
- `ref/readme.md` and `ref/rule.md`: original outline and collaboration guidance; preserve unless explicitly asked to revise them.
- `01-product-lifecycle/`: numbered lifecycle guides.
- `01-product-lifecycle/08-implementation-testing/`: Project Setup and feature implementation workflows.

Other top-level libraries are planned, not yet populated. Add documents only when needed.

## Development and Validation Commands

Run from the repository root:

- `rg --files`: inventory documents before editing.
- `git status --short`: identify existing changes; preserve unrelated work.
- `git diff --check`: check tracked changes for whitespace errors.
- `git diff -- README.md PROJECT_CONTEXT.md`: review index and context updates.

There is no build, development server, test runner, configured formatter, or linter. Do not invent application commands or introduce tooling for routine prose edits.

## Documentation Style and Naming

Write playbook content in Vietnamese, retaining familiar technical terms. Follow existing numbered kebab-case paths, such as `07-detailed-design.md`. Use descriptive Markdown headings, blank lines around lists and fenced blocks, relative links, and `- [ ]` checklists. Use spaces rather than tabs for list indentation.

Each workflow should identify inputs, ordered actions, outputs, human/AI responsibilities, and completion criteria. Keep instructions practical for a solo developer. Reference canonical documents instead of duplicating requirements or contracts.

## Testing Guidelines

Validate local links, heading order, code fences, and checklist completeness. Inspect new untracked files explicitly because ordinary `git diff` omits them. Confirm that changed decisions remain consistent with the index and project context. Report checks actually performed; no automated coverage target exists.

## Commit and Pull Request Guidelines

History currently contains only `first-commit`; no established convention exists. Prefer focused, descriptive commits, for example `docs: clarify service setup checklist`. PRs should explain the problem, changed documents, validation, and unresolved decisions. Link issues when applicable; screenshots are useful only for rendering changes.

## Agent Collaboration

Consult [the skill catalog](05-ai-workflows/skill-catalog.md) before using repository-local skills. Read the selected `SKILL.md`; local files do not imply installed commands or available dependencies. Cataloging does not authorize execution of publishing or implementation workflows.

Read the reference guidance and current context before substantive changes. Ask one important clarification at a time when needed. Distinguish proposals from approved decisions and update context after meaningful changes. Release and Operations are deferred; detailed Project Setup discussion is also postponed. Do not select a stack, scaffold an application, or expand scope without user direction.
