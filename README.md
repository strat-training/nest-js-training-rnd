# Advanced TypeScript with NestJS Training

This repo holds the Build-to-Teach version of the Advanced TypeScript with NestJS training
curriculum: nine training stages in `modules/` (M01–M09), followed by a capstone (M10). The format
is different on purpose: instead of being taught the material, the trainee builds toward each
stage's deliverable from a brief, and writes up how they did it as they go. The write-up is what
ends up teaching the next cohort.

**A note on words:** a *module* in this repository is a training stage, not a NestJS `@Module()`.
Stage M01 is the one that actually teaches what a NestJS module — and its controllers and
providers — is.

## What is in this repository

| Path | What it holds |
| --- | --- |
| `modules/` | The ten stage folders (M01–M10), each with a brief, a checklist, and a write-up template |
| `docs/prd/` | The original course PRD |
| `docs/arch-docs/` | The Solution Design doc turning the PRD into a build plan |

## Ground rules (every stage)

- **Free tools only.** No Docker, no paid licenses.
- **Pinned for the whole cohort:** Node.js (24 or 26 — confirm with your trainer), NestJS 12,
  TypeScript 6.x for the Nest build, Zod 4 via Standard Schema, Prisma ORM 7 + SQLite, Vitest +
  Supertest, oxlint, `@nestjs/swagger` 12 + `zod-openapi`. Your trainer re-verifies these are still
  current immediately before the cohort starts — versions move fast, and `npm install prisma`
  alone can resolve to a Prisma 8 release candidate instead of the pinned 7.
- **Bruno** for manual API testing, not Postman.
- **Git/GitHub workflow** throughout.
- **The capstone (M10) is built in its own separate repository**, and includes one feature you
  research outside the taught curriculum — see `modules/m10-capstone-and-review/brief.md`.

## How a stage works

1. **Your trainer hands you the brief.** Each stage's `brief.md` says what to build and how you'll
   know it's done: objective, scope, stack constraints, the deliverable, a definition of done, and
   what to confirm with your trainer before you start. It contains no lesson, no steps, no code,
   and no solutions. How to build it is yours to work out.
2. **You build and write up the stage together.** Fill in `write-up-template.md` in the stage
   folder while you build, not after it already works. Your write-up is the teaching content —
   write it for someone who will follow it with no trainer to ask.
3. **Your trainer reviews both together.** When you reach the definition of done, bring both the
   working system and the write-up to your checkpoint. The question is not only "does it work?"
   but "could someone else learn from this?"
4. **You revise.** Fix what the review finds, in both the build and the write-up, before starting
   the next stage.
5. **The finished pair goes into the content library.** An accepted stage is the build plus its
   write-up — distilled into `module_<number>.md`, the last step of every stage's checklist. Your
   trainer decides what carries into the next cohort's plan.

Review happens at the end of every stage, not just at the end of the course.

### Why review as you go, not at the end

A write-up finished after the deliverable already works tends to be thin — there's no real
pressure to make it good once the thing runs. Reviewing both pieces together, stage by stage,
means the trainer is judging whether the work is teachable, not just whether it works, and catches
problems early instead of in a finished draft nobody wants to redo.

## What is in each stage folder

| File | Who writes it | Purpose |
| --- | --- | --- |
| `brief.md` | Your trainer | Objective, scope, stack constraints, the deliverable, and definition of done. No answers. Do not edit it. |
| `write-up-template.md` | You | Blank at first; filled in as you build, not after. |
| `tasks.md` | Generated from `brief.md` via `/trainee-task-planner` | An ordered checklist mirroring the brief — setup, then build, then verify, then write-up. You tick the boxes; it holds no answers and no steps you weren't already told. |
| `module_<number>.md` | You, as the last step of `tasks.md` | The distilled teaching artifact for the content library — five comprehension questions and an understanding checklist, for the next cohort. |

Your Team Tasks API code lives outside this repository, in your own GitHub repo. Link it from the
header of your write-up. From M10 on, the capstone lives in its own separate repository — link
that one instead.

## Stages

| Stage | Title | Theme | Leaves behind |
| --- | --- | --- | --- |
| M01 | NestJS for Express Developers | Request flow, dependency injection, decorators, strict TypeScript | `ProjectsModule`/`TasksModule`, in-memory CRUD |
| M02 | Generics and Narrowing | Generic constraints, narrowing, branded types | Branded `ProjectId`/`TaskId`, `Result<T, E>`, generic `InMemoryRepository` (reused through M07/M08) |
| M03 | Utility Types | Built-in utility types, composing derived types | `CreateTaskInput`/`UpdateTaskInput`/`TaskSummary`/`TaskResponse`, `DeepPartial`, `RequireAtLeastOne` |
| M04 | Mapped Types | Mapped types from scratch, key remapping | `Getters`/`Nullable`/`Mutable`/`OmitByType`, typed `EventBus<Events>` |
| M05 | Conditional and Template Literal Types | Conditional types, `infer`, template literals | `ExtractRouteParams`, `SortKey<Task>`, `Unwrap<T>` (reused in M08/M09) |
| M06 | Validation and DTOs | Runtime validation, Zod, Standard Schema | Zod schemas replacing hand-written types, a pagination/sort/filter query schema |
| M07 | Type-Safe Data Layer | Prisma, typed queries, typed errors | Prisma + SQLite data layer, `TaskWithProject`, typed Prisma errors |
| M08 | Type-Safe API Layer | Contract-first design, typed client, OpenAPI | `contracts/` folder, `createClient(contract)`, Swagger UI, a current-user guard |
| M09 | Testing Code and Types | Unit, e2e, and type tests | A tested, CI-checkable Team Tasks API (handed off to the capstone) |
| M10 | Capstone and Review | An independent build — Comments + Labels, plus one researched feature | — (terminal stage) |

Work the stages in order. Later stages build on earlier ones: M02's branded types and
`Result<T, E>` carry through M07's typed Prisma errors and M08's typed response envelope; M05's
`ExtractRouteParams` and `SortKey<Task>` are reused by M08's typed client and M09's type tests.
Generics and narrowing (M02) come before the utility/mapped/conditional type stages (M03–M05) that
build on that foundation; Zod validation (M06) comes before the Prisma data layer (M07) so runtime
checks exist before persistence; the typed contract and client (M08) come before testing (M09) so
there's something to test end to end.

## Assessment

- Every module ends in a checkpoint (see that stage's `brief.md`).
- The capstone (M10) is scored against a fixed rubric (Type design 30%, Runtime safety 20%, Tests
  20%, NestJS structure 15%, Code review and communication 15%); 70% or more passes. The rubric
  lives in `modules/m10-capstone-and-review/brief.md` — it is the one place point values are
  specified, and it is not a solution, it is how your finished API gets graded.
- By the end of the course you should be able to evidence all six End Goals listed in the PRD's
  Section 3 — see the Solution Design doc's Traceability matrix for how each one maps to specific
  modules.
