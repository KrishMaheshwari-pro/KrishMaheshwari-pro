# Assets — How Each SVG Is Built

Every visual is a **hand-authored, JavaScript-free SVG**. They animate via CSS
keyframes and SMIL `<animate>`, which GitHub honours when an SVG is loaded as an
`<img>`. All are dark cards on a **transparent canvas**, so they sit cleanly on
GitHub Dark and Light.

> Editing tip: open any `.svg` directly in a browser to preview animations
> instantly. GitHub's camo proxy caches images for ~minutes — append `?v=2` to a
> README `src` to bust the cache while iterating.

| File | Purpose | Edit when you want to… |
| ---- | ------- | ---------------------- |
| `banners/hero-banner.svg` | The hero | Change name, eyebrow, rotating role words, brand chips, monogram |
| `banners/footer-banner.svg` | Closing strip | Change the sign-off line |
| `cards/altus-card.svg` | Company card | Edit mission / vision / values / meta chips |
| `cards/tech-stack.svg` | Stack grid | Add/remove a tool (one `<text>` line each) |
| `illustrations/ps-architecture.svg` | Product architecture | Rename tiers/nodes, retitle |
| `illustrations/roadmap-timeline.svg` | Roadmap | Move the "NOW" node, edit milestones |
| `logos/altus-logo.svg` | Company mark | Swap brand symbol (keep `viewBox`) |
| `logos/productivity-shastra-logo.svg` | Product mark | Swap brand symbol (keep `viewBox`) |
| `svg/divider.svg` | Slim section rule | — (reused everywhere) |
| `svg/wave-divider.svg` | Wave between sections | — |
| `metrics/github-metrics.svg` | Placeholder | Auto-replaced by the metrics workflow |

## Anatomy of a card SVG

```
<defs>   gradients (brand, bg, rule), patterns, <style> with keyframes
<rect>   the card: rounded, bg gradient, 1.5px border (#1E2A45)
<g>      content layers, grouped & id'd; accent bars use the brand gradient
@media (prefers-reduced-motion: reduce) { … animation:none … }
```

## Rules that keep them consistent

1. **Tokens only** — colors come from `docs/DESIGN.md`. No off-palette hex.
2. **One gradient focal point** per asset. Everything else is flat surface + border.
3. **Escape entities** — `&` → `&amp;`, `<` → `&lt;`, `>` → `&gt;` inside text,
   or the SVG won't parse. (There's a validator snippet below.)
4. **Reduced-motion** branch is mandatory for any animated asset.
5. **No external refs** — no webfonts, no `<image href="http…">`. Self-contained.

## Validate before you commit

```bash
python - <<'PY'
import glob, xml.dom.minidom as m
bad = 0
for f in glob.glob('assets/**/*.svg', recursive=True):
    try: m.parse(f)
    except Exception as e: bad += 1; print('FAIL', f, e)
print('All valid' if not bad else f'{bad} file(s) need fixing')
PY
```

A well-formed SVG that opens in a browser will render on GitHub. The most common
break is an unescaped `&` in an `aria-label` or `<text>`.
