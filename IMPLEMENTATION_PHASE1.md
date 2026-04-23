<!-- filepath: /home/vitoria/pxl-sweeper-VitoriaVanbrabantPXL/IMPLEMENTATION_PHASE1.md -->
# IMPLEMENTATION_PHASE1.md
## Phase 1 Blueprint — Scope Lock, Traceability, and Command Baseline

## 0) Phase Intent

**Phase ID:** 1  
**Source of truth:** `IMPLEMENTATION_PLAN.md` (Phase 1), `REQUIREMENTS.md`, `GEMINI.md`  
**Execution mode:** Planning/documentation only (**no feature implementation**)  
**Exit gate:** Reviewer confirms scope lock + runnable command baseline + traceability + TODO/DONE policy alignment.

---

## 1) Architectural Design (for this phase)

Phase 1 is documentation infrastructure. The “architecture” is the project-control model that later phases depend on.

### 1.1 Control Objects (documentation data structures)

#### A) Project Context Record (in `GEMINI.md`)
Use a normalized key/value block:

| Field | Type | Required | Example |
|---|---|---:|---|
| `Project Type` | enum(string) | yes | `Browser SPA (static-site JS)` |
| `Goal` | string | yes | `Deliver playable Minesweeper loop with deterministic core logic` |
| `Constraints` | list[string] | yes | `Single-page app`, `No backend`, `Static workflow` |
| `Deployment Target` | enum(string) | yes | `Local-first static hosting` |
| `Risk Tolerance` | enum(string) | yes | `Medium` |
| `Authoritative Docs` | list[path] | yes | `REQUIREMENTS.md`, `IMPLEMENTATION_PLAN.md`, ... |
| `Open Questions` | list[string] | yes | unresolved rule decisions |

#### B) Requirement Traceability Matrix (in `REQUIREMENTS.md` or `docs/REQUIREMENTS.md`)
Table schema:

| Req ID | Requirement summary | Phase | Status | Verification artifact |
|---|---|---|---|---|
| `R-001` | ... | `Phase 2` | `Planned` | `tests/...` / doc reference |

Status enum: `Planned | Implemented | Deferred | Out-of-scope`.

#### C) Command Baseline Registry (README or GEMINI)
Canonical command map:

| Capability | Command | Expected now | Notes |
|---|---|---|---|
| install | `...` | Runs/fails? | reason |
| lint | `...` | Runs/fails? | reason |
| typecheck | `...` | Runs/fails? | optional |
| test | `...` | Runs/fails? | required by setup reqs |
| build | `...` | Runs/fails? | reason |
| run | `...` | Runs/fails? | reason |

#### D) Execution Tracker Model (`TODO.md` + `DONE.md`)
- `TODO.md`: phase-ordered unchecked tasks only.
- `DONE.md`: completed tasks only, each with evidence link/output note.
- Transition invariant: item moves to DONE **only after** checks + review.

---

### 1.2 State Definitions

For planning workflow:

```text
Draft -> Ready for review -> Approved -> Baseline locked
```

Per TODO item lifecycle:

```text
Not started -> In progress -> Validation complete -> Moved to DONE with evidence
```

Blocking state:
- `Blocked` if required context cannot be resolved (must include owner + next action).

---

### 1.3 Function Signatures (operational procedures)

These are process-level signatures to execute the phase consistently:

```text
collect_project_context() -> ContextRecord
build_traceability(requirements_doc, plan_doc) -> TraceabilityTable
discover_commands(package_json, scripts, docs) -> CommandRegistry
run_baseline_checks(command_registry) -> BaselineResults
refresh_todo_from_phase(plan_phase) -> TodoChecklist
define_done_policy() -> DonePolicyText
review_phase1_outputs(outputs) -> ApprovalDecision
```

Validation predicates:

```text
is_context_complete(context) -> boolean
is_traceability_complete(matrix) -> boolean
is_command_set_explicit(registry) -> boolean
is_planning_only(diff) -> boolean
```

---

