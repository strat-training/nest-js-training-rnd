# M4 — Mapped Types — Tasks

**Objective:** Write mapped types from scratch, change keys and modifiers inside one, and use
mapped types to build reusable helpers.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.
> This is one of the two hardest modules in the course (with M5) — same 5-hour budget, no built-in
> slack.

## Setup

- [ ] Confirm M3's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M3 first.
- [ ] Confirm with your trainer where extra time should come from if you find yourself running
      short on this stage's 5 hours — the course schedule has no built-in slack for this.

## Build

- [ ] Review the basic mapped-type form: `{ [K in keyof T]: ... }`.
- [ ] Review adding and removing modifiers: `+readonly`, `-readonly`, `+?`, `-?`.
- [ ] Review key remapping with `as`, and filtering keys by their value type.
- [ ] Review the difference between homomorphic and non-homomorphic mapped types.
- [ ] Review how mapped types behave over unions.
- [ ] Review recursive mapped types (e.g. `DeepReadonly`).
- [ ] Review how `Record` and `Pick` are actually built under the hood.
- [ ] Write `Getters<T>`, `Nullable<T>`, `Mutable<T>` and `OmitByType<T, U>` from scratch.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you approached each of
      the four mapped types.
- [ ] Build a typed `EventBus<Events>` provider for the Team Tasks API, wiring in at least a
      `task.created` and `task.completed` event, each tied to its own payload type.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, how you designed
      `EventBus<Events>` and any alternatives you considered.

## Verify

- [ ] Confirm `Getters<T>`, `Nullable<T>`, `Mutable<T>` and `OmitByType<T, U>` all exist as
      hand-written mapped types.
- [ ] Confirm the `EventBus<Events>` provider is wired into the Team Tasks API and used for at
      least `task.created` and `task.completed`.
- [ ] Checkpoint: rebuild `Pick` and `Record` from scratch without looking them up.
- [ ] Checkpoint: show that `bus.emit("task.created", wrongPayload)` with a payload of the wrong
      shape fails to compile.
- [ ] Commit your work to your Team Tasks API branch, building on M3's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_04.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
