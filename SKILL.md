---
name: documentation
description: Apply whenever creating, reviewing, or reorganizing project documentation. Enforces a simple two-guide documentation model (user guide and developer guide), a curated changelog, and commit message conventions that support maintainable project history.
---

# Documentation

## Overview

This skill defines a minimal, consistent documentation structure for any codebase. It is language-agnostic. Every project should have four core documents: a front-page README, a changelog, a user guide, and a developer guide. The goal is to make the project usable by end users and understandable by humans and AI agents who need to maintain or deploy it.

## Required Documents

Every project must contain these files:

- `README.md` at the project root.
- `CHANGELOG.md` at the project root.
- `docs/USER_GUIDE.md`.
- `docs/DEVELOPER_GUIDE.md`.

Do not flatten the documentation for small projects. The `docs/` directory is the default location for the two guides in every project.

## File Organisation

```
project-root/
├── README.md
├── CHANGELOG.md
├── docs/
│   ├── USER_GUIDE.md
│   └── DEVELOPER_GUIDE.md
```

- Use UPPER_SNAKE_CASE for `USER_GUIDE.md` and `DEVELOPER_GUIDE.md` so they stand out.
- Keep `README.md` and `CHANGELOG.md` at the root for discoverability.
- Put all longer guides inside `docs/`.

## README.md

The README is the front door. Keep it short: one or two screens at most.

It must answer:

- What is this project?
- Who is it for?
- How do I install or run it?
- Where do I find more detailed documentation?

It should link to:

- `CHANGELOG.md`
- `docs/USER_GUIDE.md`
- `docs/DEVELOPER_GUIDE.md`

Do not duplicate content from the guides. Tease and link.

## CHANGELOG.md

The changelog is a curated, user-facing summary of what changed in each version. It is not a dump of git history.

Format:

- Newest version first.
- Each version has a heading like `## 1.2.0` or `## Unreleased`.
- Under each version, group entries by category when useful: Added, Changed, Deprecated, Removed, Fixed, Security.
- Only include changes that matter to users or operators.
- Omit internal refactors, style-only changes, dependency updates that do not affect behavior, and test-only changes unless they fix observable bugs.

Each entry should say what changed and, when useful, why it matters:

```markdown
- Added support for ISO 8601 dates without timezone offsets. Previously these were rejected even though they are valid input.
```

## docs/USER_GUIDE.md

The user guide explains how to use the program. Write it for someone who runs the software, not someone who maintains it.

Include:

- A short overview of what the program does.
- Installation or access instructions.
- Core concepts the user needs to understand.
- Feature descriptions with concrete examples.
- Configuration options from a user perspective.
- Common errors and how to resolve them.

Use examples liberally. Prefer showing commands and output over describing them.

## docs/DEVELOPER_GUIDE.md

The developer guide helps humans and AI agents understand the codebase and deploy it. After reading it, a maintainer should know where things live and how to change them safely.

Include:

- High-level architecture and data flow.
- Module or directory map and the responsibility of each part.
- How to build, test, and run the project locally.
- Dependency overview.
- Deployment instructions: environment variables, secrets, infrastructure assumptions, and step-by-step procedure.
- Configuration reference for operators.
- Common maintenance tasks and where to make changes.
- Any conventions or invariants that are not obvious from reading the code.

Keep this document factual and up to date. A stale developer guide is worse than none.

## When to Update Each Document

Documentation is not a separate chore. Whenever code changes, consider whether any of the four core documents need updating, and update them in the same change unless the user explicitly asks to defer.

### CHANGELOG.md

Update for any user-visible or operator-visible change:

- New feature
- Bug fix
- Behavioral change, including subtle ones
- Breaking change
- Deprecation
- Security fix
- Operational change (deployment, configuration, infrastructure)

Do **not** update for internal refactors with no observable effect, style or formatting changes, test-only changes, or dependency updates that do not change behavior.

If the project versions releases, add entries under an `## Unreleased` heading and move them to a version heading at release time.

### docs/USER_GUIDE.md

Update when users need to know something new to keep using the software correctly:

- New feature or command
- Changed feature behavior
- New, changed, or removed configuration option
- New CLI flag, argument, or subcommand
- Changed error messages users might act on
- New common error or troubleshooting scenario
- Changed installation or access steps

### docs/DEVELOPER_GUIDE.md

Update when the codebase or how to run and deploy it changes:

- Architecture or data flow changes
- Module, directory, or crate reorganization
- New build, test, or run steps
- New dependency or changed version requirements
- New environment variable, secret, or operational configuration
- New deployment step or infrastructure assumption
- New coding convention, invariant, or maintenance procedure

### README.md

Update sparingly. Only when:

- The project purpose or target audience changes
- The quick start or installation steps change
- A major new feature deserves a front-page mention
- Links to other documentation need fixing

## Cross-Referencing

- `README.md` links to `CHANGELOG.md`, `docs/USER_GUIDE.md`, and `docs/DEVELOPER_GUIDE.md`.
- The guides link back to `README.md`.
- `CHANGELOG.md` is append-only and does not need to link elsewhere.
- Use relative paths in links, for example `[User Guide](docs/USER_GUIDE.md)`.

## Commit Messages

Git history supports the changelog and future maintainers. Every commit should have a short summary and a detailed body.

Format:

```
Short summary, 50–72 characters

Detailed explanation of what changed and why. Mention any
user-visible impact, breaking changes, or deployment concerns.
```

Guidelines:

- The summary line describes the change in the imperative mood.
- The body explains the reasoning, not just the mechanics.
- Mention any issue, ticket, or decision that motivated the change if relevant.
- Do not rely on commit messages alone to replace the changelog.

Example:

```
Fix parsing of ISO dates without timezone

The previous parser rejected valid ISO 8601 dates when the offset was
omitted. Missing offsets are now treated as UTC, matching the behavior
documented in the user guide and avoiding unexpected errors for users
in environments that do not supply offsets.
```

## What to Avoid

- Do not create many small documentation files (`INSTALL.md`, `BUILD.md`, `DEPLOY.md`, `CONTRIBUTING.md`) unless the project is large enough to justify them. Build and deployment instructions belong in `DEVELOPER_GUIDE.md`.
- Do not auto-generate a table of contents unless a guide is genuinely long enough to need one.
- Do not duplicate content between `README.md` and the guides.
- Do not treat git history as the changelog.
