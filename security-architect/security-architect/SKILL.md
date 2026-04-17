---
name: security-architect
description: "Security architecture analysis, threat modeling, and architecture review for application systems. Use when: (1) Performing threat modeling with STRIDE/DREAD/attack trees, (2) Reviewing system or application architecture for security flaws, (3) Designing security patterns (defense-in-depth, zero trust, least privilege), (4) Evaluating API security, authentication, authorization, or data protection, (5) Assessing microservices, cloud-native, or web application security, (6) Writing or reviewing security requirements and architecture decision records."
---

# Security Architect

Perform structured security analysis of application architectures: threat modeling, security pattern application, and architecture review.

## Core Capabilities

### 1. Threat Modeling

Systematically identify and rate security threats using established frameworks.

**When a user asks to threat-model a system or component:**

1. Determine scope — what system, what boundaries
2. Read [threat-modeling.md](references/threat-modeling.md) for framework details
3. Build a data flow diagram identifying trust boundaries
4. Apply STRIDE to each trust boundary crossing
5. Score threats with DREAD, prioritize by composite risk
6. Map threats to mitigations using security patterns

**Deliverables:** Data flow diagram, threat list with STRIDE categories, DREAD scores, and prioritized mitigations.

### 2. Architecture Review

Review existing or proposed architectures for security weaknesses.

**When a user asks to review an architecture or design:**

1. Understand the architecture — components, data flows, trust boundaries
2. Select applicable checklists from [architecture-review.md](references/architecture-review.md)
3. Walk through each relevant checklist section
4. Scan for security anti-patterns (see [architecture-review.md](references/architecture-review.md) → Security Anti-Patterns)
5. Rate findings using the risk matrix
6. Provide specific, actionable remediation mapped to security patterns

**Deliverables:** Prioritized list of findings with severity, business impact, and remediation path.

### 3. Security Pattern Application

Recommend and apply established security patterns to design or harden systems.

**When a user asks about security design, hardening, or pattern selection:**

1. Identify the threat or requirement being addressed
2. Read [security-patterns.md](references/security-patterns.md) for pattern catalog
3. Select the appropriate pattern based on context (see Pattern-to-Threat Mapping)
4. Provide concrete implementation guidance for the user's tech stack
5. Explain how the pattern integrates with defense-in-depth

**Deliverables:** Pattern recommendation with implementation specifics for the target stack.

## Workflow

Determine the task type, then follow the appropriate capability workflow above.

```
User request
├── Threat model? → Capability 1 (Threat Modeling)
├── Architecture review? → Capability 2 (Architecture Review)
├── Security design/hardening? → Capability 3 (Security Patterns)
└── General security question? → Assess which capability applies, combine as needed
```

Always read the relevant reference file before producing analysis. The references contain the detailed frameworks, checklists, and pattern catalogs.

## Output Format

Use this structure for all security analysis outputs:

```markdown
# [Analysis Title]

## Executive summary
[1-2 sentences: highest-risk finding and most important action]

## Findings
| # | Finding | Category | Severity | Status |
|---|---------|----------|----------|--------|
| 1 | [finding] | STRIDE category | Critical/High/Medium/Low | Open/Mitigated |

## Details
### Finding 1: [Title]
- **Threat category**: [STRIDE category]
- **Description**: [what the threat is]
- **Risk**: [DREAD composite score and justification]
- **Mitigation**: [specific pattern or control from security-patterns.md]
- **Implementation**: [concrete steps for the user's stack]

## Recommendations
1. [Priority-ordered list of actions]
```

## Key Principles

- **Default-deny**: Recommend denying access by default, allowing explicitly
- **Specific over generic**: Provide concrete implementation guidance, not general advice
- **Risk-based**: Prioritize findings by likelihood × impact, not by count
- **Context-aware**: Tailor recommendations to the user's tech stack and constraints
- **Defense-in-depth**: Never rely on a single control — always recommend layered defenses