## 2) File-Level Strategy (exact files to touch)

> Scope is intentionally minimal and documentation-first.

1. **`/home/vitoria/pxl-sweeper-VitoriaVanbrabantPXL/GEMINI.md`**  
   Responsibility: lock project context fields; record unresolved blockers explicitly.

2. **`/home/vitoria/pxl-sweeper-VitoriaVanbrabantPXL/TODO.md`**  
   Responsibility: add phase-ordered actionable checklist derived from Phase 1 exact items.

3. **`/home/vitoria/pxl-sweeper-VitoriaVanbrabantPXL/DONE.md`** *(create if absent)*  
   Responsibility: add completion policy text only (no completed tasks yet).

4. **`/home/vitoria/pxl-sweeper-VitoriaVanbrabantPXL/README.md`** *(if command section missing)*  
   Responsibility: canonical runnable command table and usage hints.

5. **`/home/vitoria/pxl-sweeper-VitoriaVanbrabantPXL/REQUIREMENTS.md`** *(or `docs/REQUIREMENTS.md` if used)*  
   Responsibility: add/append traceability section mapping requirements to phases.

6. **`/home/vitoria/pxl-sweeper-VitoriaVanbrabantPXL/IMPLEMENTATION_PLAN.md`** *(only if clarifications needed)*  
   Responsibility: resolve contradictory assumptions discovered during context lock.

> Do **not** touch `AGENTS.md`.

---

## 3) Atomic Execution Steps (Plan-Act-Validate per Phase 1 checkbox)

### Item 1 — Record confirmed project goal, constraints, risk tolerance, deployment target in GEMINI.md

**Plan**
- Extract mandatory context fields from `IMPLEMENTATION_PLAN.md` + `REQUIREMENTS.md`.
- Identify unknowns vs confirmed facts.
- Prepare explicit “assumed until confirmed” labels.

**Act**
- Update `GEMINI.md` with a dedicated “Phase 1 Baseline Context” section.
- Add fixed values and a compact open-questions list.

**Validate**
- Check all required fields exist and are non-empty.
- Ensure every assumption is tagged and not presented as fact.
- Reviewer can answer: “What are we building, under which constraints?”

---

### Item 2 — Add requirement-to-phase traceability section referencing available docs

**Plan**
- Enumerate requirement statements (from `REQUIREMENTS.md`, including setup requirements).
- Assign each to Phase 1..5 or out-of-scope with rationale.

**Act**
- Insert a traceability matrix section into requirements doc location.
- Add stable IDs (`R-001`, `R-002`, ...).

**Validate**
- No requirement line left unmapped.
- Each mapping has a verification artifact placeholder.
- Ambiguous requirements flagged in “Open Questions”.

---

### Item 3 — Document exact lint/test/build/typecheck commands in README.md or GEMINI.md

**Plan**
- Inspect `package.json` scripts and any wrappers (`Makefile`, scripts dir).
- Decide single canonical command per capability.

**Act**
- Add command baseline table.
- Record command output status (pass/fail/blocker) from baseline run.

**Validate**
- Commands are copy/paste runnable on Linux.
- `test` command exists (project setup requirement).
- If missing scripts, blocker is documented with next action.

---

### Item 4 — Add phase-ordered execution checklist in TODO.md

**Plan**
- Pull exact TODO entries from `IMPLEMENTATION_PLAN.md` for all phases.
- Keep each item atomic and review-sized.

**Act**
- Populate `TODO.md` with phase-grouped checkboxes.
- Mark none as done during this step.

**Validate**
- Order is strictly Phase 1 → 5.
- No hidden implementation tasks in Phase 1.
- Items are actionable and testable.

---

### Item 5 — Add DONE.md completion policy note (binary evidence required)

**Plan**
- Define acceptance gate for moving items from TODO to DONE.
- Decide required evidence format (command output snippet, test report, reviewer sign-off).

**Act**
- Create/update `DONE.md` with policy section only.
- Include explicit “no evidence, no move” rule.

