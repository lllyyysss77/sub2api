---
name: add-or-modify-database-table-with-migration
description: Workflow command scaffold for add-or-modify-database-table-with-migration in sub2api.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-modify-database-table-with-migration

Use this workflow when working on **add-or-modify-database-table-with-migration** in `sub2api`.

## Goal

Adds or modifies a database table, including schema, migration, ent code, and related service/repository updates.

## Common Files

- `backend/ent/schema/*.go`
- `backend/ent/*`
- `backend/migrations/*.sql`
- `backend/internal/service/*`
- `backend/internal/repository/*`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit or add ent/schema/*.go
- Run ent codegen to update backend/ent/* (model, query, create, update, etc.)
- Add or update backend/migrations/*.sql migration file
- Update backend/ent/migrate/schema.go and related runtime files
- Update backend/internal/service/* and backend/internal/repository/* as needed

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.