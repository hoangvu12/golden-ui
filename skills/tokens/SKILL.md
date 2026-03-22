---
name: tokens
description: >
  Generate golden-ratio design tokens for a project. Creates a φ-based spacing scale,
  typography scale, and color system as CSS custom properties, Tailwind config, or
  theme object — adapted to whatever styling system the project uses.
allowed-tools: Read, Edit, Write, Grep, Glob, Bash
argument-hint: "[css|tailwind|theme-object]"
disable-model-invocation: true
---

# Generate Golden UI Tokens

Generate a complete set of φ-based design tokens for this project, output as `$ARGUMENTS` format.

## Detect project context

1. Styling system: !`ls tailwind.config.* postcss.config.* 2>/dev/null; grep -r "styled-components\|@emotion\|@mui\|@chakra-ui\|antd" package.json 2>/dev/null | head -3`
2. Existing tokens/theme: !`ls src/styles/tokens* src/theme* src/lib/theme* 2>/dev/null; head -20 tailwind.config.* 2>/dev/null`

## Token sets to generate

### 1. Spacing scale (φ-power progression)
```
3xs: 0.236rem, 2xs: 0.382rem, xs: 0.618rem, md: 1rem,
lg: 1.618rem, xl: 2.618rem, 2xl: 4.236rem, 3xl: 6.854rem, 4xl: 11.09rem
```

### 2. Typography scale
```
display1: 4.236rem (lh: 1.128), display2: 2.618rem (lh: 1.272),
title1: 2.058rem (lh: 1.272), title2: 1.618rem (lh: 1.272),
title3: 1.272rem (lh: 1.272), heading: 1.128rem (lh: 1.272),
body: 1rem (lh: 1.618), subheading: 0.886rem (lh: 1.272),
callout: 0.942rem (lh: 1.272), label: 0.834rem (lh: 1.272),
caption: 0.786rem (lh: 1.272)
```

### 3. Harmonic step constants
```
phi: 1.618, half-step: 1.272, quarter-step: 1.128, eighth-step: 1.062
phi-dec: 0.618, half-dec: 0.272, quarter-dec: 0.128, eighth-dec: 0.062
```

### 4. Shadow scale
```
sm: 0 0 1px 0 shadow-color
md: 0 4px 6px rgba(0,0,0,.08), 0 2px 4px rgba(0,0,0,.11), 0 0 1px rgba(0,0,0,.4)
lg: 0 11px 15px -3px rgba(0,0,0,.11), 0 2px 6px rgba(0,0,0,.07), 0 0 1px rgba(0,0,0,.4)
```

## Output formats

**If `$ARGUMENTS` = `css`**: Generate CSS custom properties on `:root`
**If `$ARGUMENTS` = `tailwind`**: Extend tailwind.config with the scales
**If `$ARGUMENTS` = `theme-object`**: Generate a JS/TS theme object
**If empty or unrecognized**: Auto-detect from project and use the matching format

Integrate into existing files when possible. Only create new files if nothing exists.
