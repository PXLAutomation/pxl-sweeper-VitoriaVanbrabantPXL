1. Product Overview
Concise description of the game
Core design goal (what makes this version distinct, in one sentence)

2. Core Gameplay Rules
Grid behavior
Mine placement rules (including first-click behavior)
Reveal mechanics
Flagging mechanics
Win/loss conditions

3. User Interface
Layout (single screen constraint)
Visual elements (grid, tiles, numbers, states)
Interaction model (mouse, touch, gestures)
Feedback (hover, click, errors, win/loss)

4. Game Configuration
Grid size(s)
Mine density
Restart behavior
Any randomness constraints (e.g., no-guessing vs classic randomness)

5. Non-Functional Requirements
Performance (instant interactions, no lag)
Responsiveness (desktop vs mobile expectations)
Accessibility considerations (color, input clarity)
Browser support (keep realistic and minimal)

6. Technical Constraints
Single-page app
No backend (unless explicitly justified)
State management approach (high-level, no code)
Persistence (if any)

7. Out of Scope
Explicitly list what will NOT be included to prevent scope creep

8. Open Questions
Any unresolved decisions that need clarification

## Project Setup Requirements

- The project shall include a `package.json` file in the repository root.
- The `package.json` file shall define the project's runnable commands in a consistent way.
- The `package.json` file shall include at least a `test` script so the same test command can be run every time.
- If the project uses ES module imports in JavaScript, `package.json` shall set `"type": "module"`.
- The project shall remain compatible with a plain JavaScript, static-site workflow.

## Requirement Traceability Matrix

| Req ID | Requirement summary | Phase | Status | Verification artifact |
|---|---|---|---|---|
| R-001 | Product overview finalized | Phase 1 | Planned | `GEMINI.md` context section |
| R-002 | Core gameplay rules defined and implemented | Phase 2 | Planned | engine unit tests (`/tests/**/game*.test.*`) |
| R-003 | UI layout/interaction/feedback implemented | Phase 3 | Planned | integration/UI tests (`/tests/**/ui*.test.*`) |
| R-004 | Game configuration behavior implemented | Phase 2/3 | Planned | engine + UI tests |
| R-005 | Non-functional requirements validated | Phase 4/5 | Planned | CI results + manual smoke notes |
| R-006 | Technical constraints respected (SPA, no backend, state approach, persistence) | Phase 1/3/4 | Planned | architecture/docs + build/CI |
| R-007 | Out-of-scope boundaries documented | Phase 1 | Planned | `REQUIREMENTS.md` section 7 |
| R-008 | Open questions tracked and resolved/deferred | Phase 1/5 | Planned | `GEMINI.md` + final traceability update |
| R-009 | `package.json` present at repo root | Phase 1 | Planned | file existence check |
| R-010 | Runnable scripts defined consistently in `package.json` | Phase 1/4 | Planned | scripts + CI parity |
| R-011 | `test` script exists and is repeatable | Phase 1/4 | Planned | `npm run test` output |
| R-012 | `"type": "module"` set if ESM imports are used | Phase 1 | Planned | `package.json` inspection |
| R-013 | Plain JS static-site compatibility maintained | Phase 1/4/5 | Planned | build/run/manual verification |