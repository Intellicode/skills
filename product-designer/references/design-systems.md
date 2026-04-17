# Design Systems

## Table of Contents

- [When to Invest](#when-to-invest)
- [System Architecture](#system-architecture)
- [Design Tokens](#design-tokens)
- [Component Design](#component-design)
- [Documentation Standards](#documentation-standards)
- [Governance](#governance)

## When to Invest

A design system is justified when the cost of inconsistency exceeds the cost of governance.

**Build a design system when:**
- 3+ designers or 5+ engineers work on the same product
- Inconsistent UI patterns proliferate across screens
- Design-to-development handoff takes longer than design itself
- New team members take >2 weeks to become productive with the UI layer

**Don't build a design system when:**
- There's one designer and <5 engineers — the overhead exceeds the benefit
- The product hasn't found product-market fit — premature consistency locks in wrong patterns
- You can adopt an existing system (Material, Ant Design, Radix, shadcn) instead

**Start with a component library first.** Graduate to a full design system when you have stable patterns and organizational buy-in.

## System Architecture

### Layers

```
┌─────────────────────────────┐
│        Product Screens       │  ← Specific layouts, compositions
├─────────────────────────────┤
│        Patterns              │  ← Page templates, layouts, flows
├─────────────────────────────┤
│        Components            │  ← Buttons, cards, forms, modals
├─────────────────────────────┤
│        Design Tokens         │  ← Colors, spacing, typography, motion
└─────────────────────────────┘
```

Each layer depends only on layers below it. Product screens use patterns and components. Components use tokens. Tokens stand alone.

### File Organization

```
design-system/
├── tokens/
│   ├── color.json
│   ├── spacing.json
│   ├── typography.json
│   └── motion.json
├── primitives/          (atomic elements)
│   ├── button/
│   ├── input/
│   ├── icon/
│   └── text/
├── components/          (composites)
│   ├── card/
│   ├── dialog/
│   ├── dropdown/
│   ├── form-field/
│   └── toast/
├── patterns/            (page-level)
│   ├── form-layout/
│   ├── data-table/
│   ├── empty-state/
│   └── navigation/
└── docs/
    ├── getting-started.md
    ├── contributing.md
    └── principles.md
```

## Design Tokens

### Token Structure

Use a three-tier token system:

1. **Global tokens** — Raw values. The source of truth for all design decisions.
   ```
   color-blue-500: #3B82F6
   spacing-4: 1rem
   font-size-lg: 1.125rem
   ```

2. **Alias tokens** — Semantic mappings. Connect global tokens to meaning.
   ```
   color-primary: color-blue-500
   color-text-default: color-gray-900
   spacing-component-gap: spacing-4
   ```

3. **Component tokens** — Specific use within a component. Enables theme overrides per component.
   ```
   button-color-bg: color-primary
   button-color-text: color-white
   button-spacing-padding: spacing-component-gap
   ```

### Token Categories

| Category | Examples | Notes |
|----------|----------|-------|
| **Color** | Primary, text, background, border, state colors | Define full palette + semantic aliases |
| **Spacing** | Page margin, component gap, element padding | Use a consistent scale (4px or 8px) |
| **Typography** | Font family, size, weight, line-height, letter-spacing | Define a type scale, not arbitrary sizes |
| **Motion** | Duration, easing | Short (100ms), medium (200ms), long (300ms) |
| **Border** | Radius, width, color | Consistent radius scale (2, 4, 8, 12, 16px) |
| **Shadow** | Elevation levels | Small (cards), medium (dropdowns), large (modals) |
| **Breakpoint** | Responsive thresholds | Align with common devices (640, 768, 1024, 1280px) |
| **Z-index** | Layer stacking | Dropdown (100), sticky (200), modal (300), toast (400) |

### Dark Mode Strategy

Use alias tokens to support theming:

1. Define global tokens per theme (light + dark)
2. Alias tokens reference different global tokens per theme
3. Components reference alias tokens, never global tokens

```
// Light
color-surface-default: color-white
color-text-default: color-gray-900

// Dark
color-surface-default: color-gray-900
color-text-default: color-gray-50
```

Components never change — only the alias-to-global mapping changes.

## Component Design

### Component Anatomy

Every component should define:

| Aspect | Description | Example |
|--------|-------------|---------|
| **Variants** | Visual variations | Primary, secondary, ghost, danger |
| **States** | Interactive states | Default, hover, focus, active, disabled, loading |
| **Sizes** | Dimension options | Small, medium, large |
| **Content** | What goes inside | Label (required), icon (optional), badge (optional) |
| **Behavior** | Interaction model | Click, long-press, keyboard activation |
| **Constraints** | Rules and limits | Max label length, icon size bounds |

### Component API Design Principles

- **Composable over monolithic.** Provide building blocks, not pre-assembled meals. `<Button>` + `<Icon>`, not `<IconButton>`.
- **Explicit over implicit.** Props should be clear. `variant="secondary"`, not `type="2"`.
- **Sensible defaults.** The common case should require minimal configuration. Override only for variations.
- **Consistent naming.** Use the same prop names across components: `size`, `variant`, `color`, `disabled`.

### Mandatory Component Variants

Every interactive component needs these states documented:

1. **Default** — Standard appearance
2. **Hover** — Mouse over (desktop only)
3. **Focus** — Keyboard navigation indicator
4. **Active/Pressed** — Currently being pressed
5. **Disabled** — Not interactive, grayed out
6. **Loading** — Action in progress (for buttons, forms)
7. **Error** — Validation failure (for inputs)

### Component Documentation

Each component needs:

1. **When to use / when not to use** — Prevents misuse
2. **All variants and states** — Visual reference
3. **Accessible usage** — Keyboard behavior, ARIA roles, screen reader text
4. **Design rationale** — Why it exists, what problem it solves
5. **Content guidelines** — Label character limits, truncation rules
6. **Related components** — Links to similar components with guidance on when to use which

Example:
```
# Button

## When to use
- Primary actions on a page
- Form submissions
- Navigation CTAs

## When not to use
- Navigation within a page (use Link)
- Toggling a setting (use Toggle)
- Opening a menu (use MenuButton)
```

## Documentation Standards

### Choosing What to Document

Document patterns that teams get wrong, not everything they get right. Prioritize:

1. **High-usage components** (used on 5+ screens)
2. **Frequently misused components** (wrong variant, wrong context)
3. **Complex components** (many variants, states, or edge cases)
4. **Cross-team components** (shared by 2+ teams)

### Writing Component Docs

Follow this structure:

1. **Name and purpose** (1 sentence)
2. **When to use / when not to use** (prevents misuse)
3. **Visual reference** (all variants and states)
4. **Props/API table** (every option, type, default, required status)
5. **Accessibility** (keyboard behavior, ARIA, screen reader guidance)
6. **Content guidelines** (labels, character limits, internationalization)
7. **Examples** (common patterns, do/don't pairs)
8. **Related components** (links to alternatives with usage guidance)

### Do/Don't Patterns

For each component, include at least 3 do/don't pairs showing common mistakes:

```
✅ DO: Use "Delete account" for destructive actions
❌ DON'T: Use "Delete account" for reversible actions

✅ DO: Place primary action on the right
❌ DON'T: Place primary action on the left (breaks convention)
```

## Governance

### Contribution Model

Choose based on team size and maturity:

| Model | Best For | Process |
|-------|----------|---------|
| **Centralized** | Small design system team, many consumers | All changes go through the system team |
| **Federated** | Multiple product teams, moderate maturity | Any team can propose, system team reviews and merges |
| **Hybrid** | Large org, mature system | Core components are centralized, product-specific patterns are federated |

### Change Management

1. **RFC process for new components** — Propose → Discuss → Approve → Build
2. **Deprecation policy** — Announce → Soft deprecate (warnings) → Hard deprecate (removal) over 2+ release cycles
3. **Versioning** — Semantic versioning. Breaking changes = major, new features = minor, fixes = patch
4. **Changelog** — Every release lists changes with migration guidance

### Measuring Success

Track these metrics:

| Metric | Target | Measurement |
|--------|--------|-------------|
| Adoption rate | % of product screens using system components | Audit UI inventory quarterly |
| Contribution rate | Components contributed by product teams | Track per quarter |
| Consistency score | % of screens following design system | Audit quarterly |
| Time to build new screen | Hours from spec to implemented | Track per project |
| Defect rate | UI bugs per release | Track per sprint |

### Maintenance Cadence

| Activity | Frequency | Owner |
|----------|-----------|-------|
| Bug fixes | As needed | System team |
| New components | Per RFC process | Proposing team + system team |
| Token updates | Monthly | System team |
| Full audit | Quarterly | Design + engineering leads |
| Breaking changes | Bi-annually max | System team |