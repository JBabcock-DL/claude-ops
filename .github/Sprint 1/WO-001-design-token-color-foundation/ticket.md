---
type: work-order
status: open
labels: [work-order, design-system, tokens]
github_issue: 2
---

# [WO-001] Establish color token foundation in design system visual guide

## Problem Story
As a design system consumer, I need a documented and visual reference for the full color token scale so that I can apply tokens confidently without guessing or referencing raw hex values.

## Hypothesis
We believe that publishing a structured color token page in the Figma design system guide — organized by tier (primitive → semantic → component) — will reduce token misuse and speed up design handoff. We'll know we're right when designers and developers reference the Figma guide instead of hardcoded values in tickets or Slack.

## Requirements
- [ ] Define and document the full primitive color scale (`neutral`, `brand`, `error`, `warning`, `success`) with all stops (50–900)
- [ ] Map semantic tokens to primitives (`color/text/primary` → `neutral-900`, etc.)
- [ ] Create a Figma frame for each token tier: Primitives, Semantic, Component-level
- [ ] Each swatch must display: token name, hex value, and contrast ratio against white/black
- [ ] Tokens must be registered as Figma variables in the correct collection

## Success Criteria
- [ ] All color tiers are visually documented in the Figma design system guide file
- [ ] Figma variables match the token names and values defined in this ticket
- [ ] A designer unfamiliar with the system can identify the correct semantic token for any UI state (default, hover, disabled, error) without external help

## Testing & VQA

### Functional
- [ ] Figma variable values match documented hex values exactly
- [ ] Semantic tokens correctly reference their primitive counterparts (no hardcoded hex in semantic layer)

### Visual / Design QA
- [ ] Matches layout spec: swatches are organized in a grid, labeled, and grouped by tier
- [ ] Token names follow the agreed naming convention (`category/variant/state`)
- [ ] Color scale visually progresses from light to dark within each hue family

### Accessibility
- [ ] Each swatch documents its contrast ratio against `#FFFFFF` and `#000000`
- [ ] Semantic tokens designated for text use pass WCAG AA (4.5:1) against their intended background token
- [ ] Semantic tokens designated for UI components pass WCAG AA (3:1)

## References
- Related bug: #1 — hover token mismatch on Button / Primary
- Figma file: ProcessDemo Design System (link TBD)
- Token naming convention: `category/variant/state`
