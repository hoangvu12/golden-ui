# Component-Specific Corrections

## Buttons

Optically-derived padding (label text creates asymmetric visual weight):

```
padY = font_size × (√φ / φ²) ≈ font_size × 0.486
padX = font_size × (φ / φ²)  = font_size / φ ≈ font_size × 0.618
```

### With Icons

- **Side with icon**: Reduce horizontal padding to `font_size / φ` (0.618×)
- **Side without icon**: Keep full padding (`1em`)
- **Gap between icon and text**: `padY / φ^0.125` ≈ padY × 0.94
- **Icon vertical shift**: Move icon up by `font_size × 0.128` (quarter-step decimal)

```css
.button-icon { margin-top: calc(-1 * 1em * 0.128); }
```

### Size Variants

Only change `font-size` — internal spacing follows via `em`:
- Small: `body / φ^0.25` (≈ 0.886em)
- Medium: `body` (1em) — default
- Large: `body × √φ` (≈ 1.272em)

---

## Icons

Size relative to text context: `icon_size = 1em × √φ ≈ 1.272em` (square)

### Stroke Width Scaling

Stroke weight *increases* at small sizes, *decreases* at large:

| Context | Stroke width |
|---------|-------------|
| Large (display/title) | 1.5px |
| Medium (body/heading) | 1.75px |
| Small (caption/label) | 2px |

---

## Switch / Toggle

```
width       = base × φ²     ≈ 2.618em
height      = base + 2 × (base × φ⁻²) ≈ 1.764em
thumb       = base (1em, square)
thumb_inset = base × φ⁻²    ≈ 0.382em
```

---

## Cards — Optical Padding

**Problem**: Equal padding looks unequal because CSS line-height adds invisible leading above cap-height.

**Offset formula**: `optical_offset = font_size × (line_height / φ)`

| Text role | Offset | ≈ value |
|----------|--------|---------|
| body | 1rem × (1.618 / 1.618) | 0.618rem |
| title2 | 1.618rem × (1.272 / 1.618) | 1.272rem |
| display1 | 4.236rem × (1.128 / 1.618) | 2.953rem |

**Apply**: Reduce top padding by the offset, or use offset as top padding directly.

**Border radius**: `largest_child_font_size / largest_child_line_height` — ties curvature to content.

---

## Snackbar / Toast

```
padding:       body_line_height × half_dec  = 1.618 × 0.272 ≈ 0.440em
gap:           xs (0.618em)
border-radius: callout_line_height × whole_dec
icon-size:     heading font-size context
icon-shift:    translateY(-0.25px) for sub-pixel alignment
```

---

## Menu Items

```
padY:          lg × half_dec = 1.618 × 0.272 ≈ 0.440em
gap:           padY / eighth_step ≈ 0.414em
padX (icon):   same as padY
padX (no icon): 1em
border-radius: same as padY — radius matches padding
```

---

## Text Input

```
padding:       xs vertical, sm horizontal
border-radius: sm (0.618em)
label float:   translate(-2xs, -61.8%)  — 61.8% = (φ−1) × 100%
```
