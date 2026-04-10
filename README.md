# hr-predictor

# ⚾ HR Scout — GitHub Pages Edition

Fully self-contained MLB home run prediction dashboard.
No AI, no API keys. Pure Python statistical scoring from live MLB/Statcast data.

---

## How it works

```
Notebook Cell 1-5 (run each morning)
  ├── Fetch today's schedule, lineups, probable pitchers  (MLB Stats API)
  ├── Fetch Statcast power metrics                        (pybaseball)
  ├── Fetch weather for outdoor parks                     (Open-Meteo)
  ├── Score every batter with built-in statistical model
  │     batter_score   40% — barrel%, hard-hit%, ISO, exit velo, HR rate
  │     pitcher_score  35% — HR/9, HR/BF, hard-hit allowed
  │     park_score     15% — park HR factor by batter hand
  │     weather_score  10% — wind direction & speed
  ├── Save predictions.json → git push
  └── GitHub Pages serves updated rankings immediately
```

---

## Setup (one-time)

### 1. Enable GitHub Pages

Go to your repo → Settings → Pages → Source → branch: main, folder: / (root).

### 2. Push these files

```
index.html             ← the dashboard (never needs editing)
predictions.json       ← placeholder; overwritten by the notebook
hr_scout_v4.ipynb      ← the pipeline notebook
history/               ← auto-created by Cell 5
```

### 3. Set REPO_PATH in Cell 2

```python
REPO_PATH = '/Users/you/projects/hr-scout'  # path to your local repo clone
```

---

## Daily workflow

Run the notebook top-to-bottom each morning:

| Cell | What it does |
|------|-------------|
| 1 | Install deps (run once) |
| 2 | Set date, config |
| 3 | Fetch MLB schedule, lineups, Statcast, weather |
| 4 | Score all batters — prints top 10 preview |
| 5 | Save predictions.json, archive to history/, git push |

The website updates the moment Cell 5 finishes.

---

## After games: track accuracy

Run Cell 6 the same evening. It prompts y/n for each player,
saves hr_scout_results.json, and pushes it. The History tab on the
site shows cumulative calibration data automatically.

---

## Scoring model

Composite = batter(40%) + pitcher_vulnerability(35%) + park(15%) + weather(10%)

Batter score uses: barrel%, hard-hit%, ISO, HR/PA, avg exit velo, FB%
Pitcher vulnerability uses: HR/9, HR/BF, hard-hit% allowed, ERA
Park score uses: park HR factor by batter handedness
Weather score uses: wind direction/speed adjustment for outdoor parks

---

*FOR ENTERTAINMENT ONLY — do not use for wagering.*
