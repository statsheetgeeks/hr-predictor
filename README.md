# hr-predictor

# ⚾ HR Scout — GitHub Pages Edition

MLB home run prediction dashboard. You update `predictions.json` each morning
by hand — no API keys, no automation, no build step required.

---

## Setup (one-time, ~5 minutes)

### 1. Create a GitHub repo and enable Pages

Go to **Settings → Pages → Source** → branch: `main`, folder: `/ (root)`.

Your site will be live at `https://your-username.github.io/repo-name/`

### 2. Push these three files

```
index.html          ← the dashboard (never needs editing)
predictions.json    ← placeholder; you overwrite this each morning
history/            ← optional per-day archive folder
```

That's it. No secrets, no Actions, no dependencies.

---

## Daily workflow (each morning)

```
1. Run notebook cells 1–4  →  generates the Claude prompt
2. Paste prompt into Claude.ai
3. Copy Claude's JSON response
4. Overwrite predictions.json with the JSON
5. git add predictions.json && git commit -m "predictions $(date +%Y-%m-%d)" && git push
```

The site updates the moment you push. Anyone visiting the URL sees the new
rankings immediately — the page fetches `predictions.json` on every load.

### One-liner (Mac)

```bash
# After copying Claude's JSON from the chat:
pbpaste > predictions.json
cp predictions.json "history/$(date +%Y-%m-%d).json"
git add predictions.json history/
git commit -m "predictions $(date +%Y-%m-%d)"
git push
```

### One-liner (Windows PowerShell)

```powershell
Get-Clipboard | Out-File predictions.json -Encoding utf8
Copy-Item predictions.json "history/$(Get-Date -Format yyyy-MM-dd).json"
git add predictions.json history/
git commit -m "predictions $(Get-Date -Format yyyy-MM-dd)"
git push
```

---

## Tracking accuracy

After games complete:
1. Paste Claude's JSON into the `PREDICTIONS` variable in **Cell 5** of the notebook
2. Run Cell 5 and enter y/n for each player
3. Commit the updated `hr_scout_results.json` to the repo
4. The **History** tab on the site shows calibration data automatically

---

## File structure

```
your-repo/
├── index.html                ← dashboard (load-and-forget)
├── predictions.json          ← overwrite this each morning
├── hr_scout_results.json     ← optional: commit after logging results
└── history/
    ├── 2026-04-10.json
    ├── 2026-04-11.json
    └── ...
```

---

*FOR ENTERTAINMENT ONLY — do not use for wagering.*
