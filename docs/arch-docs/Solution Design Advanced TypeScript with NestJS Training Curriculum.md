# Solution Design: Advanced TypeScript with NestJS Training Curriculum

Oct 27, 2026 · @Ryan Angelo

## Purpose and scope

This design turns the Advanced TypeScript with NestJS PRD into a build plan for a 4-week, 60-hour course. It covers the stack, the Team Tasks API that learners build, the module plan, testing, delivery and risks. It does not cover the course content itself (slides, lab text, starter code).

| Item | Value |
| --- | --- |
| Length | 4 weeks, about 60 hours (15 hours a week) |
| Level | Advanced, for working Node.js and Express developers |
| Style | Hands-on, one project (Team Tasks API) grows across every module |
| Structure | 9 modules of 5 hours each, then a 15-hour capstone |
| Pass mark | 70% on the capstone, pass or redo on each module checkpoint |

**How to read this document.** Items taken straight from the PRD are marked **PRD**. Items the PRD does not state are marked **Proposed** and need the program owner to confirm them. Gaps and unclear points are listed in the Open questions section, not quietly settled.

## Audience and prerequisites

The course is for developers who already ship Express APIs and want to use TypeScript's type system well inside NestJS. No NestJS experience is needed. **PRD**

**Entry requirements (PRD)**

- Has built at least one API with Node.js and Express (routes, middleware, error handling, JSON).
- Comfortable with modern JavaScript (async/await, ES modules).
- Knows basic TypeScript: types, interfaces, unions, simple generics.
- Uses Git, GitHub and VS Code.

**Optional pre-course TypeScript day (PRD).** About 6 hours for groups new to TypeScript: types, interfaces and unions, basic generics, `tsconfig` basics, and reading compiler errors. These hours sit outside the 60-hour course.

**Proposed: a short readiness check.** The PRD gives no way to decide who needs the pre-course day. A 20-minute quiz on generics and union narrowing, sent a week before day 1, would make that call clear. It needs program owner approval.

## Technology stack and version baseline

The stack uses free tools only, with no Docker. Two facts from this week change the PRD's plan: Node 24 has already left Active LTS, and Prisma 8 now installs by default. Versions below were checked on 27 October 2026 (see Sources).

| Tool | Choice | Status | Notes |
| --- | --- | --- | --- |
| Node.js | 24 or 26, pinned per cohort | PRD (left open) | Node 26 becomes LTS on 28 Oct 2026 and is supported to 30 Apr 2029. Node 24 left Active LTS on 20 Oct 2026, is now in Maintenance, and is supported to 30 Apr 2028. Nest 12 needs Node 20.19+ or 22.12+, so both work. |
| NestJS | 12 | PRD | 12.0.0 came out on 27 Aug 2026. The PRD notes 12.1.1; not re-confirmed. ESM-first: `nest new` asks for ESM or CommonJS. |
| TypeScript | 6.x for the Nest build | PRD | TypeScript 7.0 is stable but has no stable compiler API until 7.1. The Nest CLI needs that API, and `nest upgrade` moves projects to TypeScript 6. |
| Validation | Zod 4 through Standard Schema, plus class-validator | PRD | `@Body()`, `@Query()` and `@Param()` take a `schema` option. Register the Standard Schema pipe to turn it on. Zod 4 not re-checked. |
| Database | Prisma ORM 7 | PRD | Pin to 7. Since August 2026, `npm install prisma` gives a Prisma 8 release candidate. Prisma says 8 reaches general availability in October 2026, so this may change within days. |
| SQLite driver | `@prisma/adapter-better-sqlite3` | Proposed | Prisma 7 needs a driver adapter, and the PRD only says to follow the Prisma 7 docs. The adapter uses `better-sqlite3`, a native module, and a `prisma.config.ts` file. |
| Testing | Vitest + Supertest | PRD | Vitest is the default for Nest 12 ESM projects. |
| Linting | oxlint | PRD | Default for Nest 12 ESM projects. |
| API docs | `@nestjs/swagger` 12 + `zod-openapi` | PRD | Swagger 12 reads Zod schemas only after you pass a converter in the `standardSchemaConverter` option. |
| Manual API testing | Bruno | PRD | Instead of Postman. |
| Other | Git, GitHub, VS Code | PRD |  |

