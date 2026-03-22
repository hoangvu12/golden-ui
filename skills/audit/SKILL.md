---
name: audit
description: >
  Audit UI components for optical issues — identifies spacing, typography, padding,
  and visual hierarchy violations without making changes. Produces a structured report
  with severity ratings. Use when you want to review interface quality before fixing.
context: fork
agent: Explore
allowed-tools: Read, Grep, Glob
argument-hint: "[file-or-directory]"
---

# Optical UI Audit

Read the target (`$ARGUMENTS`) and produce a structured report of optical violations. **Do not make any changes** — only analyze and report.

## Detect project context

Identify the styling system (Tailwind, CSS modules, CSS-in-JS, etc.) and any existing design tokens.

## Check each category

For reference formulas, see [../optical/reference/](../optical/reference/).

### 1. Spacing consistency
- Are spacing values from a harmonic scale or arbitrary?
- Do gaps/margins/padding follow a consistent ratio?
- Is section padding larger than component padding?

### 2. Typography
- Does line height decrease as font size increases?
- Is letter spacing negative for large text, positive for small uppercase?
- Are font weights appropriate for each size tier?

### 3. Optical padding
- Do cards/modals/alerts have equal padding that looks unequal?
- Does the top padding compensate for CSS leading?
- Does border radius relate to content text size?

### 4. Button & icon balance
- Are button paddings asymmetric when icons are present?
- Are icons sized at ~1.27× text size?
- Do icon stroke weights scale inversely with size?
- Are icons vertically shifted to match text cap-height?

### 5. Color & interaction
- Do hover/focus/active states use opacity overlays or background mutations?
- Is there a surface elevation ladder or just flat backgrounds?
- Do shadows include a contact shadow base layer?

## Output format

```
## Optical UI Audit: [filename or directory]

### Critical (breaks visual balance)
- [file:line] Issue description → Suggested fix

### Warning (noticeable to trained eye)
- [file:line] Issue description → Suggested fix

### Note (minor refinement)
- [file:line] Issue description → Suggested fix

### Summary
- X critical, Y warnings, Z notes
- Primary issues: [spacing|typography|padding|icons|color]
- Styling system: [detected system]
```
