# Color System & Surfaces

## Tonal Palette (Material Design 3 / HCT)

For any primary color, generate tonal variants at these tone stops:

### Light Mode
- Primary surface: tone 40, text on it: tone 98
- Container: tone 90, text on it: tone 10
- Background: tone 99, surface: tone 98

### Dark Mode
- Primary surface: tone 80, text on it: tone 20
- Container: tone 30, text on it: tone 90
- Background: tone 10, surface: tone 6

## Surface Elevation (Container Ladder)

Use progressively lighter/darker surface tones instead of (or alongside) shadows:

```
surfaceContainerLowest  → tone 100 (light) / 4 (dark)
surfaceContainerLow     → tone 96 / 10
surfaceContainer        → tone 94 / 12
surfaceContainerHigh    → tone 92 / 17
surfaceContainerHighest → tone 90 / 22
```

## Shadow Scale

Multi-layer shadows with a constant 1px contact shadow base:

```css
shadow-sm: 0 0 1px 0 shadow-color;
shadow-md: 0 4px 6px rgba(0,0,0,.08), 0 2px 4px rgba(0,0,0,.11), 0 0 1px rgba(0,0,0,.4);
shadow-lg: 0 11px 15px -3px rgba(0,0,0,.11), 0 2px 6px rgba(0,0,0,.07), 0 0 1px rgba(0,0,0,.4);
shadow-xl: 0 0 1px 0 outline-color, 0 50px 100px rgba(0,0,0,.15);
```

## State Layers (Interactive Feedback)

Use opacity overlays rather than background color mutations:

| State | Overlay opacity |
|-------|----------------|
| Hover | 0.08–0.16 |
| Focus | 0.24–0.35 |
| Active/Pressed | 0.35–0.50 |
| Selected | 0.12–0.16 |

Transition: `opacity 100ms ease-out`. Overlays preserve the base color while providing consistent feedback across all color variants.

## Glass / Frosted Material

Layer three elements:

1. **Blur**: `backdrop-filter: blur(φ-scale)` — thick: 1.618rem, normal: 1rem, thin: 0.618rem
2. **Tint**: Semi-transparent surface color at 0.4–0.8 opacity
3. **Light**: Optional gradient with `mix-blend-mode: soft-light`
