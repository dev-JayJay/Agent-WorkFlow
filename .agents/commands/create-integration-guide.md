---
description: Create an integration guide for implemented feature changes
argument-hint: [plan-file-or-feature-name]
---

# Create Integration Guide

## Mission

Create a clear, practical integration guide that explains how another developer should use, connect to, or integrate the implemented feature.

This guide should help frontend, backend, mobile, or external developers understand what changed and how to work with it.

---

## Core Principle

Do not invent behavior.

Document only what exists in the implementation, plan, API, database, events, and configuration.

If something is unclear, mark it as:

```txt
Needs confirmation
```

---

## Inputs

Use the provided argument:

```txt
$ARGUMENTS
```

This may be:

- A plan file
- A feature name
- A ticket name
- A module name

Also read:

- `AGENT.md`
- Relevant `.agents/reference/*`
- Relevant `.agents/plans/*`
- Current `git diff HEAD`
- API routes/controllers
- DTOs/types
- Database migrations/models
- Socket/realtime events
- Environment config
- Tests

---

## Phase 1: Understand the Change

Inspect:

```bash
git status --short
git diff HEAD
git diff --stat HEAD
```

Identify:

- Feature implemented
- Files changed
- New APIs
- Updated APIs
- New database fields/tables
- New events
- New configuration
- Breaking changes
- Required client/server changes

---

## Phase 2: Identify Integration Audience

Determine who needs this guide:

```txt
Frontend Client
Backend Server
Mobile App
External API Consumer
Admin/Operations
```

If multiple audiences are affected, create separate sections for each.

---

## Phase 3: Extract Technical Contracts

Document all relevant contracts.

Include:

- API endpoints
- Request payloads
- Response payloads
- Error responses
- Auth/permission requirements
- Socket events
- Database changes
- Environment variables
- Feature flags
- Validation rules
- Status flows

---

## Phase 4: Write Integration Guide

Create or update:

```txt
.agents/reference/integration-guides/{feature-name}.md
```

If the folder does not exist, create it.

---

# Integration Guide Template

```md
# Integration Guide: <Feature Name>

## Overview

Briefly explain what was implemented and why.

## Who This Guide Is For

- Frontend developers
- Backend developers
- Mobile developers
- External integrators

## Summary of Changes

### Added

- ...

### Changed

- ...

### Removed

- ...

### Breaking Changes

- None / list changes

---

## Backend Integration

Use this section if backend/server developers need to know how to use or extend the feature.

### New/Updated Modules

| File/Module | Purpose |
|---|---|
| `path/to/file.ts` | Explanation |

### Services / Use Cases

Explain the important service/use-case methods.

### Repositories / Data Access

Explain repository methods or data access changes.

### Business Rules

List business rules enforced by the backend.

---

## API Integration

Use this section if HTTP APIs were added or changed.

### Endpoint: `METHOD /path`

**Purpose:**

Explain what this endpoint does.

**Authentication:**

Required / Not required

**Authorization:**

Role or ownership requirements.

**Request Body:**

```json
{}
```

**Success Response:**

```json
{}
```

**Error Responses:**

| Status | Code | Meaning |
|---|---|---|
| 400 | VALIDATION_ERROR | Invalid request |
| 401 | UNAUTHORIZED | Missing/invalid auth |
| 403 | FORBIDDEN | Not allowed |

**Example Request:**

```bash
curl -X POST http://localhost:3000/api/example
```

---

## Frontend Integration

Use this section if frontend/client developers need to consume the feature.

### Required UI Changes

- ...

### API Calls Needed

- ...

### Client State Updates

- ...

### Loading / Empty / Error States

Document required UI states.

### Example Flow

```txt
User clicks button
↓
Client calls API
↓
Server responds
↓
Client updates UI
```

---

## Realtime / Socket Integration

Use this section if Socket.IO/WebSocket events were added or changed.

### Event: `<event:name>`

**Direction:**

Client → Server / Server → Client

**Payload:**

```json
{}
```

**When Emitted:**

Explain trigger.

**Expected Client Behavior:**

Explain what the receiver should do.

---

## Database Changes

Use this section if schema/model changes were made.

### Tables Added

- ...

### Columns Added

- ...

### Indexes / Constraints

- ...

### Migration Notes

Explain whether migrations must be run.

```bash
npm run migrate
```

---

## Environment Variables

List new or changed environment variables.

```txt
EXAMPLE_KEY=
```

Explain each variable.

---

## Validation Rules

List validation constraints.

Example:

- `message` is required.
- `message` must not exceed 2000 characters.
- `conversationId` must belong to authenticated user.

---

## Permissions & Security

Document:

- Required roles
- Ownership checks
- Protected routes
- Sensitive actions
- Security gotchas

---

## Testing Notes

Explain how to verify the integration.

### Backend

```bash
npm test
```

### Frontend

```bash
npm run test
```

### Manual Test Flow

1. ...
2. ...
3. ...

---

## Rollout Notes

Mention:

- Feature flags
- Migration order
- Deployment order
- Backward compatibility
- Rollback concerns

---

## Known Limitations

List any known limitations or deferred work.

---

## Open Questions

List unclear items needing confirmation.

---

## Quick Start

Provide the shortest path for another developer to use the feature.

```txt
1. Run migration
2. Add env vars
3. Call endpoint
4. Listen to socket event
5. Update UI
```
```

---

## Phase 5: Update Reference Index

If `.agents/reference/README.md` exists, add this guide to the list of integration guides.

Example:

```md
## Integration Guides

- [Message Read Receipts](./integration-guides/message-read-receipts.md)
```

---

## Phase 6: Report

Provide:

### Guide Created

Path to the created guide.

### Audience

Who the guide is for.

### Main Contracts Documented

- APIs
- Events
- Database
- Environment
- Permissions

### Missing Information

Anything that needs confirmation.

---

## Quality Criteria

- Guide is based on actual implementation.
- API examples are accurate.
- Request/response contracts are documented.
- Frontend integration steps are clear.
- Backend integration steps are clear.
- Security/permission rules are included.
- Database and migration notes are included if relevant.
- Realtime events are documented if relevant.
- Known limitations are clearly stated.