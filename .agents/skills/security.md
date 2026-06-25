# Security Engineering Skill

## Purpose

Use this skill when designing, implementing, reviewing, or maintaining secure software systems.

This skill defines universal security engineering principles that apply across backend, frontend, databases, infrastructure, APIs, and deployments.

It should be combined with project-specific context from:

- `AGENT.md`
- `.agents/reference/security.md`
- `.agents/reference/business-rules.md`
- `.agents/memory/`
- `.agents/plans/`

---

# Core Principle

Security is not a feature.

Security is a fundamental quality of the system.

Every feature should be designed assuming:

- Users make mistakes.
- Attackers are intelligent.
- Networks are untrusted.
- Clients can be modified.
- Requests can be forged.
- Credentials can leak.

Always design with the principle of least privilege.

---

# Security Philosophy

Every request must answer:

```txt
Who are you?

↓

What are you allowed to do?

↓

Should this action be permitted?

↓

Can this action be audited?
```

Never trust:

- Browser
- Mobile App
- Client-side validation
- User input
- HTTP headers
- Query parameters

Trust only validated server-side data.

---

# Security Layers

Security should exist at multiple layers.

```txt
User

↓

Frontend

↓

API

↓

Authentication

↓

Authorization

↓

Business Rules

↓

Database

↓

Infrastructure
```

Never rely on only one layer.

---

# Authentication

Authentication answers:

```txt
Who is this user?
```

Common methods:

- JWT
- Session
- OAuth
- API Keys
- Passkeys
- MFA

Authentication should:

- Verify identity.
- Reject invalid credentials.
- Expire sessions.
- Rotate refresh tokens.
- Protect against replay attacks.

---

# Authorization

Authorization answers:

```txt
Is this user allowed to perform this action?
```

Examples:

```txt
Student

↓

Cannot approve withdrawals

Admin

↓

Can approve withdrawals
```

Always verify:

- Ownership
- Roles
- Permissions
- Resource access

Never trust frontend role checks.

---

# Role-Based Access Control (RBAC)

Design permissions explicitly.

Example:

```txt
Admin

Manager

Teacher

Student
```

Permissions:

```txt
Create

Read

Update

Delete

Approve

Export
```

Avoid hardcoding permissions throughout the codebase.

---

# Ownership

Ownership checks prevent users accessing another user's data.

Example:

```txt
GET

/users/123/profile
```

Verify:

```txt
Authenticated User

==

Resource Owner
```

before returning data.

---

# Input Validation

Validate everything.

Examples:

- Request body
- Query parameters
- Route parameters
- File uploads
- Headers
- Cookies
- Environment variables
- Webhooks

Reject:

- Invalid types
- Missing fields
- Invalid formats
- Unexpected values

Fail early.

---

# Output Encoding

Never render untrusted input directly.

Escape:

- HTML
- JavaScript
- CSS
- URLs

Prevent:

- Cross Site Scripting (XSS)

---

# SQL Injection

Never build SQL using string concatenation.

Bad:

```sql
SELECT * FROM users
WHERE email = '${email}'
```

Good:

Parameterized queries.

Always use ORM parameter binding or prepared statements.

---

# Cross Site Scripting (XSS)

Never trust user-generated HTML.

Prevent:

- Stored XSS
- Reflected XSS
- DOM XSS

Sanitize HTML before rendering.

Escape output.

---

# Cross Site Request Forgery (CSRF)

Protect state-changing requests.

Methods:

- CSRF Tokens
- SameSite Cookies
- Origin Validation

Applies mainly to cookie-based authentication.

---

# Clickjacking

Protect pages using:

```txt
X-Frame-Options

Content-Security-Policy
```

---

# Content Security Policy

Use CSP headers to reduce XSS risk.

Restrict:

- Scripts
- Images
- Fonts
- Frames
- Connections

---

# Password Security

Never store passwords.

Store only:

```txt
Password Hash
```

Use:

- Argon2
- bcrypt
- scrypt

Never:

- SHA256
- MD5
- Plain text

---

# Secrets Management

Secrets include:

- JWT secrets
- API keys
- Database passwords
- OAuth credentials
- Payment provider keys

Rules:

