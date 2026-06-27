---
description: Update project memory after meaningful changes
argument-hint: [optional-plan-file]
---

# Update Project Memory

## Mission

Update `.agents/memory/` with important project history, decisions, changes, lessons, and implementation notes.

The goal is to preserve context for future AI agents and developers.

Memory should explain:

- What changed
- Why it changed
- What decisions were made
- What future agents should remember
- What should not be repeated

---

## Core Principle

Memory is not documentation.

Memory is project history.

Do not duplicate full implementation details from code, plans, or reference docs.

Record only information that will matter later.

---

## Inputs

Optional plan file:

```txt
$ARGUMENTS
```

If provided, use it to understand the intended work.

Also inspect:

- `AGENT.md`
- `.agents/reference/`
- `.agents/plans/`
- Current git diff
- Review notes
- Test results
- User instructions

---

## Memory Folder Structure

Use this structure:

```txt
.agents/memory/
  project-memory.md
  decisions.md
  changelog.md
  lessons.md
```

If files do not exist, create them.

---

# File Responsibilities

## project-memory.md

Stores current high-level project state.

Use for:

- Current product status
- Active modules
- Current stack
- Current architecture
- Current development focus
- Known constraints

Example:

```md
# Project Memory

## Current State

- Authentication is implemented.
- One-to-one messaging is in progress.
- Socket.IO is used for realtime events.
- PostgreSQL stores persistent messages.
```

---

## decisions.md

Stores major technical and product decisions.

Use ADR-style entries.

Example:

```md
## DEC-001: Use Socket.IO for realtime messaging

**Date:** 2026-06-26

**Status:** Accepted

**Context:**
The chat application requires real-time message delivery, presence updates, and typing indicators.

**Decision:**
Use Socket.IO instead of raw WebSocket for MVP.

**Reason:**
Socket.IO provides rooms, reconnect handling, fallback transports, and a simpler developer experience.

**Consequences:**
The backend must maintain socket event contracts and client/server version compatibility.
```

---

## changelog.md

Stores meaningful implementation history.

Example:

```md
## 2026-06-26

### Added

- Added one-to-one chat message persistence.
- Added Socket.IO `message:send` and `message:new` events.

### Changed

- Updated message repository to support conversation-based queries.

### Fixed

- Prevented users from sending messages to themselves.
```

---

## lessons.md

Stores lessons learned from mistakes, bugs, repairs, or incidents.

Example:

```md
## 2026-06-26 — Message Read Receipts

### Lesson

The first implementation allowed users to mark unrelated messages as read.

### Prevention

Future read-receipt logic must always validate conversation membership and message ownership before updating `read_at`.
```

---

# Phase 1: Inspect Current Work

Run:

```bash
git status --short
git diff HEAD
```

Understand:

- Files changed
- Feature implemented
- Architecture changes
- Database changes
- Security-sensitive changes
- New conventions introduced

---

# Phase 2: Decide Whether Memory Is Needed

Update memory only if the work includes:

- Architecture decisions
- Database schema decisions
- Security decisions
- Payment/money rules
- New business rules
- Important bug fixes
- Repeated mistakes
- New integration choices
- Deployment/infra changes
- Project direction changes
- Lessons that future agents should remember

Do not update memory for:

- Tiny copy changes
- Pure formatting
- Minor UI text edits
- Trivial refactors
- Temporary experiments

---

# Phase 3: Select Target Memory File

Use:

```txt
project-memory.md
```

for current state.

Use:

```txt
decisions.md
```

for important decisions.

Use:

```txt
changelog.md
```

for implementation history.

Use:

```txt
lessons.md
```

for mistakes, gotchas, repairs, and prevention notes.

---

# Phase 4: Write Memory Entries

Write concise entries.

Good memory entries are:

- Dated
- Specific
- Useful later
- Easy to scan
- Not too long

Bad memory entries are:

- Vague
- Too detailed
- Duplicated from code
- Temporary
- Obvious

---

# Phase 5: Update Related Reference If Needed

If the change affects stable project knowledge, update `.agents/reference/` too.

Examples:

- New API contract → update `.agents/reference/api.md`
- New database table → update `.agents/reference/database.md`
- New business rule → update `.agents/reference/business-rules.md`
- New realtime event → update `.agents/reference/realtime-events.md`
- New deployment process → update `.agents/reference/deployment.md`

Memory records **why/when**.

Reference records **current truth**.

---

# Phase 6: Report

Provide:

### Memory Updated

List files updated.

### Entries Added

Summarize entries.

### Reference Updates

List reference files updated, if any.

### No Memory Needed

If no memory update was needed, explain why.

---

## Quality Criteria

- Memory is concise.
- Memory captures useful future context.
- Decisions include reason and consequence.
- Changelog summarizes meaningful changes.
- Lessons prevent repeated mistakes.
- Reference is updated when current truth changes.
- No sensitive secrets are recorded.