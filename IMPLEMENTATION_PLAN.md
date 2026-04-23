# Overview

This implementation plan is for **PXL Sweeper** (repository: `pxl-sweeper-VitoriaVanbrabantPXL`), a Minesweeper-style project.  
The plan is intentionally phase-driven, dependency-ordered, and review-gated to prevent scope creep and to keep each review cycle small and verifiable.

Because key context fields were not fully provided (`PROJECT_TYPE`, `GOAL`, `CONSTRAINTS`, `DEPLOYMENT_TARGET`, `RISK_TOLERANCE`, and available design docs), this plan uses minimal assumptions and flags blockers in **Open questions**.

# Assumptions

- The product goal is to deliver a stable, playable Minesweeper experience with maintainable code and tests.
- Review cadence is **small PRs per phase** (one primary deliverable per review cycle).
- Risk tolerance is treated as **medium** until confirmed.
- Deployment target is treated as **local-first** unless explicitly changed.
- Existing repository likely contains source code under `src/` and tests under `tests/` or equivalent.
- Commands are currently unknown; placeholders are used and must be replaced with project-specific commands before Phase 2 starts.
- TODO.md, DONE.md, and GEMINI.md are part of project workflow and must be updated during execution.

# Delivery strategy

The plan uses a **hybrid strategy**:  
- **Vertical slices** for user-visible gameplay outcomes (engine behavior + UI integration that can be reviewed end-to-end).  
- **Layered implementation** for quality infrastructure (CI/lint/test/build gates) to isolate delivery risk.

Why this fits:
- Minesweeper-like projects benefit from early playable slices for fast correctness feedback.
- Infrastructure and release checks are isolated so regressions and pipeline risks are reviewable on their own.
- This matches a short review cadence where each phase must end in a demonstrable, testable state.

# Phase list

- **Phase 1 — Scope, requirements traceability, and build/test command baseline locked**
- **Phase 2 — Core game engine behavior implemented and unit-tested**
- **Phase 3 — Playable UI loop integrated with the engine**
- **Phase 4 — Quality gates and packaging/deployment path validated**
- **Phase 5 — Stabilization, regression sweep, and documentation closure**

# Detailed phases

## Phase 1 — Scope, requirements traceability, and build/test command baseline locked

### Goal
Establish an unambiguous execution baseline (scope, commands, constraints, traceability) before implementation begins.

### Scope
- Confirm and record project goal, constraints, risk tolerance, and deployment target.
- Map requirements/design artifacts to planned implementation scope.
- Define exact build/test/lint/typecheck commands used in subsequent phases.
- Prepare TODO.md/DONE.md structure for phase-based execution.
- Update project context docs (including GEMINI.md) with resolved assumptions.

### Expected files to change
- IMPLEMENTATION_PLAN.md
- GEMINI.md
- TODO.md
- DONE.md (structure only, no completed execution items yet)
- README.md (if command/run instructions are missing)
- `/docs/REQUIREMENTS.md` (if traceability links are added)
- `/docs/DESIGN.md` or `/docs/ARCHITECTURE.md` (if references are normalized)

### Dependencies
- Upstream: access to current repo and any existing requirement/design documents.
- Intra-project: none (this is the first phase).
- Blockers: unresolved product goal, missing command set, unknown deployment target.

### Risks
- **Low to medium**: planning risk only.  
  Failure modes: inaccurate assumptions leading to rework in later phases.

### Tests and checks to run
- `[project install command]`
- `[project lint command]` (if available)
- `[project test command]` (baseline run; may fail but must be documented)
- `[project build command]` (baseline run; may fail but must be documented)

### Review check before moving work to DONE.md
- Confirm phase output matches stated goal/scope exactly.
- Confirm requirement traceability table exists (requirements → planned phases).
- Confirm command list is explicit and executable (or clearly marked blocker).
- Confirm documentation updates are complete (GEMINI.md, README.md as needed).
- Confirm no implementation work was mixed into this phase.
- Confirm any unresolved items are written as explicit TODO.md blockers.

### Exact TODO.md entries to refresh from this phase
- [ ] **Phase 1:** Record confirmed project goal, constraints, risk tolerance, and deployment target in GEMINI.md.
- [ ] **Phase 1:** Add requirement-to-phase traceability section referencing available requirement/design docs.
- [ ] **Phase 1:** Document exact lint/test/build/typecheck commands in README.md or GEMINI.md.
- [ ] **Phase 1:** Add phase-ordered execution checklist in TODO.md.
- [ ] **Phase 1:** Add DONE.md completion policy note (binary evidence required).

