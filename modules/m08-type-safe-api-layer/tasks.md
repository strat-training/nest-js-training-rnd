# M8 — Type-Safe API Layer — Tasks

**Objective:** Design a typed contract shared by server and client, type responses/errors/guards/
interceptors/decorators, generate OpenAPI docs from the same schemas, and build a typed client.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done.

## Setup

- [ ] Confirm M7's checkpoint has passed before starting this stage — if it hasn't, stop and finish
      M7 first.
- [ ] Confirm with your trainer how deep to go on the optional `openapi-typescript` comparison, if
      at all, given your time budget for this stage.

## Build

- [ ] Design a `contracts/` folder layout for one typed contract covering the Tasks API, used by
      both the server and the client.
- [ ] Build a typed response envelope (`ApiResponse<T>`) and a typed error model as a discriminated
      union.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you structured the
      `contracts/` folder and the response envelope.
- [ ] Review typed guards and interceptors (`NestInterceptor<T, R>`).
- [ ] Build a header-based `@CurrentUser()` decorator and guard (no real login), typing the request
      object it attaches to.
- [ ] Wire up `@nestjs/swagger` 12 with a `zod-openapi` converter via the `standardSchemaConverter`
      option so Swagger reads your Zod schemas.
- [ ] Build `createClient(contract)` so every generated method has the correct input and output
      types, reusing `ExtractRouteParams` from M5.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, how you designed the
      typed client and any alternatives you considered (including whether you explored the
      optional `openapi-typescript` comparison).
- [ ] Test every new route with Bruno.

## Verify

- [ ] Confirm the `contracts/` folder has one typed contract used by both server and client, not
      two independently maintained copies.
- [ ] Confirm `createClient(contract)` exists and every generated method has the correct
      input/output types.
- [ ] Confirm Swagger UI is live and correctly shows the Zod-schema-backed routes, not generic or
      untyped request bodies — this is what catches a missing `standardSchemaConverter` wiring.
- [ ] Confirm the header-based `@CurrentUser()` decorator and guard are wired into at least one
      route.
- [ ] Checkpoint: rename a schema field and list every place — server and client — that now fails
      to compile.
- [ ] Checkpoint: explain, for any one route, exactly what's checked at compile time versus what's
      checked at runtime.
- [ ] Commit your work to your Team Tasks API branch, building on M7's commit.
- [ ] Self-review your build against every item in `brief.md`'s Definition of done before moving on
      to the write-up.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each
      definition-of-done item to where it's satisfied.
- [ ] Author `module_08.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
