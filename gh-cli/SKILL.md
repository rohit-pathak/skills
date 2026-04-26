---
name: gh-cli
description: GitHub CLI (`gh`) workflow guide for authenticated GitHub operations from the terminal. Use when OpenCode needs to inspect or change repositories, issues, pull requests, Actions runs, releases, or GitHub API state with `gh`; translate GitHub URLs into `gh` commands; or choose the right `gh` subcommand, flags, JSON fields, and automation-friendly invocation.
---

# gh-cli

Use `gh` for GitHub work that should happen from the terminal instead of manually in the browser.

The bundled references cover the common workflows that benefit from having examples in context. For anything outside those workflows, fetch the exact manual page before using a command.

## Start Here

1. Confirm auth and host context with `gh auth status` when the target account or hostname is unclear.
2. Resolve the target repository from the current checkout, `GH_REPO`, a provided URL, or `--repo`.
3. Prefer non-interactive commands with explicit flags when automating or when the user already supplied the required data.
4. Prefer `--json`, `--jq`, and `--template` for machine-readable queries instead of scraping plain text output.
5. Before using a destructive or privilege-elevated command, re-check the exact repo, branch, and account.

## Reference Map

- Read `references/auth-context.md` for login flows, host selection, env vars, and repo targeting.
- Read `references/repos-issues-prs.md` for day-to-day repo, issue, and pull request operations.
- Read `references/actions-releases.md` for Actions runs, workflow dispatch, and releases.
- Read `references/api-formatting.md` for `gh api`, GraphQL, `--json`, `--jq`, and `--template`.
- Read `references/manual-routing.md` when a task involves a less common command family or you need the exact manual page URL.

## Working Style

- Prefer explicit selectors such as `--repo owner/repo`, PR numbers, issue numbers, and run IDs when the target could be ambiguous.
- Prefer documented flags over guessed shorthand. If a flag is not in these references, fetch the exact manual page before using it.
- Use browser mode with `--web` when the task is inherently interactive or when the web UI is faster than building a long command.
- Use `gh api` when the high-level subcommands do not expose the needed capability.
