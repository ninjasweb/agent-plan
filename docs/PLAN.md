# Plan Template — SDD + TDD

This file is the mandatory reference for creating work plans. It combines **Spec-Driven Development (SDD)** to decide what the system should do with **Test-Driven Development (TDD)** to prove it during implementation.

## How to use this template

1. Do not turn `PLAN.md` into a concrete plan or overwrite it.
2. Create a sibling file named `PLAN-<topic>.md`, with a short, descriptive kebab-case slug; for example, `PLAN-payment-idempotency.md`.
3. If an active plan for the same goal already exists, update it instead of duplicating it.
4. Keep the active plan in `docs/`. Once finished, move it to the corresponding topic subfolder.
5. Remove these instructions and any section that doesn't apply from the created plan.

## Relationship between SDD and TDD

The specification is the source of truth. Every test must be derived from an acceptance criterion, and every production change must be justified by a test or an explicit verification.

```text
Story → validated assumptions → requirements → acceptance criteria
        → tests → RED → GREEN → REFACTOR → evidence
```

Don't duplicate business rules between the specification and the testing section: use IDs and traceability.

## Process gates

- **Gate 1 — SPEC READY:** scope, assumptions, requirements, and acceptance criteria are validated.
- **Gate 2 — TEST READY:** every criterion is mapped to a test or a justifiable verification.
- **Gate 3 — SLICE DONE:** the slice completed RED → GREEN → REFACTOR and passed its checks.
- **Gate 4 — PLAN DONE:** every criterion has evidence and no known regressions remain.

---

# PLAN: [Concrete title]

> Created from `docs/PLAN.md`. The specification defines the behavior; the tests prove it.

## 0. Document control

| Field             | Value                                                                     |
| ----------------- | ------------------------------------------------------------------------- |
| File              | `docs/PLAN-[topic].md`                                                    |
| Status            | Draft / In refinement / Approved / In progress / Blocked / Completed      |
| Author / owner    | [Name or team]                                                            |
| Created           | YYYY-MM-DD                                                                |
| Updated           | YYYY-MM-DD                                                                |
| Branch / issue / PR | [Links or N/A]                                                          |

## 1. Context and problem

### Current situation

[Describe the current behavior with verifiable evidence: code, logs, metrics, screenshots, or reproduction steps.]

### Problem

[Explain who is affected, what fails or is missing, and what the impact is.]

### Expected outcome

[Describe the observable change that will indicate the problem is solved.]

## 2. User story

> As a **[actor]**, I want **[action/capability]**, so that **[measurable benefit]**.

### Related stories

- US-001: As [actor], I want [action], so that [benefit].

## 3. Goals and boundaries

### Goals

- O-001: [Concrete, verifiable outcome.]

### In scope

- [Included behavior.]

### Out of scope

- [Explicitly excluded behavior.]

## 4. Functional assumptions and decisions

Before closing the specification, list the atomic functional assumptions and refine them with the user. Don't hide product decisions inside the technical strategy.

| ID    | Assumption or decision           | Status                          | Evidence / decision |
| ----- | --------------------------------- | -------------------------------- | -------------------- |
| A-001 | [A single functional assumption.] | Pending / Validated / Rejected   | [Source or answer]   |

### Open questions

- Q-001: [Question that blocks a material decision.]

**Gate 1 cannot be approved while a material question remains open.**

## 5. SDD specification

### Actors and permissions

| Actor   | Can                   | Cannot          |
| ------- | --------------------- | --------------- |
| [Actor] | [Allowed actions]     | [Restrictions]  |

### Functional requirements

Every requirement must be atomic, mandatory, and observable.

| ID     | Requirement                                  | Priority               | Origin |
| ------ | --------------------------------------------- | ---------------------- | ------ |
| FR-001 | The system must [verifiable behavior].        | Must / Should / Could  | US-001 |

### Acceptance criteria

#### AC-001 — [Scenario name]

- **Given** [initial state]
- **When** [action or event]
- **Then** [observable outcome]
- **And** [additional outcome, if applicable]

#### AC-002 — [Error or edge case]

- **Given** [initial state]
- **When** [invalid action, failure, or concurrency]
- **Then** [safe, observable response]

### Non-functional requirements

Use measurable thresholds; omit categories that don't apply.

| ID      | Category                                                | Requirement / threshold | How it's verified      |
| ------- | -------------------------------------------------------- | ------------------------ | ----------------------- |
| NFR-001 | Performance / Security / Accessibility / Reliability     | [Concrete metric]         | [Tool or test]          |

### UX and visible states

- Entry point or trigger: [Where the flow begins.]
- Loading/progress: [What the user sees.]
- Success: [Feedback and next state.]
- Empty: [Behavior with no data.]
- Recoverable error: [Message and available action.]
- Fatal error: [Message, data preservation, and support.]
- Accessibility/localization: [Applicable requirements.]

### Data, contracts, and side effects

| Element                              | Current state      | Required change      | Compatibility / migration |
| ------------------------------------- | -------------------- | ---------------------- | -------------------------- |
| [Model, endpoint, event, or storage]  | [Current contract]   | [Target contract]      | [Strategy]                  |

### Edge cases and errors

| ID       | Case                                              | Expected behavior   | Related criterion |
| -------- | --------------------------------------------------- | --------------------- | -------------------- |
| EDGE-001 | [Duplicate, timeout, empty input, race, etc.]      | [Safe outcome]        | AC-002               |

## 6. Technical strategy

Define this section after stabilizing the functional behavior.

### Relevant current architecture

[Summary of the confirmed flow in the code; include real paths and symbols.]

