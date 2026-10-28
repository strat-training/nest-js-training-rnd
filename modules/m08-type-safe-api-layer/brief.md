# M8 — Type-Safe API Layer

**Week:** 3 · **Hours:** 5 · **Builds on:** M7's Prisma + SQLite data layer.

> No solutions file exists for this stage. This brief tells you what to build and what "done"
> looks like — the how is yours to work out.

## Objective

By the end of this stage you can:
- Design a typed contract shared by server and client.
- Type responses, errors, guards, interceptors and custom decorators.
- Generate OpenAPI docs from the same schemas used for validation.
- Build a typed client over a contract.

## Scope

- Contract-first design: one `contracts` folder of schemas used by both server and client.
- A typed response envelope (`ApiResponse<T>`) and a typed error model as a discriminated union.
- Typed guards and interceptors (`NestInterceptor<T, R>`).
- Custom parameter decorators, such as `@CurrentUser()`, and adding types to the request object.
- OpenAPI docs with `@nestjs/swagger` 12 and a `zod-openapi` converter — Swagger only reads your
  Zod schemas once you pass the `standardSchemaConverter` option.
- A typed client built over the contract using mapped and conditional types (reuse
  `ExtractRouteParams` from M5).
- Optional comparison: generating client types from the emitted OpenAPI file with a tool such as
  `openapi-typescript` — check its current version first if you explore this.

## Stack constraints

- `@nestjs/swagger` 12 + `zod-openapi`, with the `standardSchemaConverter` option wired in.
- Bruno for manual testing of the new routes.
- No real login — the "current user" guard/decorator is header-based only.

## Deliverable

Build a `contracts/` folder with a typed contract for the Tasks API. Build `createClient(contract)`
so every method it exposes has the correct input and output types. Add Swagger UI, backed by your
Zod schemas. Add a simple header-based "current user" guard and decorator (no real login). Test
everything with Bruno.

## Definition of done

- [ ] A `contracts/` folder exists with one typed contract covering the Tasks API, used by both the
      server and the client — not two independently maintained copies.
- [ ] `createClient(contract)` exists and every generated method has the correct input/output types
      derived from the contract.
- [ ] Swagger UI is live and shows the Zod-schema-backed routes correctly (not generic/untyped
      request bodies).
- [ ] A header-based `@CurrentUser()` decorator and guard exist and are wired into at least one
      route.
- [ ] Checkpoint: you can rename a schema field and list every place — server and client — that now
      fails to compile.
- [ ] Checkpoint: you can explain, for any one route, exactly what's checked at compile time versus
      what's checked at runtime.
- [ ] Work is committed to your Team Tasks API branch, building on M7's commit.

## Still open

- Confirm with your trainer: how deep to go on the optional `openapi-typescript` comparison, if at
  all, given the time budget for this stage.
