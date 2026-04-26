# Repos, Issues, and PRs

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
- `gh pr view --json number,title,state,isDraft,reviewDecision,mergeStateStatus,statusCheckRollup,url,baseRefName,headRefName,author,updatedAt`
- `gh pr checks 21 --watch --required`
- `gh pr checks 21 --json name,state,bucket,link`

Notes:

- Use `gh pr view --json ...` with no PR number to inspect the PR for the current branch.
- For example, from a checkout on `stripe-integration`, `gh pr view --json number,title,state,isDraft,reviewDecision,mergeStateStatus,statusCheckRollup,url,baseRefName,headRefName,author,updatedAt` returns the linked PR metadata for that branch.
- Do not assume `gh pr status --json` exposes branch-grouped objects such as `currentBranch`; in this environment that field was rejected as unsupported.
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