### Proposed design

[Components, boundaries, data flow, and minimal technical decisions.]

### Planned files

| File / module | Action                     | Responsibility of the change |
| -------------- | --------------------------- | ------------------------------ |
| `[path]`       | Create / Modify / Delete    | [Purpose]                       |

### Dependencies and constraints

- [Internal/external dependency, compatibility, migration, or operational limitation.]

## 7. Traceability matrix

There must be no orphan requirements and no tests without specified behavior.

| Story / goal    | Requirement | Criterion | Test / verification | Slice |
| ---------------- | ----------- | --------- | -------------------- | ----- |
| US-001 / O-001   | FR-001      | AC-001    | TEST-001             | S1    |

## 8. TDD strategy

### Baseline and characterization

- Relevant existing tests: [paths and status].
- Baseline command: `[command]`.
- Baseline result: [evidence].
- If the existing behavior isn't covered, first create characterization tests before refactoring it.
- For a bug, reproduce it first with a failing regression test for the right reason.

### Test inventory

| ID       | Criterion | Level                                | Scenario           | Planned file | Status                    |
| -------- | --------- | ------------------------------------- | -------------------- | -------------- | -------------------------- |
| TEST-001 | AC-001    | Unit / Integration / Component / E2E  | [Behavior]           | `[path]`       | Pending / RED / GREEN      |

### TDD rules

- Run one **RED → GREEN → REFACTOR** cycle per small slice.
- Confirm RED fails due to missing behavior, not broken configuration.
- Write the minimal implementation that gets to GREEN; don't anticipate future requirements.
- Refactor only with the suite green, and re-run it afterward.
- Test observable behavior, not private implementation details.
- Use integration at critical boundaries; mock only external boundaries when necessary.
- Don't skip, weaken, or delete a test to reach GREEN without documenting a specification correction.
- If TDD doesn't apply — documentation, declarative configuration, non-reversible migration, or spike — record the reason and an equivalent verification before implementing.

## 9. Implementation slices

Repeat this structure for each vertical slice. A slice must deliver verifiable behavior, not just a technical layer.

### S1 — [Small, observable outcome]

- Requirements: FR-001
- Criteria: AC-001
- Tests: TEST-001
- Dependencies: [None or prior IDs]

#### RED

- [ ] Create or modify `[test file]`.
- [ ] Run `[focused command]`.
- [ ] Record the expected failure: [message or condition].

#### GREEN

- [ ] Implement the minimal change in `[file(s)]`.
- [ ] Run `[focused command]` until it passes.
- [ ] Run related tests to rule out immediate regressions.

#### REFACTOR

- [ ] Remove duplication and improve names/boundaries without changing behavior.
- [ ] Re-run focused tests and the relevant suite.
- [ ] Update traceability, decisions, and affected documentation.

#### Slice gate

- [ ] RED was observed and recorded.
- [ ] GREEN passes reproducibly.
- [ ] The refactor preserves GREEN.
- [ ] No type, lint, or formatting errors remain in scope.

### S2 — [Next outcome]

[Repeat RED → GREEN → REFACTOR.]

## 10. End-to-end validation

### Commands

```bash
# Focused test
[command]

# Related suite
[command]

# Types / lint / build, depending on risk
[command]
```

### Manual verification

| Scenario                                | Steps                  | Expected result    | Evidence      |
| ----------------------------------------- | ------------------------ | --------------------- | --------------- |
| [Scenario not covered automatically]     | [Reproducible steps]    | [Result]              | [Screenshot/log] |

## 11. Rollout, observability, and rollback

- Deployment strategy: [direct, gradual, feature flag, migration].
- Metrics/logs/alerts: [concrete signals and thresholds].
- Compatibility: [affected versions or clients].
- Rollback: [safe steps and trigger condition].
- Data: [reversibility, backup, and reconciliation].

## 12. Risks

| Risk     | Probability          | Impact               | Mitigation | Early signal     |
| -------- | --------------------- | --------------------- | ---------- | ------------------ |
| [Risk]   | Low / Medium / High   | Low / Medium / High   | [Action]   | [Metric/error]     |

## 13. Decision and progress log

### Decisions

| Date       | ID    | Decision   | Reason      | Consequence |
| ---------- | ----- | ---------- | ------------ | ------------- |
| YYYY-MM-DD | D-001 | [Decision] | [Evidence]   | [Trade-off]   |

### Progress

| Date       | Slice | Status                          | Evidence             | Next step |
| ---------- | ----- | --------------------------------- | ----------------------- | ----------- |
| YYYY-MM-DD | S1    | RED / GREEN / REFACTOR / Done     | [Command/result]        | [Action]    |

## 14. Definition of Done

- [ ] Gate 1 — SPEC READY approved.
- [ ] Gate 2 — TEST READY approved.
- [ ] All slices completed RED → GREEN → REFACTOR.
- [ ] All `FR-*` trace to `AC-*` and to `TEST-*` or to a justified verification.
- [ ] Happy path, errors, and critical edge cases are covered.
- [ ] Focused tests and the related suite pass.
- [ ] Applicable typecheck, lint, and build pass.
- [ ] No disabled tests or undocumented known regressions.
- [ ] Observability and rollback are ready according to risk.
- [ ] Documentation and `FLOWS.md` were updated where applicable.
- [ ] Final evidence is recorded in this plan.

## 15. Final outcome

- Status: [Completed / Partial / Blocked]
- Evidence: [tests, metrics, screenshots, or links]
- Deviations from the spec: [none or `D-*` decisions]
- Follow-up work: [none or explicit out-of-scope items]
