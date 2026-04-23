---
name: accessible-web-design
description: "Build highly accessible, usable websites and web applications inspired by the GOV.UK Design System. Use when: (1) Creating new web pages, forms, or services that must meet WCAG 2.2 AA, (2) Building public-sector, government, or citizen-facing digital services, (3) Designing interfaces prioritizing clarity, inclusivity, and usability over visual flair, (4) Implementing accessible components such as error summaries, skip links, focus indicators, or semantic form patterns, (5) Reviewing or retrofitting existing pages for accessibility compliance, (6) The user asks for clean, simple, highly usable, or accessible web design. Covers semantic HTML, typography, spacing, colour contrast, keyboard navigation, screen reader support, and GOV.UK-proven interaction patterns."
---

# Accessible Web Design

Build web pages and services that are accessible, clear, and usable for everyone. This skill follows principles from the GOV.UK Design System: semantic HTML first, high contrast, generous spacing, explicit labels, and one-thing-per-page workflows.

## Workflow

1. Start from the HTML/CSS template in `assets/accessible-template/`
2. Apply design tokens from `references/design-tokens.md`
3. Build components using patterns from `references/component-patterns.md`
4. Validate against `references/accessibility-checklist.md`

## Core Principles

- **Semantic HTML first**: Use native elements (`<button>`, `<label>`, `<main>`, `<nav>`) before adding ARIA.
- **Progressive enhancement**: Page must work without CSS and without JavaScript.
- **One thing per page**: Each screen should focus on a single task or question.
- **Error prevention**: Validate on server, show error summary at top, link to each field, and never rely on colour alone for errors.
- **Keyboard-first**: Every interaction must work with Tab, Enter, Space, and Escape.
- **Focus visible**: All interactive elements have a clear 3px focus indicator using `#ffdd00` on `#0b0c0c`.

## Page Structure

Every page must include:

1. `lang` attribute on `<html>`
2. Skip-to-main-content link as first focusable element
3. `<main id="main-content">` landmark
4. Descriptive, unique `<title>`
5. Header with service name and footer with support links

## Typography

- Base size: 19px desktop, 16px mobile
- Minimum body size: 14px (never smaller)
- Headings: logical order only (h1 -> h2 -> h3)
- Line height: 1.25 for body, 1.11 for headings

## Colour

- Text: `#0b0c0c` on `#ffffff` (18.8:1 contrast)
- Links: `#1a65a6`, visited `#54319f`, hover `#0f385c`
- Focus: `#ffdd00` background with `#0b0c0c` text (16.2:1)
- Error: `#d4351c` on white (5.9:1)
- Success: `#00703c` on white (5.4:1)

Never use colour alone to convey information. Always pair with text or icons.

## Spacing

Base unit: 5px. Standard section gap: 30px. Use the spacing scale for consistency. Reduce spacing by ~1/3 on mobile where appropriate.

## Assets

### Accessible Template

`assets/accessible-template/` contains:
- `index.html` - Boilerplate with skip link, header, main, footer, semantic landmarks
- `styles.css` - Complete stylesheet with design tokens, typography, form styles, buttons, error summary, tables, and print styles

Copy this directory as the starting point for any new accessible page or service.

## References

Load these references when implementing specific aspects:

- **Design tokens**: `references/design-tokens.md` - Typography scale, spacing scale, colour palette, layout breakpoints, and focus style specifications
- **Component patterns**: `references/component-patterns.md` - Copy-paste accessible HTML for forms, error summaries, fieldsets, date inputs, tables, pagination, notifications, and task lists
- **Accessibility checklist**: `references/accessibility-checklist.md` - WCAG 2.2 AA checklist (perceivable, operable, understandable, robust), GOV.UK-specific patterns, and manual/automated testing guidance

## Testing

Always run at minimum:
1. axe DevTools or WAVE - resolve all errors and warnings
2. Lighthouse accessibility audit - target score 100
3. Keyboard-only navigation test - Tab through entire page
4. Screen reader test (NVDA, JAWS, or VoiceOver)
5. 200% zoom test - ensure no horizontal scroll or clipped content