Not re-checked in this pass: Zod, Vitest, Supertest, Bruno and oxlint versions. Check them with the other items before each cohort.

**Proposed: Node version.** Pick Node 26 as the default. It has the longer support window, which covers cohorts run through 2027 and 2028. Fall back to Node 24 if `better-sqlite3` fails to install on Node 26 on any learner operating system during the pilot.

**Proposed: TypeScript 6 and 7 side by side.** Keep `typescript` at 6.x so `nest build` works. Install TypeScript 7 under a second package name (for example `"typescript-7": "npm:typescript@7"`) and call it only in the Module 9 fast type-check step. Microsoft also ships a `@typescript/typescript6` package for tools that still need the 6.0 API. Test this setup before the cohort starts.

## Reference application architecture

Every request to the Team Tasks API takes one fixed path through NestJS, and one `contracts/` folder of Zod schemas feeds the server, the docs and the client. **PRD**

&#91;embedded content: Team Tasks API · request path and shared contracts\]

A request passes the guard, the validation pipe, the controller, the service and the data layer. The pipe and controller read their types from `contracts/`. The same schemas build the OpenAPI docs and the typed client, so renaming a schema field breaks the build on both the server and the client. **PRD**

The exception filter step is **Proposed**. The PRD asks for a typed error model but does not say how errors reach it.

## Program timeline and learning path

The course is 4 weeks of 15 hours each: weeks 1 to 3 hold three 5-hour modules, and week 4 is the 15-hour capstone. **PRD** The optional 6-hour pre-course TypeScript day comes before week 1 and is not part of the 60 hours. **PRD**

&#91;embedded content: 4 weeks · 9 modules and a capstone\]

All labs add to the same Team Tasks API. It starts in memory in M1, gets a database in M7 and a typed contract and client in M8, and each learner extends it alone in M10.

## Module design

Each of the nine teaching modules is 5 hours and ends with a pass-or-redo checkpoint. Every lab is a commit on the Team Tasks API, and each lab uses what the earlier labs built. **PRD**

| Module | Week | Lab output in the Team Tasks API | Design note |
| --- | --- | --- | --- |
| M1 NestJS for Express Developers | 1 | `ProjectsModule` and `TasksModule` with in-memory CRUD, tested in Bruno | Teach dependency injection and `emitDecoratorMetadata` here, including the type-only import failure. Set the strict `tsconfig` flags in this module. |
| M2 Generics and Narrowing | 1 | Branded `ProjectId` and `TaskId`, a `Result<T, E>` type, a generic `InMemoryRepository` | `Result` is reused in M7 and M8, so keep its shape stable. |
| M3 Utility Types | 1 | `CreateTaskInput`, `UpdateTaskInput`, `TaskSummary` and `TaskResponse` derived from one `Task`; `DeepPartial` and `RequireAtLeastOne` | Contrast TypeScript's `Partial` with Nest's `PartialType`. |
| M4 Mapped Types | 2 | `Getters`, `Nullable`, `Mutable`, `OmitByType`, and a typed `EventBus<Events>` provider | One of the two hardest modules, but it gets the same 5 hours (see Risks). |
| M5 Conditional and Template Literal Types | 2 | `ExtractRouteParams`, `SortKey<Task>`, `Unwrap<T>` | The route and sort types are reused in M8 (client) and M9 (type tests). |
| M6 Validation and DTOs | 2 | Zod schemas replace the hand-written types; a query schema for pagination, sort and filter; environment validation | Teach both the class-based and schema-first paths, then when to pick each. |
| M7 Type-Safe Data Layer | 3 | Prisma 7 + SQLite replaces the in-memory repository; `TaskWithProject`; Prisma errors become `Err` values | Version pin and SQLite adapter setup must be ready before this lab (see Stack). |
| M8 Type-Safe API Layer | 3 | A `contracts` folder, `createClient(contract)`, Swagger UI, a header-based current-user guard and decorator | The `standardSchemaConverter` setup is needed for Swagger to read the Zod schemas. No real login. |
| M9 Testing Code and Types | 3 | Unit tests for `TasksService`, e2e tests for the task routes, type tests, one npm script for lint, type-check and tests | TypeScript 7 is an optional fast type-check step. |

**Learning path (PRD).** In-memory Nest app, then branded IDs and generics, derived types, mapped types, route and query types, Zod and Standard Schema, Prisma and SQLite, typed contract and client, tests, and the capstone.

