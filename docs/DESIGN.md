# Design System

The profile is built on a small, strict token set. Every SVG references these
exact values — change them here **and** in the assets together, and the whole
profile stays coherent. The aesthetic target: *Linear / Vercel / Stripe* —
dark-first, calm, intentional, gradients used as accents only.

## Color tokens

| Token            | Hex        | Role                                  |
| ---------------- | ---------- | ------------------------------------- |
| `--bg`           | `#070A14`  | Page / deepest background             |
| `--bg-2`         | `#0B1024`  | Card background (top of gradient)     |
| `--surface`      | `#0E1530`  | Raised panels, chips, nodes           |
| `--border`       | `#1E2A45`  | Hairlines, card borders               |
| `--border-2`     | `#22305A`  | Inner panel borders                   |
| **Primary**      |            |                                       |
| `--blue`         | `#2E5BFF`  | Deep / royal blue — primary accent    |
| `--purple`       | `#8B5CF6`  | Royal purple — secondary accent       |
| `--cyan`         | `#22D3EE`  | Electric cyan — highlight / active    |
| **Text**         |            |                                       |
| `--text`         | `#F4F7FF`  | Headings, high-emphasis               |
| `--text-2`       | `#C7D2E8`  | Body text                             |
| `--slate`        | `#9AA7C2`  | Muted body / labels                   |
| `--muted`        | `#5E6B85`  | De-emphasised / future / meta         |

### The one gradient
`brand = #2E5BFF → #8B5CF6 → #22D3EE` (blue → purple → cyan).
Use it for **one** focal element per asset (a title, a rule, a progress fill) —
never as a fill behind text-heavy areas. Restraint is the whole point.

## Typography
- **Family:** `'Segoe UI', system-ui, -apple-system, sans-serif`.
  GitHub renders SVG text with the system font; we don't ship a webfont
  (camo won't fetch it), so we lean on **weight + letter-spacing** for character.
- **Display:** 800 weight, `letter-spacing: -0.5 to -1.5` (tight, modern).
- **Labels / eyebrows:** 600–700, `letter-spacing: +1.5 to +3.5`, uppercase.
- **Body:** 400–500, normal tracking.

## Spacing & shape
- Card radius **24px**; chips/nodes **13–17px**; tiles **9px**.
- Card padding **40px** desktop; inner panels **16–22px**.
- Hairlines **1.5px**; accent bars **4–5px**.

## Motion
- **Subtle by default.** Drift on glows (8–13s), one growth on load (timeline),
  slow pulses (4s), 9–12s wave loops.
- **Always** honour `prefers-reduced-motion` — every animated asset disables
  motion in that media query.
- No JavaScript (GitHub strips it). CSS keyframes + SMIL `<animate>` only.

## Theme behaviour
Custom SVGs are **self-contained dark cards on a transparent canvas**, so they
read on both GitHub Dark and Light. The only theme-switching asset is the
**snake** (`<picture>` with `prefers-color-scheme`). Third-party widgets use
`bg_color=00000000` to blend on both.
