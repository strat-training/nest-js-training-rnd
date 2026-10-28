# Advanced TypeScript with NestJS: Training Curriculum

**Length:** 4 weeks, about 60 hours (15 hours per week)
**Level:** Advanced. For working Node.js and Express developers.
**Style:** Hands-on. One project grows across every module.
**Last checked:** 27 October 2026 (see Section 4 for version notes)

---

## 1. Course Overview

This course teaches engineers how to use TypeScript's type system well, and how to apply it inside a real NestJS API. Participants already know how to build APIs with Express. Here they learn to make those APIs safe: the compiler catches mistakes, and the same schema checks data at runtime.

Participants build one project, the **Team Tasks API**, from a simple in-memory app to a fully typed API with a database, validation, docs, a typed client, and tests.

## 2. Who This Is For

**Required:**
- Has built at least one API with Node.js and Express (routes, middleware, error handling, JSON).
- Comfortable with modern JavaScript (async/await, ES modules).
- Knows basic TypeScript: types, interfaces, unions, simple generics.
- Uses Git, GitHub and VS Code.

**Not required:** any NestJS experience. Module 1 teaches it from an Express point of view.

> If the group is new to TypeScript, run the optional pre-course day in Section 9 first.

## 3. End Goals

By the end of the course, participants can confidently:

1. Use built-in **utility types** (`Partial`, `Pick`, `Omit`, `Record`, `ReturnType`, `Awaited` and more) and know when to use each one.
2. Write their own **mapped types**, including key remapping and `+`/`-` modifiers.
3. Write **conditional types** (`infer`) and **template literal types**.
4. Build a **type-safe API layer** in NestJS:
   - validated input (query, params, body)
   - typed database access
   - typed responses and errors
   - OpenAPI docs generated from the same schemas
   - a typed client that breaks at compile time when the API changes
5. Keep compile-time types and runtime checks in sync from one schema.
6. Test both the code and the types.

## 4. Stack and Version Notes

Free tools only. No Docker. No paid or licensed tools.

| Tool | Plan | Notes |
|---|---|---|
| Node.js | **Left open: 24 or 26. Pin per cohort.** | Node 24 is Active LTS. Node 26 becomes LTS on 28 Oct 2026. NestJS 12 needs Node 20.19+ or 22.12+, so both work. |
| NestJS | **v12 (stable)** | v12 is out (12.1.1 at last check). It is ESM-first. New projects can pick ESM or CommonJS. |
| TypeScript | **6.x to build the Nest app** | TypeScript 7.0 is stable, but it has no stable compiler API until 7.1. The Nest CLI needs that API, and `nest upgrade` moves projects to TypeScript 6. See the note below. |
| Validation | **Zod (v4 line)** through Nest 12's Standard Schema support | Teach class-validator + class-transformer too. The NestJS docs still use it as the default. |
| Database | **Prisma ORM 7 + SQLite** | Prisma 8 is still a release candidate, and `npm install prisma` can now pull it in. **Pin to v7** (use `prisma@prev` or an exact v7 version). Check again before each cohort, since v8 may go stable. |
| Testing | **Vitest + Supertest** | Vitest is the default for NestJS 12 ESM projects. |
| Linting | **oxlint** | Default for NestJS 12 ESM projects. |
| API docs | `@nestjs/swagger` v12 + `zod-openapi` | The v12 Swagger package can read Standard Schema objects through an adapter. |
| Manual API testing | **Bruno** | Instead of Postman. |
| Other | Git, GitHub, VS Code | |

**TypeScript 6 vs 7 note.** The Go-based TypeScript 7 compiler handles decorators and `emitDecoratorMetadata`, so it can type-check a Nest app, and it is much faster. But `nest build` calls the compiler API, which 7.0 does not have yet. Plan for this course: install TypeScript 6.x for the Nest build. In Module 9, show TypeScript 7 as an optional fast type-check step. Test this setup before the cohort starts.

**Vitest vs Jest note.** Choosing the CommonJS option in `nest new` keeps Jest. This curriculum uses the ESM option with Vitest, because it is the current default. If you want Jest to match an earlier course, only Module 9 and the project setup change.

## 5. Course Map