## Capstone design

In week 4, each participant works alone for 15 hours to add **Comments** and **Labels** to the Team Tasks API. A comment belongs to one task. A task can have many labels. **PRD**

**Required deliverables (PRD).** Each one maps to a scoring area. The mapping itself is **Proposed**.

| # | Deliverable | Scoring area it feeds |
| --- | --- | --- |
| 1 | New Prisma models and a migration | NestJS structure |
| 2 | A Zod contract for each new route (input and output) | Runtime safety |
| 3 | Controllers that use the `schema` option, with typed services | NestJS structure, Runtime safety |
| 4 | At least three utility, mapped or conditional types, used in real code and not copied from demos | Type design |
| 5 | Typed errors and a typed response envelope | Runtime safety |
| 6 | OpenAPI docs that include the new routes | NestJS structure |
| 7 | New methods on the typed client | Type design |
| 8 | Unit tests, e2e tests and type tests | Tests |
| 9 | A short README that explains the main type decisions | Code review and communication |

**Time plan (PRD).** Hours 1 to 10 are for building. Hours 11 and 12 are peer code review on types, naming and readability. Hours 13 to 15 are a short demo from each participant, then group review and Q&A.

**Scoring (PRD).** The pass mark is 70%.

| Area | Weight |
| --- | --- |
| Type design (utility, mapped, conditional, generics) | 30% |
| Runtime safety (validation, errors) | 20% |
| Tests (code and types) | 20% |
| NestJS structure | 15% |
| Code review and communication | 15% |

The PRD does not say who scores, how the peer review feeds the 15% area, or whether a participant who redoes a checkpoint can still enter the capstone. These are listed in Open questions.

## Testing and assessment strategy

The course tests the Team Tasks API at four levels, and it checks learners at three points: module checkpoints, lab commits and the capstone. Everything is taught in Module 9 and then required again in the capstone. **PRD**

| Level | What it proves | Tools |
| --- | --- | --- |
| Unit tests | `TasksService` logic works with its dependencies replaced | Vitest, `@nestjs/testing`, `vi.fn`, `vi.mocked`, `Mocked<T>` |
| End-to-end tests | The task routes, validation and errors work over HTTP | Supertest and a temporary SQLite file |
| Type tests | Helper types such as `ExtractRouteParams`, `SortKey` and the typed client do not change by accident | `expectTypeOf`, `// @ts-expect-error` |
| Static checks | The project compiles and passes lint | `tsc --noEmit`, oxlint, run from one npm script |

| Check on the learner | When | Result |
| --- | --- | --- |
| Checkpoint | End of every module | Pass or redo |
| Lab | Every module | A commit on the project branch, reviewed by the instructor |
| Capstone | Week 4 | Scored on the table above, pass mark 70% |

**Proposed: type tests must run in a type-check step.** `expectTypeOf` does nothing when the test runs, so a wrong type only fails under `tsc` or Vitest's type-check mode. The single npm script should include one of them, and Module 9 should show this with a deliberate failure.

**Proposed: one e2e database per run.** Create a new temporary SQLite file, apply the migrations, run the tests, then delete the file. This keeps tests from sharing data.

**Proposed: a dependency injection smoke test.** Add a small test that builds the testing module and resolves `TasksService`. Reports from other projects show that Vitest's default code transform can drop decorator metadata, and Nest then fails to inject without a clear error. The Nest 12 generated config should handle this, but confirm it in the pilot.

## Delivery model and instructor kit

The instructor kit is one course repository with a starter branch and a solution branch for each module, so a learner who falls behind can catch up. **PRD** Every type-level exercise stays tied to the Team Tasks API, with no toy examples. **PRD** Modules 4 and 5 are the hardest, so the instructor moves at the group's speed there. **PRD**

**Setup before day 1 (PRD).** Learners install Node.js (the pinned version), Git, VS Code and Bruno, and create a GitHub account. They clone the course repo and run a check script that confirms the Node, TypeScript and Nest CLI versions.

**Proposed: a longer check script.** Also confirm that `better-sqlite3` loads, that Prisma resolves to version 7 and not a release candidate, and that a sample test resolves a Nest provider. A learner who fails any check finds out before day 1, not during Module 1.

**Proposed: keep the branches from drifting.** With nine modules and a capstone, there are about 20 branches to keep in step. Run `npm run check` on every solution branch, and a compile check on every starter branch, each time a dependency changes.

