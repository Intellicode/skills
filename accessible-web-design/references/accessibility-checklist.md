# Accessibility Checklist

Use this checklist to verify pages meet WCAG 2.2 Level AA and GOV.UK design principles.

## Perceivable

- [ ] **Text alternatives**: All images have appropriate `alt` text. Decorative images use `alt=""` or `role="presentation"`.
- [ ] **Video/audio**: Captions provided for video. Transcripts available for audio.
- [ ] **Colour contrast**: Text meets 4.5:1 against background (3:1 for large text 18pt+ or 14pt+ bold).
- [ ] **Colour independence**: Information is never conveyed by colour alone. Always paired with text, icons, or patterns.
- [ ] **Resize text**: Page remains usable at 200% zoom.
- [ ] **Reflow**: Content fits within 320px width without horizontal scroll.
- [ ] **Focus visible**: Focus indicators are clearly visible (3px minimum, high contrast).

## Operable

- [ ] **Keyboard accessible**: All functionality works with keyboard only (Tab, Enter, Space, Arrow keys).
- [ ] **No keyboard traps**: User can Tab away from all focusable elements.
- [ ] **Skip link**: First focusable element on every page is "Skip to main content".
- [ ] **Focus order**: Tab order follows visual reading order (top-to-bottom, left-to-right in LTR).
- [ ] **Page title**: Unique, descriptive `<title>` on every page.
- [ ] **Link purpose**: Link text describes destination (no "click here" or "read more" alone).
- [ ] **Target size**: Interactive targets are at least 24x24px (44x44px preferred for mobile).
- [ ] **Motion**: No autoplaying content; if animation exists, respect `prefers-reduced-motion`.

## Understandable

- [ ] **Language**: `lang` attribute set on `<html>`. Language changes within content marked with `lang`.
- [ ] **Consistent navigation**: Navigation patterns repeated across pages in same location.
- [ ] **Error identification**: Errors identified in text, with colour as secondary indicator only.
- [ ] **Error suggestion**: Error messages explain what went wrong and how to fix it.
- [ ] **Labels**: Every input has an associated `<label>` with `for` matching input `id`.
- [ ] **Error summary**: Form errors display an error summary box at top of page with links to each error field.
- [ ] **One thing per page**: Each page addresses a single task or question.

## Robust

- [ ] **Valid HTML**: Markup passes HTML5 validation.
- [ ] **ARIA**: Native HTML semantics used where possible. ARIA only when HTML insufficient.
- [ ] **Name/Role/Value**: Custom components expose correct name, role, and state via ARIA or native HTML.
- [ ] **Status messages**: Important dynamic updates use `role="status"`, `role="alert"`, or `aria-live`.

## GOV.UK-Specific Patterns

- [ ] **Phase banner**: New services show Alpha or Beta banner with feedback link.
- [ ] **Back link**: Multi-page forms include back link when user needs to change answers.
- [ ] **Confirmation page**: After completing a transaction, show clear confirmation with reference number.
- [ ] **Service name**: Header displays the service name linking to the service start page.
- [ ] **Footer**: Contains support links, cookies, accessibility statement, and contact.

## Automated Testing Tools

Run these tools and resolve all issues:

1. **axe DevTools** browser extension
2. **WAVE** browser extension
3. **Lighthouse** accessibility audit (target: 100)
4. **html-validate** with WCAG rules

## Manual Testing

- [ ] Navigate entire page using only Tab key
- [ ] Test with screen reader (NVDA, JAWS, or VoiceOver)
- [ ] Test at 200% and 400% zoom
- [ ] Test in high contrast mode (Windows HC themes)
- [ ] Test with keyboard-only form completion