### Exit criteria for moving items to DONE.md
- Project context fields are explicitly recorded in repository docs.
- Every in-scope requirement maps to a phase or is marked out-of-scope.
- Command list exists and is runnable or marked as a blocker with owner/action.
- TODO.md has atomic phase tasks; DONE.md policy is documented.
- Review sign-off confirms planning-only changes and no hidden implementation.

---

## Phase 2 — Core game engine behavior implemented and unit-tested

### Goal
Deliver deterministic, test-covered game logic independent of UI.

### Scope
- Implement/complete board generation and mine placement rules.
- Implement reveal behavior (single reveal + propagation if applicable).
- Implement flag/unflag behavior if in requirements.
- Implement win/loss state transitions.
- Ensure engine interfaces are stable for UI integration.
- Add/adjust unit tests for all core rules and edge cases.

### Expected files to change
- `/src/**/game*.*`
- `/src/**/board*.*`
- `/src/**/engine*.*`
- `/src/**/state*.*`
- `/tests/**/game*.test.*`
- `/tests/**/board*.test.*`
- `/tests/**/engine*.test.*`
- TODO.md
- DONE.md

### Dependencies
- Depends on **Phase 1** completion (commands and scope lock).
- Upstream: clarified gameplay rules from requirements.
- Blockers: unresolved rule ambiguities (first-click safety, adjacency behavior, tie/win definition).

### Risks
- **Medium**: correctness regressions in core logic.  
  Failure modes: invalid board generation, incorrect reveal propagation, false win/loss conditions.

### Tests and checks to run
- `[project lint command]`
- `[project typecheck command]` (if applicable)
- `[project test command]` (unit suite, including new engine tests)
- `[project build command]`

### Review check before moving work to DONE.md
- Confirm engine behavior matches requirement traceability entries.
- Confirm unit tests cover normal and edge cases for each implemented rule.
- Confirm no UI-specific assumptions leaked into domain logic.
- Confirm regression risk review is documented for state-transition changes.
- Confirm docs/comments updated for any engine contract changes.
- Confirm unfinished items are explicitly written back to TODO.md.
- Confirm scope did not expand beyond engine behavior.

### Exact TODO.md entries to refresh from this phase
- [ ] **Phase 2:** Implement deterministic board generation per agreed rules.
- [ ] **Phase 2:** Implement reveal logic including neighbor propagation rules.
- [ ] **Phase 2:** Implement flag toggle logic (if in scope).
- [ ] **Phase 2:** Implement win/loss state evaluation.
- [ ] **Phase 2:** Add unit tests for board generation, reveal, flagging, and win/loss transitions.
- [ ] **Phase 2:** Update engine contract docs/comments used by UI integration.

### Exit criteria for moving items to DONE.md
- Engine code exists in expected files and compiles/builds.
- Unit tests for each core rule pass in CI/local test run.
- Lint/typecheck/build pass for modified scope.
- Review confirms rule compliance against requirement mapping.
- Any deferred edge cases are captured as explicit TODO.md items.

---

## Phase 3 — Playable UI loop integrated with the engine

### Goal
Provide a reviewable, end-to-end playable game loop connected to the engine.

### Scope
- Bind UI board rendering to engine state.
- Handle player input events for reveal/flag actions.
- Render game status (in-progress, won, lost).
- Provide restart/new-game flow if required by existing requirements.
- Add integration or UI tests for core playable path.

### Expected files to change
- `/src/**/ui*.*`
- `/src/**/components/**` (or equivalent)
- `/src/**/views/**` (or equivalent)
- `/src/**/app*.*`
- `/src/**/styles/**` (only if needed for interaction clarity)
- `/tests/**/integration*.test.*`
- `/tests/**/ui*.test.*`
- TODO.md
- DONE.md
- README.md (run/play instructions if missing)

### Dependencies
- Depends on **Phase 2** (stable engine interfaces).
- Upstream: UI framework/runtime already configured.
- Blockers: unresolved UX decisions that impact interaction model.

### Risks
- **Medium**: integration mismatch between UI and engine contracts.  
  Failure modes: stale state rendering, wrong input mapping, desync on game reset.

