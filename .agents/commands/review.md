---
description: Review implementation changes before commit
argument-hint: [optional-plan-file]
---

# Review Changes

## Mission

Review the current implementation like a senior engineer before it is committed.

The goal is to verify that the changes are correct, safe, maintainable, consistent with the project architecture, and ready for commit.

**Core Principle:**

Do not rewrite the feature during review.

Review first. Identify issues. Only apply fixes if explicitly asked.

---

## Inputs

Optional plan file:

```txt
$ARGUMENTS
```

If a plan file is provided, use it as the source of truth for what was supposed to be implemented.

---

## Preconditions

Before reviewing:

- The implementation should already be completed.
- The working tree should contain the changes to review.
- If a plan exists, read it first.
- Read `AGENT.md` before judging conventions.

---

## Phase 1: Load Review Context

Read:

- `AGENT.md`
- Relevant `.agents/reference/*` docs
- Relevant `.agents/memory/*` decisions
- Provided plan file, if any

Then inspect changes:

```bash
git status --short
git diff HEAD
git diff --stat HEAD
```

---

## Phase 2: Compare Against Plan

If a plan file is provided, verify:

- All planned tasks were completed
- No planned task was skipped
- No unrelated scope was added
- Acceptance criteria were met
- Validation commands from the plan were run or are ready to run

If no plan exists, infer the purpose of the changes from the diff.

---

## Phase 3: Code Quality Review

Check for:

- Simple, readable implementation
- Consistent naming
- Existing patterns reused
- No duplicated business logic
- No unnecessary abstractions
- No dead code
- No temporary/debug code
- No large unrelated refactors
- No hidden behavior changes

---

## Phase 4: Architecture Review

Check for:

- Correct layer boundaries
- Controllers/routes remain thin
- Business logic stays in services/use-cases
- Data access stays in repositories/models
- Shared utilities are reused
- New files are placed in correct directories
- No circular dependencies
- No architecture drift

---

## Phase 5: Security Review

Check for:

- Authentication required where needed
- Authorization/ownership checks enforced
- Input validation present
- Sensitive data not logged
- Secrets not committed
- Errors do not leak private internals
- Rate limiting considered where relevant
- Payment, wallet, or admin actions are protected

---

## Phase 6: Data & Reliability Review

Check for:

- Database migrations are safe
- Transactions are used where needed
- Idempotency is handled for webhooks/retries
- Race conditions are considered
- Rollback impact is understood
- External API failures are handled
- Error states are explicit

---

## Phase 7: Testing Review

Check for:

- Unit tests for business logic
- Integration/API tests for workflows
- Edge cases covered
- Negative cases covered
- Existing tests not weakened
- Test names are clear
- Tests follow project conventions

Suggested validation commands should be derived from the project:

```bash
npm test
npm run lint
npm run typecheck
npm run build
```

or the equivalent stack-specific commands.

---

## Phase 8: Documentation Review

Check whether documentation needs updates:

- `README.md`
- `PRD.md`
- `AGENT.md`
- `.agents/reference/*`
- `.agents/memory/*`
- API docs
- Environment variable examples

---

## Phase 9: Risk Classification

Classify the change:

```txt
Low Risk
Medium Risk
High Risk
```

Consider:

- Payment/money movement
- Authentication/security
- Database migrations
- Production deployment impact
- Backward compatibility
- User-facing behavior changes

---

## Output Report

Provide:

### Review Verdict

Choose one:

```txt
Approved
Approved With Minor Notes
Changes Requested
Blocked
```

### Summary

Briefly explain what changed and whether it matches the intended work.

### Issues Found

Group issues by severity:

#### Critical

Must fix before commit.

#### Major

Should fix before commit.

#### Minor

Can fix now or later.

#### Suggestions

Optional improvements.

### Validation

List validation commands that were run or should be run.

### Risk Level

State risk level and why.

### Files Reviewed

List key files reviewed.

### Ready For Commit

Say clearly:

```txt
Ready for commit: Yes/No
```

---

## Quality Criteria

- Review is based on actual diff, not assumptions
- Plan compliance checked when plan exists
- Security and data risks considered
- Tests and validation considered
- Unrelated changes are flagged
- Final verdict is explicit