**Validate**
- Policy is unambiguous and enforceable.
- DONE remains empty of completed implementation work in Phase 1.
- Matches `GEMINI.md` workflow rules.

---

## 4) Edge Case & Boundary Audit (Phase 1 specific)

1. **Empty/placeholder `REQUIREMENTS.md` sections**  
   Trap: false traceability completeness.  
   Mitigation: mark as unresolved requirement artifacts.

2. **Commands absent from `package.json`**  
   Trap: undocumented local tribal commands.  
   Mitigation: register blocker + owner + required script additions in later phase.

3. **Conflicting documents (plan vs requirements)**  
   Trap: dual truth sources.  
   Mitigation: explicitly declare authoritative precedence in GEMINI.

4. **TODO too coarse or too broad**  
   Trap: non-reviewable tasks.  
   Mitigation: split into atomic checkboxes with one measurable outcome each.

5. **Premature implementation leakage in Phase 1 PR**  
   Trap: hidden scope creep.  
   Mitigation: diff audit must show doc-only changes.

6. **Missing DONE policy**  
   Trap: unverifiable “done” claims.  
   Mitigation: enforce binary evidence gate before any item migration.

7. **Assumptions not labeled**  
   Trap: later rework due to implicit decisions.  
   Mitigation: add “Assumed until confirmed” tags for unresolved fields.

---

## 5) Verification Protocol (must pass before Phase 1 closes)

### 5.1 Manual UX/Process Checks
1. Open `GEMINI.md` and confirm context block contains all mandatory fields.
2. Open traceability matrix and verify every requirement has a phase mapping.
3. Open README/GEMINI command table and validate commands are explicit.
4. Open `TODO.md` and confirm phase-ordered, atomic checklist exists.
5. Open `DONE.md` and confirm policy exists with evidence requirements.
6. Run a quick diff scan: documentation-only changes in Phase 1.

### 5.2 Automated/Command Checks (baseline recording)
Run on Linux terminal from repo root:

```bash
npm run test
```

If available:

```bash
npm run lint
npm run build
npm run typecheck
```

If scripts are missing:
- Record as blocker in context docs.
- Do **not** fabricate command success.

### 5.3 Exit Checklist
- [ ] Context fields locked in `GEMINI.md`.
- [ ] Requirement-to-phase matrix exists and is complete.
- [ ] Canonical command set documented and baseline-run status captured.
- [ ] `TODO.md` phase checklist populated.
- [ ] `DONE.md` policy added; no implementation items moved.
- [ ] Reviewer signs off “planning-only phase complete”.

---

## 6) Code Scaffolding / Structural Templates

> Phase 1 adds templates (documentation scaffolding), not runtime code.

### 6.1 GEMINI Context Template

```markdown
## Phase 1 Baseline Context
- Project Type:
- Goal:
- Constraints:
- Deployment Target:
- Risk Tolerance:
- Authoritative Files:
- Assumed until confirmed:
  - ...
- Open Questions:
  - ...
```

### 6.2 Traceability Matrix Template

```markdown
## Requirement Traceability Matrix
| Req ID | Requirement | Phase | Status | Verification Artifact |
|---|---|---|---|---|
| R-001 | ... | Phase 2 | Planned | tests/... |
```

### 6.3 Command Baseline Template

```markdown
## Command Baseline
| Capability | Command | Baseline Result | Notes |
|---|---|---|---|
| test | npm run test | pass/fail/block | ... |
```

### 6.4 DONE Policy Template

```markdown
## Completion Policy
An item can move from TODO.md to DONE.md only when:
1) required checks were run,
2) evidence is attached (output/log/link),
3) docs were updated if scope changed,
4) reviewer approved.
```

---

## 7) Non-Goals for This Phase

- No gameplay engine changes.
- No UI integration work.
- No refactors unrelated to documentation baseline.
- No CI pipeline expansion beyond documenting current command state.

---

## 8) Approval Request

This blueprint is ready for review.  
Implementation starts only after explicit approval of this Phase 1 execution guide.