- Never commit secrets.
- Use environment variables.
- Rotate secrets periodically.
- Limit access.

Keep `.env.example` updated.

---

# Session Security

Sessions should:

- Expire
- Rotate
- Be invalidated on logout
- Use secure cookies

Cookies should be:

```txt
HttpOnly

Secure

SameSite
```

---

# JWT Guidelines

JWTs should:

- Expire quickly
- Contain minimal information
- Never store sensitive data
- Be signed securely

Validate:

- Signature
- Expiration
- Issuer
- Audience

---

# API Security

Protect every endpoint.

Verify:

- Authentication
- Authorization
- Validation
- Rate limiting
- Logging

Never expose internal stack traces.

Use consistent error responses.

---

# Rate Limiting

Protect against abuse.

Examples:

```txt
Login

↓

5 requests/minute

Password Reset

↓

3 requests/hour

OTP

↓

Limited attempts
```

Apply stricter limits to expensive endpoints.

---

# File Upload Security

Validate:

- File type
- File size
- MIME type

Scan uploads when possible.

Never trust file extensions.

Rename uploaded files.

Store outside the public directory when appropriate.

---

# Payment Security

Financial systems require extra protection.

Verify:

- Webhook signatures
- Idempotency
- Transaction references
- Amount validation

Never trust client payment success.

Always verify with provider.

---

# Webhook Security

Every webhook should verify:

- Signature
- Timestamp (if supported)
- Event ID
- Idempotency

Unknown events should not break the system.

---

# Logging

Log:

- Login attempts
- Permission failures
- Admin actions
- Financial operations
- Security events

Never log:

- Passwords
- JWTs
- API keys
- Secrets
- Full payment information

---

# Encryption

Encrypt sensitive information.

Examples:

- Personal documents
- Tokens
- Private files

Use TLS for all network communication.

Never send credentials over HTTP.

---

# Infrastructure Security

Protect:

- Servers
- Databases
- Storage
- Queues
- Message brokers

Disable unnecessary ports.

Use firewalls.

Restrict SSH access.

---

# Database Security

Use:

- Least privilege database users
- Prepared statements
- Database backups
- Encryption where appropriate

Never connect using superuser accounts unless required.

---

# Dependency Security

Regularly update dependencies.

Check:

- Vulnerabilities
- Deprecated packages
- Security advisories

Remove unused packages.

---

# OWASP Top 10 Awareness

Design to prevent:

- Broken Access Control
- Cryptographic Failures
- Injection
- Insecure Design
- Security Misconfiguration
- Vulnerable Components
- Authentication Failures
- Software Integrity Failures
- Logging Failures
- SSRF

The AI should recognize these risks during implementation and review.

---

# Security Testing

Test:

- Authentication
- Authorization
- SQL Injection
- XSS
- CSRF
- File uploads
- Webhooks
- Rate limiting
- Session expiration
- Token expiration

Critical security paths should have automated tests.

---

# Incident Response

If a security issue is discovered:

1. Contain the issue.
2. Protect affected users.
3. Preserve logs.
4. Identify root cause.
5. Patch the vulnerability.
6. Deploy safely.
7. Monitor.
8. Document lessons learned.

Never hide security incidents.

---

# Security Review Checklist

Before approving code verify:

- Inputs validated.
- Authorization exists.
- Authentication enforced.
- Ownership checked.
- Secrets protected.
- SQL Injection prevented.
- XSS prevented.
- CSRF considered.
- Rate limiting applied.
- Sensitive logs avoided.
- Payment verification implemented.
- Webhooks verified.
- Dependencies reviewed.

---

# Common Security Anti-Patterns

Avoid:

- Hardcoded secrets.
- Trusting frontend validation.
- Using `SELECT *` with user input.
- Logging tokens.
- Weak password hashing.
- Long-lived JWTs.
- Public admin endpoints.
- Missing ownership checks.
- Exposing stack traces.
- Ignoring failed authentication attempts.

---

# Definition of Done

Security work is complete only when:

- Authentication is implemented.
- Authorization is enforced.
- Validation exists.
- Sensitive data is protected.
- Secrets are managed securely.
- Critical security tests pass.
- Logging is appropriate.
- Documentation is updated.
- The implementation follows security best practices.