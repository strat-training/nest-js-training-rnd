# M10 — Capstone and Review — Tasks

**Objective:** Add a new feature area (Comments and Labels) to your own Team Tasks API, unaided,
applying everything from M1–M9.

> There is no solutions file for this stage. This checklist guides the work — it does not contain
> it. See `brief.md` for the full objective, scope, stack constraints, and definition of done. This
> stage is solo, scored against a fixed rubric (not pass/redo), built in its own separate
> repository, and four Still Open items below must be confirmed before you design your schema.

## Setup

- [ ] Confirm every M1–M9 checkpoint has passed (or been successfully redone) before starting this
      stage — if not, stop and resolve that first.
- [ ] Copy/export your final M1–M9 codebase into a new, separate repository — the capstone lives
      there from now on, not on the M1–M9 branch chain.
- [ ] Confirm with your trainer whether an earlier redone checkpoint affects your eligibility to
      start this stage on schedule.
- [ ] Confirm with your trainer whether one label can belong to many tasks, or each task owns its
      labels exclusively — do not assume either direction before designing your Prisma schema.
- [ ] Confirm with your trainer who scores your capstone, and how peer review feeds the 15% "Code
      review and communication" area.
- [ ] Confirm with your trainer how the injected feature (deliverable #10) factors into the fixed
      rubric's existing weights, since it's scope beyond the PRD's original 9 deliverables.

## Build

- [ ] Design and add new Prisma models and a migration for Comments and Labels, reflecting the
      cardinality you confirmed above.
- [ ] Write a Zod contract (input and output) for each new Comments/Labels route.
- [ ] Write up, in `write-up-template.md`'s "How to build it" section, how you approached the
      Comments and Labels data model and contracts.
- [ ] Build controllers for the new routes using the `schema` option, backed by typed services.
- [ ] Identify and apply at least three utility, mapped, conditional, or generic types from this
      course in real code for this feature — not copied from an earlier module's demo.
- [ ] Add typed errors and extend your typed response envelope from M8 to cover the new routes.
- [ ] Write up, in `write-up-template.md`'s "Why it's built this way" section, which three-plus
      types you chose and why, and how your typed errors/response envelope extend M8's.
- [ ] Add the new routes to your OpenAPI docs.
- [ ] Add new methods to your typed client from M8 for the new routes.
- [ ] Write unit tests, e2e tests, and type tests for everything new in this stage.
- [ ] Research NestJS's real-time/WebSocket Gateway support — no module in this course teaches it.
- [ ] Design a typed event contract for real-time notifications, extending the thinking behind M4's
      `EventBus<Events>` across a new transport boundary.
- [ ] Build the typed real-time notification feature for at least task/comment/label events
      (deliverable #10).
- [ ] Write up, in `write-up-template.md`'s "Injected feature research" section, what you researched,
      what you considered and rejected, and how it connects back to M4's `EventBus<Events>`.

## Verify

- [ ] Confirm all 10 required deliverables from `brief.md` are present and committed.
- [ ] Confirm the project lives in its own separate repository, not on the M1–M9 branch chain.
- [ ] Confirm the injected real-time feature (#10) works end to end and reflects your own research
      — not a pattern copied from an earlier module's demo.
- [ ] Confirm the project builds, lints, and passes the combined script from M9 with the new
      Comments/Labels code included.
- [ ] Confirm you've completed hours 1–10 (build).
- [ ] Complete hours 11–12: give and receive peer code review focused on types, naming and
      readability; record what came up in `write-up-template.md`'s "Peer review notes" section.
- [ ] Complete hours 13–15: demo your work, then participate in group review and Q&A.
- [ ] Commit your work to your Team Tasks API branch.
- [ ] Self-review your build and write-up against every item in `brief.md`'s Definition of done.
- [ ] Self-review your build specifically against the fixed rubric in `brief.md` (Type design 30%,
      Runtime safety 20%, Tests 20%, NestJS structure 15%, Code review and communication 15%) —
      for each area, identify where your work demonstrates it.

## Write-up

- [ ] Fill in `write-up-template.md`'s "Overview" section.
- [ ] Fill in `write-up-template.md`'s "Concepts worth explaining" section.
- [ ] Fill in `write-up-template.md`'s "What tripped me up" section.
- [ ] Fill in `write-up-template.md`'s "What I'd do differently" section.
- [ ] Fill in `write-up-template.md`'s "Checkpoint evidence" section, mapping each of the 10
      required deliverables to where it's satisfied.
- [ ] Write `README.md` **inside your capstone project's own (separate) repository** explaining
      your main type decisions (deliverable #9) — draw on `write-up-template.md`'s content, but
      this is a real file in your project, not `write-up-template.md` itself.
- [ ] Author `module_10.md` (teaching material for the content library), once write-up-template.md
      is filled in and your build passes VALIDATE: draw the lesson from write-up-template.md's
      "How to build it," "Concepts worth explaining," and "Why it's built this way" sections (not
      its "What tripped me up" / "What I'd do differently" narrative). Close the file with exactly
      5 open-ended comprehension questions — one per distinct concept (reuse concepts if fewer than
      5 distinct ones exist — never pad with an unrelated question to hit the count), never yes/no,
      never containing the answer — and an Understanding Checklist with one self-assessable item
      per question.
