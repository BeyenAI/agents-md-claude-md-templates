# AGENTS.md, CLAUDE.md, SKILL.md, Cursor .mdc & MCP Config Templates (2026)

> Copy-pasteable, linted 2026 templates for **`AGENTS.md`** (OpenAI Codex, Cursor, Cline, Roo Code, Windsurf), **`CLAUDE.md`** (Claude Code), **`SKILL.md`** (Agent Skills), **`.cursor/rules/*.mdc`** (Cursor IDE), and **`mcp.json` / `config.toml`** (Multi-Client Model Context Protocol) — plus a 2026 cross-agent specification comparison matrix.

---

## ⚡ Interactive Browser-Local Generators & Linters on [FindAITier](https://findaitier.com/)

All tools run **100% locally in your browser** (zero server uploads, zero login):

- **[`AGENTS.md` Generator & Codex 32 KiB Linter](https://findaitier.com/agents-md-generator/)** — Upload or paste `package.json`, `pyproject.toml`, `Cargo.toml`, or `go.mod` to auto-extract build/test/lint commands, check the OpenAI Codex 32 KiB (`32,768` bytes) hierarchy budget, and export a monorepo `.zip`.
- **[`CLAUDE.md` Generator & Deterministic 0–100 Auditor](https://findaitier.com/claude-md-generator/)** — Audit your `CLAUDE.md` for token bloat, missing verification commands, `@path/to/file` modular imports, and leaked secrets, or split private rules into `CLAUDE.local.md`.
- **[`SKILL.md` Builder & YAML Frontmatter Validator](https://findaitier.com/skill-md-generator/)** — Build reusable Agent Skills (`SKILL.md` + `scripts/` + `references/`) with strict YAML frontmatter validation (`name`, `description`) and 1-click `.zip` packaging.
- **[Cursor `.mdc` Rules Generator & `.cursorrules` Splitter](https://findaitier.com/cursor-rules-generator/)** — Convert legacy monolithic `.cursorrules` files into scoped `.cursor/rules/*.mdc` modules with `description`, `globs`, and `alwaysApply` frontmatter.
- **[Multi-Client MCP Config Generator (6 Clients)](https://findaitier.com/mcp-config-generator/)** — Convert MCP server definitions across Claude Code/Desktop (`mcpServers`), `claude mcp add` CLI, VS Code (`.vscode/mcp.json` `"servers"` + `"inputs"`), OpenAI Codex CLI (`[mcp_servers.*]` TOML), Cursor, and Windsurf.
- **[Claude Code Cost Calculator & Offline JSONL Analyzer](https://findaitier.com/claude-code-cost-calculator/)** — Compare Anthropic API prompt-caching costs (`cache_read_input_tokens` vs `cache_creation_input_tokens`) against Pro (`$20`), Max 5x (`$100`), and Max 20x (`$200`), or drag-and-drop `~/.claude/projects/**/*.jsonl` locally to measure your `CLAUDE.md` + MCP system prompt tax.
- **[`AGENTS.md` vs `CLAUDE.md` vs `.cursor/rules` Comparison & Converter](https://findaitier.com/agents-md-vs-claude-md/)** — Side-by-side 2026 specification table and bidirectional repository `.zip` bundle exporter.
- **[Free LLM APIs for Coding Agents (`$0` BYOK Directory)](https://findaitier.com/)** — Verified free API tiers for [Claude Code](https://findaitier.com/claude-code-free-api/), [OpenCode](https://findaitier.com/opencode-free-models/), and [Cline / Roo Code](https://findaitier.com/cline-free-models/).

---

## 1. 2026 Coding Agent Instruction File Specification Matrix

Need to convert between formats automatically? Use the **[Bidirectional `AGENTS.md` ↔ `CLAUDE.md` ↔ `.mdc` Converter](https://findaitier.com/agents-md-vs-claude-md/)**.

| Dimension | `AGENTS.md` | `CLAUDE.md` | `.cursor/rules/*.mdc` | `SKILL.md` | `.github/copilot-instructions.md` |
| --- | --- | --- | --- | --- | --- |
| **Primary Clients** | OpenAI Codex, Cursor, Cline, Roo Code, Windsurf, Aider | Anthropic Claude Code CLI & IDE extensions | Cursor IDE (`v0.45+`) | Claude Code, OpenAI Codex, Antigravity, Goose | GitHub Copilot Chat & Coding Agent |
| **Canonical File Paths** | `./AGENTS.md`, nested `<subdir>/AGENTS.md`, `~/.codex/AGENTS.md` | `./CLAUDE.md`, `./CLAUDE.local.md`, `~/.claude/CLAUDE.md` | `.cursor/rules/<name>.mdc` | `.agents/skills/<skill-name>/SKILL.md` or `.claude/skills/<name>/SKILL.md` | `.github/copilot-instructions.md`, `.github/instructions/*.instructions.md` |
| **Frontmatter / Imports** | Standard Markdown (no frontmatter required) | Supports `@path/to/doc.md` inline file imports | Required YAML frontmatter (`description`, `globs`, `alwaysApply`) | Required YAML frontmatter (`name`, `description`) | Optional `applyTo` glob frontmatter in `*.instructions.md` |
| **Hard Size / Token Limit** | **32 KiB (`32,768` bytes)** default `project_doc_max_bytes` in Codex | Loaded on every turn; keep under **~150 lines / 4 KB** to avoid prompt cache tax | Scoped per matching file glob or semantic description | Progressive disclosure: only `name` + `description` loaded until triggered | Keep concise (< 2,000 tokens recommended) |
| **Override & Local File** | `AGENTS.override.md` in any directory | `CLAUDE.local.md` (auto-gitignored personal overrides) | Local untracked `.mdc` rule | User-scope `~/.agents/skills/` | Personal GitHub Copilot instructions |

---

## 2. Included Production Templates in This Repository

| Template Path | Target Stack / Tool | Highlights | Interactive Customizer |
| --- | --- | --- | --- |
| [`templates/agents-md/nextjs-typescript-AGENTS.md`](templates/agents-md/nextjs-typescript-AGENTS.md) | Next.js 15 + TypeScript + Tailwind + Vitest | Under 4 KB; explicit single-file test runner & App Router boundaries | [Customize in `AGENTS.md` Generator](https://findaitier.com/agents-md-generator/) |
| [`templates/agents-md/python-fastapi-uv-AGENTS.md`](templates/agents-md/python-fastapi-uv-AGENTS.md) | Python 3.12 + FastAPI + `uv` + `ruff` + `pytest` | Enforces `uv run` workflow, Pydantic v2, and async SQLAlchemy rules | [Customize in `AGENTS.md` Generator](https://findaitier.com/agents-md-generator/) |
| [`templates/agents-md/rust-cargo-workspace-AGENTS.md`](templates/agents-md/rust-cargo-workspace-AGENTS.md) | Rust Cargo Workspace + `clippy` + `nextest` | Scoped crate testing and zero-unwrap error handling conventions | [Customize in `AGENTS.md` Generator](https://findaitier.com/agents-md-generator/) |
| [`templates/claude-md/CLAUDE.md`](templates/claude-md/CLAUDE.md) | Claude Code (`CLAUDE.md` + `@docs/` imports) | Scores **98/100** on the deterministic auditor; low token overhead | [Audit Your `CLAUDE.md` (0–100)](https://findaitier.com/claude-md-generator/) |
| [`templates/claude-md/CLAUDE.local.md`](templates/claude-md/CLAUDE.local.md) | Claude Code Personal Overrides (`CLAUDE.local.md`) | Local sandbox URLs, DB ports, and personal test preferences | [Split `CLAUDE.local.md`](https://findaitier.com/claude-md-generator/) |
| [`templates/cursor-rules/typescript-architecture.mdc`](templates/cursor-rules/typescript-architecture.mdc) | Cursor `.cursor/rules/*.mdc` | Scoped `globs: src/**/*.{ts,tsx}` with strict type & server boundary rules | [Split `.cursorrules` to `.mdc`](https://findaitier.com/cursor-rules-generator/) |
| [`templates/cursor-rules/pytest-verification.mdc`](templates/cursor-rules/pytest-verification.mdc) | Cursor `.cursor/rules/*.mdc` | Scoped `globs: tests/**/*.py` for deterministic fixture & test patterns | [Build `.mdc` Rules](https://findaitier.com/cursor-rules-generator/) |
| [`templates/skills/db-migration-check/SKILL.md`](templates/skills/db-migration-check/SKILL.md) | Agent Skills (`SKILL.md` standard) | On-demand database migration safety verifier with strict YAML frontmatter | [Package `SKILL.md` `.zip`](https://findaitier.com/skill-md-generator/) |
| [`templates/mcp/multi-client-mcp-examples.md`](templates/mcp/multi-client-mcp-examples.md) | Claude Code, VS Code `.vscode/mcp.json`, Codex `config.toml`, Cursor | Side-by-side schema differences (`mcpServers` vs `"servers"` + `"inputs"` vs TOML) | [Convert MCP Configs](https://findaitier.com/mcp-config-generator/) |

---

## 3. Why Bloat in `CLAUDE.md` and `AGENTS.md` Hurts Performance & Cost

1. **The Per-Turn Context Tax**: Unlike on-demand `SKILL.md` files or glob-scoped `.cursor/rules/*.mdc` files, root `CLAUDE.md` and `AGENTS.md` files are injected into the system context on **every single turn**. A 12,000-token `CLAUDE.md` combined with 5 active MCP servers can add `$15–$40/month` in unnecessary API cache-write and cache-read overhead (test your exact session logs in the **[Claude Code Cost Calculator](https://findaitier.com/claude-code-cost-calculator/)**).
2. **Codex 32 KiB Truncation**: OpenAI Codex enforces a default `project_doc_max_bytes = 32768` limit across root + nested `AGENTS.md` files. Anything beyond 32 KiB is silently truncated. Check your byte budget with the **[Codex 32 KiB Linter](https://findaitier.com/agents-md-generator/)**.
3. **Instruction Dilution**: Models follow 30 concrete, executable commands (`pnpm test -- <file>`, `uv run ruff check .`) reliably, but ignore 400 lines of vague style essays ("write clean, maintainable, SOLID code").

---

## 4. Dual-Compatibility Trick: Use `AGENTS.md` + `CLAUDE.md` Together

If your team uses both **Claude Code** and **OpenAI Codex / Cursor / Cline**, maintain your canonical instructions in `AGENTS.md` and create a 3-line `CLAUDE.md` that imports it using Claude Code's native `@path` syntax:

```markdown
# Project Instructions
@AGENTS.md
```

Or generate a synchronized multi-agent repository `.zip` (`AGENTS.md` + `CLAUDE.md` + `.cursor/rules/*.mdc` + `.github/copilot-instructions.md`) in one click at **[findaitier.com/agents-md-vs-claude-md/](https://findaitier.com/agents-md-vs-claude-md/)**.

---

## License

MIT License · Maintained alongside **[FindAITier](https://findaitier.com/)** ([LLM Context `/llms.txt`](https://findaitier.com/llms.txt) · [Full Dataset `/llms-full.txt`](https://findaitier.com/llms-full.txt)).
