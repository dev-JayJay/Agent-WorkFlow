# Database Engineering Skill

## Purpose

Use this skill when designing, implementing, reviewing, or debugging database-related work.

This skill defines reusable database engineering principles for building reliable, scalable, and safe data systems.

It should be combined with project-specific context from:

- `AGENT.md`
- `.agents/reference/database.md`
- `.agents/reference/business-rules.md`
- `.agents/memory/decisions.md`
- `.agents/plans/`

---

# Core Principles

- Design data around business rules.
- Keep data consistent.
- Prefer explicit relationships.
- Use constraints to protect critical rules.
- Use transactions for multi-step state changes.
- Add indexes intentionally.
- Avoid storing derived data unless justified.
- Protect money, wallet, payment, and audit records carefully.
- Migrations must be safe, reversible where possible, and reviewable.

---

# Database Design Philosophy

A database is not just storage.

It protects the truth of the system.

Application code can have bugs, but database constraints should prevent invalid critical states where possible.

Use the database to enforce:

- Uniqueness
- Required relationships
- Valid states
- Referential integrity
- Auditability
- Idempotency

---

# Recommended Relational Design

Prefer relational databases such as PostgreSQL for systems that need:

- Payments
- Wallets
- Orders
- Bookings
- Ownership
- Reporting
- Audit trails
- Role-based access
- Complex relationships

Recommended entity modeling:

```txt
users
roles
permissions
wallets
transactions
payments
withdrawals
webhook_events
audit_logs
roles
permissions
wallets
wallet_transactions
payments
withdrawals
orders
audit_logs
webhook_events
notifications
```

---

# Relationships

Design relationships around business rules.

Use explicit foreign keys.

Example:

```txt
users
 ├── wallets
 ├── payments
 ├── withdrawals
 ├── audit_logs
 └── notifications

wallets
 └── wallet_transactions

orders
 ├── order_items
 └── payments

roles
 └── permissions
```

Relationship Guidelines:

- Use foreign keys.
- Avoid duplicate relationships.
- Model ownership explicitly.
- Prefer junction tables for many-to-many relationships.
- Avoid storing lists inside JSON unless justified.

---

# Primary Keys

Every table should have a stable primary key.

Preferred IDs:

- UUID
- ULID
- CUID

Avoid exposing auto-increment IDs publicly.

Example:

```sql
id UUID PRIMARY KEY
```

---

# Foreign Keys

Always protect referential integrity.

Example:

```sql
wallet.user_id
→ users.id

payment.wallet_id
→ wallets.id
```

Prefer:

```txt
ON DELETE RESTRICT
```

for financial records.

Avoid deleting history accidentally.

---

# Constraints

Use constraints to enforce business rules.

Examples:

```sql
UNIQUE(email)

UNIQUE(reference)

CHECK(amount > 0)

CHECK(balance >= 0)
```

Examples of protected business rules:

- One wallet per user.
- One payment reference.
- One webhook event.
- Positive transaction amount.
- Valid status values.

---

# Normalization

Prefer Third Normal Form (3NF).

Goals:

- Reduce duplication.
- Eliminate update anomalies.
- Keep one source of truth.

Avoid storing the same information in multiple tables.

Example:

Bad

```txt
orders
customer_name
customer_email
customer_phone
```

Good

```txt
customers

orders

orders.customer_id
```

---

# Denormalization

Only denormalize when justified.

Good reasons:

- Reporting
- Analytics
- Performance
- Read optimization

Never denormalize without documenting why.

---

# Naming Conventions

Use consistent names.

Tables:

```txt
users
payments
wallets
orders
```

Primary Keys:

```txt
id
```

Foreign Keys:

```txt
user_id

wallet_id

payment_id
```

Timestamps:

```txt
created_at

updated_at

deleted_at
```

Avoid mixed naming styles.

---

# Money Handling

Never store money using floating point types.

Prefer:

```txt
BIGINT

NUMERIC(18,2)
```

Store the smallest currency unit where appropriate.

Example:

```txt
₦1000

↓

100000 kobo
```

Money rules:

- Never lose precision.
- Every balance change should have a transaction.
- Never allow negative balances unless explicitly designed.
- Never update balances without recording history.

---

# Transactions

Use database transactions whenever multiple writes must succeed together.

Examples:

- Purchase
- Wallet debit
- Wallet credit
- Withdrawal approval
- Payment processing
- Refunds

Workflow:

```txt
BEGIN

↓

Validate

↓

Update records

↓

Create transaction record

↓

Create audit log

↓

COMMIT
```

Rollback if any step fails.

---

# Row Locking

Use row locking for concurrent updates.

Typical cases:

