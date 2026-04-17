---
name: software-architect
description: "Software architecture design, decision-making, and planning. Use when: (1) Designing system architecture or selecting architectural patterns, (2) Evaluating technology choices (databases, languages, frameworks, messaging), (3) Planning migrations or refactoring, (4) Writing Architecture Decision Records (ADRs), (5) Analyzing trade-offs between architectural approaches, (6) Structuring code at the module/service level, (7) Reviewing or improving existing architecture, (8) Discussing scalability, reliability, or performance architecture."
---

# Software Architect

Guide architectural decisions with structured frameworks, pattern catalogs, and trade-off analysis. Optimized for producing clear, documented decisions rather than theoretical pontification.

## Workflow

1. **Understand constraints** — Identify business context, team size, timeline, existing systems, and hard requirements before proposing solutions.
2. **Classify the decision** — Determine whether the question is about structure (patterns, boundaries), technology (databases, runtimes, frameworks), or process (migration, evolution).
3. **Apply relevant framework** — Use the workflows below, then drill into reference files as needed.
4. **Document the decision** — Capture decisions in ADRs. See [decision-frameworks.md](references/decision-frameworks.md) for ADR templates.

## Architecture Design

When designing system architecture:

1. **Map the domain** — Identify bounded contexts, core vs supporting vs generic subdomains
2. **Select pattern** — See [patterns.md](references/patterns.md) for the full catalog and selection guide. Quick reference:

| Signal | Lean Toward |
|---|---|
| Small team, early product | Monolith |
| Multiple teams, clear domain boundaries | Microservices |
| Need loose coupling, async workflows | Event-Driven |
| Read/write workload divergence | CQRS |
| Framework-independent domain | Hexagonal |
| Event-driven, intermittent workloads | Serverless |

3. **Define boundaries** — Services/modules aligned with business capabilities, not technical layers. Each boundary owns its data and deploys independently.
4. **Specify communication** — Prefer async (events) between boundaries. Use sync (REST/gRPC) only for real-time queries within the same boundary.
5. **Plan for evolution** — Start with the simplest architecture that meets current needs. Extract services at clear boundaries when team scale or deployment pressure demands it.

## Technology Selection

When choosing technologies:

1. **Define requirements** — Performance, team expertise, ecosystem, compliance, budget
2. **Identify 2-4 candidates** — Not every option, just realistic contenders
3. **Evaluate with criteria** — See the evaluation matrix in [tech-selection.md](references/tech-selection.md)
4. **Prototype the top 2** — Build a thin slice exercising the critical path
5. **Document in an ADR** — Include alternatives considered and why they fell short

See [tech-selection.md](references/tech-selection.md) for focused selection guides on databases, languages, messaging, API design, infrastructure, and observability.

## Migration & Refactoring

When planning architecture changes:

1. **Assess current state** — Document existing architecture, pain points, and constraints
2. **Define target state** — Use pattern selection to identify the target architecture
3. **Identify the strangler path** — Incrementally replace components, never big-bang rewrite
4. **Prioritize by risk and value** — Migrate the highest-value, lowest-risk piece first
5. **Plan rollback** — Every migration step must be reversible
6. **Validate with fitness functions** — Define measurable success criteria before starting

### Migration Strategies

| Strategy | When to Use |
|---|---|
| Strangler fig | Replacing a monolith incrementally |
| Feature toggle | Deploying new architecture alongside old |
| Parallel run | Running both systems and comparing results |
| CQRS migration | Splitting read/write before extracting a service |
| Anti-corruption layer | Protecting new domain from legacy model |

## Trade-Off Analysis

For any architectural decision, explicitly state trade-offs:

- **What becomes easier?** — Benefits of the chosen approach
- **What becomes harder?** — Costs of the chosen approach
- **What are the risks?** — Failure modes and mitigations
- **How reversible is this?** — One-way door or two-way door?

See [decision-frameworks.md](references/decision-frameworks.md) for structured trade-off matrices, fitness functions, risk assessment, stakeholder alignment, and build-vs-buy frameworks.

## Code Structure

When advising on code organization:

1. **Align structure with architecture** — Module boundaries in code should match service boundaries in architecture
2. **Apply hexagonal architecture** — Keep domain logic free of framework and infrastructure imports. See [patterns.md](references/patterns.md) for hexagonal architecture details.
3. **Enforce boundaries** — Use package structure, access modifiers, or ArchUnit-style tests to prevent boundary violations
4. **Dependencies point inward** — Outer layers depend on inner layers, never the reverse

## Key Principles

- **Start simple, evolve** — Choose the simplest architecture that meets requirements. Refactor when constraints demand it, not in anticipation.
- **Optimize for team velocity** — The best tech choice is usually what the team already knows, unless a hard requirement forces otherwise.
- **Document decisions, not opinions** — Every significant choice gets an ADR with context, alternatives, and consequences.
- **Prefer reversible decisions** — When a decision is easily reversible, decide quickly. When it's a one-way door, analyze carefully.
- **Measure, don't guess** — Define fitness functions for architectural characteristics you care about. Validate assumptions with data.

## References

- **[patterns.md](references/patterns.md)** — Architectural pattern catalog (monolith, microservices, event-driven, CQRS, hexagonal, serverless, etc.) with selection guide
- **[decision-frameworks.md](references/decision-frameworks.md)** — ADR templates, trade-off analysis, fitness functions, risk assessment, stakeholder alignment, build-vs-buy
- **[tech-selection.md](references/tech-selection.md)** — Database selection, language/runtime comparison, messaging, API design, infrastructure, observability