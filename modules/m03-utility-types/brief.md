# M3 — Utility Types

**Week:** 1 · **Hours:** 5 · **Builds on:** M2's branded IDs, `Result<T, E>` and generic
`InMemoryRepository`.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.

## Objective

By the end of this stage you can:
- Use the common built-in utility types and know when to reach for each one.
- Combine utility types to derive several related types from one source type.
- Spot the traps — shallow `Partial`, `Omit` behaving oddly on unions.

## Scope

- Object-shape utilities: `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, `Record`.
- Union tools: `Exclude`, `Extract`, `NonNullable`.
- Function and class tools: `ReturnType`, `Parameters`, `ConstructorParameters`, `InstanceType`,
  `Awaited`.
- String helpers: `Uppercase`, `Lowercase`, `Capitalize`, `Uncapitalize`.
- Compile-time types vs. runtime classes — TypeScript's utility types vs. `PartialType`,
  `PickType`, `OmitType` and `IntersectionType` from `@nestjs/mapped-types`.
- Common traps with these utilities and how to avoid them.

## Stack constraints

- TypeScript 6.x utility types, plus `@nestjs/mapped-types` from your M1 Nest project — no new
  tooling beyond that.

## Deliverable

Define one `Task` type. From it, derive `CreateTaskInput`, `UpdateTaskInput`, `TaskSummary` and
`TaskResponse` using only built-in utility types — no hand-written duplicate shapes. Then write
your own `DeepPartial<T>` and `RequireAtLeastOne<T>` utility types (not built into TypeScript).

## Definition of done

- [ ] `CreateTaskInput`, `UpdateTaskInput`, `TaskSummary` and `TaskResponse` are all derived from
      one `Task` type using built-in utility types.
- [ ] `DeepPartial<T>` and `RequireAtLeastOne<T>` exist, are hand-written (not pulled from a
      library), and are exercised somewhere real in the Team Tasks API.
- [ ] Checkpoint: given a new field added to `Task`, you can show which of your derived types pick
      it up automatically and which need a manual edit — and why.
- [ ] Checkpoint: you can explain when to reach for TypeScript's `Partial` versus Nest's
      `PartialType`.
- [ ] Work is committed to your Team Tasks API branch, building on M2's commit.

## Still open

None beyond what's already flagged in earlier stages — proceed once M2's checkpoint has passed.