| Week | Modules | Hours |
|---|---|---|
| 1 | M1 NestJS for Express Developers, M2 Generics and Narrowing, M3 Utility Types | 15 |
| 2 | M4 Mapped Types, M5 Conditional and Template Literal Types, M6 Validation and DTOs | 15 |
| 3 | M7 Type-Safe Data Layer, M8 Type-Safe API Layer, M9 Testing Code and Types | 15 |
| 4 | M10 Capstone and Review | 15 |

**Project path:** in-memory Nest app → branded IDs and generics → derived types → mapped types → route and query types → Zod and Standard Schema → Prisma/SQLite → typed contract and client → tests → independent capstone.

---

## 6. Modules

### Module 1: NestJS for Express Developers (5 hours)

**Learning objectives**
- Map Express ideas (routes, middleware, error handlers) to NestJS ideas.
- Build modules, controllers and providers.
- Explain how dependency injection works and how decorators make it possible.
- Set up a strict TypeScript config.

**Topics**
- Express vs NestJS: the request flow (middleware, guards, interceptors, pipes, controller, filters).
- Modules, controllers and providers.
- Dependency injection: constructor types, injection tokens, provider scope.
- Decorators and `emitDecoratorMetadata`: how Nest reads constructor types at runtime, and why a type-only import can break injection.
- Creating a project with `nest new` (ESM option) and reading the project layout.
- Strict compiler flags: `strict`, `noUncheckedIndexedAccess`, `exactOptionalPropertyTypes`. Talk about the trade-offs.
- Setting up a Bruno collection.

**Hands-on lab**
Start the Team Tasks API. Build `ProjectsModule` and `TasksModule` with in-memory data and full CRUD. Test every route with Bruno.

**Checkpoint**
- Draw the injection chain for `TasksController` → `TasksService`.
- Fix a broken injection caused by a type-only import.

---

### Module 2: Generics and Narrowing (5 hours)

**Learning objectives**
- Write generic functions, classes and interfaces with constraints.
- Narrow union types safely.
- Use branded types to stop mixing up IDs.

**Topics**
- Generic constraints (`extends`), defaults, and inference.
- `keyof`, `typeof` and indexed access types.
- `as const` and `satisfies`.
- Type guards, assertion functions, and discriminated unions.
- Exhaustive checks with `never`.
- `unknown` vs `any`.
- Branded (opaque) types for IDs.

**Hands-on lab**
In the Team Tasks API:
- Add `ProjectId` and `TaskId` branded types.
- Build a `Result<T, E>` type (`Ok | Err`) and use it in the services.
- Build a generic `InMemoryRepository<T extends { id: string }>` and use it in both modules.

**Checkpoint**
- Explain why passing a `ProjectId` where a `TaskId` is expected fails to compile.
- Add a new `Err` case and let the compiler show every `switch` that needs updating.

---

### Module 3: Utility Types (5 hours)

**Learning objectives**
- Use every common built-in utility type.
- Combine utility types to derive new types from one source.
- Know the traps (shallow `Partial`, `Omit` on unions).

