# golden-ui

Golden-ratio design science for any UI library. A skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) and [40+ AI agents](https://skills.sh) that makes interfaces feel balanced and intentional.

> Inspired by [LiftKit](https://github.com/Chainlift/liftkit) — the UI framework for perfectionists.

## What it does

Most UI code uses mathematically equal spacing — but equal measurements often *look* unequal on screen. This skill applies perceptual corrections based on the golden ratio (φ = 1.618), so your interfaces feel balanced without you thinking about the math.

Works with **any styling system**: Tailwind, shadcn/ui, Radix, MUI, Chakra, Ant Design, vanilla CSS, CSS-in-JS.

## Install

### Via skills.sh (works with Claude Code, Cursor, Copilot, and 40+ agents)

```bash
npx skills add hoangvu12/golden-ui
```

### Via Claude Code plugin system

```bash
/plugin marketplace add hoangvu12/golden-ui
/plugin install golden-ui@golden-ui
```

## Skills

| Skill | Command | What it does |
|-------|---------|-------------|
| **golden-ui** | `/golden-ui` | Full pass — audit, correct, and generate tokens in one run |
| **optical** | `/golden-ui:optical [path]` | Optical corrections — spacing, typography, padding, icons |
| **audit** | `/golden-ui:audit [path]` | Read-only audit — severity-rated report, no changes |
| **correct** | `/golden-ui:correct [path]` | Targeted fix — applies corrections directly |
| **tokens** | `/golden-ui:tokens [css\|tailwind\|theme-object]` | Generate φ-based design tokens for your project |

## The math

Everything derives from **φ = 1.618**:

```
Spacing:    3xs ← φ⁻³ ... md = 1× ... 4xl ← φ⁵
Type:       caption ← 1/√φ ... body = 1× ... display1 ← φ³
Padding:    optical_offset = font_size × (line_height / φ)
Buttons:    padY = fontSize × (√φ / φ²), padX = fontSize / φ
Icons:      size = 1em × √φ, shift = −0.128em
Line-ht:    display→1.13, heading→1.27, body→1.62
Tracking:   display→−0.022em, body→−0.011em, CAPS→+0.062em
Shadows:    always include 0 0 1px contact shadow base
States:     opacity overlays (hover 0.08–0.16, active 0.35–0.50)
```

## What it corrects

- **Optical padding** — compensates for CSS line-height leading in cards, modals, alerts
- **Typography** — φ-derived sizes with inverse line-height and tracking rules
- **Button spacing** — asymmetric padding when icons are present, vertical icon shift
- **Icon sizing** — `1.272em` (√φ) with stroke weight that scales inversely with size
- **Spacing scale** — powers of φ from `0.236×` to `11.09×` base
- **State layers** — opacity overlays instead of background mutations
- **Color tones** — Material Design 3 tonal palette stops for light/dark modes
- **Shadows** — multi-layer with constant contact shadow base
- **Glass materials** — layered blur/tint/light at φ-harmonic blur radii

## Credits

Design patterns derived from [LiftKit](https://github.com/Chainlift/liftkit) by [Chainlift](https://chainlift.io).

## License

MIT
