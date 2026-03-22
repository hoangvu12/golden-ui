# Typography Scale

Font sizes use mixed φ-power steps for perceptual balance:

| Role | Formula | ≈ rem | Purpose |
|------|---------|-------|---------|
| display1 | base × φ³ | 4.236 | Hero headlines |
| display2 | base × φ² | 2.618 | Section headers |
| title1 | base × φ × √φ | 2.058 | Page titles |
| title2 | base × φ | 1.618 | Card titles |
| title3 | base × √φ | 1.272 | Subsections |
| heading | base × φ^0.25 | 1.128 | UI headings |
| body | base | 1.0 | Body text |
| subheading | base / φ^0.25 | 0.886 | Meta text |
| callout | base / φ^0.125 | 0.942 | Annotations |
| label | (base / φ^0.25) / φ^0.125 | 0.834 | Form labels |
| caption | base / √φ | 0.786 | Fine print |

## Line Height

Line height should *decrease* as font size *increases*:

| Text size | Line height | Rationale |
|-----------|-------------|-----------|
| Display (display1) | φ^0.25 ≈ 1.13 | Very tight — large text has ample internal whitespace |
| Heading/title | √φ ≈ 1.27 | Moderately tight |
| Body | φ ≈ 1.62 | Generous — maximally readable for long-form text |

## Letter Spacing (Tracking)

Negative for large text, positive for small uppercase:

| Size range | Tracking |
|-----------|----------|
| Display (>2rem) | −0.02em to −0.022em |
| Title (1.2–2rem) | −0.014em to −0.02em |
| Body (1rem) | −0.011em |
| Small text (<1rem) | −0.004em to −0.009em |
| Uppercase labels | +0.062em (= φ^0.125 − 1) |

## Font Weight

- Display/title: Regular (400) — large size carries the weight
- Headings/labels: Semibold (600) — needs weight at medium sizes
- Body: Regular (400)
- Bold variants: promote by one stop (400→600, 600→700)
