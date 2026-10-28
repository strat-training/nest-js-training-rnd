# M6 — Validation and DTOs — Tasks

**Objective:** Explain why types alone don't protect a running API, validate input with
class-based DTOs and schema-first Zod, use NestJS 12's `schema` option, and get one source of
truth for types and runtime checks.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.
> This is the densest module outside M4/M5 — confirm scope depth early (Setup) before diving in.

## Setup

- [ ] Confirm M5's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M5 first.
- [ ] Confirm with your trainer whether to build the class-based DTO path as a full working example
      or only as a short comparison against the schema-first path — this decides how much of this
      stage's time goes to the class-based scope item below.

## Build

- [ ] Review why types disappear at runtime, and what that means for an API that only has
      compile-time checks.
- [ ] Review the class-based validation path — `ValidationPipe`, class-validator,
      class-transformer, `@nestjs/mapped-types` — built to the depth you confirmed above.
- [ ] Review the schema-first path: Zod schemas, `z.infer`, and the difference between `z.input`
      and `z.output`.
- [ ] Review NestJS 12's Standard Schema support: the `schema` option on `@Body()`/`@Query()`/
      `@Param()`, and `StandardSchemaValidationPipe`.
- [ ] Review how to turn query strings into the right types (`coerce`, `transform`).
- [ ] Review response shaping with `@SerializeOptions({ schema })`.
- [ ] Review validating environment variables through `@nestjs/config` with a schema.
- [ ] Review when to reach for classes versus when to reach for schemas.
- [ ] Replace M3's hand-written Task types with Zod schemas, starting with `CreateTaskSchema`.
- [ ] Derive `UpdateTaskSchema` from `CreateTaskSchema` using `.partial()` rather than duplicating
      it.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you replaced the
      hand-written types with Zod schemas.
- [ ] Build a query schema that validates and coerces pagination, sort and filter params on the
      task list endpoint.
- [ ] Validate your environment variables with a schema at startup.
- [ ] Make sure a request that fails validation returns a clear, structured error rather than a
      raw stack trace or unhandled exception.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, how you decided on
      the class-based-vs-schema-first depth, and your query-schema design.

## Verify

- [ ] Confirm `CreateTaskSchema` and `UpdateTaskSchema` exist as Zod schemas, with
      `UpdateTaskSchema` derived via `.partial()`.
- [ ] Confirm the query schema correctly validates and coerces pagination, sort and filter.
- [ ] Confirm environment variables are validated through a schema at startup.
- [ ] Confirm a request that fails validation returns a clear, structured error.
- [ ] Checkpoint: produce a request that passes TypeScript's compile-time checks but still fails
      runtime validation, and explain why both layers are needed.
- [ ] Checkpoint: show a case where `z.input` and `z.infer` give different types for the same
      schema.
- [ ] Commit your work to your Team Tasks API branch, building on M5's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_06.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
