# M7 — Type-Safe Data Layer

**Week:** 3 · **Hours:** 5 · **Builds on:** M6's Zod schemas.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.
>
> Before you start: confirm the Prisma version pin and SQLite adapter setup with your trainer (see
> Still open) — this stage's lab depends on both being settled first.

## Objective

By the end of this stage you can:
- Use Prisma's generated types without losing safety.
- Derive result types from Prisma queries.
- Keep database types and API types separate.

## Scope

- Setting up Prisma with SQLite (follow the current Prisma 7 docs for the SQLite + driver-adapter
  setup).
- A `PrismaService` provider and its Nest lifecycle hooks.
- Generated types and `Prisma.TaskGetPayload<{ include: ... }>`.
- `Prisma.validator` and `satisfies` to keep query objects typed.
- Mapping database models to API response types using mapped types from M4.
- Typed error handling: turning Prisma errors into `Result<T, E>` values from M2.
- Generic repositories: when they help, and when they cause harm.
- Transactions.

## Stack constraints

- Prisma ORM 7 (pinned — not the Prisma 8 release candidate that `npm install prisma` may resolve
  to by default; confirm the exact pinned version with your trainer).
- SQLite as the database.
- A driver adapter is required for Prisma 7 + SQLite, plus a `prisma.config.ts` file — follow the
  current Prisma 7 docs rather than an older Prisma guide.
- No Docker.

## Deliverable

Replace the in-memory repository from M2 with Prisma + SQLite. Build a `TaskWithProject` type
derived from a Prisma payload. Map database models to `TaskResponse` (from M3) using mapped types.
Turn "not found" and "unique constraint" Prisma errors into typed `Err` values using the
`Result<T, E>` type from M2.

## Definition of done

- [ ] `ProjectsModule`/`TasksModule` read and write through Prisma + SQLite — the in-memory
      repository from M2 is gone, not left in place alongside it.
- [ ] `TaskWithProject` is derived from a Prisma payload type (e.g. via `Prisma.TaskGetPayload` or
      `satisfies`), not hand-duplicated.
- [ ] Database models are mapped to `TaskResponse` before leaving the service layer — no raw Prisma
      model is returned directly from a controller.
- [ ] "Not found" and "unique constraint" errors from Prisma are turned into typed `Err` values via
      `Result<T, E>`, not left as raw exceptions.
- [ ] Checkpoint: you can change a field on a Prisma model and follow the resulting compile errors
      through your services and mappers to fix every one.
- [ ] Checkpoint: you can explain why raw database types shouldn't be sent straight to clients.
- [ ] Work is committed to your Team Tasks API branch, building on M6's commit.

## Still open

- Confirm with your trainer: the exact Prisma 7 version to pin, and whether
  `@prisma/adapter-better-sqlite3` installs cleanly on your machine's Node version — the solution
  design flags both as needing a pilot check before this stage, since Prisma 8 may now install by
  default and `better-sqlite3` is a native module that can fail per-OS.
