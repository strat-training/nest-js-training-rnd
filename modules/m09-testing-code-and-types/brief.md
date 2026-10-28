# M9 — Testing Code and Types

**Week:** 3 · **Hours:** 5 · **Builds on:** M8's contract, client and Swagger docs.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.

## Objective

By the end of this stage you can:
- Write unit and end-to-end tests for a NestJS application.
- Use typed mocks correctly.
- Test types so helper types don't silently break later.

## Scope

- `@nestjs/testing` and `Test.createTestingModule`.
- Overriding providers in a testing module.
- Typed mocks with Vitest (`vi.fn`, `vi.mocked`, `Mocked<T>`).
- End-to-end tests with Supertest against a running instance.
- Type tests with `expectTypeOf` and `// @ts-expect-error`.
- Running `tsc --noEmit` and oxlint as checks, from one script.
- Optional: TypeScript 7 as a fast type-check step alongside the TypeScript 6 build.

## Stack constraints

- Vitest + Supertest for unit and e2e tests.
- oxlint for linting.
- Optional TypeScript 7 package installed alongside TypeScript 6 (see Still open) — used only for a
  fast type-check step, never for `nest build`.

## Deliverable

Write unit tests for `TasksService`. Write end-to-end tests for the task routes. Add type tests for
`ExtractRouteParams`, `SortKey<Task>` (both from M5) and the typed client (from M8). Add one npm
script that runs lint, type-check, and tests together.

## Definition of done

- [ ] `TasksService` has unit tests that replace its dependencies with typed mocks (not real Prisma
      calls).
- [ ] The task routes have end-to-end tests run via Supertest against a real, running instance of
      the app.
- [ ] Type tests exist for `ExtractRouteParams`, `SortKey<Task>`, and the typed client, using
      `expectTypeOf` and/or `// @ts-expect-error`.
- [ ] One npm script runs lint, type-check and tests together, and exits non-zero on any failure.
- [ ] Checkpoint: you can show a type test that fails the moment a helper type is changed by
      mistake — proving the test actually catches the regression it's meant to catch.
- [ ] Checkpoint: you can show a typed mock that fails to compile when it no longer matches the real
      provider's shape.
- [ ] Work is committed to your Team Tasks API branch, building on M8's commit.

## Still open

- Confirm with your trainer: whether `expectTypeOf` type tests need to run inside your single npm
  script's type-check step specifically (not just at test-run time) — `expectTypeOf` does nothing
  at runtime, so a wrong type only fails under `tsc` or Vitest's type-check mode.
- Confirm with your trainer: whether to set up a fresh temporary SQLite file per e2e test run so
  tests don't share data between runs.
- Confirm with your trainer: whether to add a small dependency-injection smoke test (a test that
  just builds the testing module and resolves `TasksService`) — there are reports that Vitest's
  default transform can drop decorator metadata, which breaks injection with an unclear error.
