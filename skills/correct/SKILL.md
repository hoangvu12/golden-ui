---
name: correct
user-invocable: true
description: >
  Fix optical UI issues in components — applies golden-ratio corrections to spacing,
  typography, padding, icons, and visual hierarchy. Makes changes directly. Use when
  you want to fix identified optical issues or polish UI components.
allowed-tools: Read, Edit, Write, Grep, Glob
argument-hint: "[file-or-directory]"
---

# Optical UI Correction

Apply optical corrections to `$ARGUMENTS`. Make changes directly using the project's native styling system.

## Detect project context

1. Identify styling system: !`ls tailwind.config.* postcss.config.* 2>/dev/null; grep -r "styled-components\|@emotion\|@mui\|@chakra-ui\|antd" package.json 2>/dev/null | head -3`
2. Read the target files
3. Adapt all corrections to the project's conventions

## Apply corrections (priority order)

Reference formulas: [../optical/reference/](../optical/reference/)

1. **Optical padding** — Reduce top padding in containers: `top_pad = font_size × (line_height / 1.618)`
2. **Typography** — Tighten line height for large text, loosen for body; negative tracking for headlines
3. **Spacing** — Snap arbitrary values to nearest φ-power step
4. **Buttons** — Asymmetric padding with icons (`padY = fontSize × 0.486`, `padX = fontSize × 0.618`)
5. **Icons** — Size at 1.272em, shift up 0.128em in buttons, inverse stroke weight scaling
6. **State layers** — Prefer opacity overlays over background mutations

## For each change

- Apply the fix
- In your response (not code comments), note: `[file:line] what changed — why`

## Constraints

- Don't introduce abstractions the project doesn't use
- Don't refactor architecture — visual properties only
- Don't add φ comments in production code
- Size variants: change `font-size` only, let `em` cascade
