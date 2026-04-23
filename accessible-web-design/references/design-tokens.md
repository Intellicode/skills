# Design Tokens Reference

GOV.UK-inspired design tokens for typography, spacing, colour, and layout. Use CSS custom properties or equivalent variables in your build system.

## Typography

### Font Stack
```css
font-family: "GDS Transport", arial, sans-serif;
```
If GDS Transport is unavailable, fall back to system fonts:
```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
```

### Type Scale

| Token | Mobile | Desktop (min 641px) | Line Height | Weight |
|-------|--------|---------------------|-------------|--------|
| 80 | 53px | 80px | 1.1 | 700 |
| 48 | 32px | 48px | 1.1 | 700 |
| 36 | 24px | 36px | 1.1 | 700 |
| 27 | 18px | 27px | 1.1 | 700 |
| 24 | 18px | 24px | 1.25 | 700 |
| 19 | 16px | 19px | 1.25 | 400 |
| 16 | 14px | 16px | 1.25 | 400 |
| 14 | 12px | 14px | 1.25 | 400 |

Usage rule: never use font size alone to create hierarchy. Combine with weight and spacing.

### Headings

| Level | Mobile | Desktop |
|-------|--------|---------|
| h1 (xl) | 32px | 48px |
| h2 (l) | 24px | 36px |
| h3 (m) | 18px | 24px |
| h4 (s) | 16px | 19px |

Always maintain logical heading order. Do not skip levels (e.g., h1 -> h3).

### Body Text

- Default: 19px on desktop, 16px on mobile
- Lead paragraph: 24px on desktop, 18px on mobile
- Small text: 16px on desktop, 14px on mobile
- Minimum text size: 14px (never smaller for body content)

## Spacing Scale

Base unit: 5px

| Token | Value | Common Use |
|-------|-------|------------|
| 0 | 0 | Reset |
| 1 | 5px | Tight gaps, inline spacing |
| 2 | 10px | Small padding |
| 3 | 15px | Mobile padding, form element gaps |
| 4 | 20px | Standard padding/margin |
| 5 | 25px | Medium gaps |
| 6 | 30px | Section gaps, large padding |
| 7 | 40px | Major section separators |
| 8 | 50px | Page-level spacing |
| 9 | 60px | Hero/banner spacing |

Responsive rule: reduce spacing by approximately 1/3 on mobile where appropriate.

## Colour

### Functional Colours

| Purpose | Hex | Usage |
|---------|-----|-------|
| text | #0b0c0c | Primary text, borders, buttons |
| secondary-text | #484949 | Supporting text |
| link | #1a65a6 | Default link colour |
| link-hover | #0f385c | Link hover state |
| link-visited | #54319f | Visited link colour |
| link-active | #0b0c0c | Active/pressed link |
| border | #b1b4b6 | Section borders, dividers |
| input-border | #0b0c0c | Form input borders |
| focus | #ffdd00 | Keyboard focus indicator only |
| focus-text | #0b0c0c | Focused text colour |
| error | #d4351c | Error states, validation |
| success | #00703c | Success states, confirmation panels |
| brand | #1d70b8 | Header bottom border, phase tags |
| template-background | #f3f2f1 | Footer background, secondary surfaces |
| body-background | #ffffff | Page background |

### Colour Contrast Requirements

All text must meet WCAG 2.2 AA:
- Normal text (< 18pt, < 14pt bold): 4.5:1 minimum
- Large text (>= 18pt, >= 14pt bold): 3:1 minimum
- UI components / graphical objects: 3:1 minimum

Key combinations that pass AA:
- #0b0c0c on #ffffff: 18.8:1
- #ffffff on #1d70b8: 4.8:1
- #0b0c0c on #ffdd00: 16.2:1 (focus state)
- #d4351c on #ffffff: 5.9:1
- #00703c on #ffffff: 5.4:1

### Colour Rules

1. Never rely on colour alone to convey meaning. Pair with text, icons, or patterns.
2. Do not use colour for decorative purposes only.
3. Only use `#ffdd00` (focus yellow) for focus states.
4. Maintain consistent colour semantics (red = error, green = success).

## Layout

### Width Container

```
Max width: 960px
Side padding: 15px (mobile), 30px (desktop)
Horizontal centering: auto margins
```

For wider content (e.g., tables):
```
Max width: 1200px
```

### Grid System

Two-thirds / one-third split is the standard content layout.
```
.two-thirds { width: 66.666%; }
.one-third { width: 33.333%; }
.one-half { width: 50%; }
.full-width { width: 100%; }
```

Stack columns on mobile (below 640px).

### Breakpoints

| Name | Width | Usage |
|------|-------|-------|
| mobile | < 640px | Single column, reduced spacing |
| tablet | 640px - 769px | Adjusted grid, medium spacing |
| desktop | >= 769px | Full grid, maximum spacing |

## Focus Styles

The focus indicator is critical for keyboard navigation. Implement consistently:

```css
:focus {
  outline: 3px solid #ffdd00;
  outline-offset: 0;
  box-shadow: inset 0 0 0 2px #0b0c0c; /* for contrast on light backgrounds */
}
```

For links:
```css
a:focus {
  outline: 3px solid transparent;
  color: #0b0c0c;
  background-color: #ffdd00;
  box-shadow: 0 -2px #ffdd00, 0 4px #0b0c0c;
  text-decoration: none;
}
```

Rules:
- Focus indicator must be at least 3px thick
- Must have sufficient contrast against background (4.5:1 minimum)
- Must not be obscured by other elements
- Must be visible on all interactive elements
