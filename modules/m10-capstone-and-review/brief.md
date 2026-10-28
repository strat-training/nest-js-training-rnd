# M10 — Capstone and Review

**Week:** 4 · **Hours:** 15 · **Builds on:** your own M1–M9 Team Tasks API, fully typed, Prisma-backed,
contract-driven, and tested. You must have passed every prior checkpoint (or redone it
successfully) before starting this stage — see Still open.

**Repository:** the capstone is built in a **new, separate repository** — copy/export your final
M1–M9 codebase into it before starting. From this stage on, the capstone no longer lives on the
M1–M9 branch chain. *(Local addition — not in the original PRD.)*

> No solutions file exists for this stage. This brief tells you what to build and how you'll be
> scored — the how is yours to work out, and this time you work alone.

## Objective

Add a new feature area to your own Team Tasks API, unaided, applying everything from M1–M9:
branded types and generics, utility/mapped/conditional types, Zod validation, a type-safe Prisma
data layer, a typed contract and client, and a tested implementation.

## Scope

Add **Comments** and **Labels** to tasks:
- A comment belongs to exactly one task.
- A task can have labels (confirm the cardinality with your trainer — see Still open; the brief
  wording alone doesn't settle whether a label can be shared across tasks).

Every concept from M1–M9 is in scope here — this stage doesn't introduce new topics, it's where you
show you can combine everything on your own, without a brief telling you the type signatures in
advance.

## Stack constraints

Everything pinned for the course so far: Node.js (your cohort's pinned version), NestJS 12,
TypeScript 6.x, Zod 4, Prisma 7 + SQLite, Vitest + Supertest, oxlint, `@nestjs/swagger` 12 +
`zod-openapi`, Bruno. No Docker, no new tools, no new stack decisions this stage.

## Deliverable

Must include:
1. New Prisma models and a migration for Comments and Labels.
2. A Zod contract (input and output) for each new route.
3. Controllers using the `schema` option, backed by typed services.
4. At least three utility, mapped, conditional, or generic types from this course, used in real
   code — not copied from an earlier module's demo.
5. Typed errors and a typed response envelope, consistent with what you built in M8.
6. OpenAPI docs that include the new routes.
7. New methods on your typed client from M8.
8. Unit tests, e2e tests, and type tests for everything new.
9. A short README explaining the main type decisions you made.
10. **One injected feature outside the M1–M9 curriculum:** typed, real-time notifications for
    task/comment/label events, built with NestJS's WebSocket Gateway support. No module in this
    course teaches this — research NestJS's real-time/Gateway support yourself and design a typed
    event contract for it, the same way M4's `EventBus<Events>` typed events in-process. *(Local
    addition — not in the original PRD; see Still Open on how this factors into scoring.)*

## Definition of done

- [ ] All 10 required deliverables above are present and committed.
- [ ] The project lives in its own separate repository, not on the M1–M9 branch chain.
- [ ] The injected real-time feature (#10) works end to end and reflects your own research — not a
      pattern copied from an earlier module's demo.
- [ ] The project builds, lints, and passes its combined type-check + test script from M9 with the
      new Comments/Labels code included.
- [ ] You've completed hours 1–10 (build), then given/received peer code review in hours 11–12
      focused on types, naming and readability, then demoed your work in hours 13–15.
- [ ] Your work is scored against the course rubric:

  | Area | Weight |
  | --- | --- |
  | Type design (utility, mapped, conditional, generics) | 30% |
  | Runtime safety (validation, errors) | 20% |
  | Tests (code and types) | 20% |
  | NestJS structure | 15% |
  | Code review and communication | 15% |

  Passing score: 70%.

## Still open

- Confirm with your trainer: can one label belong to many tasks (many-to-many), or does each task
  own its own labels exclusively? The course materials leave this genuinely open — don't assume
  either direction before starting your Prisma schema.
- Confirm with your trainer: who scores your capstone, and how peer review feeds the 15%
  "Code review and communication" area.
- Confirm with your trainer: if you redid a checkpoint earlier in the course, whether that affects
  your eligibility to start this stage on schedule.
- Confirm with your trainer: how the injected feature (#10) factors into the fixed rubric's
  existing weights above — it's scope beyond the PRD's original 9 deliverables, and the rubric
  table itself isn't changed here; only the EM owns rubric weights.
