# M5 — Conditional and Template Literal Types — Tasks

**Objective:** Write conditional types and use `infer`, build string types with template
literals, and keep type-level code readable and fast.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.
> This is the other of the two hardest modules in the course (with M4) — same 5-hour budget, no
> built-in slack.

## Setup

- [ ] Confirm M4's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M4 first.
- [ ] Confirm with your trainer where extra time should come from if you find yourself running
      short on this stage's 5 hours — same open question as M4.

## Build

- [ ] Review conditional types and `infer`.
- [ ] Review distributive conditional types, and how wrapping in `[T] extends [U]` turns
      distribution off.
- [ ] Review template literal types and string manipulation at the type level.
- [ ] Review recursive types.
- [ ] Review how to spot type-level code that's too deep or too slow for the compiler.
- [ ] Review how to write type-level code that other people can actually read.
- [ ] Build `ExtractRouteParams<T>` that extracts route param names from a route string literal
      into an object type — keep in mind M8's typed client and M9's type tests will reuse this.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you approached
      `ExtractRouteParams`.
- [ ] Build `SortKey<Task>` that derives the full set of valid sort-query values from `Task`'s
      keys — this is reused in M8 and M9 as well.
- [ ] Build `Unwrap<T>` that unwraps both `Promise<T>` and `T[]`.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, how you shaped
      `ExtractRouteParams` and `SortKey<Task>` knowing later stages reuse them.

## Verify

- [ ] Confirm `ExtractRouteParams<T>` correctly extracts route param names into an object type.
- [ ] Confirm `SortKey<Task>` correctly derives the full set of valid sort-query values.
- [ ] Confirm `Unwrap<T>` correctly unwraps both `Promise<T>` and `T[]`.
- [ ] Checkpoint: explain, in your own words, why a conditional type applied to a union input
      produces a union result.
- [ ] Checkpoint: show a type you hit that was too deep for the compiler, and how you simplified
      it to fix that.
- [ ] Commit your work to your Team Tasks API branch, building on M4's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_05.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