**Re-check before each cohort.** The PRD lists four items. Two more are Proposed.

| Item | What to re-check | State on 27 Oct 2026 |
| --- | --- | --- |
| Node.js version | Which version to pin | Node 26 enters LTS on 28 Oct 2026. Node 24 is in Maintenance. |
| NestJS | Latest 12.x and the CLI | 12.0.0 released 27 Aug 2026. |
| TypeScript | Whether the Nest CLI works with TypeScript 7 | 7.0 has no stable compiler API. 7.1 had not shipped when the PRD was checked. |
| Prisma | Version 7 vs 8 | 8 is a release candidate, general availability expected in October 2026. |
| `better-sqlite3` (Proposed) | Installs on every learner operating system and on the pinned Node | Native module, needs a pilot run on Node 26. |
| Vitest config (Proposed) | Decorator metadata survives the Vitest transform | Check the generated config and run the injection smoke test. |

The PRD does not describe how the course is delivered (live or remote, class size, number of instructors). See Open questions.

## Risks and mitigations

Most risks come from tool versions moving under a stack that is new. The PRD already covers some of them; the rest are **Proposed**.

| Risk | Why it matters | Mitigation | Source |
| --- | --- | --- | --- |
| Prisma 8 installs by default | `npm install prisma` has given a release candidate since August 2026, and its commands differ from Prisma 7 (for example `prisma contract emit` replaces `prisma generate`). The Module 7 lab would break. | Pin an exact Prisma 7 version in `package.json` and commit the lockfile on every branch. Re-check at cohort start, since 8 may go stable this month. | PRD (pin), Proposed (lockfile) |
| `better-sqlite3` fails to install | It is a native module. A failed install on Node 26 or on a learner's laptop blocks Module 7 and the e2e tests, and there is no Docker fallback. | Pilot on every learner operating system. The longer check script catches it before day 1. Fall back to Node 24. | Proposed |
| Nest CLI and TypeScript 7 mismatch | `nest build` needs a compiler API that TypeScript 7.0 does not have. | Build with TypeScript 6.x. Show TypeScript 7 only as an optional check in Module 9. Test the setup before the cohort. | PRD |
| Decorator metadata lost in Vitest | Injection can fail in tests with no clear error. | Check the generated Vitest config in the pilot. Add the injection smoke test. | Proposed |
| Swagger cannot read Zod schemas | Swagger 12 needs a converter passed in `standardSchemaConverter`, and its nullable output changed from version 11. | Build the converter in the Module 8 starter branch. Add a snapshot test of the OpenAPI document. | Proposed |
| Modules 4 and 5 run short | They are the hardest modules, but every module has 5 hours and the plan has no spare hours (9 × 5 + 15 = 60). | The PRD says to move at the group's speed. The program owner must decide where the extra time comes from. | PRD (note), open decision |
| Learners lack TypeScript basics | Advanced material in 4 weeks leaves no room to teach the basics. | Run the optional 6-hour pre-course day. Use the readiness check to decide who needs it. | PRD, Proposed (check) |

## Open questions for the program owner

Nine points need a decision or a correction before the course is built. Each has a suggested answer, which is a **Proposed** default and not a PRD requirement.

| # | Question | Why it matters | Suggested answer |
| --- | --- | --- | --- |
| 1 | Which Node version do we pin, 24 or 26? The PRD says Node 24 is Active LTS, but it moved to Maintenance on 20 Oct 2026. | Sets the install pilot and the support window for later cohorts. | Node 26, with Node 24 as the fallback if the pilot fails. |
| 2 | Where do extra hours for Modules 4 and 5 come from? | The plan is exactly 60 hours with no spare time. | Reserve 2 of the 10 capstone build hours as flex time, or add an optional office hour. |
| 3 | Can one label be on many tasks, or does each task own its labels? The brief says "a task can have many labels". | Decides the Prisma model and migration in the capstone. | Many-to-many: one `Label` model shared by tasks. |
| 4 | Who scores the capstone, and how does peer review count in the 15% area? | The PRD gives weights but no scorer or rubric. | The instructor scores with a written rubric. Peer review feeds the 15% area but does not set it alone. |
| 5 | Can a learner start the capstone with a failed checkpoint? | The PRD says pass or redo but not what happens after a redo. | Redo before the end of week 3, and block the capstone until it passes. |
| 6 | How is the course delivered: live or remote, class size, number of instructors? | The instructor reviews every lab commit, which does not scale to a large group. | Confirm the format and set a maximum class size. |
| 7 | Are there success measures, such as completion rate, capstone pass rate or time to competency? | The PRD has none, so we cannot say if the course works. | Add at least capstone pass rate and checkpoint redo rate. |
| 8 | Does Module 6 keep all eight topics in 5 hours? It covers the class-based path, the schema-first path, query coercion, response shaping and environment validation. | It is the densest module outside 4 and 5. | Keep both paths, but teach the class-based path as a short comparison. |
| 9 | Do we stay on Prisma 7 for the next cohort if Prisma 8 goes stable this month? | The labs and the commands differ between the two. | Stay on 7 for this cohort. Prisma supports 7 for 18 months after 8 reaches general availability. |

