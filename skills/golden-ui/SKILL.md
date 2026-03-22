---
name: golden-ui
user-invocable: true
description: >
  Golden-ratio design science for any UI library. Audits, corrects, and generates
  design tokens in one pass. Fixes spacing, typography, optical padding, icon alignment,
  button spacing, shadows, state layers, and visual hierarchy using φ-derived formulas.
  Use when building, reviewing, or polishing UI components.
allowed-tools: Read, Edit, Write, Grep, Glob, Bash, Agent
argument-hint: "[file-or-directory]"
---

# Golden UI

You apply perceptual corrections derived from **φ = 1.618** (the golden ratio) to make interfaces feel balanced. Equal measurements often *look* unequal on screen — you fix that.

Works with any UI library: Tailwind, shadcn/ui, Radix, MUI, Chakra, Ant Design, vanilla CSS, CSS-in-JS.

## Before touching anything

1. Detect the project's styling system: !`ls tailwind.config.* 2>/dev/null; ls postcss.config.* 2>/dev/null; grep -r "styled-components\|@emotion\|@mui\|@chakra-ui\|antd" package.json 2>/dev/null | head -3`
2. Check for existing tokens: !`ls src/styles/tokens* src/theme* src/lib/theme* 2>/dev/null; head -5 tailwind.config.* 2>/dev/null`
3. Read the target files (`$ARGUMENTS`) and the project's theme/config
4. Never force a new system — adapt corrections to whatever conventions exist

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

---

## Phase 1: Audit

Analyze `$ARGUMENTS` for optical violations. For each issue found, note:
- `[file:line]` what's wrong → what the fix should be
- Severity: **critical** / **warning** / **note**

### What to check

**Spacing** — Are values from a harmonic scale or arbitrary? Do gaps/margins/padding follow a consistent ratio? Is section padding larger than component padding?

**Typography** — Does line height decrease as font size increases? Is letter spacing negative for large text, positive for small uppercase? Are font weights appropriate per size tier? See [typography.md](reference/typography.md)

**Optical padding** — Do cards/modals/alerts have equal padding that looks unequal? Does top padding compensate for CSS leading? Does border radius relate to content text size? See [components.md](reference/components.md)

**Buttons & icons** — Are button paddings asymmetric when icons are present? Are icons sized at ~1.27× text size? Do stroke weights scale inversely with size? Are icons vertically shifted? See [components.md](reference/components.md)

**Color & interaction** — Do hover/focus/active states use opacity overlays or background mutations? Is there a surface elevation ladder? Do shadows include a contact shadow base? See [color-and-surfaces.md](reference/color-and-surfaces.md)

---

## Phase 2: Correct

Apply all fixes from the audit using the project's native styling system.

Priority order:
1. **Optical padding** — `top_pad = font_size × (line_height / 1.618)`
2. **Typography** — tighten line-height for large text, negative tracking for headlines
3. **Spacing** — snap to nearest φ-power step. See [spacing.md](reference/spacing.md)
4. **Buttons** — asymmetric padding with icons (`padY = fontSize × 0.486`, `padX = fontSize × 0.618`)
5. **Icons** — size at 1.272em, shift up 0.128em, inverse stroke scaling
6. **State layers** — opacity overlays over background mutations

For each change, note in your response (not in code): `[file:line] what changed — why`

---

## Phase 3: Tokens (if needed)

If the project has no design tokens or spacing scale, generate φ-based tokens in the project's native format.

### Token sets

**Spacing** (φ-power progression):
`3xs: 0.236rem, 2xs: 0.382rem, xs: 0.618rem, md: 1rem, lg: 1.618rem, xl: 2.618rem, 2xl: 4.236rem, 3xl: 6.854rem, 4xl: 11.09rem`

**Typography**:
`display1: 4.236rem (lh:1.128), display2: 2.618rem (lh:1.272), title1: 2.058rem (lh:1.272), title2: 1.618rem (lh:1.272), title3: 1.272rem (lh:1.272), heading: 1.128rem (lh:1.272), body: 1rem (lh:1.618), subheading: 0.886rem (lh:1.272), callout: 0.942rem (lh:1.272), label: 0.834rem (lh:1.272), caption: 0.786rem (lh:1.272)`

**Shadows**:
```
sm: 0 0 1px 0 shadow-color
md: 0 4px 6px rgba(0,0,0,.08), 0 2px 4px rgba(0,0,0,.11), 0 0 1px rgba(0,0,0,.4)
lg: 0 11px 15px -3px rgba(0,0,0,.11), 0 2px 6px rgba(0,0,0,.07), 0 0 1px rgba(0,0,0,.4)
```

**Output as**: CSS custom properties on `:root`, Tailwind config extension, or JS/TS theme object — whichever matches the project. Integrate into existing files when possible.

Skip this phase if the project already has a well-defined token system.

---

## Constraints

- Adapt to whatever styling conventions exist — never force a new system
- Only adjust visual properties — no architecture changes
- No φ comments in production code
- Don't over-correct — some asymmetry is intentional
- Size variants: only change `font-size`, let `em`-based spacing cascade

## Library-specific adaptation

- **Tailwind**: Use nearest tokens; arbitrary values `[0.618em]` only when no close match
- **shadcn/ui**: Modify CSS variables in `globals.css`, respect `--radius`/`--spacing`
- **MUI/Chakra/Ant**: Use the theme spacing function
- **CSS Modules/Vanilla**: Use `calc()` with `em` units
- **CSS-in-JS**: Define constants for φ steps
