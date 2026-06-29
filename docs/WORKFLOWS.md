# GitHub Actions — Explained

Three workflows keep the profile alive without any external server. All use
**least-privilege** permissions (`contents: write` only), **concurrency guards**
(no overlapping runs), **timeouts** (no hung jobs), and a **manual trigger**
(`workflow_dispatch`) so you can run them on demand.

| Workflow            | File                              | What it does                              | Token needed      |
| ------------------- | -------------------------------- | ----------------------------------------- | ----------------- |
| Contribution Snake  | `.github/workflows/snake.yml`    | Animated snake → `output` branch          | built-in          |
| GitHub Metrics      | `.github/workflows/metrics.yml`  | Rich stats SVG → `assets/metrics/`        | `METRICS_TOKEN`   |
| Recent Activity     | `.github/workflows/recent-activity.yml` | Fills the activity list in README  | built-in          |

> **One-time:** Settings → Actions → General → **Allow all actions and reusable workflows**.
> Then open the **Actions** tab and run each workflow once (▶ *Run workflow*).

---

## 1. Contribution Snake 🐍

```
schedule: every 12h · on push to main · manual
```

Uses [`Platane/snk`](https://github.com/Platane/snk) to render two SVGs
(a light palette and a dark palette tuned to our brand colors), then publishes
them to a dedicated **`output` branch** via `crazy-max/ghaction-github-pages`.

The README points a `<picture>` at the raw URLs on that branch:

```
…/KrishMaheshwari-pro/output/github-snake-dark.svg   (dark theme)
…/KrishMaheshwari-pro/output/github-snake.svg        (light theme)
```

**Why a branch instead of committing to main?** Generated binaries never touch
your source history, and the raw URLs stay stable. The images show blank until
the first successful run — that's expected.

---

## 2. GitHub Metrics 📈

```
schedule: daily 01:30 UTC · on push to main · manual
```

Uses [`lowlighter/metrics`](https://github.com/lowlighter/metrics) to render
`assets/metrics/github-metrics.svg` (committed back to `main`), embedded in the
README's collapsible **Detailed metrics** section. A placeholder SVG ships in
that path so the embed is never broken before the first run.

**Token setup (required for full data):**
1. Create a **classic** PAT with scopes `repo`, `read:user` (add `read:org`
   for org/private contributions). https://github.com/settings/tokens
2. Repo → **Settings → Secrets and variables → Actions → New repository secret**
   - Name: `METRICS_TOKEN`
   - Value: *your token*
3. Run the workflow.

Plugins enabled: languages (with %), iso-calendar (half-year), habits. Tune them
in `metrics.yml` — full plugin list at the metrics repo. See also
`.github/config/metrics.md`.

---

## 3. Recent Activity 🛰️

```
schedule: every 6h · manual
```

Uses [`jamesgeorge007/github-activity-readme`](https://github.com/jamesgeorge007/github-activity-readme)
to rewrite the block between these markers in `README.md`:

```html
<!--START_SECTION:activity-->
<!--END_SECTION:activity-->
```

No token setup — the built-in `GITHUB_TOKEN` is enough. `MAX_LINES: 5` keeps it
tidy. If you remove the markers, this workflow has nothing to update (and that's fine).

---

## Caching, errors & hygiene

- **Concurrency** — each workflow uses a `concurrency` group with
  `cancel-in-progress: true`, so a new run supersedes a stale one (no pile-ups,
  effectively a freshness cache).
- **Timeouts** — every job sets `timeout-minutes`, so a hung action fails fast
  instead of burning minutes.
- **Resilience** — Metrics degrades gracefully without a token rather than
  failing the profile; the README ships placeholders so missing generated images
  never render broken.
- **Least privilege** — only `contents: write`. No other scopes are requested.

## Troubleshooting

| Symptom                              | Fix                                                            |
| ------------------------------------ | ------------------------------------------------------------- |
| Snake image blank                    | Run the workflow once; confirm the `output` branch exists.    |
| Metrics shows the placeholder        | Add `METRICS_TOKEN`, then run "GitHub Metrics".               |
| Activity list never changes          | Ensure the `START/END_SECTION:activity` markers are intact.   |
| "Resource not accessible"            | Settings → Actions → Workflow permissions → **Read and write**. |
| Action won't start                   | Settings → Actions → General → allow actions.                 |
