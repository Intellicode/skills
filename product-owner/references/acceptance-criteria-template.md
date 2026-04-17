# Acceptance Criteria Template

## Format: Given/When/Then

Use Behavior-Driven Development (BDD) format for clear, testable criteria.

---

## Acceptance Criteria Types

### 1. Functional Criteria (Required)

Core behavior the feature must exhibit.

**Given** [precondition/context]
**When** [trigger/action]
**Then** [expected outcome]

**Given** [precondition/context]
**When** [trigger/action]
**Then** [expected outcome]

### 2. Non-Functional Criteria

Performance, security, accessibility requirements.

| Category | Criterion | Threshold |
|----------|----------|-----------|
| Performance | [e.g., Page load time] | [< 2 seconds] |
| Accessibility | [e.g., WCAG compliance] | [Level AA] |
| Security | [e.g., Input sanitization] | [All inputs validated] |

### 3. Edge Cases & Error Handling

**Given** [error condition]
**When** [failure action]
**Then** [expected error behavior]

Examples:
- Given user has no network, When attempting save, Then show offline message with retry
- Given invalid input, When form is submitted, Then show inline validation errors
- Given insufficient permissions, When accessing resource, Then show 403 and redirect

### 4. Negative Criteria (What Should NOT Happen)

- The system should NOT [specific behavior to prevent]
- The system should NOT [specific behavior to prevent]

---

## Example: Complete Acceptance Criteria

**Story**: As a returning user, I want to log in with my saved credentials so that I can access my account quickly.

### Functional Criteria

**Given** user has previously saved credentials
**When** user visits the login page
**Then** the email field is pre-filled and the password field shows masked dots

**Given** user has saved credentials displayed
**When** user clicks "Sign In"
**Then** the user is authenticated and redirected to their dashboard within 2 seconds

**Given** user has saved credentials but password has changed on server
**When** user clicks "Sign In"
**Then** show error "Your password has changed. Please enter your current password." and clear the password field

### Non-Functional Criteria

| Category | Criterion | Threshold |
|----------|----------|-----------|
| Performance | Login response time | < 2 seconds |
| Security | Password transmission | TLS 1.2+ only |
| Security | Credential storage | Encrypted at rest, never logged |
| Accessibility | Login form | WCAG 2.1 AA |

### Edge Cases

**Given** user account is locked
**When** user attempts login
**Then** show "Account locked. Contact support." and do NOT reveal lock reason

**Given** more than 5 failed login attempts
**When** user enters incorrect password
**Then** apply rate limiting (lock for 15 minutes) and show generic error message

### Negative Criteria

- System should NOT display whether the email exists (prevents enumeration)
- System should NOT store passwords in plaintext or logs
- System should NOT auto-submit saved credentials without user interaction

---

## Role-Specific Review Checklist

Before acceptance criteria are finalized, verify:

### Product Owner
- [ ] Criteria cover the full user intent, not just the happy path
- [ ] Success is objectively measurable (no "works well" or "looks good")
- [ ] Edge cases include at least: empty state, error state, permission boundaries

### Product Designer
- [ ] UI behavior is specified for each criterion
- [ ] Loading and transition states are covered
- [ ] Accessibility requirements are addressed

### Engineer
- [ ] Each criterion is technically testable
- [ ] API contracts and data states are clear
- [ ] Technical feasibility is confirmed

### Security Architect
- [ ] Data classification for each input/output is defined
- [ ] Authentication and authorization are specified where needed
- [ ] Error messages do not expose sensitive information
- [ ] Input validation rules are explicit

### Software Architect
- [ ] Criteria align with system boundaries and integration contracts
- [ ] Performance thresholds are realistic and measurable
- [ ] Failure modes and recovery paths are addressed