# Threat Modeling Reference

## Table of Contents
- [STRIDE Analysis](#stride-analysis)
- [DREAD Risk Assessment](#dread-risk-assessment)
- [Attack Trees](#attack-trees)
- [Data Flow Diagrams](#data-flow-diagrams)
- [Threat Modeling Workflow](#threat-modeling-workflow)

## STRIDE Analysis

Map each threat category to its security property and common application security manifestations:

| Threat | Property | Application Security Examples |
|---|---|---|
| **S**poofing | Authentication | Token theft, credential stuffing, session hijacking, identity provider misconfiguration |
| **T**ampering | Integrity | API parameter manipulation, SQL/CMD injection, JWT modification, insecure deserialization |
| **R**epudiation | Non-repudiation | Missing audit logs, reusable tokens, unverifiable actions, no correlation ID tracking |
| **I**nformation Disclosure | Confidentiality | Excessive data in responses, verbose errors, missing encryption, CORS misconfiguration |
| **D**enial of Service | Availability | Unbounded queries, regex DoS, missing rate limiting, resource exhaustion, dependency on slow services |
| **E**levation of Privilege | Authorization | IDOR, missing RBAC checks, privilege escalation via role manipulation, insecure direct object references |

### Application-Specific STRIDE Prompts

For each trust boundary, ask:

1. **Authentication boundary**: Can an unauthenticated user reach this component? What identity assertions are trusted?
2. **Authorization boundary**: Does this component enforce least privilege? Can a lower-privilege user access higher-privilege operations?
3. **Data boundary**: Is data encrypted at rest and in transit? Are there sanitization checks at every input boundary?
4. **Network boundary**: Is service-to-service communication authenticated? Are internal APIs exposed externally?

## DREAD Risk Assessment

Score each threat 1-10 on each dimension, then compute the composite risk:

| Dimension | 1-3 (Low) | 4-6 (Medium) | 7-10 (High) |
|---|---|---|---|
| **D**amage potential | Minor data exposure | Significant data loss, auth bypass | Full system compromise, data breach |
| **R**eproducibility | Rarely reproducible | Consistent under specific conditions | Always reproducible |
| **E**xploitability | Expert knowledge + specialized tools | Authenticated user with tools | Unauthenticated, simple request |
| **A**ffected users | Small subset | Significant portion | All users |
| **D**iscoverability | Obscure, hard to find | Visible in logs/monitoring | Obvious in public interfaces |

**Risk Score** = (D + R + E + A + D) / 5

- **Critical**: 8-10 — Fix immediately, block deployment
- **High**: 6-7 — Fix before next release
- **Medium**: 4-5 — Fix within sprint, add mitigations
- **Low**: 1-3 — Track, fix when convenient

## Attack Trees

### Structure

```
Goal: [Attacker's objective]
├── OR: [Approach 1]
│   ├── AND: [Sub-step A] + [Sub-step B]
│   └── OR: [Alternative path]
└── OR: [Approach 2]
    └── LEAF: [Simplest path]
```

### Application Security Attack Tree Example

```
Goal: Access another user's data
├── OR: Bypass authorization
│   ├── AND: Obtain valid token + exploit IDOR vulnerability
│   ├── OR: Exploit missing access control check in API
│   └── OR: Abuse GraphQL field suggestions for data exposure
├── OR: Escalate privileges
│   ├── AND: Compromise user account + exploit role manipulation
│   └── OR: Exploit JWT algorithm confusion
└── OR: Exploit data exposure
    ├── OR: Mass assignment via API
    ├── OR: Excessive fields in API response
    └── OR: Insecure direct object reference
```

### Annotation

Add to each leaf node:
- **Feasibility**: Trivial / Moderate / Hard
- **Required access**: None / Authenticated / Admin
- **Detection likelihood**: Low / Medium / High
- **Risk rating**: From DREAD assessment

## Data Flow Diagrams

### Elements

- **External entities**: Users, third-party services, external systems (rectangles)
- **Processes**: Application services, microservices, Lambda functions (circles)
- **Data stores**: Databases, caches, queues, object storage (open rectangles)
- **Data flows**: Arrows labeled with data type and protocol
- **Trust boundaries**: Dashed lines grouping elements at the same trust level

### Layers for Application Architecture

1. **Client layer**: Browser, mobile app, desktop — mark authentication boundaries
2. **API gateway layer**: Rate limiting, auth validation, routing — mark policy enforcement points
3. **Service layer**: Business logic, data access — mark authorization boundaries
4. **Data layer**: Databases, caches, queues — mark encryption boundaries

### Checklist per Data Flow

For each data flow crossing a trust boundary:
- Is authentication verified?
- Is authorization enforced?
- Is data validated and sanitized?
- Is data encrypted in transit?
- Is the protocol secured (TLS 1.2+, mutual TLS where appropriate)?
- Is there rate limiting?
- Are there audit logs?

## Threat Modeling Workflow

1. **Scope the system**: Identify components, trust boundaries, and entry points. Focus on the application layer.
2. **Create data flow diagram**: Map all data flows, especially those crossing trust boundaries.
3. **Identify threats systematically**: Apply STRIDE to each trust boundary crossing using the prompts above.
4. **Assess risk**: Score each threat with DREAD. Prioritize Critical and High risks.
5. **Design mitigations**: Map threats to security patterns (see security-patterns.md).
6. **Validate**: Walk through mitigated architecture. Verify each threat has an effective control.
7. **Document**: Record threats, rankings, and mitigations for traceability.