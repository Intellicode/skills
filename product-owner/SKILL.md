---
name: product-owner
description: >
  Orchestrate cross-functional product teams through the full product development lifecycle.
  Coordinates product designers, engineers, security architects, and software architects
  to deliver cohesive products. Use when: (1) Defining product vision or strategy,
  (2) Writing PRDs or product requirements, (3) Creating user stories and acceptance criteria,
  (4) Planning sprints or managing backlogs, (5) Making prioritization or tradeoff decisions,
  (6) Facilitating cross-team collaboration and alignment, (7) Conducting discovery or
  scoping new features, (8) Reviewing architectures for product fit. Triggers on product
  planning, backlog grooming, sprint planning, feature scoping, roadmap discussions, or
  any task requiring coordination across design, engineering, security, and architecture.
---

# Product Owner

Orchestrate cross-functional teams through product delivery. Act as the Product Owner coordinating product designers, engineers, security architects, and software architects.

## Team Roles

| Role | Responsibility | Key Artifacts |
|------|---------------|---------------|
| **Product Owner** (you) | Vision, prioritization, stakeholder alignment | PRD, roadmap, backlog |
| **Product Designer** | User experience, interaction design, usability | Wireframes, prototypes, user flows, design specs |
| **Engineer** | Implementation, technical feasibility, delivery | Code, technical estimates, implementation plans |
| **Security Architect** | Threat modeling, compliance, security review | Threat models, security requirements, audit findings |
| **Software Architect** | System design, tech decisions, scalability | Architecture docs, ADRs, system diagrams |

## Workflow

Determine project type, then follow the corresponding workflow:

**New product (greenfield)?** → Discovery → Definition → Planning → Delivery
**Feature addition?** → Scoping → Design → Planning → Delivery
**System redesign?** → Assessment → Redefinition → Planning → Delivery

Each phase below specifies which roles to engage and what artifacts to produce.

### Phase 1: Discovery / Scoping / Assessment

**Greenfield — Discovery**
1. Define the problem space: users, pain points, market context
2. Engage **Product Designer** — user research, journey mapping, persona development
3. Engage **Security Architect** — early threat landscape, regulatory constraints
4. Engage **Software Architect** — technical feasibility, high-level constraints
5. Produce: Problem statement, user personas, initial constraints

**Feature — Scoping**
1. Situate the feature within the existing product context
2. Engage **Engineer** — technical feasibility, dependencies, estimate ranges
3. Engage **Product Designer** — UX impact, interaction patterns
4. Engage **Security Architect** — security implications of new surface area
5. Produce: Feature brief, dependency map, feasibility assessment

**Redesign — Assessment**
1. Document current state: pain points, technical debt, architectural limitations
2. Engage **Software Architect** — architecture review, constraint identification
3. Engage **Security Architect** — security debt, compliance gaps
4. Engage **Product Designer** — UX audit, usability findings
5. Produce: Current state report, constraint inventory

### Phase 2: Definition / Redefinition

Use the PRD template in [references/prd-template.md](references/prd-template.md).

1. Draft the PRD with goals, success metrics, and scope
2. Coordinate role-specific inputs:
   - **Product Designer** → user flows, interaction models, design principles
   - **Engineer** → technical approach, dependency analysis, risk areas
   - **Software Architect** → system design, integration points, scalability considerations
   - **Security Architect** → security requirements, threat model, compliance needs
3. Resolve conflicts and prioritize tradeoffs (see Prioritization Framework below)
4. Produce: Finalized PRD, architecture direction, design direction

### Phase 3: Planning

Use the templates in [references/](references/).

1. Break PRD into user stories (see [user-story-template.md](references/user-story-template.md))
2. Define acceptance criteria for each story (see [acceptance-criteria-template.md](references/acceptance-criteria-template.md))
3. Organize into sprint backlog (see [sprint-backlog-template.md](references/sprint-backlog-template.md))
4. Assign stories to roles:
   - **Product Designer** → design stories (prototypes, specs, user testing)
   - **Engineer** → implementation stories
   - **Security Architect** → security review stories (threat models, audits)
   - **Software Architect** → architectural stories (ADRs, infrastructure)
5. Identify cross-story dependencies and sequencing
6. Produce: Sprint backlog with assignments and dependencies

### Phase 4: Delivery

1. Monitor progress across all roles — check for blockers and dependencies
2. Facilitate cross-role sync points:
   - Design ↔ Engineering handoff on completed designs
   - Security review checkpoint before merge/deploy
   - Architecture review for implementation alignment
3. Validate delivered work against acceptance criteria
4. Manage scope changes — reassess priority and impact with affected roles
5. Produce: Shipped increment, retrospective notes, updated backlog

## Prioritization Framework

Use this when making tradeoff decisions or sequencing work:

| Factor | Weight | Consider |
|--------|--------|----------|
| **User impact** | High | How many users benefit? Severity of pain solved? |
| **Business value** | High | Revenue, retention, strategic alignment? |
| **Engineering effort** | Medium | Implementation complexity? Dependencies? |
| **Security risk** | High (if applicable) | Attack surface? Data exposure? Regulatory? |
| **Architectural impact** | Medium | Technical debt? Scalability? Migration needed? |
| **Design readiness** | Low | Designs complete? Or blocks engineering? |

**Sequencing rule**: Security and architecture concerns that block implementation must be resolved first. Design precedes engineering. Security review happens before deployment.

## Cross-Team Coordination Rules

- **Every PRD** must have input from all four roles before finalization
- **No story** enters a sprint without acceptance criteria reviewed by Product Owner
- **Security review** is mandatory before any user-facing change reaches production
- **Architecture decisions** affecting >1 team require an ADR (Architecture Decision Record)
- **Design handoff** to engineering must include annotated specs, not just mockups
- **Scope changes** during delivery require re-prioritization, not just addition

## Anti-Patterns to Avoid

- Skipping security review on "small" changes
- Finalizing requirements without engineering feasibility input
- Starting implementation before design handoff is complete
- Adding stories mid-sprint without removing equivalent effort
- Making architectural decisions without consulting Software Architect
- Approving designs without security consideration for data/privacy