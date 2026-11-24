# AGENTS.md — Next.js 15 (App Router) + TypeScript + Tailwind + Vitest
<!-- Generated & linted with https://findaitier.com/agents-md-generator/ (Codex 32 KiB budget: ~1.8 KiB / 5.5%) -->

## Project Overview
Full-stack Next.js 15 App Router application using TypeScript 5.7, Tailwind CSS v4, Drizzle ORM (PostgreSQL), and Vitest.

## Commands (Run Before Finishing Any Task)
- **Install dependencies**: `pnpm install --frozen-lockfile`
- **Typecheck**: `pnpm tsc --noEmit`
- **Lint & Format check**: `pnpm biome check .`
- **Run single unit test (preferred)**: `pnpm vitest run <path/to/file.test.ts>`
- **Run full unit test suite**: `pnpm test:unit`
- **Database schema check**: `pnpm db:check`

## Architecture & Directory Boundaries
- `src/app/` — Next.js App Router pages, layouts, and Route Handlers (`route.ts`). Default to React Server Components (RSC); only add `"use client"` on leaf interactive components.
- `src/server/` — Server-only business logic, Drizzle queries, and external API clients. Every file in `src/server/` must import `"server-only"` at the top.
- `src/components/ui/` — Stateless shared UI primitives. Do not import database or session helpers here.
- `src/lib/schemas/` — Shared Zod validation schemas used by both server actions and client forms.

## Code & Verification Conventions
- Validate all external inputs (Route Handlers, Server Actions, webhook payloads, URL searchParams) with Zod before touching `src/server/`.
- Never use `any` or `@ts-ignore`. Prefer discriminated unions and `satisfies`.
- When fixing a bug or adding a route/action, add or update the colocated `*.test.ts` file and verify it passes via `pnpm vitest run <file>`.

## Security & Git Rules
- Never hardcode API keys, tokens, or connection strings; read from `src/env.mjs` (validated env schema) and document new keys in `.env.example`.
- Do not modify existing committed migrations in `drizzle/migrations/`; generate new migrations via `pnpm db:generate`.
- Never run destructive git commands (`git reset --hard`, `git push --force`) or commit `.env*` files.
