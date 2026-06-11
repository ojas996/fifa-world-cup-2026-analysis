# FIFA World Cup 2026 — Data Analysis & Match Predictor

**Built by Ojas Jamdar** | 2nd Year ECE Student, VIT Mumbai

Live prediction accuracy tracked throughout the tournament.
Full accuracy report published post-tournament.

---

## What This Is

A stats-based match prediction system and squad value analyzer
for the 2026 FIFA World Cup — built on 49,378 international
results from 1872 to 2026. No machine learning — pure Pandas,
weighted scoring, and honest data.

---

## Two Tracks

### Track 1 — Match Predictor
Weighted scoring model built on recent competitive match data
for all 48 WC 2026 teams.

| Feature | Weight |
|---|---|
| Win rate (last 40 competitive matches) | 35% |
| FIFA ranking score | 30% |
| Goal difference per game | 25% |
| Goals scored per game | 10% |

**Adjustments applied:**
- Confederation strength multipliers on goal difference
  (OFC and weak CONCACAF opposition discounted)
- Low confidence overrides for teams with <15 meaningful
  competitive matches (New Zealand, Curaçao)
- Fixed 24% draw probability reflecting WC group stage averages

**Confidence tiers:** Every prediction rated High / Medium / Low
based on probability margin between the two teams.

### Track 2 — Squad Value Analysis
Transfermarkt squad market values across all 32 nations.

Charts produced:
- Squad value rankings — all 32 nations by continent
- Value vs FIFA ranking scatter — who is overpriced, who is undervalued
- Underdog index — best ranked teams relative to squad cost

---

## Accuracy Tracking

All 48 group stage predictions logged before June 11 (tournament
kickoff). Results updated after every match.

Tracked metrics:
- Overall accuracy %
- Accuracy by confidence tier (High / Medium / Low)
- Accuracy by stage
- Most confident wrong predictions

Full accuracy report: LinkedIn Post 8 (post-tournament)

---

## Key Data Decisions

**Why n_matches=40?**
Using 20 matches made features too sensitive to short bad patches.
40 matches gives stable, reliable averages for active nations.

**Why fixed 24% draw probability?**
Real World Cup group stage draw rates sit at 23–25%.
A fixed allocation is honest and consistent across all predictions.

**Why confederation multipliers?**
New Zealand's goal difference was 4.0 from beating Tahiti, Vanuatu,
and Samoa. Curaçao's wins came largely against Barbados, Saint Martin,
and Aruba. Raw stats from weak opposition are noise, not signal.

**Draws counted as wrong predictions.**
If the model predicts Argentina and the match ends in a draw,
that counts as incorrect. Draws are the hardest outcome to predict
and penalising them keeps the accuracy tracking honest.

---

## Tech Stack

Python · Pandas · Matplotlib · Seaborn · Jupyter · VS Code

---

## Data Sources

| Source | Contents |
|---|---|
| Kaggle | 49,378 international results, 1872–2026 |
| football-data.org API | WC 2026 fixtures, 104 matches |
| Transfermarkt via Kaggle | Squad market values, all 32 nations |

---

## Project Structure

world-cup-2026/
├── data/
│   ├── results.csv               # 49,378 historical matches
│   ├── wc_2026_fixtures.csv      # 104 WC 2026 fixtures
│   ├── team_features.csv         # engineered features, 48 teams
│   ├── squads.csv                # Transfermarkt squad values
│   └── predictions.csv           # live predictions + results
├── charts/
│   ├── squad_values_all32.png
│   ├── value_vs_ranking.png
│   ├── underdog_index.png
│   └── ...match prediction charts
├── analysis.ipynb
├── requirements.txt
└── README.md

---

## V2 Roadmap 

- Replace weighted scoring with Logistic Regression
- Add recency weighting — 2025 matches count more than 2018
- Add head-to-head historical record as explicit feature
- Add tournament experience feature
- Add squad age feature
- Data-driven draw probability replacing fixed 24%
- Confidence score per prediction based on model output

V2 will be evaluated by running it retroactively on 2026 WC matches
and comparing accuracy against V1.

---

## Modeling Limitations 

- No injury data
- No squad selection / manager decisions
- No home advantage modelling (this WC has 3 co-hosts)
- No tournament experience weighting in V1
- Draw prediction not attempted — draws logged as wrong
- Small dataset teams (New Zealand, Curaçao) use manually
  adjusted conservative estimates