# documentation-skill

An agent skill that gives every project the same small documentation set, and makes the agent keep it current in the same change as the code.

## What it enforces

- **Four documents, always:** a short `README.md`, a curated `CHANGELOG.md`, `docs/USER_GUIDE.md` for people who run the software, and `docs/DEVELOPER_GUIDE.md` for the humans and agents who maintain and deploy it.
- **Update rules per document.** The skill lists which kinds of change touch the changelog, which touch each guide, and which touch nothing (refactors, formatting, test-only changes).
- **A changelog, not a git log.** User-facing entries grouped by version, newest first.
- **Commit messages** with a 50–72 character imperative summary and a body that explains why.

[performance-envelope](https://github.com/Louis-Saglio/performance-envelope) follows this layout.

## Use

Nothing to invoke: the skill applies whenever the agent creates, reviews or reorganizes documentation, and whenever a code change has a user-visible or operator-visible effect.

## License

[MIT](LICENSE)
