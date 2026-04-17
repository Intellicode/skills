# Prototyping

## Table of Contents

- [Fidelity Selection](#fidelity-selection)
- [Wireframing](#wireframing)
- [Interaction Design](#interaction-design)
- [Prototyping Approaches](#prototyping-approaches)
- [Design Handoff](#design-handoff)

## Fidelity Selection

Choose prototype fidelity based on what you need to learn:

| Fidelity | Best For | Time Investment | When to Use |
|----------|----------|-----------------|-------------|
| **Paper** | Concept validation, early flow testing | Minutes | Can you explain the idea? Does the flow make sense? |
| **Low-fidelity digital** | Layout, navigation, content hierarchy | Hours | What goes where? Does the structure work? |
| **Mid-fidelity** | Task completion, information architecture, terminology | Hours to a day | Can users complete key tasks? Is the language clear? |
| **High-fidelity** | Visual design, microinteractions, emotional response | Days | Does this feel right? How do people respond to the aesthetic? |
| **Code prototype** | Performance, edge cases, real data, technical feasibility | Days | Does this work at scale? What breaks with real data? |

**Rule of thumb:** Use the lowest fidelity that can answer your question. Every pixel of polish is time you can't get back if the concept is wrong.

### Fidelity Decision Tree

1. Are you testing whether the concept itself makes sense? → Paper/low-fi
2. Are you testing whether users can complete tasks? → Mid-fi
3. Are you testing whether it feels polished and trustworthy? → High-fi
4. Are you testing technical feasibility with real data? → Code

## Wireframing

### Principles

- **Content precedes layout.** Know what needs to be on the screen before deciding where it goes.
- **One screen, one primary action.** Every screen should have a clear call to action.
- **Progressive disclosure.** Show only what's needed. Reveal complexity on demand.
- **Consistent patterns.** Use the same component for the same function everywhere.
- **Show, don't tell.** Wireframes communicate structure; copy communicates intent.

### Screen Types

| Type | Purpose | Key Elements |
|------|---------|--------------|
| **Landing/Home** | Orient users, provide entry points | Value proposition, primary actions, navigation |
| **List/Index** | Browse and scan items | Search, filters, sort, item previews |
| **Detail** | Deep dive on one item | Metadata, content, actions, related items |
| **Form** | Input or edit data | Labels, validation, clear submit, error states |
| **Dashboard** | Monitor and act on data | Key metrics, status indicators, actionable alerts |
| **Flow/Process** | Multi-step task | Progress indicator, back/forward, clear steps |

### Wireframe Annotations

Annotate wireframes with:
- **Content source:** Where data comes from (API, user input, default)
- **States:** Default, loading, empty, error, success
- **Interactions:** What happens on tap/click/hover
- **Constraints:** Responsive behavior, character limits, image ratios

### Information Architecture

Before wireframing individual screens, define the structure:

**Navigation depth rule:** Any page reachable in 3 clicks or fewer. If deeper, restructure.

**Card sorting for IA:**
1. List all content/functionality items (20-50 items)
2. Have users group them into categories that make sense
3. Look for patterns across participants
4. Test the resulting structure with tree testing

### Common Flow Patterns

| Flow | Pattern | When to Use |
|------|---------|-------------|
| **Onboarding** | Progressive disclosure + skip | First-time users. Show value before asking for effort. |
| **Search → Filter → Results** | Faceted search | Large content sets. Let users narrow progressively. |
| **Create/Submit** | Wizards for complex, single-page for simple | Complex data: break into steps. Simple: one form. |
| **Approval/Review** | Status → Action → Confirmation | Asynchronous workflows. Clear status and next action. |

## Interaction Design

### Feedback Principles

Every user action should produce a visible response within:

| Action Type | Response Time | Feedback |
|-------------|---------------|----------|
| Button tap | < 100ms | Visual state change |
| Screen transition | < 300ms | Animation |
| Network request | Show progress within 1000ms | Skeleton, spinner, progress bar |
| Uncertain operation | Indeterminate | Optimistic UI with undo |

### Error Handling

- **Prevent errors** over showing messages. Constraints, defaults, auto-formatting.
- **When errors happen:** Explain what went wrong, why, and how to fix it. In plain language.
- **Validation timing:** Validate inline (on blur) for immediate feedback. Validate on submit for final check.
- **Error message template:** `[What happened]. [Why]. [What to do next.]`
  - Bad: "Invalid input"
  - Good: "Username must be at least 8 characters. Try adding more characters."

### Loading States

| State | When | Pattern |
|-------|------|---------|
| Initial load | First time content appears | Skeleton screen |
| Action in progress | Button tap, form submit | Button state change + spinner |
| Background refresh | Feed, dashboard, list | Pull-to-refresh, silent reload |
| Long operation | > 3 seconds | Progress bar, percentage |

### Accessibility Checklist

- Color contrast: WCAG AA minimum (4.5:1 for text, 3:1 for large text)
- Don't convey information by color alone — use icons, patterns, or labels
- All interactive elements reachable by keyboard
- Focus order matches visual order
- Alt text on images, ARIA labels on icons
- Touch targets: minimum 44x44px (mobile), 24x24px (desktop)
- Support screen readers: semantic HTML, ARIA landmarks, proper heading hierarchy

## Prototyping Approaches

### Paper Prototyping

Best for early-stage concept validation.

**When to use:** Testing core concept, flow, or terminology before any digital work.

**Materials:** Paper, markers, sticky notes, scissors. Optionally: printed device frames.

**Process:**
1. Sketch each screen on a separate sheet
2. Cut interactive elements (dropdowns, modals) as overlays
3. Have a "computer" who swaps screens based on user actions
4. Another person moderates and takes notes
5. User points and speaks their intent out loud

### Clickable Wireframes

Best for testing navigation, flow, and task completion.

**Tools:** Figma, Sketch + InVision, Balsamiq

**Process:**
1. Create all key screens at mid-fidelity
2. Link screens with hotspots for main flows
3. Include error and empty states
4. Test with 5 users on core tasks
5. Iterate on the top 2-3 issues before re-testing

### Interactive Prototypes

Best for testing interactions, transitions, and emotional response.

**When to use:** Validating specific interactions (drag-and-drop, gestures, animations) that static screens can't demonstrate.

**Approaches:**
- **Figma prototyping** — Good for most interfaces. Supports conditional logic, variables, component states.
- **Principle/Framer** — Complex animations and microinteractions. Higher learning curve.
- **Code prototypes** — When you need real data, API integration, or performance testing.

### Prototype Scope

**Scope for testing:**
- Test 3-5 core tasks per session, not the entire product
- Each task should map to a specific research question
- Include the happy path and 1-2 edge cases
- Don't prototype features you're not testing

## Design Handoff

### What Engineers Need

- **All states:** Default, hover, active, focus, disabled, loading, empty, error
- **Responsive behavior:** Breakpoint-specific layouts, overflow handling
- **Spacing system:** Consistent values (4px or 8px grid)
- **Typography scale:** Font sizes, weights, line heights for each heading/body style
- **Color tokens:** Semantic names (e.g., `color-text-primary`, `color-surface-error`), not hex values
- **Interaction specs:** Animations (duration, easing), transitions, scroll behavior
- **Content guidelines:** Character limits, truncation rules, pluralization
- **Accessibility notes:** ARIA roles, keyboard behavior, focus management

### Handoff Format

Organize handoff by component, not by screen:

1. **Component catalog** — Every UI component with all states and variations
2. **Page layouts** — How components compose into pages, with spacing and responsive rules
3. **Flows** — End-to-end user flows with decision points and error paths
4. **Content specs** — Copy guidelines, character limits, variable content handling
5. **Assets** — Icons, images, illustration files in appropriate formats