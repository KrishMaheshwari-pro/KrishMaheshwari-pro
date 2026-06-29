# Metrics configuration notes

The **GitHub Metrics** workflow (`.github/workflows/metrics.yml`) renders
`assets/metrics/github-metrics.svg`. This file documents what's enabled and how
to extend it.

## Enabled plugins

| Plugin        | Setting                              | Shows                              |
| ------------- | ------------------------------------ | ---------------------------------- |
| Base          | `header, activity, community, repositories, metadata` | Core profile summary |
| Languages     | `plugin_languages` + `details: percentage` (limit 8) | Most-used languages |
| Iso-calendar  | `plugin_isocalendar` (`half-year`)   | 3D-style contribution calendar     |
| Habits        | `plugin_habits` + charts             | Coding time-of-day & patterns      |

Timezone is `Asia/Kolkata` so streaks and habits align to your day.

## Add more

The metrics action ships **40+ plugins** (wakatime, music, stars, topics,
achievements, …). To add one:

1. Open `metrics.yml`.
2. Add `plugin_<name>: yes` plus any options.
3. Some plugins need extra secrets/tokens — check the plugin's docs:
   https://github.com/lowlighter/metrics/tree/master/source/plugins

Keep the SVG readable — 4–6 plugins is the sweet spot. More than that and the
image gets tall and slow to load, which works against the "premium, fast" goal.

## Token

`METRICS_TOKEN` (classic PAT, scopes `repo` + `read:user`) must be set as a repo
secret for private/complete data. Without it the workflow still runs with public
data only. Setup steps are in `docs/WORKFLOWS.md`.
