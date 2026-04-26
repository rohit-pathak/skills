# API and Formatting

These notes were verified against the official manual pages for `gh api` and `gh help formatting`.

## `gh api`

Use `gh api` when the high-level `gh repo`, `gh issue`, `gh pr`, `gh run`, or `gh release` commands do not expose the required capability.

### Core Patterns

- `gh api repos/{owner}/{repo}/releases`
- `gh api repos/{owner}/{repo}/issues/123/comments -f body='Hi from CLI'`
- `gh api -X GET search/issues -f q='repo:cli/cli is:open remote'`
- `gh api repos/{owner}/{repo}/rulesets --input file.json`
- `gh api repos/{owner}/{repo}/issues --jq '.[].title'`

### GraphQL

```bash
gh api graphql -F owner='{owner}' -F name='{repo}' -f query='
  query($name: String!, $owner: String!) {
    repository(owner: $owner, name: $name) {
      releases(last: 3) {
        nodes { tagName }
      }
    }
  }
'
```

### Field Semantics

- `-f/--raw-field key=value`: always sends string values.
- `-F/--field key=value`: performs type conversion, placeholder expansion, and `@file` loading.
- `--input <file>`: uses a prebuilt request body; field flags then go on the query string.
- `--paginate`: follows paginated results automatically.
- `--slurp`: wraps paginated JSON pages into a single outer array.

### Placeholders

- `{owner}`, `{repo}`, and `{branch}` are resolved from the current repository or `GH_REPO`.
- Quote placeholders in shells that treat `{...}` specially.

## JSON, `jq`, and Templates

### Rules

- Commands that support JSON require `--json` before `--jq` or `--template`.
- Omit the field list after `--json` to see the available field names for that command.
- `--jq` uses built-in jq support; the standalone `jq` binary is not required for `gh --jq`.

### Examples

- `gh repo view owner/repo --json nameWithOwner,url`
- `gh repo list cli --json nameWithOwner,visibility --jq '.[] | [.nameWithOwner, .visibility] | @tsv'`
- `gh pr list --json number,title,headRefName,updatedAt --template '{{range .}}{{tablerow (printf "#%v" .number) .title .headRefName (timeago .updatedAt)}}{{end}}'`

### Useful Template Helpers

- `tablerow` and `tablerender`
- `timeago`
- `hyperlink`
- `join`
- `pluck`
- `color` and `autocolor`
- `truncate`

Use templates when the output should still be human-readable but more structured than the default terminal format.
