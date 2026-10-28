# M6 — Validation and DTOs

**Week:** 2 · **Hours:** 5 · **Builds on:** M5's route and sort types.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.

## Objective

By the end of this stage you can:
- Explain why types alone don't protect a running API.
- Validate input with class-based DTOs and with schema-first Zod.
- Use NestJS 12's `schema` option on route decorators.
- Get one source of truth for types and runtime checks.

## Scope

- The problem: types disappear at runtime.
- Class-based path: `ValidationPipe`, class-validator, class-transformer, `@nestjs/mapped-types`.
- Schema-first path: Zod schemas, `z.infer`, and the difference between `z.input` and `z.output`.
- NestJS 12's Standard Schema support: the `schema` option on `@Body()`, `@Query()` and `@Param()`,
  and `StandardSchemaValidationPipe`.
- Turning query strings into the right types (`coerce`, `transform`).
- Response shaping with `@SerializeOptions({ schema })`.
- Validating environment variables through `@nestjs/config` with a schema.
- Picking an approach: when to reach for classes and when to reach for schemas.

## Stack constraints

- Zod 4, used through NestJS 12's Standard Schema support.
- class-validator + class-transformer for the class-based path.
- `@nestjs/config` for environment validation.

## Deliverable

Replace the hand-written Task types from M3 with Zod schemas. Build `CreateTaskSchema`,
`UpdateTaskSchema` (derived with `.partial()`), and a query schema for pagination, sort and filter
on the task list endpoint. Validate your environment variables with a schema. Return clear
validation errors to the caller.

## Definition of done

- [ ] `CreateTaskSchema` and `UpdateTaskSchema` exist as Zod schemas, with `UpdateTaskSchema`
      derived from `CreateTaskSchema` via `.partial()` rather than duplicated.
- [ ] A query schema validates and coerces pagination, sort and filter params on the task list
      endpoint.
- [ ] Environment variables are validated through a schema at startup.
- [ ] A request that fails validation returns a clear, structured error — not a raw stack trace or
      an unhandled exception.
- [ ] Checkpoint: you can produce a request that passes TypeScript's compile-time checks but still
      fails runtime validation, and explain why both layers are needed.
- [ ] Checkpoint: you can explain a case where `z.input` and `z.infer` (`z.output`) give different
      types for the same schema.
- [ ] Work is committed to your Team Tasks API branch, building on M5's commit.

## Still open

- Confirm with your trainer: whether to keep the class-based path as a full working example in this
  stage, or only as a short comparison alongside the schema-first path — the solution design flags
  this module as the densest outside M4/M5 and leaves the depth of the class-based coverage open.
