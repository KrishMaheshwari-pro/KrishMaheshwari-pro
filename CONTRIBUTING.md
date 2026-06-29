# Contributing & Customizing

This repository is **Krish Maheshwari's GitHub profile** (`KrishMaheshwari-pro/KrishMaheshwari-pro`).
It renders automatically on the profile page because the repo name matches the username.

It is also built to be **forked and re-skinned**. Whether you found this because you
want to suggest an improvement, or because you want to use it as a starting point for
your own profile — welcome. Here's how everything fits together.

---

## Repository map

```
.
├── README.md                     ← the profile (everything you see on the page)
├── LICENSE                       ← MIT
├── CONTRIBUTING.md               ← you are here
│
├── .github/
│   ├── workflows/                ← automation (snake, metrics, recent activity)
│   │   ├── snake.yml
│   │   ├── metrics.yml
│   │   └── recent-activity.yml
│   └── config/
│       └── metrics.md            ← what the metrics workflow renders & how to tune it
│
├── assets/
│   ├── banners/                  ← the hero banner (animated SVG, dark + light)
│   ├── svg/                      ← reusable wave / section dividers & patterns
│   ├── logos/                    ← Altus + Productivity Shastra marks, KM monogram
│   ├── illustrations/            ← architecture diagram, roadmap timeline
│   └── cards/                    ← tech-stack panels, company card
│
└── docs/
    ├── CUSTOMIZATION.md          ← change your name, links, colors, copy
    ├── WORKFLOWS.md              ← every GitHub Action, explained line by line
    ├── DESIGN.md                 ← the design system (tokens, type, spacing)
    └── ASSETS.md                 ← how each SVG is built & how to edit it
```

---

## Quick start (fork → make it yours)

1. **Fork** this repo, then **rename** it to your own username (e.g. `your-username/your-username`).
2. Open [`docs/CUSTOMIZATION.md`](docs/CUSTOMIZATION.md) and run the find-and-replace table.
3. Swap the brand marks in `assets/logos/` for your own (same `viewBox`, drop-in).
4. Enable Actions (**Settings → Actions → General → Allow all**), then run each workflow
   once from the **Actions** tab so the dynamic SVGs generate.
5. Commit. The profile page updates within a minute.

Everything is **relative-path** based, so once renamed, no URLs need editing.

---

## Suggesting a change (PRs welcome)

- Keep the **design tokens** in [`docs/DESIGN.md`](docs/DESIGN.md) as the single source of truth —
  if you touch a color, change it there and in the SVGs that reference it.
- SVGs are **hand-authored and commented**. Match the existing style: 2-space indent,
  grouped `<g>` layers with `id`s, animations via `<animate>`/CSS keyframes only
  (no JavaScript — GitHub strips it).
- No new third-party render services without a fallback. The goal is a profile that
  still looks intentional even if an external widget goes down.
- Test your SVG by opening it directly in a browser **and** by checking it on a GitHub
  Markdown preview (camo caching strips some features — see `docs/ASSETS.md`).

## Reporting something broken

Open an issue with the section name, a screenshot, and whether you're on
**GitHub Dark** or **GitHub Light**. Theme-specific rendering bugs are the most common.

---

Thanks for reading. Build something that feels like *yours*. 🛠️
