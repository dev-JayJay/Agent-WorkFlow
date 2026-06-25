# DevOps Engineering Skill

## Purpose

Use this skill when designing, implementing, deploying, monitoring, or maintaining software systems.

This skill defines universal DevOps engineering principles for building reliable, scalable, observable, and maintainable production systems.

It should be combined with project-specific context from:

- `AGENT.md`
- `.agents/reference/infrastructure.md`
- `.agents/reference/deployment.md`
- `.agents/memory/`
- `.agents/plans/`

---

# Core Principle

Software is not finished when it compiles.

Software is complete only when it can be:

- Built
- Tested
- Deployed
- Observed
- Monitored
- Recovered
- Scaled

---

# DevOps Philosophy

Every system should answer:

```txt
Can it be deployed?

↓

Can it be monitored?

↓

Can it recover?

↓

Can it scale?

↓

Can it be maintained?
```

Development and operations should work together.

---

# Environment Strategy

Maintain separate environments.

```txt
Development

↓

Testing

↓

Staging

↓

Production
```

Rules:

- Never use production credentials locally.
- Never test directly in production.
- Keep configuration isolated.
- Production should be reproducible.

---

# Configuration Management

Configuration belongs outside the application.

Use:

- Environment variables
- Secret managers
- Configuration files

Never hardcode:

- API keys
- Passwords
- Tokens
- Database URLs

Example:

```txt
DATABASE_URL
JWT_SECRET
PAYSTACK_SECRET_KEY
REDIS_URL
```

---

# Docker

Containerize applications.

Every production service should have:

- Dockerfile
- .dockerignore

Prefer multi-stage builds.

Example flow:

```txt
Builder

↓

Production Image
```

Keep images:

- Small
- Secure
- Reproducible

---

# Docker Compose

Use Docker Compose for local development.

Typical services:

```txt
App

↓

PostgreSQL

↓

Redis

↓

RabbitMQ

↓

Mailhog
```

Avoid using Docker Compose for production orchestration.

---

# CI/CD

Every project should have Continuous Integration.

CI should automatically run:

```txt
Install

↓

Lint

↓

Type Check

↓

Unit Tests

↓

Integration Tests

↓

Build
```

Deployment should only happen if validation succeeds.

---

# GitHub Actions

Preferred CI platform.

Typical workflow:

```txt
Push

↓

Install

↓

Lint

↓

Test

↓

Build

↓

Deploy
```

Never deploy broken builds.

---

# Deployment Strategy

Prefer automated deployments.

Deployment flow:

```txt
Merge

↓

CI

↓

Build

↓

Deploy

↓

Health Check

↓

Traffic
```

Avoid manual production deployments where possible.

---

# Health Checks

Every service should expose health endpoints.

Examples:

```txt
/health

/health/db

/health/ready
```

Health checks should verify:

- Application
- Database
- Cache
- External dependencies (where appropriate)

---

# Logging

Applications should produce structured logs.

Log:

- Startup
- Shutdown
- Errors
- External API failures
- Authentication failures
- Payment events
- Background jobs

Avoid logging:

- Passwords
- Tokens
- Secrets
- Personal information

---

# Monitoring

Every production application should be monitored.

Monitor:

- CPU
- Memory
- Disk
- Response time
- Request count
- Error rate
- Queue size
- Database performance

Know when something breaks before users report it.

---

# Metrics

Collect meaningful metrics.

Application metrics:

- Requests/sec
- Error rate
- Response time
- Active users

Business metrics:

- Purchases
- Deposits
- Withdrawals
- Registrations

Infrastructure metrics:

- CPU
- RAM
- Disk
- Network

---

# Alerting

Create alerts for:

- Service down
- High latency
- High error rate
- Database unavailable
- Queue backlog
- Failed deployments
- Failed backups

Alerts should be actionable.

Avoid alert fatigue.

---

# Reverse Proxy

Use a reverse proxy in production.

Common choices:

- Nginx
- Caddy
- Traefik

Responsibilities:

- HTTPS
- Load balancing
- Static assets
- Compression
- Security headers

---

# HTTPS

Always use HTTPS in production.

Redirect HTTP to HTTPS.

Use trusted certificates.

Never expose login or payment endpoints over HTTP.

---

# Scaling

Design applications to scale horizontally.

Prefer:

