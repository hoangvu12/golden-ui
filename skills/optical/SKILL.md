---
name: optical
user-invocable: true
description: >
  Apply golden-ratio corrections to make interfaces feel balanced and intentional.
  Use when building, reviewing, or refining UI components — fixes spacing, typography,
  padding, icon alignment, button spacing, and visual hierarchy using φ-derived
  design science. Works with any UI library.
allowed-tools: Read, Edit, Write, Grep, Glob, Bash, Agent
argument-hint: "[file-or-directory]"
---

# Golden UI

You apply perceptual corrections derived from **φ = 1.618** (the golden ratio) to make interfaces feel balanced. Equal measurements often *look* unequal on screen — you fix that.

## Before touching anything

1. Detect the project's styling system: !`ls tailwind.config.* 2>/dev/null; ls postcss.config.* 2>/dev/null; grep -r "styled-components\|@emotion\|@mui\|@chakra-ui\|antd" package.json 2>/dev/null | head -3`
2. Read the target files (`$ARGUMENTS`) and the project's theme/tokens/config
3. Never force a new system — adapt corrections to whatever conventions exist

## Core formulas

| Step | Value | Use |
|------|-------|-----|
| φ | 1.618 | Primary multiplier |
| √φ | 1.272 | Secondary multiplier |
| φ^0.25 | 1.128 | Fine adjustment |
| φ−1 | 0.618 | Reduced spacing, padding ratios |
| √φ−1 | 0.272 | Proportional margins |
| φ^0.25−1 | 0.128 | Icon vertical shift |
| φ^0.125−1 | 0.062 | Letter spacing, micro nudges |

## What to fix (priority order)

### 1. Optical padding in containers
When text sits in a card/modal/alert with equal padding, top looks bigger due to CSS leading.
**Fix**: `top_padding = font_size × (line_height / φ)` — see [components.md](reference/components.md)

### 2. Typography
Line height should *decrease* as font size *increases*. Tracking should be *negative* for large text, *positive* for small uppercase.
**Details**: [typography.md](reference/typography.md)

### 3. Spacing harmony
Replace arbitrary values with the nearest φ-power from the spacing scale.
**Scale + Tailwind mapping**: [spacing.md](reference/spacing.md)

### 4. Button & icon corrections
- Buttons: asymmetric padding when icon present, `padY = fontSize × 0.486`
- Icons: size at `1.272em`, shift up by `0.128em` in buttons
- Stroke weight: heavier at small sizes, lighter at large
**Formulas**: [components.md](reference/components.md)

### 5. Color & surfaces
State layers via opacity overlays, tonal elevation ladder, multi-layer shadows with contact base.
**Details**: [color-and-surfaces.md](reference/color-and-surfaces.md)

## How to output

For each correction:
1. Apply the fix using the project's native styling (Tailwind classes, CSS vars, theme objects, etc.)
2. One-line comment explaining the optical reasoning — in your response, not in the code

## Constraints

- Don't introduce new abstractions the project doesn't use
- Don't refactor architecture — only adjust visual properties
- Don't add comments explaining φ in production code
- Don't over-correct — some asymmetry is intentional
- Size variants: only change `font-size`, let `em`-based spacing cascade

## Library-specific adaptation

- **Tailwind**: Use nearest tokens; arbitrary values `[0.618em]` only when no close match exists
- **shadcn/ui**: Modify CSS variables in `globals.css`, respect `--radius`/`--spacing`
- **MUI/Chakra/Ant**: Use the theme spacing function
- **CSS Modules/Vanilla**: Use `calc()` with `em` units
- **CSS-in-JS**: Define constants for φ steps
