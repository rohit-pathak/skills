# Repos, Issues, and PRs

These notes were verified against the official manual pages for `gh repo clone`, `gh repo create`, `gh repo list`, `gh repo view`, `gh issue create`, `gh issue list`, `gh issue view`, `gh pr create`, `gh pr view`, `gh pr checks`, and `gh pr merge`.

## Repositories

### Clone

- `gh repo clone cli/cli`
- `gh repo clone cli/cli workspace/cli`
- `gh repo clone cli/cli -- --depth=1`
- `gh repo clone myfork --no-upstream`

Notes:

- `gh repo clone` adds an `upstream` remote automatically when cloning a fork unless `--no-upstream` is used.
- Extra `git clone` flags go after `--`.

### List and View

- `gh repo list cli --limit 50 --json nameWithOwner,visibility`
- `gh repo list my-org --source --json nameWithOwner,updatedAt --jq '.[] | [.nameWithOwner, .updatedAt] | @tsv'`
- `gh repo view owner/repo`
- `gh repo view owner/repo --json nameWithOwner,defaultBranchRef,url`
- `gh repo view owner/repo --web`

### Create

- `gh repo create`
- `gh repo create my-project --public --clone`
- `gh repo create my-org/my-project --public`
- `gh repo create my-project --private --source=. --remote=upstream`

Notes:

- Non-interactive creation requires one of `--public`, `--private`, or `--internal`.
- `--source` creates the remote from an existing local repository.
- `--push` pushes local commits after creating the remote.

## Issues

### Create

- `gh issue create --title "I found a bug" --body "Nothing works"`
- `gh issue create --label bug --label "help wanted"`
- `gh issue create --assignee "@me"`
- `gh issue create --project "Roadmap"`
- `gh issue create --template "Bug Report"`

Important:

- The flag is `--label`, not `--labels`.
- `--assignee` supports `@me` and `@copilot`, but `@copilot` is not supported on GitHub Enterprise Server.

### List and View

- `gh issue list`
- `gh issue list --state all`
- `gh issue list --assignee "@me"`
- `gh issue list --search "error no:assignee sort:created-asc"`
- `gh issue view 21`
- `gh issue view 21 --comments`
- `gh issue view 21 --json title,state,labels,url`

## Pull Requests

### Create

- `gh pr create --title "The bug is fixed" --body "Everything works again"`
- `gh pr create --reviewer monalisa --reviewer myorg/team-name`
- `gh pr create --base develop --head monalisa:feature`
- `gh pr create --draft`
- `gh pr create --project "Roadmap"`

Notes:

- `--head <user>:<branch>` supports a user owner, not an organization owner.
- `--fill`, `--fill-first`, and `--fill-verbose` can derive title/body from commits.
- Mention `Fixes #123` or `Closes #123` in the PR body to auto-close the issue on merge.

### View and Checks

- `gh pr view 21`
- `gh pr view 21 --comments`
- `gh pr view 21 --json title,reviewDecision,statusCheckRollup,url`
- `gh pr checks 21 --watch --required`
- `gh pr checks 21 --json name,state,bucket,link`

Notes:

- `gh pr checks` exits with code `8` while checks are still pending.
- The JSON output includes `bucket`, which groups states into `pass`, `fail`, `pending`, `skipping`, or `cancel`.

### Merge

- `gh pr merge 21 --merge`
- `gh pr merge 21 --squash --delete-branch`
- `gh pr merge 21 --rebase`
- `gh pr merge 21 --auto`

Important:

- Use `--admin` only when the task explicitly requires bypassing protections or a merge queue.
- If the repo uses a merge queue, `gh pr merge` may add the PR to the queue or enable auto-merge instead of merging immediately.
