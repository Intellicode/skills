# Decision Frameworks

## Table of Contents

- [Architecture Decision Records (ADRs)](#architecture-decision-records-adrs)
- [Trade-Off Analysis](#trade-off-analysis)
- [Fitness Functions](#fitness-functions)
- [Risk Assessment](#risk-assessment)
- [Stakeholder Alignment](#stakeholder-alignment)
- [Build vs Buy vs Open Source](#build-vs-buy-vs-open-source)

## Architecture Decision Records (ADRs)

### ADR Template

```markdown
# ADR-[NUMBER]: [TITLE]

## Status
[Proposed | Accepted | Deprecated | Superseded by ADR-XXX]

## Context
What is the issue that we're seeing that is motivating this decision or change?

## Decision
What is the change that we're proposing and/or doing?

## Consequences
What becomes easier or more difficult to do because of this change?

### Positive
- [benefit 1]
- [benefit 2]

### Negative
- [drawback 1]
- [drawback 2]

### Risks
- [risk 1 and mitigation]
- [risk 2 and mitigation]
```

### ADR Guidelines

- Write ADRs for significant decisions: tech choices, pattern selections, data modeling, API contracts, security policies
- Skip ADRs for trivial decisions: variable naming, minor refactors
- Link ADRs to each other when one decision depends on another
- Revisit ADRs when context changes; don't delete — supersede
- Store ADRs in version control alongside code (`docs/adr/`)

### When to Write an ADR

| Decision Impact | ADR Required? |
|---|---|
| Affects one module, easy to reverse | No |
| Affects one service, medium reversal cost | Optional |
| Affects multiple services/teams | Yes |
| Affects overall system architecture | Yes |
| Affects security, compliance, or cost | Yes |

## Trade-Off Analysis

### Structured Trade-Off Framework

For each candidate solution, evaluate across these dimensions:

| Dimension | Weight | Option A | Option B | Option C |
|---|---|---|---|---|
| Developer velocity | [1-5] | [1-5] | [1-5] | [1-5] |
| Operational complexity | [1-5] | [1-5] | [1-5] | [1-5] |
| Scalability ceiling | [1-5] | [1-5] | [1-5] | [1-5] |
| Fault tolerance | [1-5] | [1-5] | [1-5] | [1-5] |
| Cost efficiency | [1-5] | [1-5] | [1-5] | [1-5] |
| Team expertise fit | [1-5] | [1-5] | [1-5] | [1-5] |
| Reversibility | [1-5] | [1-5] | [1-5] | [1-5] |

Weighted score = Σ(dimension weight × option score)

### Common Architecture Trade-Offs

| Trade-Off | Spectrum |
|---|---|
| Consistency ↔ Availability | CAP theorem: choose based on business needs |
| Simplicity ↔ Scalability | YAGNI vs pre-optimization |
| Speed ↔ Reliability | Fast but fragile vs slow but stable |
| Coupling ↔ Coordination | Tight coupling reduces coordination but creates fragility |
| Latency ↔ Throughput | Optimize for responsive UX or batch processing |
| Consistency ↔ Partition Tolerance | CP vs AP systems |
| Build ↔ Buy | Custom fit vs time-to-market |

### Reversibility Heuristic

**Easily reversible** (decide quickly, adjust later):
- UI framework choice
- API versioning strategy
- Caching layer implementation

**One-way doors** (decide carefully, hard to reverse):
- Database type (relational vs document vs graph)
- Monolith vs microservices boundary
- Cloud provider selection
- Data model / schema design

**Principle**: For easily reversible decisions, bias toward action. For one-way doors, bias toward analysis and ADRs.

## Fitness Functions

Fitness functions quantify how well an architecture meets its objectives.

### Common Fitness Functions

| Category | Example Metric |
|---|---|
| Performance | p99 latency < 200ms |
| Scalability | Handles 10x current load |
| Availability | 99.9% uptime SLA |
| Deployability | < 15 min from commit to prod |
| Modularity | Time to add new feature < 2 days |
| Testability | < 30 min full test suite |
| Observability | MTTR < 30 min |

### Defining Fitness Functions

1. **Identify the architectural characteristic** (e.g., deployability)
2. **Determine a measurable metric** (e.g., deployment frequency)
3. **Set a threshold** (e.g., deploy to prod < 15 min)
4. **Automate verification** (CI pipeline check, monitoring alert)

### Prioritization

Not all characteristics matter equally. Prioritize based on:
- **Business criticality**: What happens if this characteristic fails?
- **Current pain**: Where is the team spending disproportionate effort?
- **Strategic direction**: Where is the product heading?

## Risk Assessment

### Risk Categories for Architecture

| Category | Examples | Mitigation Strategy |
|---|---|---|
| Technical | Tech doesn't scale, vendor goes under | Prototyping, multi-vendor strategy |
| Organizational | Key person leaves, team restructure | Documentation, cross-training |
| Data | Data loss, schema migration failures | Backups, reversible migrations |
| Security | Auth bypass, data exposure | Threat modeling, security review |
| Operational | Deployment failures, monitoring gaps | Runbooks, alerting |
| Financial | Cost overrun, licensing changes | Cost monitoring, FOSS alternatives |

### Risk Assessment Matrix

| | Low Impact | Medium Impact | High Impact |
|---|---|---|---|
| **High Probability** | Monitor | Mitigate | Avoid / Redesign |
| **Medium Probability** | Accept | Monitor | Mitigate |
| **Low Probability** | Accept | Accept | Monitor |

### Defensive Architecture Patterns

- **Circuit breaker**: Fail fast instead of cascading failures
- **Bulkhead**: Isolate failures to one subsystem
- **Retry with backoff**: Handle transient failures
- **Fallback/degradation**: Serve partial results when dependencies fail
- **Rate limiting**: Protect against load spikes
- **Feature flags**: Decouple deployment from release
- **Blue-green / canary deployments**: Reduce deployment risk
- **Chaos engineering**: Validate resilience assumptions

## Stakeholder Alignment

### Architecture Decision Stakeholder Map

| Decision Type | Who Must Approve | Who Should Consult | Who Informed |
|---|---|---|---|
| Tech stack change | Tech lead, Architect | Senior engineers, Ops | Product, Security |
| Data model change | Architect, Data owner | Backend engineers | Frontend engineers |
| API contract change | API owner | Consumers of the API | Product, Docs |
| Infrastructure change | SRE/Ops, Architect | Security, Finance | All engineers |
| Security policy | Security team, Architect | Engineering leads, Legal | All engineering |

### Communication Templates

**Proposing an architecture change**:
1. Problem statement (what's broken or missing)
2. Proposed solution with trade-offs analyzed
3. Alternatives considered and why they fall short
4. Impact: who/what is affected and how
5. Migration plan (if applicable)
6. Success metrics (fitness functions)

**Getting buy-in**:
- Lead with the problem, not the solution
- Quantify the cost of inaction
- Start with a small proof of concept
- Address specific concerns of each stakeholder group

## Build vs Buy vs Open Source

### Decision Matrix

| Factor | Build | Buy (SaaS) | Open Source |
|---|---|---|---|
| Time to market | Slow | Fast | Medium |
| Customization | Full | Limited | Moderate |
| Maintenance cost | High | Low (subscription) | Medium |
| Vendor lock-in | None | High | Low |
| Differentiation potential | High | Low | Medium |
| Team expertise needed | High | Low | Medium-High |
| Long-term cost | High upfront, low ongoing | Ongoing subscription | Medium (ops burden) |

### When to Build

- The capability is a core differentiator / competitive advantage
- No existing solution fits the specific domain requirements
- The team has deep expertise and long-term commitment
- Full control over data, performance, and roadmap is needed

### When to Buy

- The capability is a commodity (auth, payments, email, monitoring)
- Speed to market is critical
- The team lacks expertise and has higher-priority work
- The vendor's SLA meets reliability requirements

### When to Use Open Source

- The capability is well-served by mature projects
- The team can support operational complexity
- Customization is needed but not at build-from-scratch level
- Community ecosystem is active and healthy

### Red Flags

- **Build**: Spending > 30% of engineering on non-differentiating infrastructure
- **Buy**: Vendor is the sole source of a critical path with no exit strategy
- **Open source**: Project has < 3 active maintainers or < 6 months of recent activity