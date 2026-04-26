# Auth and Context

These notes were verified against the official manual pages for `gh auth login` and `gh help environment`.

## Core Rules

- Use `gh auth status` first when the active account, hostname, or stored credentials are unclear.
- Use `--repo [HOST/]OWNER/REPO` when the current checkout is not the intended target.
- Prefer environment-based auth for automation and headless usage.
- Treat `github.com` as the default host unless `--hostname` or `GH_HOST` says otherwise.

## Login

- `gh auth login` starts the default browser-based flow.
- `gh auth login --web --clipboard` opens the browser flow and copies the one-time code.
- `gh auth login --with-token < mytoken.txt` reads a token from stdin.
- `gh auth login --hostname enterprise.internal` authenticates against a GitHub Enterprise host.
- `gh auth login --git-protocol ssh` sets the git protocol for that host.

Use `GH_TOKEN` for fine-grained PAT or automation use. The manual explicitly warns that `--with-token` is better suited to classic PATs and can be confusing with fine-grained token scoping.

## Environment Variables

- `GH_TOKEN` or `GITHUB_TOKEN`: auth token for `github.com` or `ghe.com` subdomains.
- `GH_ENTERPRISE_TOKEN` or `GITHUB_ENTERPRISE_TOKEN`: auth token for GitHub Enterprise Server.
- `GH_HOST`: default hostname when it cannot be inferred.
- `GH_REPO`: default repository in `[HOST/]OWNER/REPO` format.
- `GH_PROMPT_DISABLED`: disable interactive prompts.
- `GH_EDITOR`, `GH_BROWSER`, `GH_PAGER`: override editor, browser, and pager.
- `GH_FORCE_TTY`: force terminal-style output even when redirected.
- `GH_CONFIG_DIR`: override the config directory.
- `GH_TELEMETRY`: set to `false` or `0` to disable telemetry; `log` prints telemetry locally instead.

## Project Scope

Issue and PR creation can add items to Projects, but that requires `project` scope.

- Use `gh auth refresh -s project` before using `--project` on issue or PR commands.

## Target Selection Checklist

1. If the user gave a GitHub URL, derive the host, owner, repo, and resource number from the URL.
2. If the task is outside the current checkout, pass `--repo` explicitly.
3. If the task targets GitHub Enterprise, confirm the hostname and auth context before running the command.
