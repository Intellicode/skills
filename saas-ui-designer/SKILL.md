---
name: saas-ui-designer
description: "Create clean, user-friendly SaaS application UI designs in HTML and CSS. Use when Codex needs to design or implement SaaS dashboards, admin panels, productivity tools, collaboration apps, cloud consoles, file managers, docs/editors, email clients, commerce back offices, deployment platforms, settings pages, billing flows, onboarding, empty states, or dense operational interfaces inspired by products such as Dropbox, Gmail, Google Docs, Google Cloud, Vercel, Netlify, Shopify, Linear, Stripe, and Notion. Covers information architecture, responsive layouts, navigation, tables, forms, command bars, component states, visual hierarchy, accessibility, and polished production-quality HTML prototypes."
---

# SaaS UI Designer

Design and implement polished SaaS application interfaces in HTML/CSS. Prioritize product usability, clarity, responsiveness, and realistic workflow coverage over marketing-style presentation.

## Workflow

1. Identify the product category, primary user, core workflow, and information density.
2. Choose an app shell before styling: sidebar, top nav, split pane, canvas/editor, inbox, table workspace, or console.
3. Build the first screen as the actual working product surface, not a landing page.
4. Use the template in `assets/saas-html-template/` when starting a standalone HTML prototype.
5. Load references only as needed:
   - `references/interface-patterns.md` for SaaS layout and component patterns.
   - `references/visual-system.md` for typography, spacing, color, density, and polish.
   - `references/quality-checklist.md` before final verification.
6. Verify at desktop and mobile widths that text fits, controls are reachable, empty/loading/error states exist where relevant, and layout does not overlap.

## Design Rules

- Make the app useful immediately: show real controls, realistic data, states, filters, and actions a SaaS user would expect.
- Keep styling quiet and work-focused: restrained color, crisp borders, subtle shadows, strong alignment, and clear hierarchy.
- Avoid hero sections, decorative cards, gradient blobs, oversized typography, and marketing copy unless the user explicitly asks for a landing page.
- Do not put cards inside cards. Use cards for repeated objects, modals, and framed tools; use full-width bands or unframed layouts for page structure.
- Use icons for tool actions when the project has an icon set. Pair icons with text for ambiguous primary commands.
- Use tables, lists, split panes, tabs, sidebars, command bars, inspectors, breadcrumbs, search, filters, and bulk actions where they match the workflow.
- Design all states: default, hover, focus, selected, disabled, loading, empty, error, success, and destructive confirmation.
- Prefer compact controls and dense-but-readable spacing for operational tools. Reserve large display type for true product-level headings.
- Keep accessibility built in: semantic landmarks, keyboard-visible focus, labels, contrast, non-color status cues, and responsive touch targets.

## HTML Implementation Guidance

- Start with semantic HTML and CSS custom properties before adding JavaScript.
- Use stable dimensions for app shells, sidebars, toolbars, tables, grids, and tiles so hover labels or dynamic values do not shift layout.
- Use responsive constraints: `minmax()`, `clamp()` for container sizes, `aspect-ratio`, `overflow-wrap`, and `min-width: 0` inside flex/grid children.
- Do not scale font size with viewport width. Use fixed type tokens that adapt by breakpoint only when necessary.
- Keep letter spacing at `0` unless matching an existing design system.
- Ensure buttons, badges, and table cells can handle long labels by wrapping, truncating with tooltips, or widening predictably.
- Use real-looking but fake data: names, file titles, timestamps, metrics, statuses, and permissions that reveal the product workflow.

## Product Patterns

- Dropbox-style file tools: sidebar, file table/grid toggle, breadcrumbs, sharing state, sync status, preview/details pane, upload/create actions.
- Gmail-style inbox tools: folder sidebar, searchable message list, reading pane, labels, bulk selection, archive/snooze/move controls.
- Google Docs-style editors: top app bar, document title, toolbar, comments/activity panel, collaborator presence, canvas/editor surface.
- Cloud consoles: project switcher, resource navigation, metrics cards, logs/table view, filters, region/status badges, create/configure flows.
- Vercel/Netlify-style deployment apps: project list, deployment timeline, build logs, environment badges, domain settings, rollback controls.
- Shopify-style commerce back offices: order/product/customer tables, filters, saved views, status chips, bulk actions, side panels.

## Assets

Use `assets/saas-html-template/` as a copyable starter for standalone HTML SaaS prototypes:

- `index.html` contains an app shell with sidebar, top bar, KPI strip, command bar, table, detail panel, and responsive mobile behavior.
- `styles.css` contains neutral SaaS design tokens, layout primitives, controls, states, and responsive rules.

Adapt the template to the requested product instead of treating it as a fixed dashboard.
