# PXL Sweeper Project Rules

This repository builds the PXL Sweeper game.

`REQUIREMENTS.md` is the current project truth.

# Browser Game Project Rules

This repository builds PXL Sweep across the course.
Do not start a different project unless the course instructions explicitly change the project.

Authoritative project files:

- `REQUIREMENTS.md`
- `IMPLEMENTATION_PLAN.md`
- `TODO.md`
- `DONE.md`
- `GEMINI.md`

Project rules:

- Keep one `TODO.md` item small enough for one review cycle.
- Refresh `TODO.md` from the current phase in `IMPLEMENTATION_PLAN.md`.
- Update `TODO.md` before starting a new implementation chunk.
- Update `TODO.md` and `DONE.md` after implementation.
- Move an item to `DONE.md` only after the required checks, review, and doc updates are complete.
- `DONE.md` holds only verified work.
- Update `REQUIREMENTS.md` when scope or acceptance criteria change.
- Update `IMPLEMENTATION_PLAN.md` when the order or grouping of work changes.
- For narrow tasks, pass the exact authoritative files in the prompt instead of retyping context.
- Ask before making a large refactor, changing the directory structure, or removing tests.
- Before moving work to `DONE.md`, review the diff, run the required checks, and update docs if the change affected scope or structure.

## Phase 1 Baseline Context

- **Project Type:** Browser SPA (static-site JavaScript)
- **Goal:** Deliver a stable, playable Minesweeper experience with maintainable code and tests.
- **Constraints:**
  - Single-page app
  - No backend (unless explicitly justified)
  - Plain JavaScript static-site workflow compatibility
- **Deployment Target:** Local-first static hosting (**assumed until confirmed**)
- **Risk Tolerance:** Medium (**assumed until confirmed**)

### Assumed until confirmed
- Final product/assignment scope details
- Deployment target details beyond local-first
- Official risk tolerance from reviewer/instructor

### Open Questions
- Confirm exact project type/runtime constraints beyond browser SPA baseline.
- Confirm exact in-scope feature set from assignment.
- Confirm deployment target (local-only vs hosted).
- Confirm required review cadence and risk policy.

## Command Baseline

| Capability | Command | Baseline Result | Notes |
|---|---|---|---|
| install | `npm install` | Not yet executed in this session | Run from repo root |
| lint | `npm run lint` | Not yet executed in this session | Blocker if script missing |
| typecheck | `npm run typecheck` | Not yet executed in this session | Optional if not configured |
| test | `npm run test` | Not yet executed in this session | Required by setup requirements |
| build | `npm run build` | Not yet executed in this session | Blocker if script missing |
| run | `npm run start` (or project-specific) | Not yet executed in this session | Confirm actual script in `package.json` |

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.