- Wallets
- Inventory
- Seats
- Booking
- Transfers

Example:

```sql
SELECT *
FROM wallets
FOR UPDATE;
```

Protect against double spending.

---

# Idempotency

Every retryable operation should be idempotent.

Examples:

- Webhooks
- Payment callbacks
- Transfer callbacks
- Queue jobs

Strategies:

- Unique event IDs.
- Processed events table.
- Status checks.
- Database constraints.

Example:

```txt
webhook_events

provider

event_id

processed_at
```

The same webhook should never update data twice.

---

# Indexing

Indexes improve reads but slow writes.

Create indexes for:

- Foreign keys
- Search fields
- Status
- Dates
- References

Example:

```sql
INDEX(user_id)

INDEX(status)

INDEX(reference)

INDEX(created_at)
```

Avoid indexing every column.

---

# Query Optimization

Queries should:

- Select only required columns.
- Filter early.
- Use indexes.
- Limit results.
- Paginate.

Avoid:

```sql
SELECT *
```

unless truly needed.

---

# Pagination

Never return huge datasets.

Preferred approaches:

Offset Pagination

```txt
LIMIT

OFFSET
```

Cursor Pagination

```txt
created_at

id
```

Cursor pagination is preferred for large datasets.

---

# Soft Deletes

Prefer soft deletes for important business data.

Use:

```txt
deleted_at
```

Good candidates:

- Users
- Orders
- Products
- Wallets

Avoid deleting historical financial data.

---

# Audit Logging

Every sensitive action should be auditable.

Record:

- Actor
- Action
- Resource
- Before
- After
- Timestamp

Example:

```txt
Admin approved withdrawal

Before:

Pending

After:

Processing
```

---

# Status Design

Statuses should be explicit.

Example:

Payments

```txt
pending

processing

success

failed

cancelled
```

Withdrawals

```txt
pending

approved

processing

success

failed
```

Avoid ambiguous values.

---

# Migrations

Treat migrations as production code.

Rules:

- Never edit old migrations.
- Create new migrations.
- Keep them small.
- Review generated SQL.
- Test locally.
- Test rollback when possible.

Migration Flow

```txt
Generate

↓

Review

↓

Test

↓

Commit

↓

Deploy
```

---

# ORM Guidelines

ORMs are implementation details.

Business logic should never depend on ORM classes.

Repositories should map:

```txt
ORM Model

↓

Domain Entity
```

Keep ORM-specific code inside Infrastructure.

---

# PostgreSQL Guidelines

Prefer PostgreSQL for production systems.

Use:

- Foreign keys
- Constraints
- Transactions
- JSONB only when appropriate
- Indexes
- Row locking

Avoid using JSON as a replacement for relational design.

---

# Sequelize Guidelines

Keep Sequelize inside:

```txt
infrastructure/database/sequelize
```

Keep:

- Models
- Migrations
- Config

inside Infrastructure.

Do not import Sequelize models into:

- Domain
- Application

---

# Performance

Consider:

- Indexes
- Query plans
- N+1 queries
- Caching
- Read replicas
- Batch operations

Optimize after measuring.

Never optimize blindly.

---

# Backup Strategy

Production databases should have:

- Automated backups.
- Recovery testing.
- Disaster recovery plan.
- Backup verification.

A backup that has never been restored cannot be trusted.

---

# Security

Protect:

- Personal information.
- Payment information.
- Secrets.
- Audit records.

Never expose:

- Password hashes.
- Tokens.
- Internal IDs unnecessarily.

Encrypt sensitive data when appropriate.

---

# Environment Variables

Database configuration should come from:

```txt
DATABASE_URL

DB_HOST

DB_PORT

DB_NAME

DB_USER

DB_PASSWORD
```

Never commit production credentials.

Keep `.env.example` updated.

---

# Database Testing

Test:

- Constraints
- Relationships
- Transactions
- Rollbacks
- Idempotency
- Repository methods
- Migrations
- Performance-sensitive queries

Critical workflows should have integration tests.

---

# Database Review Checklist

Before approving database work verify:

- Schema reflects business rules.
- Relationships are correct.
- Constraints exist.
- Indexes exist where needed.
- Migrations are safe.
- Transactions protect critical operations.
- Money uses safe data types.
- Audit logs exist where required.
- Soft deletes are used appropriately.
- Tests pass.

---

# Definition of Done

Database work is complete only when:

- Database schema supports business requirements.
- Relationships are normalized.
- Constraints protect critical data.
- Migrations are reviewed and tested.
- Transactions are implemented where necessary.
- Queries are performant.
- Sensitive data is protected.
- Tests pass.
- Documentation is updated.
- Implementation follows project architecture and conventions.