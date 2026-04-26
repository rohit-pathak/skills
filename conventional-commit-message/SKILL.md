---
name: conventional-commit-message
description: Generate commit messages that follow Conventional Commits 1.0.0. Use when OpenCode needs to draft, refine, or review a git commit message, choose an appropriate Conventional Commit type or scope, decide whether a change is feat, fix, refactor, chore, docs, style, perf, test, ci, build, revert, or determine whether a breaking change should use ! or a BREAKING CHANGE footer.
---

# Conventional Commit Message

Write commit messages in Conventional Commits format and bias toward short, precise subjects that describe the dominant change.

## Format

Use this structure:

```text
<type>[optional scope][optional !]: <description>

[optional body]

[optional footer(s)]
```

Follow these rules:

- Start with a lowercase type such as `feat`, `fix`, or `refactor`.
- Add a scope only when it helps disambiguate the area being changed.
- Put `!` immediately before `:` only for breaking changes.
- Keep the description short, specific, and action-oriented.
- Use a blank line between subject, body, and footers.
- Use uppercase `BREAKING CHANGE:` if a footer is needed.
- Use additional footers in trailer style, for example `Refs: #123`.

## Type Selection

Choose the type that best matches the primary effect of the commit:

- `feat`: add a user-visible or developer-visible capability.
- `fix`: correct incorrect behavior or a regression.
- `refactor`: improve structure without changing intended behavior.
- `perf`: improve performance characteristics.
- `docs`: change documentation only.
- `style`: formatting or presentation changes without logic changes.
- `test`: add or update tests only.
- `build`: change packaging, dependencies, or build tooling.
- `ci`: change CI or automation workflows.
- `chore`: repository maintenance that does not fit the above.
- `revert`: revert an earlier change.

If a change cleanly spans multiple types, prefer splitting it into multiple commits. If only one commit is possible, pick the dominant user impact.

## Scope Guidance

Add a scope when the repo has a clear subsystem and the extra context makes scanning history easier.

Good scope candidates:

- Angular feature or page names such as `dashboard`, `transcript-detail`, or `auth`
- Backend areas such as `functions`, `firestore`, `storage`, or `billing`
- Infrastructure areas such as `ci`, `deps`, or `playwright`

Examples:

- `fix(upload): reject unsupported audio mime types earlier`
- `feat(functions): add Fireworks transcription pipeline`
- `refactor(dashboard): simplify upload progress state`

Omit the scope when the subject is already clear without it.

## Description Style

Write the subject as a compact summary, not a changelog paragraph.

Prefer:

- an imperative or concise action phrase
- the dominant behavior or outcome
- lowercase text after the colon unless a proper noun requires capitals

Avoid:

- issue or PR numbers in the subject unless the host workflow requires them
- vague summaries like `update stuff`
- stacked clauses joined with commas when one clearer phrase will do
- title-cased subjects like `Move Firebase Project to JetScribe`

## Breaking Changes

For breaking changes, use one of these:

```text
feat(api)!: rename transcript segments response shape
```

or:

```text
refactor(storage): change upload path layout

BREAKING CHANGE: uploads now move from transcripts/{id} to users/{uid}/uploads/{id}
```

Use the footer when the impact needs more explanation than fits in the subject.

## Message Drafting Workflow

When asked to produce a commit message:

1. Identify the single dominant change.
2. Choose the narrowest accurate type.
3. Add a scope only if it clarifies the affected subsystem.
4. Write one short subject line.
5. Add a body only if the why or tradeoff is not obvious from the diff.
6. Add footers only for breaking changes, references, or required trailers.

Return one preferred message first. If the change could reasonably be classified more than one way, return up to two alternatives and explain the tradeoff briefly.

## Output Pattern

Default to this form:

```text
<type>[scope]: <description>
```

If a body is warranted:

```text
<type>[scope]: <description>

<why this change exists and any key tradeoff>
```

If reverting:

```text
revert: <short description>

Refs: <sha>
```
