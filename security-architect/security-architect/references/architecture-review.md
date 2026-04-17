# Architecture Review Reference

## Table of Contents
- [Review Workflow](#review-workflow)
- [Application Security Checklist](#application-security-checklist)
- [API Security Checklist](#api-security-checklist)
- [Authentication & Authorization Checklist](#authentication--authorization-checklist)
- [Data Security Checklist](#data-security-checklist)
- [Infrastructure & Deployment Checklist](#infrastructure--deployment-checklist)
- [Resilience & Operations Checklist](#resilience--operations-checklist)
- [Security Anti-Patterns](#security-anti-patterns)
- [Risk Rating Framework](#risk-rating-framework)

## Review Workflow

1. **Understand the architecture**: Read design docs, architecture diagrams, data flow descriptions. Ask clarifying questions about trust boundaries.
2. **Identify trust boundaries**: Map where data crosses between trust levels (external → gateway, gateway → service, service → database, service → third-party).
3. **Apply threat model**: Use STRIDE per trust boundary crossing (see threat-modeling.md). Focus on the top 5-10 most likely/exploitable threats.
4. **Run checklists**: For each component, apply relevant checklists below. Skip items that don't apply.
5. **Find anti-patterns**: Scan for known anti-patterns (see below). These are high-signal indicators of systemic issues.
6. **Rate findings**: Score each finding using the risk rating framework. Group by severity.
7. **Recommend mitigations**: Map findings to security patterns (see security-patterns.md). Provide specific, actionable recommendations — not generic advice.
8. **Summarize**: Produce a prioritized list of findings with clear severity, business impact, and remediation path.

## Application Security Checklist

### Input Handling
- [ ] All inputs validated at trust boundaries (whitelist approach)
- [ ] Input length limits enforced on all string fields
- [ ] File uploads: type/size validation, virus scanning, isolated storage
- [ ] Deserialization: avoid untrusted object deserialization or use safe alternatives
- [ ] Command injection: no shell execution with user input; use parameterized APIs
- [ ] SQL injection: parameterized queries or ORM everywhere, no raw SQL拼接
- [ ] XSS: output encoding for correct context (HTML, JS, URL, CSS)

### Output Handling
- [ ] Sensitive data excluded from API responses (no over-posting/mass assignment)
- [ ] Error responses contain no internal details (stack traces, DB errors, paths)
- [ ] Consistent Content-Type headers, X-Content-Type-Options: nosniff
- [ ] Logging: sensitive data masked or omitted; correlation IDs present

### Dependency Management
- [ ] Dependabot/Renovate or equivalent automated dependency scanning
- [ ] No known critical/high vulnerabilities in direct dependencies
- [ ] Lock files committed and enforced
- [ ] Minimal dependency footprint — unused dependencies removed

## API Security Checklist

### Authentication & Session
- [ ] All endpoints authenticated unless explicitly public (allowlist approach)
- [ ] Short-lived access tokens (≤15 min), secure refresh token flow
- [ ] Tokens stored in HttpOnly, Secure, SameSite cookies (web) or secure storage (mobile)
- [ ] Session invalidated on logout and password change
- [ ] No tokens in URLs, logs, or client-side storage (localStorage)

### Authorization
- [ ] Authorization enforced at both gateway and service level
- [ ] Fine-grained permissions (not just role checks) on sensitive operations
- [ ] IDOR prevention: verify object ownership or access rights before returning data
- [ ] Consistent authz enforcement — no endpoints bypassed

### API Design
- [ ] Rate limiting per user/IP with appropriate thresholds
- [ ] Request size limits enforced (body, headers, URL length)
- [ ] CORS configured explicitly — no wildcard origins with credentials
- [ ] GraphQL: depth/complexity limiting, introspection disabled in production
- [ ] API versioning Strategy that avoids breaking existing clients
- [ ] Pagination for list endpoints, no unbounded queries

### Headers
- [ ] Strict-Transport-Security (HSTS)
- [ ] X-Content-Type-Options: nosniff
- [ ] Content-Security-Policy (for HTML responses)
- [ ] X-Frame-Options: DENY or SAMEORIGIN (for HTML responses)
- [ ] Cache-Control: no-store for sensitive responses

## Authentication & Authorization Checklist

### Identity
- [ ] Password requirements: ≥12 chars, no composition rules, check against breach databases
- [ ] Multi-factor authentication available and enforced for privileged actions
- [ ] Account lockout with exponential backoff (not perma-lock)
- [ ] Credential rotation possible for service accounts

### Token Security
- [ ] Asymmetric signing (RS256/ES256) for JWTs — avoid symmetric (HS256) across services
- [ ] Token claims: minimum required (sub, scope, exp, iss, aud)
- [ ] Refresh tokens: one-time use, rotation on refresh, detection of reuse
- [ ] No sensitive data in token payload (it's base64, not encrypted)

### Authorization Model
- [ ] Authorization model chosen and consistently applied (RBAC/ABAC/ReBAC)
- [ ] Default-deny: access denied unless explicitly granted
- [ ] Privilege boundaries documented and enforced
- [ ] Admin/superuser actions require re-authentication

## Data Security Checklist

### Data at Rest
- [ ] Encryption at rest for all data stores containing Confidential or Restricted data
- [ ] Encryption key management via KMS/HSM, not co-located with encrypted data
- [ ] Database access restricted to application service accounts, no human user direct access

### Data in Transit
- [ ] TLS 1.2+ enforced for all connections, TLS 1.3 preferred
- [ ] No internal HTTP connections — all service-to-service calls over TLS
- [ ] Certificate management and rotation automated

### Data in Processing
- [ ] Sensitive data masked in logs, error messages, and non-production environments
- [ ] PII handling compliant with relevant regulations (GDPR, CCPA, etc.)
- [ ] Data retention policies defined and enforced
- [ ] Backup and disaster recovery tested, with encryption for backups

### Secrets
- [ ] No secrets in source code, config files in repos, or environment variables in logs
- [ ] Secrets injected at runtime from secrets manager
- [ ] Secret rotation automated, no shared secrets across services

## Infrastructure & Deployment Checklist

### Container Security
- [ ] Minimal base images (distroless, alpine) — no shell where possible
- [ ] Containers run as non-root with read-only filesystem
- [ ] No sensitive data in image layers or environment variables
- [ ] Image scanning in CI pipeline (Trivy, Snyk Container)

### CI/CD
- [ ] Pipeline enforces SAST, dependency scanning, container scanning before deploy
- [ ] Signed deployments/artifacts (Sigstore/cosign)
- [ ] Separate pipelines for separate environments, no prod access from dev pipelines
- [ ] Infrastructure as Code with security scanning (Checkov, tfsec)

### Network
- [ ] Network segmentation between services/tiers
- [ ] No direct internet access from data tier
- [ ] Egress filtering — services can only reach declared dependencies
- [ ] Service mesh or mutual TLS for service-to-service communication

## Resilience & Operations Checklist

### Monitoring & Detection
- [ ] Security events logged and aggregated (SIEM)
- [ ] Anomaly detection on authentication events
- [ ] Alerts for: repeated auth failures, privilege escalations, unusual data access patterns

### Incident Response
- [ ] Runbooks for common security incidents
- [ ] Ability to revoke tokens/credentials rapidly
- [ ] Ability to quarantine compromised services

### Availability
- [ ] Rate limiting and backpressure for all public endpoints
- [ ] Circuit breakers on downstream dependencies
- [ ] Graceful degradation under load
- [ ] Health checks separate from deep dependency checks

## Security Anti-Patterns

High-signal indicators that warrant deeper investigation:

| Anti-Pattern | Why It Matters | Severity |
|---|---|---|
| Shared database credentials | Lateral movement on compromise, no audit trail | Critical |
| Admin endpoints without auth | Immediate full compromise | Critical |
| Secrets in environment variables passed to frontend | Exposed to all users | Critical |
| `SELECT *` returned to client | Data leakage via mass assignment/excessive response | High |
| Token in URL/query string | Logged by proxies, stored in browser history | High |
| Trust based on network location alone | Ineffective against lateral movement | High |
| Single role for all operations | Least privilege violation | Medium |
| No rate limiting on auth endpoints | Enables credential stuffing | Medium |
| CORS `Access-Control-Allow-Origin: *` with credentials | CSRF via cross-origin | Medium |
| Inline SQL with string concatenation | SQL injection | Critical |
| Custom crypto implementations | Near-certain implementation flaws | Critical |
| Logging sensitive data in plaintext | Compliance violation, data leakage | High |

## Risk Rating Framework

### Likelihood

| Level | Criteria |
|---|---|
| **High** | Attack requires no special access, publicly documented exploit exists, common attack vector |
| **Medium** | Attack requires authenticated access or specific conditions, exploit possible but not trivial |
| **Low** | Attack requires privileged access, insider knowledge, or unlikely conditions |

### Impact

| Level | Criteria |
|---|---|
| **High** | Full data breach, system compromise, regulatory violation, significant financial loss |
| **Medium** | Limited data exposure, partial service disruption, compliance gap |
| **Low** | Information disclosure, minor availability impact, easily contained |

### Risk Matrix

|  | Low Impact | Medium Impact | High Impact |
|---|---|---|---|
| **High Likelihood** | Medium | High | **Critical** |
| **Medium Likelihood** | Low | Medium | High |
| **Low Likelihood** | Low | Low | Medium |

### Remediation Priority

- **Critical**: Block deployment, fix immediately, may require incident response
- **High**: Fix before release, add compensating controls if delayed
- **Medium**: Fix within sprint, document accepted risk if deferred
- **Low**: Backlog, fix opportunistically, track for trend analysis