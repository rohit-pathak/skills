---
name: agents-refactor
description: "Refactor AGENTS.md files to follow progressive disclosure principles. Use when an AGENTS.md file is too large, repetitive, stale, contradictory, generated, or full of domain-specific details that should move into focused docs, nested AGENTS.md files, or skills."
---

# Agents Refactor

Use this skill to make `AGENTS.md` files small, focused, and useful on every request.

## Principle

Treat `AGENTS.md` as an instruction budget, not a documentation dump. Every token loads into the agent context on every request, so only keep guidance that is relevant at that file's scope.

Prefer progressive disclosure:

- Put universal, repo-wide instructions in the root `AGENTS.md`.
- Move domain-specific guidance into focused docs.
- Put package-specific guidance in nested `AGENTS.md` files.
- Use skills for specialized workflows that should load only when needed.

## What Belongs In Root AGENTS.md

Keep the root file close to this minimum:

- One-sentence project description.
- Package manager or command runner details when non-obvious.
- Non-standard build, test, typecheck, or validation commands.
- Stable domain vocabulary that affects many tasks.
- Links to focused docs, nested `AGENTS.md` files, or skills.

Do not keep broad style guides, framework basics, long command walkthroughs, file inventories, volatile paths, or instructions that apply only to one area.

## What To Move Out

Move instructions out of `AGENTS.md` when they are:

- Redundant with agent defaults or installed skills.
- Relevant only to one language, framework, package, or workflow.
- Too vague to be actionable.
- Obvious, such as generic reminders to write clean code.
- Stale-prone, especially file-system structure or generated inventories.
- Contradictory with other instructions.

Use capability-oriented docs instead of file inventories. Prefer "authentication uses OAuth with organization-scoped access" over "auth code lives in `src/auth/handlers.ts`".

## Refactor Workflow

1. Read every relevant `AGENTS.md` file for the current scope.
2. Identify contradictions and ask the user which version to keep before rewriting conflicting instructions.
3. Extract essentials that are relevant to every task at that scope.
4. Group remaining instructions by domain, such as TypeScript conventions, testing patterns, API design, deployment, or Git workflow.
5. Move grouped details into focused docs, nested `AGENTS.md` files, or skills.
6. Rewrite `AGENTS.md` as a concise entry point with links to the deeper resources.
7. Delete redundant, vague, obvious, stale, or generated guidance instead of preserving it.
8. Verify links and check that the resulting instruction set is non-contradictory.

## Monorepo Guidance

For monorepos, keep each `AGENTS.md` scoped to its directory:

- Root: monorepo purpose, shared package manager, shared commands, and how to navigate packages.
- Package: package purpose, tech stack, package-specific commands, and links to package-specific conventions.

Do not overload any level. Agents see merged `AGENTS.md` files, so each file should contain only what is relevant from that directory downward.

## Examples

Minimal root pattern:

```markdown
This is a monorepo containing web services and CLI tools.

- Use pnpm workspaces to manage dependencies.
- Run `pnpm test` before changes that affect shared packages.
- See each package's `AGENTS.md` for package-specific guidance.
```

Focused package pattern:

```markdown
This package is a Node.js GraphQL API using Prisma.

- Run `pnpm test --filter api` for API changes.
- For API design patterns, see [`docs/api-conventions.md`](./docs/api-conventions.md).
```

Progressive disclosure pattern:

```markdown
This is a React component library for accessible data visualization.

- Use pnpm for dependencies.
- For TypeScript conventions, see [`docs/typescript.md`](./docs/typescript.md).
- For accessibility testing, see [`docs/accessibility-testing.md`](./docs/accessibility-testing.md).
```

## Output Expectations

When using this skill:

- Keep the final `AGENTS.md` short enough to skim quickly.
- Preserve only instructions with clear behavioral value.
- Prefer links over copied detail.
- Avoid creating another ball of mud in the linked docs.
- Report any contradictions, deleted stale guidance, and new documentation locations.
