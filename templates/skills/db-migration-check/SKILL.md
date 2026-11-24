---
name: db-migration-check
description: Audits SQL / Prisma / Drizzle / Alembic database migrations for lock hazards, non-nullable column drops, and rollback safety. Use whenever creating, reviewing, or running database schema migrations.
---
<!-- Built & validated with https://findaitier.com/skill-md-generator/ -->

# Database Migration Safety Check Skill

When this skill is activated, inspect all pending or modified migration files before applying them:

## 1. Zero-Downtime Hazard Checklist
1. **Adding a `NOT NULL` column without a safe default**: On PostgreSQL 11+, adding a column with a constant `DEFAULT` is metadata-only, but adding a `NOT NULL` column without a default on a populated table fails or requires a table rewrite. Prefer expand-and-contract (`ADD COLUMN nullable` → backfill → `SET NOT NULL`).
2. **Blocking Index Creation**: Flag any `CREATE INDEX` on existing production tables that omits `CONCURRENTLY` (PostgreSQL).
3. **Destructive Drops**: Flag `DROP TABLE`, `DROP COLUMN`, or narrowing column type changes unless explicitly confirmed by the user.
4. **Historical Migration Mutation**: Verify via `git status` / `git diff` that no previously committed migration file was altered in-place.

## 2. Required Output Format
Report findings in a 3-column table:
| Migration File | Check Item | Status (`PASS` / `WARN` / `BLOCK`) & Fix |
| --- | --- | --- |
