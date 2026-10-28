# Advanced TypeScript with NestJS — Training Curriculum

A 4-week, ~60-hour Build-to-Teach course for working Node.js/Express developers moving into
NestJS's type system. One project — the **Team Tasks API** — grows across every stage, from an
in-memory NestJS app to a fully typed, Prisma-backed, contract-driven, tested API.

## How this program runs

Built under the [Build-to-Teach framework](docs/build-to-teach-framework.md): an EM lays out the
curriculum and each stage's brief; the trainee builds the stage for real and writes up how they did
it as they go. Both the working system and the write-up feed the next cohort's teaching material.

## Repository layout

| Path | What's there |
| --- | --- |
| `docs/prd/` | The original course PRD |
| `docs/arch-docs/` | The Solution Design doc turning the PRD into a build plan |
| `docs/build-to-teach-framework.md` | How a Build-to-Teach cycle runs, and who owns what |
| `modules/` | Trainee-facing stage guides — no solutions, just briefs and checklists |

## Where to start

- **Trainees:** start at [`modules/README.md`](modules/README.md) for the full stage sequence,
  then open `m01-nestjs-for-express-developers/brief.md`.
- **EMs / trainers:** read the [Build-to-Teach framework](docs/build-to-teach-framework.md) first,
  then the [PRD](docs/prd/advanced-typescript-nestjs-curriculum.md) and
  [Solution Design](<docs/arch-docs/Solution Design Advanced TypeScript with NestJS Training Curriculum.md>).

Each stage folder under `modules/` has a `brief.md` (what to build) and a `write-up-template.md`
(filled in live, as the trainee builds). A stage's `tasks.md` checklist is generated from its brief
via the `/trainee-task-planner` command — it isn't hand-written, so re-run that command after
editing a brief rather than hand-editing `tasks.md` directly.