**Topics**
- Object shape: `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, `Record`.
- Union tools: `Exclude`, `Extract`, `NonNullable`.
- Function and class tools: `ReturnType`, `Parameters`, `ConstructorParameters`, `InstanceType`, `Awaited`.
- String helpers: `Uppercase`, `Lowercase`, `Capitalize`, `Uncapitalize`.
- Compile-time types vs runtime classes: TypeScript utility types vs `PartialType`, `PickType`, `OmitType` and `IntersectionType` from `@nestjs/mapped-types`.
- Common traps and how to avoid them.

**Hands-on lab**
Define one `Task` type. From it, derive `CreateTaskInput`, `UpdateTaskInput`, `TaskSummary` and `TaskResponse` using only utility types. Then write your own `DeepPartial<T>` and `RequireAtLeastOne<T>`.

**Checkpoint**
- Given a new field on `Task`, show which derived types change on their own and which need a manual edit.
- Explain when to use TypeScript's `Partial` and when to use Nest's `PartialType`.

---

### Module 4: Mapped Types (5 hours)

**Learning objectives**
- Write mapped types from scratch.
- Change keys and modifiers inside a mapped type.
- Use mapped types to build reusable helpers.

**Topics**
- The basic form: `{ [K in keyof T]: ... }`.
- Adding and removing modifiers: `+readonly`, `-readonly`, `+?`, `-?`.
- Key remapping with `as`, and filtering keys by their value type.
- Homomorphic vs non-homomorphic mapped types.
- Mapped types over unions.
- Recursive mapped types (`DeepReadonly`).
- How `Record` and `Pick` are built.

**Hands-on lab**
Write `Getters<T>`, `Nullable<T>`, `Mutable<T>` and `OmitByType<T, U>`. Then build a typed `EventBus<Events>` provider for the Team Tasks API (for example, `task.created` and `task.completed`), where each event name is tied to its payload type.

**Checkpoint**
- Rebuild `Pick` and `Record` without looking.
- Show that `bus.emit("task.created", wrongPayload)` fails to compile.

---

### Module 5: Conditional and Template Literal Types (5 hours)

**Learning objectives**
- Write conditional types and use `infer`.
- Build string types with template literals.
- Keep type-level code readable and fast.

**Topics**
- Conditional types and `infer`.
- Distributive conditional types, and how `[T] extends [U]` turns that off.
- Template literal types and string manipulation at the type level.
- Recursive types.
- Type-level code that is too deep or too slow, and how to spot it.
- Writing type-level code that other people can read.

**Hands-on lab**
- `ExtractRouteParams<"/projects/:projectId/tasks/:taskId">` returns `{ projectId: string; taskId: string }`.
- `SortKey<Task>` gives values like `"title" | "-title" | "dueDate" | "-dueDate"` for the list endpoint's sort query.
- `Unwrap<T>` for promises and arrays.

**Checkpoint**
- Explain why a conditional type gives a union result for a union input.
- Fix a type that is too deep for the compiler.

---

### Module 6: Validation and DTOs (5 hours)

**Learning objectives**
- Explain why types alone do not protect a running API.
- Validate input with class-based DTOs and with schema-first Zod.
- Use NestJS 12's `schema` option on route decorators.
- Get one source of truth for types and runtime checks.

**Topics**
- The problem: types disappear at runtime.
- Class-based path: `ValidationPipe`, class-validator, class-transformer, and `@nestjs/mapped-types`.
- Schema-first path: Zod schemas, `z.infer`, and `z.input` vs `z.output`.
- NestJS 12 Standard Schema support: the `schema` option on `@Body()`, `@Query()` and `@Param()`, and `StandardSchemaValidationPipe`.
- Turning query strings into the right types (`coerce`, `transform`).
- Response shaping with `@SerializeOptions({ schema })`.
- Validating environment variables through `@nestjs/config` with a schema.
- Picking an approach: when to use classes and when to use schemas.

**Hands-on lab**
Replace the hand-written Task types with Zod schemas. Build `CreateTaskSchema`, `UpdateTaskSchema` (from `.partial()`), and a query schema for pagination, sort and filter. Validate environment variables with a schema. Return clear validation errors.

**Checkpoint**
- Show a request that passes TypeScript but fails runtime validation.
- Explain when `z.input` and `z.infer` give different types.

---

### Module 7: Type-Safe Data Layer (5 hours)

**Learning objectives**
- Use Prisma's generated types without losing safety.
- Derive result types from queries.
- Keep database types and API types separate.

**Topics**
- Setting up Prisma 7 with SQLite (follow the current Prisma 7 docs for the SQLite setup).
- A `PrismaService` provider and lifecycle hooks in Nest.
- Generated types and `Prisma.TaskGetPayload<{ include: ... }>`.
- `Prisma.validator` and `satisfies` to keep query objects typed.
- Mapping database models to API response types with mapped types.
- Typed error handling: turning Prisma errors into the `Result` type from Module 2.
- Generic repositories: when they help and when they cause harm.
- Transactions.

**Hands-on lab**
Replace the in-memory repository with Prisma + SQLite. Build a `TaskWithProject` type from a Prisma payload. Map database models to `TaskResponse`. Turn "not found" and "unique constraint" errors into typed `Err` values.

**Checkpoint**
- Change a Prisma model and follow the compile errors through the service and mappers.
- Explain why database types should not be sent straight to clients.

---

### Module 8: Type-Safe API Layer (5 hours)

**Learning objectives**
- Design a typed contract shared by server and client.
- Type responses, errors, guards, interceptors and custom decorators.
- Generate OpenAPI docs from the same schemas.
- Build a typed client.

**Topics**
- Contract-first design: one `contracts` folder of schemas used by the server and the client.
- A typed response envelope, `ApiResponse<T>`, and a typed error model as a discriminated union.
- Typed guards and interceptors (`NestInterceptor<T, R>`).
- Custom parameter decorators, such as `@CurrentUser()`, and adding types to the request object.
- OpenAPI with `@nestjs/swagger` v12 and a `zod-openapi` converter.
- A typed client built with mapped and conditional types over the contract.
- Optional comparison: generating client types from the OpenAPI file with a tool such as `openapi-typescript`. Check the current version first.

**Hands-on lab**
Write a contract object for the Tasks API. Build `createClient(contract)` so every method has the right input and output types. Add Swagger UI. Add a simple header-based "current user" guard and decorator (no real login). Test with Bruno.

**Checkpoint**
- Rename a schema field. List every place that breaks at compile time (server and client).
- Explain what is checked at compile time and what is checked at runtime.

---

### Module 9: Testing Code and Types (5 hours)

**Learning objectives**
- Write unit and end-to-end tests for NestJS.
- Use typed mocks.
- Test types so they do not break later.

**Topics**
- `@nestjs/testing` and `Test.createTestingModule`.
- Overriding providers.
- Typed mocks with Vitest (`vi.fn`, `vi.mocked`, `Mocked<T>`).
- End-to-end tests with Supertest and a temporary SQLite file.
- Type tests with `expectTypeOf` and `// @ts-expect-error`.
- Running `tsc --noEmit` and oxlint as checks.
- Optional: TypeScript 7 as a fast type-check step.

