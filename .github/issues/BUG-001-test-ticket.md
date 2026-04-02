---
type: bug
status: open
labels: [bug, test]
---

# [BUG-001] Button component renders incorrect hover state color

## Summary
The primary button's hover state is using the wrong token — it renders `brand-500` instead of `brand-600`, causing insufficient contrast against the white label text.

## Steps to Reproduce
1. Open the design system visual guide in Figma
2. Navigate to the **Buttons** section
3. Hover over the **Primary Button** component
4. Observe the background color on hover

## Expected Behavior
Background color should transition to `brand-600` (`#1D4ED8`) on hover, maintaining a 4.5:1 contrast ratio with white text.

## Actual Behavior
Background color transitions to `brand-500` (`#3B82F6`), which only achieves a 3.1:1 contrast ratio — failing WCAG AA.

## Environment
- Component: `Button / Primary`
- Area: Design System / Tokens
- Figma file: ProcessDemo Design System

## Additional Context
This likely affects all button variants that use the `brand` token scale on hover. Related to design token audit work.
