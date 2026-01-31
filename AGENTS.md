# Repository Guidelines
- Repo: https://github.com/megakid/openclaw-ha-addon

## Project Structure & Files
- Add-on source and metadata live in `openclaw_gateway/`.
- Add-on metadata: `openclaw_gateway/config.json` (version, options, ingress settings).
- Docs: `openclaw_gateway/README.md`, `openclaw_gateway/DOCS.md`.
- Changelog: `openclaw_gateway/CHANGELOG.md` (latest release at top, no `Unreleased`).

## Commit Messages
- Follow conventional commit format: `type(scope): short description`.
- Keep messages concise and action-oriented (imperative, lowercase, no trailing period).
- Example: `feat(gateway): add verbose flag to send`.
- Group related changes; avoid bundling unrelated refactors.

## Pull Requests & Approval
- New features and bugfixes must be opened as GitHub PRs.
- PRs should summarize scope, note testing performed, and mention any user-facing changes or new flags.
- Wait for approval from `ngutman` before merging.

## Docs & Data Safety
- When changing add-on behavior or options, update docs and the changelog.
- Do not commit secrets or real user data; use obvious placeholders.

## Retrospective (2026-01-31 local docker run)
### Good
- Built the add-on image locally and launched a “supervisor-style” container with `/config` and `/data` volumes.
- Collected and shared logs showing setup, dependency bootstrap, and the failing `openclaw update` step.
### Bad
- Initial build timed out once before completing.
- The container exited after `openclaw update` due to missing `dist/entry.js`, and root cause was not investigated yet.

## Lessons (local run outside supervisor)
- When running locally, `openclaw update` must use `--no-restart` to avoid systemd failures.
- If the repo SHA changes after pull, run the git installer (git checkout mode) to rebuild `dist/` and UI.
- The gateway now requires a token even on loopback; generate headlessly via `openclaw doctor --generate-gateway-token`.
- Without a token, the gateway will crash-loop with “Gateway auth is set to token, but no token is configured.”
