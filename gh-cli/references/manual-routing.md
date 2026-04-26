# Manual Routing

Use this file when a task involves a `gh` command that is not already covered by the bundled references.

## URL Pattern

- Manual home: `https://cli.github.com/manual/`
- Command family page: `gh pr` -> `https://cli.github.com/manual/gh_pr`
- Subcommand page: `gh pr create` -> `https://cli.github.com/manual/gh_pr_create`
- Hyphenated subcommands keep the hyphen: `gh pr update-branch` -> `https://cli.github.com/manual/gh_pr_update-branch`
- Help topics follow the same rule: `gh help environment` -> `https://cli.github.com/manual/gh_help_environment`

## Useful Families To Fetch On Demand

- Collaboration: `gh repo`, `gh issue`, `gh pr`, `gh search`, `gh label`
- Automation: `gh run`, `gh workflow`, `gh cache`, `gh secret`, `gh variable`
- Platform and admin: `gh auth`, `gh api`, `gh release`, `gh ruleset`, `gh org`, `gh attestation`
- Less common but available: `gh project`, `gh gist`, `gh codespace`, `gh extension`, `gh alias`, `gh browse`, `gh status`

## On-Demand Workflow

1. Derive the exact manual page URL for the command.
2. Read that page before using unfamiliar flags or examples.
3. If the command supports JSON output, inspect the documented `JSON Fields` section or run the command with `--json` and no field list.
4. Prefer copying the documented syntax shape instead of inventing flags from memory.

## Examples

- `gh browse` -> `https://cli.github.com/manual/gh_browse`
- `gh project item-add` -> `https://cli.github.com/manual/gh_project_item-add`
- `gh repo deploy-key add` -> `https://cli.github.com/manual/gh_repo_deploy-key_add`
- `gh release verify-asset` -> `https://cli.github.com/manual/gh_release_verify-asset`
