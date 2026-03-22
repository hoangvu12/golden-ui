---
name: golden-ui
description: >
  Full golden-ratio UI pass — audits, corrects, and generates tokens in one run.
  Use when you want to comprehensively improve a component or directory's visual
  quality. Runs optical audit, applies corrections, then generates design tokens
  if none exist. Works with any UI library.
allowed-tools: Read, Edit, Write, Grep, Glob, Bash, Agent
argument-hint: "[file-or-directory]"
---

# Golden UI — Full Pass

Run a complete golden-ratio design pass on `$ARGUMENTS`. This combines all sub-skills in sequence.

## Detect project context

1. Styling system: !`ls tailwind.config.* 2>/dev/null; ls postcss.config.* 2>/dev/null; grep -r "styled-components\|@emotion\|@mui\|@chakra-ui\|antd" package.json 2>/dev/null | head -3`
2. Existing tokens: !`ls src/styles/tokens* src/theme* src/lib/theme* 2>/dev/null; head -5 tailwind.config.* 2>/dev/null`
3. Read the target files and the project's theme/config

## Phase 1: Audit

Analyze `$ARGUMENTS` for optical violations. For each issue found, note:
- `[file:line]` what's wrong → what the fix should be
- Severity: critical / warning / note

Reference formulas: [../optical/reference/](../optical/reference/)

Check: spacing consistency, typography (line-height vs font-size, tracking, weight), optical padding in containers, button/icon balance, color/state layers, shadows.

## Phase 2: Correct

Apply all fixes from the audit using the project's native styling system.

Priority order:
1. Optical padding — `top_pad = font_size × (line_height / 1.618)`
2. Typography — tighten line-height for large text, negative tracking for headlines
3. Spacing — snap to nearest φ-power step
4. Buttons — asymmetric padding with icons (`padY = fontSize × 0.486`)
5. Icons — size at 1.272em, shift up 0.128em, inverse stroke scaling
6. State layers — opacity overlays over background mutations

For each change, note in your response (not in code): `[file:line] what changed — why`

## Phase 3: Tokens (if needed)

If the project has no design tokens or spacing scale, generate φ-based tokens in the project's native format (CSS custom properties, Tailwind config extension, or theme object).

Skip this phase if the project already has a well-defined token system.

## Constraints

- Adapt to whatever styling conventions exist — never force a new system
- Only adjust visual properties — no architecture changes
- No φ comments in production code
- Don't over-correct — some asymmetry is intentional
