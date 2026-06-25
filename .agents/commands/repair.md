---
description: Repair an incomplete or incorrect implementation
argument-hint: [plan-file]
---

# Repair Implementation

## Mission

Fix an implementation that does not correctly satisfy its plan, acceptance criteria, tests, or project conventions.

The goal is to repair the current implementation with the smallest safe change, not rewrite the feature from scratch.

---

## Core Principle

Do not create a new architecture.

Do not expand scope.

Do not rewrite working code unnecessarily.

Repair only what is broken, incomplete, unsafe, or inconsistent with the plan.

---

## Inputs

Plan file:

```txt
$ARGUMENTS
```

If no plan file is provided, infer the intended behavior from:

- `AGENT.md`
- `.agents/reference/`
- `.agents/memory/`
- Existing tests
- User feedback
- Current diff

---

## Preconditions

Before repairing:

- Read `AGENT.md`.
- Read the provided plan file if available.
- Read relevant `.agents/reference/` documents.
- Read relevant `.agents/skills/` files.
- Inspect the current implementation.
- Inspect the current failing behavior, review notes, or failed validation output.

---

## Phase 1: Diagnose

Run or inspect:

```bash
git status --short
git diff HEAD
```

If validation failed, inspect the failing command output.

Identify:

- What was expected
- What was implemented
- What is missing
- What is incorrect
- What is unsafe
- What tests fail
- What files are involved

Do not edit files yet.

---

## Phase 2: Compare Against Plan

If a plan file exists, compare implementation against:

- Feature description
- Step-by-step tasks
- Acceptance criteria
- Testing strategy
- Validation commands
- Out-of-scope items

Classify each issue:

```txt
Missing
Incorrect
Unsafe
Unclear
Out of Scope
Regression
```

---

## Phase 3: Create Repair Plan

Before editing, produce a small repair plan:

```txt
Repair Task 1
Repair Task 2
Repair Task 3
```

Each task should include:

- File to modify
- What to change
- Why it is needed
- Validation command

Keep the repair plan minimal.

---

## Phase 4: Apply Fixes

Apply fixes in order.

Rules:

- Preserve existing working code.
- Follow project conventions.
- Reuse existing utilities.
- Do not introduce unrelated refactors.
- Do not silently change public behavior.
- Do not remove tests to make validation pass.
- Add or update tests when behavior was missing.

---

## Phase 5: Validate

Run relevant validation commands.

Examples:

```bash
npm run lint
npm run typecheck
npm test
npm run build
```

Also run feature-specific tests from the plan.

If validation fails:

- Diagnose again.
- Fix the root cause.
- Re-run validation.

Do not claim success while validation is failing.

---

## Phase 6: Report

Provide:

### Repair Summary

Explain what was wrong and what was fixed.

### Files Modified

List changed files.

### Tests Added or Updated

List test changes.

### Validation Results

Show commands run and their result.

### Remaining Risks

List anything still uncertain.

### Ready for Review

Say clearly:

```txt
Ready for review: Yes/No
```

---

## Quality Criteria

- Fix addresses the root cause.
- No unrelated changes included.
- Existing architecture preserved.
- Tests cover repaired behavior.
- Validation passes.
- Implementation now matches the plan.
- Ready to run `review.md` again.