### Tests and checks to run
- `[project lint command]`
- `[project typecheck command]` (if applicable)
- `[project test command]` (includes integration/UI tests)
- `[project build command]`
- Manual smoke test: start game → reveal cells → flag cells → trigger win/loss → restart.

### Review check before moving work to DONE.md
- Confirm playable loop works end-to-end in manual verification.
- Confirm UI behavior maps to engine rules without custom duplicate logic.
- Confirm integration tests cover critical path and loss/win transitions.
- Confirm requirement traceability for user-visible behavior is updated.
- Confirm docs updated for local run/test instructions.
- Confirm unfinished UX or accessibility follow-ups are written to TODO.md.
- Confirm no unrelated features were added.

### Exact TODO.md entries to refresh from this phase
- [ ] **Phase 3:** Connect board rendering to engine state model.
- [ ] **Phase 3:** Implement reveal interaction wiring.
- [ ] **Phase 3:** Implement flag interaction wiring (if in scope).
- [ ] **Phase 3:** Render and update game status (in progress / won / lost).
- [ ] **Phase 3:** Implement restart/new-game flow (if required).
- [ ] **Phase 3:** Add integration/UI tests for core playable scenarios.
- [ ] **Phase 3:** Update usage instructions for running the playable app.

### Exit criteria for moving items to DONE.md
- Playable path is demonstrable and repeatable by reviewer.
- Integration/UI tests for core paths pass.
- Build succeeds and app launches locally.
- Review confirms UI uses engine contracts correctly.
- Documentation reflects actual run/test flow.

---

## Phase 4 — Quality gates and packaging/deployment path validated

### Goal
Ensure reproducible quality checks and verify release path for the confirmed deployment target.

### Scope
- Standardize lint/test/typecheck/build commands in automation.
- Add/update CI workflow for required checks.
- Validate packaging/release process for deployment target (local or hosting target).
- Add smoke verification checklist for release artifacts.

### Expected files to change
- `/.github/workflows/*.yml` (or CI equivalent)
- `/package.json` or `/pyproject.toml` or `/Cargo.toml` (scripts/tasks as applicable)
- `/Makefile` or `/scripts/*.sh` (if command wrapper is used)
- README.md (CI + build/release verification steps)
- `/docs/DEPLOYMENT.md` (if deployment is in scope)
- TODO.md
- DONE.md

### Dependencies
- Depends on **Phase 3** for stable app behavior.
- Upstream: CI provider availability and repository permissions.
- Blockers: unresolved deployment target (local only vs hosted).

### Risks
- **Medium**: pipeline or release failure close to completion.  
  Failure modes: flaky tests, missing environment config, non-reproducible build.

### Tests and checks to run
- `[project lint command]`
- `[project typecheck command]`
- `[project test command]`
- `[project build command]`
- CI run of full pipeline on clean environment
- Deployment/package smoke check:
  - Local artifact/run verification, or
  - Hosted deploy verification (if target is not local-only)

### Review check before moving work to DONE.md
- Confirm CI executes all required gates and fails on violations.
- Confirm build artifacts are reproducible from clean checkout.
- Confirm deployment/package procedure is documented and tested.
- Confirm regression risk from pipeline/tooling changes is reviewed.
- Confirm no product-scope feature work was mixed into infra phase.
- Confirm unresolved infra tasks are added to TODO.md.

### Exact TODO.md entries to refresh from this phase
- [ ] **Phase 4:** Add/update CI workflow to run lint, typecheck, tests, and build.
- [ ] **Phase 4:** Ensure local command scripts match CI commands exactly.
- [ ] **Phase 4:** Document packaging/deployment steps for confirmed target.
- [ ] **Phase 4:** Execute clean-environment pipeline run and record result.
- [ ] **Phase 4:** Add release smoke checklist to docs.

### Exit criteria for moving items to DONE.md
- CI config exists and passes required gates.
- Commands documented in repo are the same commands used in CI.
- Build artifact or deployment verification completed with evidence.
- Reviewer confirms infra phase contained no hidden feature work.
- Any flaky/unstable checks are tracked as explicit follow-up items.

---

## Phase 5 — Stabilization, regression sweep, and documentation closure

### Goal
Close remaining defects, finalize documentation, and perform formal review before completion.

### Scope
- Fix only validated defects and integration regressions.
- Run full regression and manual smoke checks.
- Finalize requirement traceability status (implemented/deferred/out-of-scope).
- Ensure TODO.md and DONE.md are fully synchronized with evidence links.
- Produce final readiness summary.

