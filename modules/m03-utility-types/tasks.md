# M3 — Utility Types — Tasks

**Objective:** Use common built-in utility types well, combine them to derive several related
types from one source, and spot the traps (shallow `Partial`, `Omit` on unions).

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.

## Setup

- [ ] Confirm M2's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M2 first.

## Build

- [ ] Review object-shape utilities: `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, `Record`.
- [ ] Review union tools: `Exclude`, `Extract`, `NonNullable`.
- [ ] Review function/class tools: `ReturnType`, `Parameters`, `ConstructorParameters`,
      `InstanceType`, `Awaited`.
- [ ] Review string helpers: `Uppercase`, `Lowercase`, `Capitalize`, `Uncapitalize`.
- [ ] Review the difference between TypeScript's compile-time utility types and Nest's runtime
      `PartialType`/`PickType`/`OmitType`/`IntersectionType` from `@nestjs/mapped-types`.
- [ ] Review common traps with these utilities (e.g. shallow `Partial`, `Omit` on a union) and how
      to avoid them.
- [ ] Define one `Task` type to serve as the single source for this stage's derived types.
- [ ] Derive `CreateTaskInput`, `UpdateTaskInput`, `TaskSummary` and `TaskResponse` from `Task`
      using only built-in utility types.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you derived each of the
      four types from `Task`.
- [ ] Write your own `DeepPartial<T>` utility type and use it somewhere real in the Team Tasks API.
- [ ] Write your own `RequireAtLeastOne<T>` utility type and use it somewhere real in the Team
      Tasks API.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, why `DeepPartial`
      and `RequireAtLeastOne` needed to be hand-written rather than pulled from a built-in or
      library type.

## Verify

- [ ] Confirm `CreateTaskInput`, `UpdateTaskInput`, `TaskSummary` and `TaskResponse` are all
      derived from the one `Task` type using only utility types, with no hand-duplicated shapes.
- [ ] Confirm `DeepPartial<T>` and `RequireAtLeastOne<T>` are each exercised somewhere real, not
      just defined and unused.
- [ ] Checkpoint: add a new field to `Task`, then show which of your derived types pick it up
      automatically and which need a manual edit — and explain why.
- [ ] Checkpoint: explain when to reach for TypeScript's `Partial` versus Nest's `PartialType`.
- [ ] Commit your work to your Team Tasks API branch, building on M2's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_03.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
