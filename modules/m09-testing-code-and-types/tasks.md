# M9 — Testing Code and Types — Tasks

**Objective:** Write unit and end-to-end tests for NestJS, use typed mocks, and test types so
helper types don't silently break later.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.
> Three Still Open items below shape how this stage gets built — resolve them before writing the
> combined npm script.

## Setup

- [ ] Confirm M8's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M8 first.
- [ ] Confirm with your trainer whether your single combined npm script needs to run `expectTypeOf`
      tests specifically inside a type-check mode (not just at normal test-run time) —
      `expectTypeOf` does nothing at runtime on its own.
- [ ] Confirm with your trainer whether to use a fresh temporary SQLite file per e2e test run.
- [ ] Confirm with your trainer whether to add a dependency-injection smoke test (build the testing
      module, resolve `TasksService`) given reports that Vitest's default transform can drop
      decorator metadata.

## Build

- [ ] Review `@nestjs/testing` and `Test.createTestingModule`.
- [ ] Review overriding providers in a testing module.
- [ ] Review typed mocks with Vitest (`vi.fn`, `vi.mocked`, `Mocked<T>`).
- [ ] Write unit tests for `TasksService` using typed mocks in place of real Prisma calls.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you structured
      `TasksService`'s unit tests and mocks.
- [ ] Review end-to-end testing with Supertest against a running instance, applying your decision
      above on the e2e database setup.
- [ ] Write e2e tests for the task routes using Supertest.
- [ ] Review type tests with `expectTypeOf` and `// @ts-expect-error`.
- [ ] Write type tests for `ExtractRouteParams`, `SortKey<Task>`, and the typed client.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, how you structured
      your type tests and applied your decision above on where they run.
- [ ] Add one npm script that runs lint, type-check, and tests together, incorporating your
      decisions on `expectTypeOf` placement and the DI smoke test.

## Verify

- [ ] Confirm `TasksService`'s unit tests use typed mocks, not real Prisma calls.
- [ ] Confirm the task routes' e2e tests run via Supertest against a real, running instance.
- [ ] Confirm type tests exist for `ExtractRouteParams`, `SortKey<Task>`, and the typed client.
- [ ] Confirm the single npm script runs lint, type-check and tests together, and exits non-zero on
      any failure.
- [ ] Checkpoint: show a type test failing the moment a helper type is changed by mistake.
- [ ] Checkpoint: show a typed mock failing to compile when it no longer matches the real
      provider's shape.
- [ ] Commit your work to your Team Tasks API branch, building on M8's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_09.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