## Traceability matrix

Six PRD end goals are covered by the module plan. The three items that are not fully covered are about assessment, delivery and success measures, and each one points to an open question. Pick a status in the last column to track it.

| PRD item | Built in | Design element | Status |
| --- | --- | --- | --- |
| Goal 1: use utility types | M3 | One `Task` type that four types are derived from; custom `DeepPartial` and `RequireAtLeastOne` | Covered |
| Goal 2: write mapped types | M4 | `Getters`, `Nullable`, `Mutable`, `OmitByType`, typed `EventBus` | Covered |
| Goal 3: write conditional and template literal types | M5 | `ExtractRouteParams`, `SortKey<Task>`, `Unwrap<T>` | Covered |
| Goal 4: build a type-safe API layer | M6 to M8 | Zod schemas, Prisma data layer, `contracts` folder, Swagger, typed client | Covered |
| Goal 5: keep types and runtime checks in sync from one schema | M6, M8 | One Zod schema feeds `z.infer`, the Nest `schema` option and the OpenAPI document | Covered |
| Goal 6: test code and types | M9, M10 | Unit, e2e and type tests, one npm script | Covered |
| Stack and version pins (Node, Prisma) | Setup, M7 | Pinned versions and a longer check script (questions 1 and 9) | Needs decision |
| Assessment and scoring | M1 to M10 | Checkpoints, lab commits, capstone rubric (questions 4 and 5) | Needs decision |
| Delivery model | Whole course | Starter and solution branches; format and class size missing (question 6) | Needs decision |
| Success measures | Whole course | None in the PRD (question 7) | Gap in PRD |

## Sources

Checked on 27 October 2026. Everything not listed here comes from the PRD, *Advanced TypeScript with NestJS: Training Curriculum*.

- Node.js: [endoflife.date Node.js schedule](https://endoflife.date/nodejs) and [DevX on Node.js 26 LTS](https://www.devx.com/coding/nodejs-26-lts-new-features-release-date/)
- NestJS 12: [Nest v12.0.0 release](https://github.com/nestjs/nest/releases/tag/v12.0.0), [Nest schematics 12.0.0](https://github.com/nestjs/schematics/releases/tag/12.0.0) and [InfoQ on NestJS 12](https://infoq.com/news/2026/10/nestjs-12-observability)
- Swagger and Zod: [@nestjs/swagger 12.0.0 release](https://github.com/nestjs/swagger/releases/tag/12.0.0)
- TypeScript 7: [InfoQ on TypeScript 7.0](https://infoq.com/news/2026/08/typescript-7-released/) and [Microsoft's TypeScript 7 post](https://devblogs.microsoft.com/typescript/?p=5246)
- Prisma: [Prisma release status](https://www.prisma.io/docs/prisma-orm/release-status) and [Prisma 7 SQLite quickstart](https://www.prisma.io/docs/v7/prisma-orm/quickstart/sqlite)
- Third-party reports, not official documentation: [Prisma 8 vs Prisma 7 command differences](https://dev.to/fabwaseem/prisma-8-vs-prisma-7-should-you-upgrade-a-tested-migration-guide-p5b) and [Vitest decorator metadata and NestJS injection](https://raw.githubusercontent.com/AI-Unified-Process/marketplace/f6d063ef36d4f42defbd41eebcd3b25896bdd8ef/aiup-nestjs-nextjs/skills/nest-test/SKILL.md)
