# Security Patterns Reference

## Table of Contents
- [Defense-in-Depth](#defense-in-depth)
- [Zero Trust](#zero-trust)
- [Least Privilege](#least-privilege)
- [Authentication Patterns](#authentication-patterns)
- [Authorization Patterns](#authorization-patterns)
- [API Security Patterns](#api-security-patterns)
- [Data Protection Patterns](#data-protection-patterns)
- [Secure Communication Patterns](#secure-communication-patterns)
- [Resilience Patterns](#resilience-patterns)
- [Pattern-to-Threat Mapping](#pattern-to-threat-mapping)

## Defense-in-Depth

Layer security controls so that failure of one layer does not result in complete compromise.

### Application Layers

| Layer | Controls |
|---|---|
| Edge/CDN | WAF, DDoS protection, geographic restrictions |
| API Gateway | Rate limiting, request validation, auth token verification, IP allowlisting |
| Application | Input validation, output encoding, business rule enforcement, audit logging |
| Database | Parameterized queries, row-level security, encryption at rest, access controls |
| Infrastructure | Network segmentation, secrets management, container hardening, runtime protection |

### Key Principles
- No single point of security failure
- Each layer validates inputs independently — never trust upstream layers
- Assume any single layer can be bypassed
- Log at every layer for detection and forensics

## Zero Trust

### Core Tenets for Application Security
1. **Never trust, always verify**: Every request is authenticated and authorized regardless of source
2. **Assume breach**: Design as if attackers are already inside the network
3. **Verify explicitly**: Authenticate and authorize based on all available data points (identity, location, device health, data classification, anomalies)
4. **Least privilege access**: Grant minimum required access, just-in-time, with bounded duration

### Application Design Implications
- Service-to-service calls require authentication (mutual TLS, service mesh, signed tokens)
- No implicit trust based on network location — internal APIs enforce the same auth as external
- Short-lived credentials with automatic rotation
- Every access decision logged with context
- Microservice boundaries are trust boundaries

## Least Privilege

### Implementation by Layer

**Runtime**: Run processes as non-root, read-only filesystem where possible, drop capabilities
**Application**: Scope API keys/tokens to minimum required permissions, use scoped service accounts
**Database**: Separate read/write accounts, restrict to specific tables/columns, use views for minimal exposure
**Infrastructure**: IAM roles with minimal permissions, per-service accounts, no shared credentials

### Common Anti-Patterns
- Using admin/root service accounts for routine operations
- Over-scoped JWT tokens (claim: `role: admin` instead of granular permissions)
- Shared database credentials across services
- IAM policies with `*:*` permissions
- Long-lived API keys without rotation

## Authentication Patterns

### Token-Based Auth (OAuth 2.0 + OIDC)
- Use short-lived access tokens (15 min) + refresh tokens
- Validate tokens at the gateway and again at the service level (defense-in-depth)
- Store tokens securely: HttpOnly, Secure, SameSite cookies for web; secure storage for mobile
- Never pass tokens in URLs or logs

### Service-to-Service Auth
- **Mutual TLS**: Both sides verify identity via certificates. Best for internal service meshes.
- **Signed JWTs**: Services verify token signatures. Best for request-scoped delegation.
- **API Keys**: Simple but limited — use only for machine-to-machine, rotate frequently, scope narrowly.

### Session Management
- Regenerate session IDs after authentication
- Bind sessions to identity context (user, device, IP range)
- Implement absolute and inactivity timeouts
- Invalidate sessions server-side on logout and password change

## Authorization Patterns

### RBAC (Role-Based Access Control)
- Best for coarse-grained access with well-defined roles
- Keep roles flat and specific — avoid deep hierarchies
- Map roles to specific operations, not broad resource classes

### ABAC (Attribute-Based Access Control)
- Best for fine-grained, context-dependent decisions
- Evaluate: subject attributes + resource attributes + action + environment
- Example: `deny if resource.complianceLevel == "pci" AND subject.department != "finance" AND action != "read"`

### ReBAC (Relationship-Based Access Control)
- Best for shared resources with complex ownership models (files, orgs, repos)
- Model relationships explicitly: user → member_of → organization → owns → resource

### Enforcement Points
- **Gateway**: Coarse-grained (can user access this service?)
- **Application**: Fine-grained (can user perform this operation on this resource?)
- **Data**: Row/column-level (which rows can user see?)

## API Security Patterns

### Input Validation
- Validate at trust boundaries (gateway + application)
- Whitelist allowed input patterns, reject everything else
- Enforce max lengths on all string inputs
- Validate content-type headers match actual content
- Decode then validate (URL decode, base64 decode, then check)

### Output Encoding
- Encode output for the correct context (HTML, JSON, URL, CSS, JS)
- Never serialize raw user input into responses
- Apply consistent response headers: `X-Content-Type-Options: nosniff`, `Content-Type` always set

### Rate Limiting
- Per-user limits (authenticated) and per-IP limits (unauthenticated)
- Different limits for different operations (read vs write, expensive vs cheap)
- Return `429 Too Many Requests` with `Retry-After` header
- Implement at gateway level, backfill at application level for defense-in-depth

### API-Specific Controls
- **REST**: Validate HTTP methods, enforce CORS policies, limit query complexity
- **GraphQL**: Limit query depth and complexity, disable introspection in production, implement query allowlisting
- **gRPC**: Validate protobuf messages, enforce message size limits, use TLS

## Data Protection Patterns

### Encryption
- **In transit**: TLS 1.2+ (prefer 1.3), HSTS headers, certificate pinning for mobile
- **At rest**: AES-256-GCM for stored data, envelope encryption with KMS for key management
- **In processing**: Minimize plaintext exposure, use secure enclaves for sensitive computation

### Data Classification
| Level | Examples | Controls |
|---|---|---|
| Public | Marketing content, public APIs | Integrity protection only |
| Internal | Internal docs, non-sensitive metrics | Access control, audit logging |
| Confidential | PII, financial data, credentials | Encryption at rest + transit, access logs, masking |
| Restricted | Encryption keys, secrets, health records | HSM storage, mTLS, strict access, real-time monitoring |

### Principle of Data Minimization
- Collect only what is needed for the specific purpose
- Return only required fields in API responses (no `SELECT *`)
- Mask/redact sensitive fields in logs and non-production environments
- Delete data when retention period expires

## Secure Communication Patterns

### TLS Configuration
- Minimum TLS 1.2, prefer 1.3
- Disable weak cipher suites (RC4, DES, 3DES, MD5)
- Use forward secrecy (ECDHE key exchange)
- Enable HSTS with long max-age and includeSubDomains

### Service Mesh
- Enforce mTLS between all services automatically
- Use service identity (SPIFFE/SPIRE) rather than IP-based identity
- Implement traffic policies at mesh level (retry budgets, circuit breakers)

### Secrets Management
- Never hardcode secrets, never commit secrets to repos
- Use dedicated secrets manager (Vault, AWS SM, GCP SM)
- Inject secrets at runtime via environment or volume mounts
- Rotate secrets automatically, never share secrets across services

## Resilience Patterns

### Circuit Breaker
- Prevent cascading failures by failing fast when downstream is unhealthy
- Configure: failure threshold, recovery timeout, half-open probe interval

### Bulkhead
- Isolate critical services from each other's failures
- Separate thread pools, connection pools, rate limit quotas per dependency

### Rate Limiting + Backpressure
- Reject requests when overloaded (503 + Retry-After) rather than queuing indefinitely
- Use adaptive rate limiting based on system health metrics

### Fail Securely
- Default-deny: access denied on auth/authz failure, system errors, or missing configuration
- Never expose internal error details to clients
- Log failures with context for debugging, but sanitize sensitive data

## Pattern-to-Threat Mapping

| Threat Category | Primary Patterns | Secondary Patterns |
|---|---|---|
| Spoofing | mTLS, token-based auth, certificate pinning | Defense-in-depth, zero trust |
| Tampering | Input validation, output encoding, HMAC/JWT signatures | Immutable audit logs |
| Repudiation | Correlation IDs, immutable audit trails, signed tokens | Non-repudiation logs |
| Information Disclosure | Encryption, data minimization, RBAC/ABAC | TLS, masking, classification |
| Denial of Service | Rate limiting, circuit breakers, backpressure | Bulkheads, auto-scaling |
| Elevation of Privilege | Least privilege, RBAC/ABAC/ReBAC, zero trust | Defense-in-depth, fail secure |