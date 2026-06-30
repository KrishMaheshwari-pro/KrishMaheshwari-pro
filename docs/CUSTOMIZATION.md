# Customization Guide

Everything you'd want to change, in the order you'd change it. No build step —
edit files, commit, done.

---

## 1. Make it yours (find & replace)

Run these replacements across the whole repo (your editor's "Replace in Files"):

| Find                        | Replace with                          | Appears in            |
| --------------------------- | ------------------------------------- | --------------------- |
| `KrishMaheshwari-pro`       | your GitHub username                  | README, workflows     |
| `Krish Maheshwari`          | your name                             | README, assets        |
| `Altus Corp`                | your company / employer               | README                |
| `krishmaheshwari111@gmail.com` | your email                         | README                |
| `krishmaheshwari07`         | your Instagram handle                 | README                |
| `krishmaheshwari.vercel.app` | your portfolio domain                | README                |
| `linkedin.com/in/krish--maheshwari` | your LinkedIn URL            | README                |

> ⚠️ The repo **must** be named exactly like your username
> (`your-username/your-username`) for GitHub to show it on your profile.

All image paths are **relative**, so nothing else needs editing once renamed.

---

## 2. The visual assets

The hand-authored SVGs live in `assets/`. The two you'll most likely touch:

- `banners/hero-banner.svg` — name, eyebrow, rotating role words, chips
- `cards/highlights.svg` — Highlights stat counters
- `cards/achievements.svg` — Honors & Awards card

Want to recolor them? See `docs/ASSETS.md`.

---

## 3. Change the colors

All colors live as literal hex in the SVGs and as widget URL params. To rebrand:

1. Pick your three accents (replace `#2E5BFF`, `#8B5CF6`, `#22D3EE`).
2. Find-and-replace those hex values across `assets/**/*.svg`.
3. Update the same three in the **widget URLs** in `README.md`
   (`title_color`, `icon_color`, `line`, `point`, `ring`, `fire`, …).
4. Update the token table in `docs/DESIGN.md` so future-you remembers.

Backgrounds: `#070A14`, `#0B1024`, `#0E1530`. Borders: `#1E2A45`, `#22305A`.

---

## 4. Edit the copy

- **Hero text** → `assets/banners/hero-banner.svg` (name, eyebrow, role words, chips).
- **About / projects / experience / education** → `README.md` (plain Markdown — easiest to edit).
- **Tech stack** → `README.md` (shields.io badges — one line per tool).

---

## 5. The dynamic widgets (optional, replaceable)

These call maintained third-party render services. They're themed to match; if
any ever goes down, the rest of the profile still looks intact. To swap or drop:

| Widget            | Source                                   | In README   |
| ----------------- | ---------------------------------------- | ----------- |
| Typed subtitle    | `readme-typing-svg.demolab.com`          | hero        |
| Stats / Top langs | `github-readme-stats.vercel.app`         | GitHub Stats |
| Streak            | `github-readme-streak-stats.herokuapp…`  | GitHub Stats |
| Activity graph    | `github-readme-activity-graph.vercel…`   | GitHub Stats |
| Trophies          | `github-profile-trophy.vercel.app`       | GitHub Stats |
| Profile views     | `komarev.com/ghpvc`                       | hero        |

The **snake**, **metrics**, and **recent activity** are **self-hosted** via
GitHub Actions (`.github/workflows/`) — see `docs/WORKFLOWS.md`.

---

## 6. First-run checklist

- [ ] Repo renamed to `your-username/your-username`
- [ ] Find-and-replace table above applied
- [ ] Brand logos swapped
- [ ] **Settings → Actions → General → Allow all actions**
- [ ] Run **Contribution Snake**, **GitHub Metrics**, **Recent Activity** once each
- [ ] (Metrics only) add `METRICS_TOKEN` secret — see `docs/WORKFLOWS.md`
- [ ] Pin your best repositories (Profile → Customize your pins)