```txt
Stateless API

↓

Shared Database

↓

Shared Cache

↓

Load Balancer
```

Avoid storing user sessions in application memory.

---

# Caching

Use caching carefully.

Common caches:

- Redis
- CDN
- Browser Cache

Cache:

- Frequently read data
- Expensive queries
- Computed values

Do not cache sensitive or rapidly changing data without an invalidation strategy.

---

# Background Jobs

Move long-running work out of HTTP requests.

Examples:

- Emails
- Imports
- Exports
- Notifications
- Image processing

Use:

- BullMQ
- RabbitMQ
- Kafka
- SQS

---

# Database Operations

Production databases require:

- Backups
- Migrations
- Monitoring
- Connection pooling
- Slow query analysis

Never modify production data manually without approval and backups.

---

# Backup Strategy

Backups should be:

- Automated
- Verified
- Restorable

Test restores regularly.

A backup that cannot be restored is not a backup.

---

# Disaster Recovery

Prepare for failure.

Document:

- Recovery steps
- Backup location
- Recovery time objectives
- Recovery point objectives

Practice recovery procedures.

---

# Deployment Strategies

Choose appropriate deployment methods.

Examples:

Rolling Deployment

```txt
Old

↓

New
```

Blue-Green Deployment

```txt
Blue

↓

Green
```

Canary Deployment

```txt
10%

↓

25%

↓

50%

↓

100%
```

Prefer zero-downtime deployments.

---

# Feature Flags

Use feature flags for risky releases.

Benefits:

- Gradual rollout
- Easy rollback
- A/B testing
- Safer deployments

Avoid long-lived unused feature flags.

---

# Rollback Strategy

Every deployment should have a rollback plan.

Rollback should be:

- Fast
- Safe
- Tested

Never deploy without knowing how to recover.

---

# Infrastructure as Code

Prefer infrastructure defined as code.

Examples:

- Terraform
- Pulumi
- CloudFormation

Infrastructure should be version controlled.

---

# Secrets Management

Secrets belong in:

- Secret Manager
- Vault
- Environment Variables

Never commit secrets.

Rotate compromised secrets immediately.

---

# Cloud Storage

Store uploads outside the application server.

Examples:

- S3
- Cloud Storage
- DigitalOcean Spaces

Never rely on local disk for permanent storage.

---

# CDN

Use CDN for:

- Images
- JavaScript
- CSS
- Fonts

Improve global performance.

---

# Performance

Measure before optimizing.

Watch:

- Response time
- Slow queries
- Memory leaks
- CPU spikes
- Cache hit rate

Use profiling tools where necessary.

---

# Production Readiness Checklist

Before deploying verify:

- Tests pass.
- Build succeeds.
- Environment variables exist.
- Database migrations reviewed.
- Health checks work.
- Logging enabled.
- Monitoring enabled.
- Alerts configured.
- Rollback prepared.

---

# Incident Response

When an incident occurs:

```txt
Detect

↓

Triage

↓

Contain

↓

Fix

↓

Recover

↓

Review
```

Document:

- Root cause
- Timeline
- Impact
- Resolution
- Prevention

Avoid blame.

Focus on system improvement.

---

# Observability

Every production system should support:

- Logs
- Metrics
- Traces

Questions you should answer quickly:

- What failed?
- When?
- Why?
- Who was affected?
- How do we fix it?

---

# DevOps Review Checklist

Before approving infrastructure work verify:

- Containers build correctly.
- CI passes.
- Deployment is repeatable.
- Health checks exist.
- Logging is structured.
- Monitoring is configured.
- Alerts are meaningful.
- Secrets are protected.
- Rollback exists.
- Documentation is updated.

---

# Common DevOps Anti-Patterns

Avoid:

- Manual deployments.
- Hardcoded secrets.
- Running everything on one server without backups.
- No monitoring.
- No health checks.
- No rollback plan.
- Deploying without tests.
- Editing production databases manually.
- Ignoring failed alerts.
- Treating infrastructure as undocumented.

---

# Definition of Done

DevOps work is complete only when:

- Infrastructure is reproducible.
- Containers build successfully.
- CI/CD pipelines pass.
- Deployments are automated.
- Monitoring and alerting are configured.
- Health checks are implemented.
- Backups are verified.
- Rollback procedures exist.
- Documentation is updated.
- The system is production-ready.