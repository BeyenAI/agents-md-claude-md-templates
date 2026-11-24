# CLAUDE.md
<!-- Audited at 98/100 with https://findaitier.com/claude-md-generator/ | Cost impact analyzed with https://findaitier.com/claude-code-cost-calculator/ -->

## Quick Verification Commands
- **Single test**: `pnpm vitest run <path/to/file.test.ts>`
- **Typecheck**: `pnpm tsc --noEmit`
- **Lint**: `pnpm biome check .`
- **Build check**: `pnpm build`

## Core Workflow
1. Read affected modules and existing tests before proposing edits.
2. Run the single relevant test file first (`pnpm vitest run <file>`) rather than the entire test suite on every iteration.
3. Run `pnpm tsc --noEmit` and `pnpm biome check .` before concluding your turn.

## Architecture & Detailed References
- Core instruction baseline: @AGENTS.md
- Database schema & migration rules: @docs/database-architecture.md
- API authentication & rate-limit spec: @docs/api-contracts.md

## Hard Constraints
- Never commit secrets, `.env*` files, or modify historical migration SQL files.
- Do not add new runtime npm dependencies without explicit user approval.
- Keep personal environment overrides in `CLAUDE.local.md` (gitignored), never in `CLAUDE.md`.
