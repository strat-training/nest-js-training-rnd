# M4 — Mapped Types

**Week:** 2 · **Hours:** 5 · **Builds on:** M3's derived `Task` types.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.
>
> This is one of the two hardest modules in the course (the other is M5). You still get the same
> 5 hours — budget your time and flag it early with your trainer if you're running short (see
> Still open).

## Objective

By the end of this stage you can:
- Write mapped types from scratch.
- Change keys and modifiers inside a mapped type.
- Use mapped types to build reusable helpers.

## Scope

- The basic form: `{ [K in keyof T]: ... }`.
- Adding and removing modifiers: `+readonly`, `-readonly`, `+?`, `-?`.
- Key remapping with `as`, and filtering keys by their value type.
- Homomorphic vs. non-homomorphic mapped types.
- Mapped types over unions.
- Recursive mapped types (e.g. `DeepReadonly`).
- How `Record` and `Pick` are actually built under the hood.

## Stack constraints

- TypeScript 6.x — no new tooling this stage.

## Deliverable

Write `Getters<T>`, `Nullable<T>`, `Mutable<T>` and `OmitByType<T, U>` from scratch. Then build a
typed `EventBus<Events>` provider for the Team Tasks API (for example `task.created` and
`task.completed`), where each event name is tied to its own payload type.

## Definition of done

- [ ] `Getters<T>`, `Nullable<T>`, `Mutable<T>` and `OmitByType<T, U>` all exist as hand-written
      mapped types.
- [ ] A typed `EventBus<Events>` provider exists and is wired into the Team Tasks API, used for at
      least the `task.created` and `task.completed` events.
- [ ] Checkpoint: you can rebuild `Pick` and `Record` from scratch without looking them up.
- [ ] Checkpoint: you can show that calling `bus.emit("task.created", wrongPayload)` with a payload
      of the wrong shape fails to compile.
- [ ] Work is committed to your Team Tasks API branch, building on M3's commit.

## Still open

- Confirm with your trainer: if you're running short on the 5 hours, where the extra time should
  come from — the solution design flags this module as exactly 60/60 hours with no built-in slack,
  and leaves the source of extra time (flex time elsewhere, an office hour) to the program owner.
