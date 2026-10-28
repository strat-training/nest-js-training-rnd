# M7 — Type-Safe Data Layer — Tasks

**Objective:** Use Prisma's generated types without losing safety, derive result types from
queries, and keep database types and API types separate.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.
> Two Still Open items below block this stage's Setup — resolve them before writing any Prisma
> code.

## Setup

- [ ] Confirm M6's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M6 first.
- [ ] Confirm with your trainer the exact Prisma 7 version to pin for this cohort.
- [ ] Confirm with your trainer (or by testing it yourself) that `@prisma/adapter-better-sqlite3`
      installs cleanly on your Node version — if it doesn't, follow your trainer's fallback
      guidance before continuing.
- [ ] Set up Prisma with SQLite using the driver adapter and a `prisma.config.ts` file, following
      the current Prisma 7 docs.

## Build

- [ ] Build a `PrismaService` provider with the appropriate Nest lifecycle hooks.
- [ ] Replace M2's in-memory repository with Prisma + SQLite in both `ProjectsModule` and
      `TasksModule`.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you replaced the
      in-memory repository with Prisma.
- [ ] Review generated types and `Prisma.TaskGetPayload<{ include: ... }>`.
- [ ] Review `Prisma.validator` and `satisfies` for keeping query objects typed.
- [ ] Build a `TaskWithProject` type derived from a Prisma payload (via `Prisma.TaskGetPayload` or
      `satisfies`), not hand-duplicated.
- [ ] Review generic repositories — when they help and when they cause harm — and decide whether to
      use one here.
- [ ] Review transactions and where they'd apply in the Team Tasks API.
- [ ] Map database models to `TaskResponse` (from M3) using mapped types from M4, before anything
      leaves the service layer.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, how you mapped
      database models to API types and any generic-repository decision you made.
- [ ] Turn "not found" and "unique constraint" Prisma errors into typed `Err` values using
      `Result<T, E>` from M2.

## Verify

- [ ] Confirm the in-memory repository from M2 is gone, not left in place alongside Prisma.
- [ ] Confirm `TaskWithProject` is derived from a Prisma payload type, not hand-duplicated.
- [ ] Confirm no raw Prisma model is ever returned directly from a controller — everything crossing
      the service boundary is mapped to `TaskResponse` first.
- [ ] Confirm "not found" and "unique constraint" errors are turned into typed `Err` values, not
      left as raw exceptions.
- [ ] Checkpoint: change a field on a Prisma model and follow the resulting compile errors through
      your services and mappers, fixing every one.
- [ ] Checkpoint: explain why raw database types shouldn't be sent straight to clients.
- [ ] Commit your work to your Team Tasks API branch, building on M6's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_07.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
