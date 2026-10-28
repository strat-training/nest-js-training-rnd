# M1 — NestJS for Express Developers

**Week:** 1 · **Hours:** 5 · **Builds on:** none — this is the first stage.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.

## Objective

By the end of this stage you can:
- Map Express concepts (routes, middleware, error handlers) onto their NestJS equivalents.
- Build modules, controllers and providers.
- Explain how dependency injection works in Nest and how decorators make it possible.
- Set up a strict TypeScript config for a Nest project.

## Scope

- The NestJS request flow, and where it differs from an Express middleware chain: middleware,
  guards, interceptors, pipes, controller, filters.
- Modules, controllers and providers.
- Dependency injection: constructor types, injection tokens, provider scope.
- Decorators and `emitDecoratorMetadata` — how Nest reads constructor types at runtime, and why a
  type-only import can silently break injection.
- Creating a project with `nest new` (ESM option) and understanding the generated project layout.
- Strict compiler flags: `strict`, `noUncheckedIndexedAccess`, `exactOptionalPropertyTypes` — and
  the trade-offs each one brings.
- Setting up a Bruno collection for manual API testing.

## Stack constraints

- Node.js — the version pinned for your cohort (24 or 26; see your trainer if this isn't settled
  yet).
- NestJS 12, ESM project mode (`nest new` → ESM option).
- TypeScript 6.x.
- Bruno for manual API testing (not Postman).
- Git + GitHub + VS Code.
- No Docker.

## Deliverable

Start the Team Tasks API. Build a `ProjectsModule` and a `TasksModule`, each with full CRUD over
in-memory data (no database yet — that arrives in M7). Every route must be reachable and testable
from a Bruno collection.

## Definition of done

- [ ] `ProjectsModule` and `TasksModule` exist, each exposing full CRUD routes over in-memory data.
- [ ] Every route is covered by a request in your Bruno collection, and every one of those requests
      succeeds against your running app.
- [ ] The project's `tsconfig.json` has `strict`, `noUncheckedIndexedAccess` and
      `exactOptionalPropertyTypes` all turned on, and the project still compiles.
- [ ] Checkpoint: you can draw the injection chain for `TasksController` → `TasksService` — what
      gets injected, by what token, and in what scope.
- [ ] Checkpoint: given an injection that's broken by a type-only import, you can explain why Nest
      can't resolve it and fix it.
- [ ] Work is committed to your Team Tasks API branch, one commit the instructor can review.

## Still open

- Confirm with your trainer: which Node.js version (24 or 26) is pinned for your cohort — the
  solution design leaves this open pending a pilot install check.
