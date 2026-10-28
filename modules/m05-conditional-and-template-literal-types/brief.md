# M5 — Conditional and Template Literal Types

**Week:** 2 · **Hours:** 5 · **Builds on:** M4's mapped types.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.
>
> This is the other of the two hardest modules in the course (along with M4). You still get the
> same 5 hours — see Still open if you're running short.

## Objective

By the end of this stage you can:
- Write conditional types and use `infer`.
- Build string types with template literals.
- Keep type-level code readable and fast to compile.

## Scope

- Conditional types and `infer`.
- Distributive conditional types, and how wrapping in `[T] extends [U]` turns distribution off.
- Template literal types and string manipulation at the type level.
- Recursive types.
- Type-level code that's too deep or too slow for the compiler, and how to spot it.
- Writing type-level code that other people can actually read.

## Stack constraints

- TypeScript 6.x — no new tooling this stage.

## Deliverable

Build:
- `ExtractRouteParams<"/projects/:projectId/tasks/:taskId">` that resolves to
  `{ projectId: string; taskId: string }`.
- `SortKey<Task>` that gives values like `"title" | "-title" | "dueDate" | "-dueDate"` for the list
  endpoint's sort query.
- `Unwrap<T>` that works over both promises and arrays.

`ExtractRouteParams` and `SortKey<Task>` matter beyond this stage — M8's typed client and M9's type
tests both reuse them.

## Definition of done

- [ ] `ExtractRouteParams<T>` correctly extracts route param names from a route string literal into
      an object type.
- [ ] `SortKey<Task>` correctly derives the full set of valid sort-query values from `Task`'s keys.
- [ ] `Unwrap<T>` correctly unwraps both `Promise<T>` and `T[]`.
- [ ] Checkpoint: you can explain, in your own words, why a conditional type applied to a union
      input produces a union result (distribution).
- [ ] Checkpoint: you've hit a type that's too deep for the compiler at some point in this stage,
      and can show how you simplified it to fix that.
- [ ] Work is committed to your Team Tasks API branch, building on M4's commit.

## Still open

- Confirm with your trainer: if you're running short on the 5 hours, where the extra time should
  come from — same open question as M4, since the two hardest modules share this risk.
