---
name: agents-readme-refactor
description: "Refactor root AGENTS.md and README.md files to follow progressive disclosure principles. Use when AGENTS.md or README.md is too large, repetitive, stale, or full of domain-specific details that should move into focused docs under .docs, while keeping the root files as small entry points with links to deeper documentation."
---

# Agents Readme Refactor

Use this skill to shrink root documentation and move detailed guidance into targeted docs.

## Goals

- Keep `AGENTS.md` minimal and relevant to every task in the repo.
- Keep `README.md` as a short human entry point, not a dumping ground for all operational detail.
- Move stable, topic-specific documentation into `.docs/`.
- Replace duplication with links.

## Root File Rules

For `AGENTS.md`, keep only:

- one-sentence project description
- package manager or command runner details if non-default
- core validation commands if they are important repo-wide defaults
- links to deeper docs in `.docs/`

For `README.md`, keep only:

- short project description
- quick start or the smallest useful getting-started path
- links to deeper docs in `.docs/`

Do not leave long operational walkthroughs, architecture dumps, or repeated command lists in both files.

## What To Move Into .docs

Move detailed material into topic-specific docs such as:

- `.docs/project-overview.md` for stable project context
- `.docs/local-development.md` for Docker, database, and daily commands
- `.docs/testing.md` for test workflows
- `.docs/deployment.md` for staging or production operations
- `.docs/<topic>.md` for domain-specific conventions

Prefer capability- or workflow-based docs over file-system inventories.

## Refactor Workflow

1. Read the current `AGENTS.md` and `README.md`.
2. Identify content that is truly root-level versus topic-specific.
3. Group topic-specific content into a small `.docs/` structure.
4. Create or update the focused docs under `.docs/`.
5. Rewrite `AGENTS.md` as a concise root instruction file.
6. Rewrite `README.md` as a concise human-oriented entry point.
7. Remove duplication between the two root files.
8. Verify links and make sure the new docs are non-contradictory.

## Heuristics

- If a rule matters only when editing one area, move it out of `AGENTS.md`.
- If the same commands appear in both `AGENTS.md` and `README.md`, keep the details in `.docs/` and link from both.
- If documentation contains volatile file paths, prefer describing the capability and linking to a focused doc instead.
- If a statement is obvious to a coding agent, delete it instead of preserving it.

## Examples

Example root `AGENTS.md` pattern:

```markdown
This is the backend Django service for the PureScribe audio transcription app.

- Use `uv` for dependency and command management.
- Run Django management commands with `uv run python manage.py <command>`.
- Core validation commands: `uv sync`, `uv run python manage.py check`, `uv run python manage.py test`, `uv run python manage.py migrate --check`.
- For project context, see [`.docs/project-overview.md`](./.docs/project-overview.md).
- For local Docker and PostgreSQL development workflow, see [`.docs/local-development.md`](./.docs/local-development.md).
```

Example root `README.md` pattern:

```markdown
This is the backend Django service for the PureScribe audio transcription app.

## Documentation

- Project context and repository baseline: [`.docs/project-overview.md`](./.docs/project-overview.md)
- Local Docker and PostgreSQL workflow: [`.docs/local-development.md`](./.docs/local-development.md)

## Quick Start

```bash
docker compose up --build
```
```

Example of content to move out of root files:

- long lists of commands with explanations
- Docker reset procedures
- detailed architecture notes
- testing patterns
- domain conventions

## Output Expectations

When using this skill:

- create or update the `.docs/` files first
- then trim `AGENTS.md` and `README.md`
- keep examples short and concrete
- avoid turning `.docs/` into another ball of mud by splitting docs by topic when needed
