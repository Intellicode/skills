# Visual System

## Typography

- Use a system UI stack unless the product already defines a font.
- Base body size: `14px` or `15px` for dense SaaS tools.
- Page title: `20px` to `28px`.
- Section headings: `13px` to `16px`, medium or semibold.
- Metadata: `12px` to `13px`, with sufficient contrast.
- Line height: `1.35` to `1.55` depending on density.
- Letter spacing: `0`.

## Spacing

Use a 4px-based spacing scale:

- `4px`: tight icon/text gap, compact cell padding.
- `8px`: default inline gap.
- `12px`: compact block gap.
- `16px`: default panel padding.
- `24px`: section gap.
- `32px`: large content separation.

Keep vertical rhythm consistent. Dense screens can still breathe when spacing is predictable.

## Color

Use a neutral base plus one restrained accent:

- Background: off-white or very light neutral.
- Surface: white or near-white.
- Border: subtle neutral with enough contrast to separate regions.
- Text: strong neutral for primary, muted neutral for secondary.
- Accent: blue, green, black, or product-specific brand color.
- Status: green success, amber warning, red error, blue/info, gray neutral.

Avoid one-note palettes dominated by a single hue family. Avoid heavy purple-blue gradients, beige/tan dashboards, and dark slate-heavy layouts unless the user asks for that brand direction.

## Borders, Radius, and Shadows

- Cards and panels: `6px` to `8px` radius.
- Inputs and buttons: `6px` to `8px` radius.
- Tables and shells: crisp 1px borders.
- Shadows: subtle and functional, mainly for menus, modals, and sticky bars.

## Density

Choose density by product:

- Productivity and console tools: compact, scan-friendly, high information density.
- Commerce/admin tools: moderate density with clear tables and filters.
- Creator/editor tools: larger canvas, compact chrome.
- Executive analytics: more whitespace, but still avoid marketing composition.

## Polish Details

- Align icons, labels, and values on a common grid.
- Use consistent heights for buttons, inputs, tabs, and rows.
- Make active navigation obvious but restrained.
- Keep hover/focus/selected states visually distinct.
- Use skeletons or subtle loading states for data regions.
- Use realistic timestamps, user names, counts, and status labels.
