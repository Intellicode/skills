# Technology Selection

## Table of Contents

- [Selection Process](#selection-process)
- [Database Selection](#database-selection)
- [Language & Runtime Selection](#language--runtime-selection)
- [Messaging & Event Streaming](#messaging--event-streaming)
- [API Design](#api-design)
- [Infrastructure & Deployment](#infrastructure--deployment)
- [Observability Stack](#observability-stack)
- [Common Anti-Patterns](#common-anti-patterns)

## Selection Process

### Technology Selection Workflow

1. **Define requirements**: Performance, team skills, ecosystem, compliance, budget
2. **Identify candidates**: 2-4 realistic options
3. **Evaluate with criteria matrix** (see below)
4. **Prototype the top 2**: Build a thin slice that exercises the critical path
5. **Decide**: Document in an ADR with trade-offs

### Evaluation Criteria Matrix

| Criterion | Weight | Candidate A | Candidate B | Candidate C |
|---|---|---|---|---|
| Fit for purpose | 5 | /5 | /5 | /5 |
| Team expertise | 4 | /5 | /5 | /5 |
| Ecosystem & community | 4 | /5 | /5 | /5 |
| Performance | 3 | /5 | /5 | /5 |
| Operational complexity | 3 | /5 | /5 | /5 |
| Long-term viability | 4 | /5 | /5 | /5 |
| Cost | 2 | /5 | /5 | /5 |
| **Weighted Total** | | | | |

### Technology Radar Categories

- **Adopt**: Proven, use with confidence
- **Trial**: Promising, use for non-critical paths
- **Assess**: Worth exploring, prototype only
- **Hold**: Avoid for new projects, plan migration away

## Database Selection

### Decision Tree

```
What is the primary data shape?
├── Structured, relational data → Relational (PostgreSQL, MySQL)
│   ├── Need strong consistency? → Relational with ACID
│   └── Need flexible schema? → Relational with JSON columns
├── Document/variable structure → Document (MongoDB, DynamoDB)
│   ├── Need flexible queries? → MongoDB
│   └── Need predictable performance at scale? → DynamoDB
├── Connected data, graph relationships → Graph (Neo4j, Neptune)
├── Time-series data → Time-series (TimescaleDB, InfluxDB)
├── Key-value lookups, high throughput → Key-value (Redis, DynamoDB)
├── Wide column, analytical queries → Columnar (ClickHouse, Cassandra)
│   ├── Need real-time analytics? → ClickHouse
│   └── Need massive write throughput? → Cassandra
└── Full-text search primary → Search (Elasticsearch, Meilisearch)
```

### Selection Criteria

| Database Type | Best For | Avoid When |
|---|---|---|
| PostgreSQL | Complex queries, ACID, diverse workloads | Extreme write throughput (>100k writes/s) |
| MongoDB | Rapid iteration, variable schemas | Strong relational integrity required |
| Redis | Caching, session storage, rate limiting | Complex queries, persistent data store |
| DynamoDB | Predictable scale, serverless workloads | Complex queries, ad-hoc analytics |
| Cassandra | Massive write throughput, multi-region | Strong consistency, complex reads |
| Neo4j | Graph traversal, relationship-heavy queries | Large-volume sequential scans |
| ClickHouse | Analytical queries, log analytics | OLTP, frequent small updates |
| Elasticsearch | Full-text search, log analysis | Primary data store, ACID compliance |

### Data Modeling Principles

- Model read patterns first, then write patterns
- Denormalize for read-heavy, normalize for write-heavy
- Prefer one well-modeled database over polyglot persistence for simple systems
- Choose the database that handles 80% of your queries well; supplement for the remaining 20%
- Index strategy: add indexes for known queries, not speculative ones

## Language & Runtime Selection

### Decision Framework

| Factor | When it matters most |
|---|---|
| Team expertise | Always (productivity > theoretical performance) |
| Ecosystem & libraries | When integrating with many external systems |
| Performance requirements | When latency or throughput is a binding constraint |
| Concurrency model | When handling many simultaneous connections |
| Type safety | When long-term maintainability and large team |
| Time to market | Always, but especially for early-stage products |
| Deployment target | When constrained (embedded, serverless, browser) |

### Language Characteristics

| Language | Strengths | Common For | Weaknesses |
|---|---|---|---|
| TypeScript/JS | Full-stack, fast iteration, large ecosystem | Web apps, APIs, serverless | Type safety (JS legacy), runtime perf |
| Python | ML/data ecosystem, rapid prototyping | Data pipelines, ML APIs, scripts | GIL limits concurrency, runtime perf |
| Go | Concurrency, simple deployment, fast compile | Microservices, CLI tools, infra | Generics maturity, ecosystem depth |
| Java | Mature ecosystem, performance, tooling | Enterprise, Android, large systems | Verbose, slow startup (mitigated by GraalVM) |
| Rust | Memory safety, performance, zero-cost abstractions | Systems, perf-critical paths | Learning curve, slow compile |
| C# | .NET ecosystem, performance, Azure integration | Enterprise, Windows, game dev | Linux/Cloud ecosystem less mature |
| Kotlin | JVM ecosystem, concise, null safety | Android, server-side JVM | Smaller ecosystem than Java |
| Ruby | Developer happiness, fast prototyping | Web apps, scripts | Runtime performance |

### Principle: Optimize for team velocity

The best language for a project is usually the one the team knows best. Only deviate when the team's expertise genuinely can't meet a hard requirement.

## Messaging & Event Streaming

### Selection Guide

| System | Best For | Not Ideal For |
|---|---|---|
| Kafka | High-throughput event streaming, log aggregation, event sourcing | Low-latency request-response, simple pub/sub |
| RabbitMQ | Task queues, pub/sub, request-response patterns | High-throughput streaming, event sourcing |
| SQS/SNS | AWS-native, simple queues, serverless | Multi-cloud, complex routing, ordering guarantees |
| Redis Streams | Lightweight streaming, real-time feeds | Durability requirements, massive scale |
| NATS | Lightweight messaging, microservices request-reply | Event sourcing, durable log |
| Pulsar | Multi-tenant streaming, geo-replication | Simple use cases (overkill) |

### Messaging Pattern Selection

| Need | Pattern | Implementation |
|---|---|---|
| Fire-and-forget notification | Pub/Sub | Kafka topics, SNS, RabbitMQ exchanges |
| Task distribution | Queue/Worker | SQS, RabbitMQ, Redis |
| Request-response over async | RPC over messaging | Reply queues, correlation IDs |
| Event sourcing log | Append-only log | Kafka (compacted topics), EventStoreDB |
| State change notification | Event notification | Lightweight events, consumers query back |
| Data replication | CDC (Change Data Capture) | Debezium, Kafka Connect |

### Key Decisions

- **Ordering**: Do you need per-key ordering? If yes, partition by key. If global ordering isn't needed, avoid single-partition topics.
- **Delivery guarantees**: At-most-once (fast, may lose), at-least-once (common, may duplicate), exactly-once (complex, use idempotent consumers instead)
- **Schema**: Use schema registries for event contracts (Avro, Protobuf, JSON Schema)

## API Design

### Style Selection

| Style | Best For | Trade-offs |
|---|---|---|
| REST | CRUD operations, resource-oriented APIs | Widely understood, but over-fetching/under-fetching |
| GraphQL | Client-driven queries, varied consumers | Flexible but complex, N+1 risk |
| gRPC | Service-to-service, low-latency, strongly typed | Limited browser support, harder to debug |
| WebSocket | Real-time bidirectional (chat, live updates) | Connection management, scaling challenges |
| AsyncAPI (event-driven) | Decoupled services, event notification | Eventual consistency, schema evolution |

### API Versioning Strategies

| Strategy | How | When to Use |
|---|---|---|
| URL path | `/v1/resource` | Most common, explicit, easy routing |
| Header | `Accept: application/vnd.api.v2+json` | Clean URLs, more complex routing |
| Query param | `?version=2` | Simple, but less RESTful |
| Content negotiation | `Content-Type` header | REST purist approach |

**Principle**: Default to URL path versioning. Only consider alternatives when URL versioning creates specific problems.

## Infrastructure & Deployment

### Container Orchestration Decision

| Scale | Recommendation |
|---|---|
| < 5 services | Docker Compose (dev), single host (prod) or managed containers |
| 5-20 services | Managed Kubernetes (EKS, GKE, AKS) or managed containers (ECS, Cloud Run) |
| 20+ services | Managed Kubernetes with GitOps (ArgoCD, Flux) |

### Deployment Strategy Selection

| Strategy | Risk Level | When to Use |
|---|---|---|
| Rolling update | Low | Most deployments, no DB changes |
| Blue-green | Medium | When instant rollback is needed |
| Canary | Low | High-traffic services, gradual validation |
| Feature flags | Low | Decoupling deploy from release, A/B testing |

### CI/CD Pipeline Essentials

```
Commit → Lint/Type-check → Unit Tests → Build → Integration Tests 
  → Security Scan → Deploy to Staging → Smoke Tests → Deploy to Prod
```

**Key principles**:
- Every commit should be deployable (trunk-based development)
- Pipeline failures block the merge, not prod
- Deploy to staging automatically, prod requires gating
- Smoke tests must run against deployed environment

## Observability Stack

### The Three Pillars

| Pillar | Purpose | Tools |
|---|---|---|
| Metrics | Quantitative system health | Prometheus, Datadog, CloudWatch |
| Logs | Discrete event records | ELK, Loki, CloudWatch Logs |
| Traces | Request flow across services | Jaeger, Zipkin, Datadog, X-Ray |

### What to Instrument

**Always**:
- Request rate, error rate, latency (RED method for services)
- CPU, memory, disk, network (USE method for resources)
- Deployment markers

**Conditionally**:
- Business metrics (orders/min, revenue, conversion rate)
- Custom application metrics
- Detailed trace spans for critical paths

### Dashboard Hierarchy

1. **System overview**: Health of all services at a glance
2. **Service-level**: Single service deep dive
3. **Business-level**: Business KPIs and user-facing metrics
4. **Debug views**: Detailed logs, traces, and metrics for troubleshooting

## Common Anti-Patterns

| Anti-Pattern | Description | Fix |
|---|---|---|
| Golden hammer | Using familiar tech for every problem | Evaluate at least 2 alternatives before choosing |
| Resume-driven development | Choosing tech for career appeal | Optimize for team and project, not individual resumes |
| Distributed monolith | Microservices with monolithic coupling | Enforce bounded contexts and independent deployability |
| Premature optimization | Optimizing before measuring | Profile first, optimize bottlenecks |
| Architecture astronautics | Over-abstracting before understanding domain | Start simple, refactor when patterns emerge |
| Not invented here | Rebuilding what exists | Default to established solutions for commodity problems |
| Shiny object syndrome | Chasing new tech without evaluating fit | Apply the selection process above |
| Yin-yang programmer | Designing for extensibility that never comes | Build for today's requirements with clear extension points |
| Big design up front | Months of design before any code | Iterative architecture: design, build, validate, iterate |