# Team Tasks API — Module Guides

Trainee's copy for the *Advanced TypeScript with NestJS* course. You build each stage of the
**Team Tasks API** for real, write up how you did it as you go, and what you produce becomes the
teaching material for the next cohort.

**There are no solutions in this folder, and none are coming until you've built your own.**
Each `brief.md` tells you *what* to build and *what "done" looks like* — never *how*. That's
deliberate: the point of this course is the type-system and NestJS reasoning you do to get there,
not a diff you can copy. Source grounding for every brief is the course PRD
(`docs/prd/advanced-typescript-nestjs-curriculum.md`) and the solution design
(`docs/arch-docs/Solution Design Advanced TypeScript with NestJS Training Curriculum.md`).

## Sequence

One project, the Team Tasks API, grows across every stage — each one builds on the last.

| Stage | Week | Hours | Title | Adds to the Team Tasks API |
| --- | --- | --- | --- | --- |
| [m01](m01-nestjs-for-express-developers/brief.md) | 1 | 5 | NestJS for Express Developers | `ProjectsModule` + `TasksModule`, in-memory CRUD |
| [m02](m02-generics-and-narrowing/brief.md) | 1 | 5 | Generics and Narrowing | Branded `ProjectId`/`TaskId`, `Result<T, E>`, generic `InMemoryRepository` |
| [m03](m03-utility-types/brief.md) | 1 | 5 | Utility Types | `CreateTaskInput`, `UpdateTaskInput`, `TaskSummary`, `TaskResponse`, `DeepPartial`, `RequireAtLeastOne` |
| [m04](m04-mapped-types/brief.md) | 2 | 5 | Mapped Types | `Getters`, `Nullable`, `Mutable`, `OmitByType`, typed `EventBus<Events>` |
| [m05](m05-conditional-and-template-literal-types/brief.md) | 2 | 5 | Conditional and Template Literal Types | `ExtractRouteParams`, `SortKey<Task>`, `Unwrap<T>` |
| [m06](m06-validation-and-dtos/brief.md) | 2 | 5 | Validation and DTOs | Zod schemas replace hand-written types; pagination/sort/filter query schema; env validation |
| [m07](m07-type-safe-data-layer/brief.md) | 3 | 5 | Type-Safe Data Layer | Prisma 7 + SQLite replaces the in-memory repository; `TaskWithProject`; typed Prisma errors |
| [m08](m08-type-safe-api-layer/brief.md) | 3 | 5 | Type-Safe API Layer | `contracts/` folder, `createClient(contract)`, Swagger UI, header-based current-user guard |
| [m09](m09-testing-code-and-types/brief.md) | 3 | 5 | Testing Code and Types | Unit, e2e and type tests; one npm script for lint/type-check/test |
| [m10](m10-capstone-and-review/brief.md) | 4 | 15 | Capstone and Review | Comments + Labels, built solo, scored against the course rubric |

## How to use a stage folder

Each folder has:
- `brief.md` — objective, scope, stack constraints, deliverable, definition of done, and anything
  still open that you should confirm with your trainer before starting.
- `write-up-template.md` — fill this in **as you build**, not after. It's both your checkpoint
  evidence and the draft of `module_<number>.md`, the teaching artifact that future trainees will
  actually read.

If a stage doesn't yet have a `tasks.md`, ask your trainer to run `/trainee-task-planner` against
it, or work directly from `brief.md`.

## Rules every stage shares

- **No Docker.** Free tools only.
- **Every lab is a commit** on your Team Tasks API branch — each one building on the last.
- **Every module ends with a checkpoint** (pass or redo) before you move to the next stage.
- Keep every exercise tied to the Team Tasks API — no toy examples with no link to the project.