**Hands-on lab**
Write unit tests for `TasksService` and e2e tests for the task routes. Add type tests for `ExtractRouteParams`, `SortKey` and the typed client. Add one npm script that runs lint, type-check and tests.

**Checkpoint**
- Show a type test that fails when a helper type is changed by mistake.
- Show a mock that fails to compile when it does not match the real provider.

---

### Module 10: Capstone and Review (15 hours)

**Goal:** Participants add a new feature area to the Team Tasks API on their own.

**Brief:** Add **Comments** and **Labels** to tasks. A comment belongs to a task. A task can have many labels.

**Must include**
1. New Prisma models and a migration.
2. A Zod contract for each new route (input and output).
3. Controllers using the `schema` option, with typed services behind them.
4. At least three of the utility, mapped or conditional types from this course, used in real code (not copied demos).
5. Typed errors and a typed response envelope.
6. OpenAPI docs that include the new routes.
7. New methods on the typed client.
8. Unit tests, e2e tests, and type tests.
9. A short README explaining the main type decisions.

**Time plan**
- Hours 1–10: build.
- Hours 11–12: peer code review (types, naming, readability).
- Hours 13–15: short demo from each participant, plus group review and Q&A.

**Scoring**

| Area | Weight |
|---|---|
| Type design (utility, mapped, conditional, generics) | 30% |
| Runtime safety (validation, errors) | 20% |
| NestJS structure | 15% |
| Tests (code and types) | 20% |
| Code review and communication | 15% |

Passing score: 70%.

---

## 7. Assessment

- **Checkpoints:** every module ends with a short checkpoint (pass or redo).
- **Labs:** each lab is a commit on the project branch. The instructor reviews the commits.
- **Capstone:** scored with the table above.

## 8. Instructor Notes

- Each module has a **starter branch** and a **solution branch**, so someone who falls behind can catch up.
- Keep every type-level exercise tied to the Team Tasks API. Avoid "toy" examples with no link to the project.
- Allow time in Modules 4 and 5. Most people find them the hardest. Move at the group's speed.
- Before each cohort, re-check: NestJS version, TypeScript 6 vs 7 support in the Nest CLI, Prisma 7 vs 8 status, and the Node.js version to pin.

## 9. Pre-Course Setup (and optional TypeScript day)

**Setup before day 1**
- Node.js (24 or 26 LTS, as pinned for the cohort), Git, VS Code, Bruno.
- A GitHub account.
- Clone the course repo and run the check script that confirms the Node, TypeScript and Nest CLI versions.

**Optional pre-course day (about 6 hours)** for groups new to TypeScript:
- Types, interfaces and unions
- Basic generics
- `tsconfig` basics
- Reading compiler errors
