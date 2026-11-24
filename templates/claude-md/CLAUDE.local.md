# CLAUDE.local.md (Personal / Untracked Overrides)
<!-- Split & generated via https://findaitier.com/claude-md-generator/ — add CLAUDE.local.md to .gitignore -->

## Local Sandbox Endpoints
- Local Postgres test DB: `postgresql://postgres:postgres@127.0.0.1:54322/app_test`
- Local Redis instance: `redis://127.0.0.1:63799`
- Mock webhook receiver: `http://127.0.0.1:8788/webhooks/test`

## Personal Preferences
- When running Playwright smoke tests locally, pass `--project=chromium` only.
- Prefer concise unified diffs in explanations without repeating unchanged functions.
