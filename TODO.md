# TODO

## Phase 1 — Scope, requirements traceability, and build/test command baseline locked
- [ ] **Phase 1:** Record confirmed project goal, constraints, risk tolerance, and deployment target in GEMINI.md.
- [ ] **Phase 1:** Add requirement-to-phase traceability section referencing available requirement/design docs.
- [ ] **Phase 1:** Document exact lint/test/build/typecheck commands in README.md or GEMINI.md.
- [ ] **Phase 1:** Add phase-ordered execution checklist in TODO.md.
- [ ] **Phase 1:** Add DONE.md completion policy note (binary evidence required).

## Phase 2 — Core game engine behavior implemented and unit-tested
- [ ] **Phase 2:** Implement deterministic board generation per agreed rules.
- [ ] **Phase 2:** Implement reveal logic including neighbor propagation rules.
- [ ] **Phase 2:** Implement flag toggle logic (if in scope).
- [ ] **Phase 2:** Implement win/loss state evaluation.
- [ ] **Phase 2:** Add unit tests for board generation, reveal, flagging, and win/loss transitions.
- [ ] **Phase 2:** Update engine contract docs/comments used by UI integration.

## Phase 3 — Playable UI loop integrated with the engine
- [ ] **Phase 3:** Connect board rendering to engine state model.
- [ ] **Phase 3:** Implement reveal interaction wiring.
- [ ] **Phase 3:** Implement flag interaction wiring (if in scope).
- [ ] **Phase 3:** Render and update game status (in progress / won / lost).
- [ ] **Phase 3:** Implement restart/new-game flow (if required).
- [ ] **Phase 3:** Add integration/UI tests for core playable scenarios.
- [ ] **Phase 3:** Update usage instructions for running the playable app.

## Phase 4 — Quality gates and packaging/deployment path validated
- [ ] **Phase 4:** Add/update CI workflow to run lint, typecheck, tests, and build.
- [ ] **Phase 4:** Ensure local command scripts match CI commands exactly.
- [ ] **Phase 4:** Document packaging/deployment steps for confirmed target.
- [ ] **Phase 4:** Execute clean-environment pipeline run and record result.
- [ ] **Phase 4:** Add release smoke checklist to docs.

## Phase 5 — Stabilization, regression sweep, and documentation closure
- [ ] **Phase 5:** Triage and fix remaining high-priority defects only.
- [ ] **Phase 5:** Add regression tests for each fixed defect.
- [ ] **Phase 5:** Run full lint/typecheck/test/build suite and record outputs.
- [ ] **Phase 5:** Execute manual smoke checklist and record outcomes.
- [ ] **Phase 5:** Finalize requirement traceability matrix (implemented/deferred/out-of-scope).
- [ ] **Phase 5:** Reconcile TODO.md and DONE.md with evidence links.
- [ ] **Phase 5:** Publish final readiness summary.