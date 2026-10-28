# M2 — Generics and Narrowing — Tasks

**Objective:** Write generic functions/classes/interfaces with constraints, narrow unions safely,
and use branded types to stop IDs of different kinds from being mixed up.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.

## Setup

- [ ] Confirm M1's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M1 first.

## Build

- [ ] Review generic constraints (`extends`), defaults, and inference before writing your own
      generics.
- [ ] Review `keyof`, `typeof`, and indexed access types.
- [ ] Review `as const` and `satisfies` and where each one is useful.
- [ ] Review type guards, assertion functions, and discriminated unions.
- [ ] Review exhaustive checks with `never`.
- [ ] Review the distinction between `unknown` and `any`, and when each is appropriate.
- [ ] Add `ProjectId` and `TaskId` as branded types to the Team Tasks API.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you implemented the
      branded ID pattern.
- [ ] Build a `Result<T, E>` (`Ok | Err`) type and use it in at least one service method in place
      of a thrown exception.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, how you shaped
      `Result<T, E>` — note that M7 and M8 reuse this shape, so capture why it should still work
      for errors you haven't seen yet.
- [ ] Build a generic `InMemoryRepository<T extends { id: string }>` and use it from both
      `ProjectsModule` and `TasksModule`, removing any duplicated repository logic.

## Verify

- [ ] Confirm passing a `ProjectId` where a `TaskId` is expected fails to compile, and vice versa.
- [ ] Confirm `Result<T, E>` is used by at least one service method in place of a thrown exception.
- [ ] Confirm `ProjectsModule` and `TasksModule` both use the same generic `InMemoryRepository`
      with no duplicated logic between them.
- [ ] Checkpoint: explain, in your own words, why passing a `ProjectId` where a `TaskId` is
      expected fails to compile.
- [ ] Checkpoint: add a new `Err` case to your `Result` type and let the compiler point out every
      `switch`/exhaustiveness check that now needs updating — fix each one.
- [ ] Commit your work to your Team Tasks API branch, building on M1's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_02.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
