# User Story Template

## Story Format

**As a** [persona] **I want to** [action] **so that** [benefit]

---

## Story Card

### Identification
- **Story ID**: [PROJECT-###]
- **Title**: [Brief descriptive title]
- **Epic**: [Parent epic name]
- **Priority**: P0 | P1 | P2
- **Story Points**: [1, 2, 3, 5, 8, 13]

### Description

**As a** [persona],
**I want to** [action],
**So that** [benefit/value].

### Context & Motivation

[Why this story matters. What user problem it solves. Business context.]

### Acceptance Criteria

See [acceptance-criteria-template.md](acceptance-criteria-template.md) for detailed format.

1. Given [context], When [action], Then [expected result]
2. Given [context], When [action], Then [expected result]
3. Given [context], When [action], Then [expected result]

### Design Specifications

[Link or reference to design deliverables. Required before engineering starts.]

- Wireframes:
- Prototypes:
- Interaction specs:

### Technical Notes

[Engineering and architecture considerations.]

- Affected components:
- API changes:
- Database changes:
- Dependencies on other stories:

### Security Checklist

[Required for stories involving data, auth, permissions, or external integrations.]

- [ ] Data classification reviewed
- [ ] Authentication/authorization requirements defined
- [ ] Input validation strategy defined
- [ ] No sensitive data in logs/URLs

### Out of Scope

- [Explicitly excluded items]

### Definition of Done

- [ ] Acceptance criteria met
- [ ] Design review completed (Product Designer sign-off)
- [ ] Code review completed
- [ ] Security review completed (if applicable)
- [ ] Architecture review completed (if applicable)
- [ ] Tests pass (unit, integration, E2E)
- [ ] Documentation updated (if applicable)

---

## Story Writing Guidelines

### INVEST Criteria

Every story should satisfy INVEST:

- **I**ndependent — Can be delivered without dependencies on other stories
- **N**egotiable — Details can be discussed and refined
- **V**aluable — Delivers clear value to users or business
- **E**stimable — Team can estimate effort required
- **S**mall — Completable within a sprint
- **T**estable — Has clear acceptance criteria

### Priority Guidelines

| Priority | Meaning |
|----------|---------|
| P0 | Must have. Product does not function without it. |
| P1 | Should have. Significant value, planned for current release. |
| P2 | Nice to have. Planned for future release. |

### Story Sizing Reference

| Points | Effort | Example |
|--------|--------|---------|
| 1 | Trivial | Text change, config update |
| 2 | Small | Simple UI component, minor API endpoint |
| 3 | Medium | Feature with interacting parts, moderate complexity |
| 5 | Large | Multi-component feature, integration work |
| 8 | Very Large | Consider splitting into smaller stories |
| 13 | Epic | Must be broken down into smaller stories |