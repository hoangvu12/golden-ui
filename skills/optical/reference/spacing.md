# Spacing Scale

All spacing derives from powers of φ (1.618) centered on a base unit (typically `1rem = 16px`):

```
3xs = base × φ⁻³  ≈ 0.236 × base   (3.8px)
2xs = base × φ⁻²  ≈ 0.382 × base   (6.1px)
xs  = base × φ⁻¹  ≈ 0.618 × base   (9.9px)
md  = base          = 1 × base       (16px)
lg  = base × φ     ≈ 1.618 × base   (25.9px)
xl  = base × φ²    ≈ 2.618 × base   (41.9px)
2xl = base × φ³    ≈ 4.236 × base   (67.8px)
3xl = base × φ⁴    ≈ 6.854 × base   (109.7px)
4xl = base × φ⁵    ≈ 11.09 × base   (177.4px)
```

## Tailwind Mapping

| φ-scale | Exact | Nearest Tailwind |
|---------|-------|-----------------|
| 3xs | 3.8px | `1` (4px) |
| 2xs | 6.1px | `1.5` (6px) |
| xs | 9.9px | `2.5` (10px) |
| md | 16px | `4` (16px) |
| lg | 25.9px | `6` (24px) or `7` (28px) |
| xl | 41.9px | `10` (40px) or `11` (44px) |
| 2xl | 67.8px | `16` (64px) or `17` (68px) |

## Section vs Component Padding

Section-level padding should be one step *above* component-level padding on the φ scale:
- Component uses `md` → Section uses `lg` or `xl`

## Grid Gaps

Default: `md` (1em). Tight: `xs` (0.618em). Spacious: `lg` (1.618em).
