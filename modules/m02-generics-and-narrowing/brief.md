# M2 — Generics and Narrowing

**Week:** 1 · **Hours:** 5 · **Builds on:** M1's `ProjectsModule`/`TasksModule` in-memory CRUD.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.

## Objective

By the end of this stage you can:
- Write generic functions, classes and interfaces with constraints.
- Narrow union types safely.
- Use branded types to stop IDs of different kinds from being mixed up.

## Scope

- Generic constraints (`extends`), generic defaults, and inference.
- `keyof`, `typeof`, and indexed access types.
- `as const` and `satisfies`.
- Type guards, assertion functions, and discriminated unions.
- Exhaustive checks with `never`.
- `unknown` vs `any`.
- Branded (opaque) types for IDs.

## Stack constraints

- TypeScript 6.x — no new tooling this stage, this is type-system work on top of M1's project.

## Deliverable

In the Team Tasks API:
- Add `ProjectId` and `TaskId` as branded types.
- Build a `Result<T, E>` type (an `Ok | Err` discriminated union) and use it in your services in
  place of thrown exceptions where it fits.
- Build a generic `InMemoryRepository<T extends { id: string }>` and use it from both
  `ProjectsModule` and `TasksModule`.

`Result<T, E>`'s shape matters beyond this stage — M7 and M8 reuse it, so whatever you settle on
here should still make sense once Prisma errors and API responses need to flow through it.

## Definition of done

- [ ] `ProjectId` and `TaskId` are branded types, and passing one where the other is expected fails
      to compile.
- [ ] `Result<T, E>` exists and is used by at least one service method in place of a thrown
      exception.
- [ ] A generic `InMemoryRepository<T extends { id: string }>` exists and is used by both
      `ProjectsModule` and `TasksModule` — no duplicated repository logic between them.
- [ ] Checkpoint: you can explain, in your own words, why passing a `ProjectId` where a `TaskId` is
      expected fails to compile.
- [ ] Checkpoint: adding a new `Err` case to your `Result` type and letting the compiler point out
      every `switch`/exhaustiveness check that now needs updating.
- [ ] Work is committed to your Team Tasks API branch, building on M1's commit.

## Still open

None beyond what's already flagged in M1 — proceed once M1's checkpoint has passed.
