# M1 — NestJS for Express Developers — Tasks

**Objective:** Map Express concepts onto NestJS, build your first modules/controllers/providers,
and understand dependency injection well enough to diagnose it when it breaks.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.

## Setup

- [ ] Confirm with your trainer which Node.js version (24 or 26) is pinned for this cohort, and
      install it before continuing.
- [ ] Initialize the Team Tasks API with `nest new`, choosing the ESM project option, and read
      through the generated project layout before changing anything.
- [ ] Set the strict compiler flags `strict`, `noUncheckedIndexedAccess`, and
      `exactOptionalPropertyTypes` in `tsconfig.json`, and confirm the project still compiles.

## Build

- [ ] Study the NestJS request flow (middleware, guards, interceptors, pipes, controller, filters)
      and map each stage to its closest Express equivalent from your own experience.
- [ ] Review how NestJS modules, controllers and providers fit together before writing your first
      one.
- [ ] Review how NestJS dependency injection works — constructor types, injection tokens, and
      provider scope — before relying on it in your build.
- [ ] Look into decorators and `emitDecoratorMetadata`: how Nest reads constructor types at
      runtime, and why a type-only import on a constructor parameter can break injection.
- [ ] Build `ProjectsModule` with full CRUD over in-memory data.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you structured
      `ProjectsModule` while it's fresh.
- [ ] Build `TasksModule` with full CRUD over in-memory data.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how `TasksModule` relates
      to `ProjectsModule`.
- [ ] Set up a Bruno collection with a request covering every route across both modules.

## Verify

- [ ] Confirm `ProjectsModule` and `TasksModule` each expose complete CRUD (create, read, update,
      delete) routes over in-memory data — not just the routes you happened to test first.
- [ ] Run every request in your Bruno collection against your running app and confirm each one
      succeeds.
- [ ] Verify `tsconfig.json` still has `strict`, `noUncheckedIndexedAccess` and
      `exactOptionalPropertyTypes` all enabled, and that the project compiles with no errors.
- [ ] Checkpoint: draw the injection chain for `TasksController` → `TasksService` — what gets
      injected, by what token, and in what scope — and record it in your write-up.
- [ ] Checkpoint: deliberately break an injection using a type-only import, confirm it fails, then
      fix it and explain in your own words why the fix works.
- [ ] Commit your work to your Team Tasks API branch as one reviewable commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "Why it's built this way" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_01.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
