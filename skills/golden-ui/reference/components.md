# Component-Specific Optical Corrections

## Universal Rules

1. **Padding scales with font-size via `em`**, not fixed tokens. Changing font-size recalculates all spacing.
2. **Icon-adjacent sides get reduced padding.** Text-only sides keep full padding.
3. **Gap = vertical padding ÷ φ^0.125** (eighthstep). Applies to buttons, menu items, selects.
4. **Border-radius = font-size ÷ line-height.** Corners track typographic density.
5. **Icon optical shift = `-(1em × 0.128)`** upward. Aligns icon center with text cap-height.
6. **Line-height IS the φ step value directly** — body = φ (1.618), headings = √φ (1.272), display1 = φ^0.25 (1.128).

---

## Buttons

```
padY     = fontSize × (√φ / φ²)           ≈ fontSize × 0.486
padX     = 1em                              (default, no icon)
gap      = padY / φ^0.125                  ≈ 0.414em
line-ht  = √φ                              = 1.272
```

### Asymmetric padding with icons

| Scenario | Left padding | Right padding |
|----------|-------------|---------------|
| No icon | 1em | 1em |
| Start icon only | fontSize / φ (0.618em) | 1em |
| End icon only | 1em | fontSize / φ (0.618em) |
| Both icons | fontSize / φ (0.618em) | fontSize / φ (0.618em) |

### Icon vertical shift
```
margin-top: -(1em × 0.128)
```

### Size variants — only change font-size
- Small: ≈ 0.886em (subheading)
- Medium: 1em (body) — default
- Large: ≈ 1.272em (title3)

All padding/gap recalculates automatically via `em`.

---

## Menu Items / Select Options

Same asymmetric icon pattern as buttons, different formula:

```
padY          = size-lg × halfstep-dec     = 1.618em × 0.272 ≈ 0.440em
gap           = padY / φ^0.125            ≈ 0.414em
border-radius = padY                       (radius matches vertical padding!)
```

### Asymmetric padding with icons

| Scenario | Side with icon | Side without icon |
|----------|---------------|-------------------|
| Has icon | 0.440em (same as padY) | — |
| No icon | — | 1em (body font-size) |

**Key insight**: border-radius equals vertical padding — unified optical cohesion.

---

## Cards

### Padding = largest child font-size
Card padding on all sides equals the font-size of the largest text inside. Card "breathes" proportionally to its content.

### Border-radius = font-size / line-height
```
border-radius = largest_child_font_size / largest_child_line_height
```

### Optical correction per side
Reduces padding on specific sides:
```
opticalCorrectedPadding = font-size / line-height
```
Apply to top, bottom, left, right, x, y, or all — compensates for visual "air" that leading creates.

---

## Icons

### Base sizing
```
width = 1em × √φ ≈ 1.272em (square, aspect-ratio: 1)
```

### Stroke width scaling (inverse)
| Context | Stroke width |
|---------|-------------|
| Large (display/title) | 1.5px |
| Medium (body/heading) | 1.75px |
| Small (caption/label) | 2px |

### Standalone optical shift
```
margin-top: -(1em × 0.128)
```
Same as button icon shift. Use when icon is standalone next to text.

### Inside icon-button
Icon sizing is unset — defers to button context. Icon-button padding = 0.618em (size-xs).

---

## Text Input

### Input-wrap margin
```
margin-top = bodyBoxHeight × halfstep-dec
           = (1em × 1.618) × 0.272 ≈ 0.440em
```

### Floating label transform
```
transform: translate(-0.382em, -61.8%)
```
`-61.8%` = `(1/φ) × 100` — the golden ratio reciprocal.

### Input padding & radius
```
padding: 0.618em (vertical) 0.618em (horizontal)
border-radius: 0.618em
```

---

## Snackbar / Toast

```
padding       = body-line-height × halfstep-dec  = 1.618 × 0.272 ≈ 0.440em
gap           = 0.618em
border-radius = callout-line-height × wholestep-dec
icon-size     = heading font-size context
icon-shift    = translateY(-0.25px)  (sub-pixel empirical nudge)
icon-margin   = 1em / √φ ≈ 0.786em
actions-margin = 1em / √φ ≈ 0.786em
```

---

## Switch / Toggle

```
width       = base × φ²                 ≈ 2.618em
height      = base + 2 × (base × φ⁻²)  ≈ 1.764em  (thumb + 2× border)
thumb       = base (1em, square)
thumb_inset = base × φ⁻²               ≈ 0.382em
on-position = 100% - (thumb + inset)
```

---

## Badge

```
padding       = 0.618em (size-xs)
border-radius = 0.618em (size-sm)
font-size     = 1em (size-md)
```

## Sticker (asymmetric pill)

```
padding: 0.618em (vertical) 0.618em (horizontal — one step above vertical)
```
Horizontal > vertical for pill shapes.

---

## Section Padding

Section padding is **offset one full tier above** component padding:

| Section prop | Actual token |
|-------------|-------------|
| xs | 1.618em (size-lg) |
| sm | 2.618em (size-xl) |
| md | 4.236em (size-2xl) |
| lg | 6.854em (size-3xl) |
| xl | 11.09em (size-4xl) |

Mobile: horizontal padding clamps to 1em (size-md).

---

## Dropdown

Transform origin matches trigger corner — menu opens from trigger position:
- Top-left → `translate(0%, -100%)`, origin `top left`
- Top-right → `translate(-100%, -100%)`, origin `top right`
- Bottom-right → `translate(-100%, 0%)`, origin `bottom right`
- Bottom-left → `translate(0%, 0%)`, origin `bottom left`

---

## State Layers

| State | Overlay opacity |
|-------|----------------|
| Hover | 0.16 |
| Focus | 0.35 |
| Active/Pressed | 0.50 |
| Forced active | 0.12 |
| Selected (.is-active) | 0.16 |

Transition: `opacity 100ms ease-out`. Absolute-positioned overlay div — never mutate background color.
