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