### Expected files to change
- `/src/**` (bug fixes only)
- `/tests/**` (regression tests)
- README.md
- `/docs/**` (traceability, release notes, deployment notes if applicable)
- TODO.md
- DONE.md
- GEMINI.md (final context alignment)

### Dependencies
- Depends on **Phase 4** completion.
- Upstream: all critical open questions resolved or explicitly deferred with approval.

### Risks
- **Low to medium**: late regression discovery.  
  Failure modes: hidden edge cases, incomplete documentation, unresolved deferred work.

### Tests and checks to run
- `[project lint command]`
- `[project typecheck command]`
- `[project test command]` (full suite)
- `[project build command]`
- Full manual smoke checklist
- If deployment in scope: post-deploy verification checklist

### Review check before moving work to DONE.md
- Confirm all phase goals are met and traceability is complete.
- Confirm regression risk review completed and no critical unresolved defects remain.
- Confirm docs are current and sufficient for handoff.
- Confirm scope creep review: no unapproved features introduced.
- Confirm every unfinished item is in TODO.md with clear owner/next step.
- Confirm final reviewer approval for project completion.

### Exact TODO.md entries to refresh from this phase
- [ ] **Phase 5:** Triage and fix remaining high-priority defects only.
- [ ] **Phase 5:** Add regression tests for each fixed defect.
- [ ] **Phase 5:** Run full lint/typecheck/test/build suite and record outputs.
- [ ] **Phase 5:** Execute manual smoke checklist and record outcomes.
- [ ] **Phase 5:** Finalize requirement traceability matrix (implemented/deferred/out-of-scope).
- [ ] **Phase 5:** Reconcile TODO.md and DONE.md with evidence links.
- [ ] **Phase 5:** Publish final readiness summary.

### Exit criteria for moving items to DONE.md
- All critical/high defects in scope are resolved or explicitly accepted/deferred.
- Regression tests exist for fixed defects and pass.
- Full quality gate suite passes.
- Documentation and traceability are complete and reviewed.
- Final review sign-off confirms completion criteria met.

# Dependency notes

- Strict sequence: **Phase 1 → Phase 2 → Phase 3 → Phase 4 → Phase 5**.
- No phase may begin without previous phase review gate approval.
- Phase 2 is blocked by unresolved gameplay-rule ambiguities.
- Phase 4 is blocked by unresolved deployment target decision.
- Parallel work is allowed only for independent documentation updates that do not alter implementation scope.

# Review policy

- Expected review size: one phase per review cycle, with one primary outcome and atomic TODO items.
- A phase must be split **before implementation starts** if any of the following apply:
  - It contains more than one major deliverable.
  - It cannot be reviewed in a single cycle.
  - It mixes risky infra/refactor work with feature delivery.
- Oversized phases are not allowed to proceed unchanged.
- Every phase requires explicit reviewer confirmation against:
  - goal/scope match
  - requirement traceability
  - regression risk
  - documentation completeness
  - TODO/DONE synchronization

# Definition of done for the plan

The project is complete when all of the following are true:

- All planned phases are completed in order and approved through review gates.
- In-scope requirements are implemented and traceable to code/tests.
- Required quality checks (lint/typecheck/test/build) pass consistently.
- Core gameplay is demonstrably playable end-to-end.
- CI/automation and packaging/deployment path (as applicable to target) are verified.
- Documentation is current (`README`, context docs, traceability notes, deployment/run instructions).
- TODO.md contains only approved deferred work; completed items are moved to DONE.md with evidence.
- Final stabilization review confirms no critical unresolved defects.

# Open questions

## Blocking unknowns

- What is the confirmed **project type** (web app, desktop app, CLI, other)?
- What is the exact **delivery goal** and in-scope feature set from product/assignment requirements?
- What is the confirmed **deployment target** (local-only vs hosted/platform)?
- What is the official **risk tolerance** and required review cadence?
- Which existing docs are authoritative (REQUIREMENTS.md, `DESIGN.md`, `ARCHITECTURE.md`, other)?
- What are the exact project commands for:
  - install
  - lint
  - typecheck
  - test
  - build
  - run

## Non-blocking unknowns

- Are accessibility checks required as release gates?
- Is performance benchmarking required (e.g., large board sizes)?
- Are telemetry/logging requirements expected for this project?