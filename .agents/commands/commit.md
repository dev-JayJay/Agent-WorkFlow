---
description: Create a clean, atomic Git commit
---

# Commit Changes

## Mission

Create a clean, atomic Git commit that accurately represents a single logical unit of work.

The commit should be production-quality and follow the project's commit conventions.

**Core Principle:**

A commit should tell one complete story.
Never combine unrelated changes into the same commit.

---

## Preconditions

Before committing:

- Ensure implementation is complete.
- Ensure all validation commands have passed.
- Ensure no failing tests remain.
- Ensure the code has already been reviewed.

If these conditions are not met, stop and explain why.

---

## Phase 1: Inspect Repository State

Run:

```bash
git status
git diff HEAD
git status --porcelain
```

Determine:

- Modified files
- New files
- Deleted files
- Renamed files

Identify whether unrelated work exists.

If unrelated changes are detected:

- Recommend creating separate commits.
- Do not combine unrelated work.

---

## Phase 2: Review Changes

Inspect every changed file.

Determine:

- What changed?
- Why it changed.
- Whether changes belong together.
- Whether temporary/debug code exists.
- Whether generated files should be committed.

Flag anything suspicious before continuing.

---

## Phase 3: Stage Changes

Stage only the files related to this feature.

Prefer selective staging over blindly staging everything.

```bash
git add <files>
```

Avoid:

```bash
git add .
```

unless every modified file belongs to the same logical change.

---

## Phase 4: Generate Commit Message

Follow Conventional Commits.

Supported types include:

- feat
- fix
- docs
- refactor
- perf
- test
- build
- ci
- chore
- style

Format:

```text
type(scope): concise summary
```

Example:

```text
feat(wallet): implement withdrawal approval workflow
```

Body (optional):

- Why the change was made
- Major implementation notes
- Breaking changes if applicable

---

## Phase 5: Create Commit

Execute:

```bash
git commit
```

using the generated commit message.

---

## Output Report

Provide:

### Commit Type

```
feat
```

### Commit Message

```
feat(wallet): implement withdrawal approval workflow
```

### Files Included

- app/services/wallet.ts
- app/routes/wallet.ts
- tests/wallet.test.ts

### Summary

Brief explanation of the completed work.

### Ready For

- Push
- Pull Request
- Review

---

## Quality Criteria

✓ Commit is atomic

✓ Commit message follows Conventional Commits

✓ No unrelated changes included

✓ No temporary/debug code committed

✓ Validation already passed

✓ Commit can be reverted independently