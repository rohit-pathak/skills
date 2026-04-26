# Actions and Releases

## Workflow Runs

### List

- `gh run list`
- `gh run list --branch main`
- `gh run list --workflow ci.yml`
- `gh run list --status failure --limit 10 --json databaseId,workflowName,headBranch,status,conclusion`

Notes:

- Use `gh pr checks` instead of `gh run list` when the task is specifically about a pull request's CI state.
- `gh run list --workflow <name>` does not include disabled workflows unless `--all` is also passed.

### View

- `gh run view 12345`
- `gh run view 12345 --attempt 3`
- `gh run view 12345 --log`
- `gh run view --job 456789 --log`
- `gh run view 12345 --exit-status`

Notes:

- `--job` takes a job ID, not a job name.
- `--log-failed` is useful when only failed steps matter.

### Watch

- `gh run watch 12345`
- `gh run watch 12345 --compact --exit-status`

Important:

- `gh run watch` does not support authentication via fine-grained PATs because the required `checks:read` permission cannot currently be expressed for those tokens.

## Workflow Dispatch

- `gh workflow run`
- `gh workflow run triage.yml`
- `gh workflow run triage.yml --ref my-branch`
- `gh workflow run triage.yml -f name=scully -f greeting=hello`
- `echo '{"name":"scully","greeting":"hello"}' | gh workflow run triage.yml --json`

Notes:

- The target workflow must define `on: workflow_dispatch`.
- `-f/--raw-field` and `-F/--field` behave like the corresponding `gh api` flags.

## Releases

- `gh release create`
- `gh release create v1.2.3 --notes "bugfix release"`
- `gh release create v1.2.3 --generate-notes`
- `gh release create v1.2.3 -F release-notes.md`
- `gh release create v1.2.3 ./dist/*.tgz`
- `gh release create v1.2.3 '/path/to/asset.zip#My display label'`
- `gh release create v1.2.3 --notes-from-tag`
- `gh release create v1.2.3 --verify-tag`

Important:

- If the tag does not exist, `gh release create` creates it from the default branch unless `--target` points elsewhere.
- Use `--verify-tag` to require that the tag already exists remotely.
- Use `--fail-on-no-commits` to avoid creating duplicate releases when nothing new has landed.
- When release immutability is enabled, published releases and their tags/assets cannot be modified, but drafts remain editable until publication.
