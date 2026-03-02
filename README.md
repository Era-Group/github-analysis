<div align="center">

# 📊 GitHub Activity Comparator

**Compare your GitHub activity across any two time periods — visualized, analyzed, and exported.**
A zero-dependency, single-file tool that puts your real commit history, PRs, and code changes side-by-side so you can see exactly how your workflow has shifted over time.

[![Single File](https://img.shields.io/badge/Architecture-Single%20HTML%20File-58a6ff?style=for-the-badge)]()
[![No Dependencies](https://img.shields.io/badge/Dependencies-Zero%20(CDN%20only)-3fb950?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-GPL--3.0-d29922?style=for-the-badge)](LICENSE)

![Dark theme dashboard preview](.github/preview-dark.png)

</div>

---

## ✨ What It Does

Pick any two date ranges, select your repositories, and instantly see how your GitHub activity compares between them — commit frequency, lines of code, PR throughput, issue close rates, and more.

Everything runs entirely in your browser. No server, no account, no tracking. Just your GitHub token and your data.

---

## 🚀 Features

### 📈 Activity Score
A weighted composite metric combining commit frequency, lines of code, files changed, and PR throughput — normalized between periods so both are always comparable regardless of length.

### 🗂 6 Dashboard Sections

| Section | What you get |
|---|---|
| **Overview** | KPI cards with delta %, commits-over-time line chart |
| **Charts** | Code volume, language breakdown, daily activity bar, changed lines per week |
| **Heatmap** | Side-by-side calendar heatmaps for both periods |
| **PRs & Issues** | Per-repository table with merge times and issue close rates |
| **Repositories** | Card grid with per-repo stats + click-to-expand modal with recent commits |
| **Insights** | Auto-generated analysis paragraphs comparing both periods, in **English and Arabic** |

### 📤 Export Everything
- **JSON** — full raw data payload
- **CSV Summary** — all metrics in one spreadsheet-ready file
- **CSV Commits** — per-commit log for either period
- **PNG Charts** — export any individual chart as an image
- **All Charts** — download all 5 charts as PNGs in one click

### 🌍 Bilingual & Themeable
- Full **Arabic / English** UI toggle with RTL layout support
- **Dark / Light** theme toggle
- Persists your preferences in `localStorage`

### ⚡ Smart API Usage
- Paginated GitHub API calls (`per_page=100`)
- Live **rate-limit badge** showing remaining requests
- Retry logic for stats endpoints (GitHub returns `202` while computing)
- Batched concurrent commit-stat fetching (max 10 in parallel)

---

## 🛠 How to Use

### Option A — Open directly (no server needed)
```
git clone https://github.com/sadeem-cloud-org/github-analysis.git
open index.html
```

### Option B — GitHub Pages
1. Fork this repo
2. Go to **Settings → Pages → Source → main branch / root**
3. Your dashboard is live at `https://sadeem-cloud-org.github.io/github-analysis/`

### Option C — Any static host
Just upload `index.html` to Netlify, Vercel, S3, or any web server. One file, done.

---

## 🔑 GitHub Token Setup

The dashboard needs a **Personal Access Token** with `repo` scope to read your commit and PR history.

1. Go to [github.com/settings/tokens/new](https://github.com/settings/tokens/new?scopes=repo&description=Productivity+Analytics)
2. Check the `repo` scope
3. Click **Generate token** and paste it in the setup screen

> Your token is stored only in your browser's `localStorage`. It is never sent anywhere except directly to the GitHub API.

---

## 📐 Architecture

```
index.html  (~2,450 lines, ~90 KB)
│
├── CSS          Design tokens, dark/light theme, RTL, all component styles
├── HTML         4 screens: Setup → Config → Dashboard → (modal overlays)
└── JavaScript
    ├── i18n     English + Arabic translation map
    ├── API      ghPaginate(), ghStats(), ghJson() — all GitHub calls
    ├── Render   Chart.js charts, heatmap, KPI cards, PR table, repo cards
    ├── Score    calcScore() + normalizeScore() — productivity formula
    ├── Export   JSON / CSV / PNG / all-charts
    └── UI       Theme, language, navigation, modal, keyboard shortcuts
```

**Dependencies:** [Chart.js 4.4.0](https://www.chartjs.org/) via CDN — that's it.

---

## 📊 Activity Score Formula

```
score = (commitFreq × 30) + (linesPerDay × 0.5) + (mergedPRs × 5) + (filesPerDay × 2)
```

Both periods are normalized to a 0–100 scale so the scores are always comparable regardless of period length.

---

## 🖼 Screenshots

> **To add screenshots:** take your screenshots, then upload them to the `.github/` folder in this repo
> (create it if it doesn't exist). Name them exactly as referenced below and they'll appear here automatically.

| File to upload | What to capture |
|---|---|
| `.github/preview-dark.png` | Full dashboard in dark mode (hero image at the top) |
| `.github/screenshot-setup.png` | The setup / token entry screen |
| `.github/screenshot-overview.png` | Overview section with KPI cards and commits chart |
| `.github/screenshot-charts.png` | Charts section showing code volume & language breakdown |
| `.github/screenshot-repos.png` | Repositories card grid or the repo details modal |

<table>
  <tr>
    <td><b>Setup Screen</b></td>
    <td><b>Overview (Dark)</b></td>
  </tr>
  <tr>
    <td><img src=".github/screenshot-setup.png" width="400"/></td>
    <td><img src=".github/screenshot-overview.png" width="400"/></td>
  </tr>
  <tr>
    <td><b>Charts Section</b></td>
    <td><b>Repository Details Modal</b></td>
  </tr>
  <tr>
    <td><img src=".github/screenshot-charts.png" width="400"/></td>
    <td><img src=".github/screenshot-repos.png" width="400"/></td>
  </tr>
</table>

---

## 🤝 Contributing

Issues and PRs are welcome. Since the entire app is one HTML file, contributions are as simple as editing `index.html`.

```bash
git clone https://github.com/sadeem-cloud-org/github-analysis.git
cd GithubDashboard
# Edit index.html, open in browser, done.
```

---

## 📄 License

GPL-3.0 — see [LICENSE](LICENSE) for details.

---

<div align="center">
  <sub>Built with vanilla HTML + CSS + JS. No build tools. No frameworks. No nonsense.</sub>
</div>
