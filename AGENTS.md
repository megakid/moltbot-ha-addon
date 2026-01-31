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

## Local Testing Notes
- Use Docker “supervisor-style” runs with `/config` and `/data` volumes to simulate HA.
- Use `openclaw update --no-restart` to avoid systemd errors inside containers.
- If a repo pull changes the SHA, re-run the git installer to rebuild `dist/` + UI.
- Gateway auth now requires a token even on loopback; generate non-interactively with `openclaw doctor --generate-gateway-token`.
- Missing token causes a crash loop: “Gateway auth is set to token, but no token is configured.”
