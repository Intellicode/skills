# Architectural Patterns

## Table of Contents

- [Monolithic Architecture](#monolithic-architecture)
- [Microservices](#microservices)
- [Event-Driven Architecture](#event-driven-architecture)
- [CQRS](#cqrs)
- [Event Sourcing](#event-sourcing)
- [Layered Architecture](#layered-architecture)
- [Hexagonal Architecture](#hexagonal-architecture)
- [Serverless](#serverless)
- [Plugin Architecture](#plugin-architecture)
- [Space-Based Architecture](#space-based-architecture)
- [Pattern Selection Guide](#pattern-selection-guide)

## Monolithic Architecture

**What**: Single deployable unit containing all application logic.

**When to use**:
- Small team (1-5 developers)
- Early-stage product / MVP
- Simple domain with clear boundaries
- Time-to-market is critical
- Deployment coordination overhead is unacceptable

**Strengths**: Simple deployment, easy debugging, no distributed complexity, low operational overhead
**Weaknesses**: Scaling bottlenecks, tight coupling over time, deploy everything to change one thing, harder to adopt new tech

**Warning signs**: Monolith should be split when deploys become risky (many people shipping to same codebase), scaling requires entire app (not just hot paths), or team coordination overhead dominates.

## Microservices

**What**: Independently deployable services organized around business capabilities.

**When to use**:
- Multiple teams (5+ per service)
- Domain boundaries are well-understood
- Independent scaling is needed
- Polyglot technology requirements
- High availability requirements per domain

**Strengths**: Independent deployment, fault isolation, per-service scaling, team autonomy
**Weaknesses**: Distributed system complexity, network latency, data consistency challenges, operational overhead, debugging across services

**Key decisions**:
- Service boundaries: Align with bounded contexts, not technical layers
- Communication: Prefer async (events) over sync (REST/gRPC) between services
- Data: Each service owns its data; no shared databases
- Deployment: Each service deploys independently

**Common mistake**: Starting with microservices before understanding the domain. Begin monolithic, extract services at clear boundaries when scaling or team structure demands it.

## Event-Driven Architecture

**What**: Components communicate through asynchronous events rather than direct calls.

**When to use**:
- Loose coupling is critical
- System must react to state changes across domains
- Workflows span multiple services
- Eventual consistency is acceptable
- High throughput, variable processing time

**Strengths**: Decoupling, extensibility (add consumers without modifying producers), temporal decoupling, replay capability
**Weaknesses**: Eventual consistency, debugging complexity, event schema evolution, exactly-once processing challenges

**Patterns**:
- **Event Notification**: Lightweight events signaling that something happened; consumers query back for details
- **Event-Carried State Transfer**: Events include all data consumers need; no query-back required
- **Event Sourcing**: State derived from event log (see separate section)
- **CQRS**: Separate read/write models (see separate section)

## CQRS

**What**: Separate command (write) and query (read) models.

**When to use**:
- Read/write workloads differ significantly
- Complex read patterns with different projection needs
- Event sourcing (CQRS is almost always paired with event sourcing)
- Performance optimization for hot paths

**Strengths**: Optimized reads, scalable read replicas, clean separation of concerns
**Weaknesses**: Complexity (two models to maintain), eventual consistency, sync lag between write and read models

**Implementation note**: Write model is the source of truth. Read models are projections rebuilt from events. Deny access to the write database from read paths.

## Event Sourcing

**What**: Store state as a sequence of events rather than current state.

**When to use**:
- Full audit trail is required (finance, healthcare, legal)
- Temporal queries needed ("what was the state on date X?")
- Complex domain logic that benefits from replay
- Undo/redo functionality needed

**Strengths**: Complete audit trail, temporal queries, replay/debug capability, natural fit for event-driven systems
**Weaknesses**: Event schema evolution, storage growth, eventual consistency, learning curve

## Layered Architecture

**What**: Organize code into horizontal layers (presentation, business, data).

**When to use**:
- Traditional business applications
- Teams accustomed to this pattern
- When simplicity and familiarity matter more than testability

**Strengths**: Simple, well-understood, clear separation per layer
**Weaknesses**: Tendency toward anemic domain models, layers become leaky abstractions, hard to test business logic in isolation

## Hexagonal Architecture (Ports & Adapters)

**What**: Core business logic isolated from external concerns via ports (interfaces) and adapters (implementations).

**When to use**:
- Business logic needs to be testable in isolation
- Multiple input/output channels (REST API, CLI, message consumer)
- Long-lived domain logic that may outlive its current infrastructure
- DDD-focused projects

**Strengths**: Framework-independent domain, easy testing (mock adapters), swap infrastructure without touching domain
**Weaknesses**: More interfaces/abstraction, can feel like over-engineering for simple apps

**Implementation**:
- **Ports**: Interfaces defined by the domain (inbound = driving, outbound = driven)
- **Adapters**: Implementations of ports (REST controller, DB repository, message publisher)
- **Domain**: Pure business logic with no framework or infrastructure imports

## Serverless

**What**: Functions-as-a-Service where compute is provisioned on-demand.

**When to use**:
- Event-driven, intermittent workloads
- Unpredictable or bursty traffic
- Small team with limited ops capacity
- Prototyping and rapid iteration

**Strengths**: No infrastructure management, pay-per-use, auto-scaling, fast deployment
**Weaknesses**: Cold starts, execution time limits, vendor lock-in, debugging/distributed tracing challenges, cost unpredictability at scale

## Plugin Architecture

**What**: Core system with extensible plugin/modules that add functionality.

**When to use**:
- Platform or extensible tool building
- Need third-party extensibility
- Core feature set varies by deployment/customer
- IDEs, build tools, CMS platforms

**Strengths**: Extensibility, open-closed principle, community ecosystem potential
**Weaknesses**: Plugin API stability burden, versioning complexity, security surface area

## Space-Based Architecture

**What**: In-memory data grids and processing units that avoid database bottlenecks.

**When to use**:
- High-volume, low-latency requirements
- Variable/unpredictable load patterns
- Real-time systems (trading, gaming, IoT)
- Database is the bottleneck

**Strengths**: Eliminates database bottleneck, near-linear scalability, high availability
**Weaknesses**: Complexity, data consistency challenges, memory cost, hard to debug

## Pattern Selection Guide

| Signal | Pattern |
|---|---|
| Small team, early product | Monolith |
| Clear domain boundaries, multiple teams | Microservices |
| Need loose coupling between domains | Event-Driven |
| Read/write workload divergence | CQRS |
| Full audit trail required | Event Sourcing + CQRS |
| Framework-independent domain logic | Hexagonal |
| Intermittent, event-driven workloads | Serverless |
| Extensibility platform | Plugin |
| Ultra-low latency, high throughput | Space-Based |

**Common progressions**:
1. **Monolith → Microservices**: Start monolithic, extract services when team scale or deployment independence demands it
2. **Monolith + Event-Driven**: Add event bus to monolith before extracting services; establishes async communication patterns early
3. **Hexagonal + Event Sourcing**: Use hexagonal for domain isolation, event sourcing for audit and replay
4. **Serverless + Event-Driven**: Natural pairing for intermittent, event-driven workloads