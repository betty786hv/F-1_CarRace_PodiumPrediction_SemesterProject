# 🏎️ Formula 1 British Grand Prix — Podium Prediction
**CMSE 201 · Betty He**
 
---
 
## Overview
 
Can data predict who stands on the podium at Silverstone? This project uses historical Formula 1 race data (2019–2024) from the British Grand Prix to explore how starting grid position, fastest lap performance, and team history relate to race outcomes — and builds a machine learning model to predict podium finishers.
 
---
 
## Research Questions
 
1. Does starting grid position impact race result?
2. Can we predict which teams are likely to reach the podium using historical race data?
3. Is the driver who sets the fastest lap most likely to finish on the podium?
---
 
## Dataset
 
- Formula 1 season driver and race result CSVs for 2019–2024
- Filtered to **Silverstone (Great Britain)** races only to control for track layout and conditions
- Features used: `Starting_Grid`, `Finish_Position`, `Fastest_Lap`, `Team`
---
 
## Methods
 
### Data Cleaning & Preprocessing
- Dropped fully empty rows across all season datasets
- Filtered combined race results to Great Britain track only
- Converted non-numeric values (e.g. `'NC'`) to NaN and dropped incomplete rows
- Standardized column names and stripped whitespace from team names
### Exploratory Analysis
- **Scatter plot + regression line**: Starting Grid vs. Finish Position across all Silverstone races (2019–2024)
- **Pearson correlation**: r = 0.78 — strong positive relationship between starting and finishing position
- **Box plot**: Finish position distribution by fastest lap status — fastest lap achievers consistently finish in the top 3
### Machine Learning — Random Forest Classifier
- Grouped by team per race; labeled podium = top 3 finish
- Features: average starting grid position, best finish position, fastest lap count
- Train/test split with stratification (`random_state=1`)
- Predicted podium probability for each team in the test set
---
 
## Key Findings
 
- **Grid position strongly predicts finish position** (correlation = 0.78). Starting near the front is a significant advantage at Silverstone.
- **Fastest lap is a strong signal of competitiveness** — drivers achieving the fastest lap almost always finish in the top 3.
- **Top 3 predicted podium teams**: Mercedes, Red Bull Racing Honda RBPT, Alpine Renault
- Model achieved ~100% training accuracy (expected given the small dataset size)
---
 
## Limitations & Future Work
 
- Small dataset (6 years × ~20 drivers per race) leads to overfitting
- Class imbalance: far fewer podium finishers than non-podium
- Future improvements: add weather data, pit stop strategy, driver ratings, and expand to 10–20 years of Silverstone history
---
 
## Tools & Libraries
 
`Python` · `pandas` · `numpy` · `matplotlib` · `seaborn` · `scikit-learn`
 
---
 
## Repository Structure
 
```
├── CMSE_BettyHe_FinalProject.ipynb   # Full analysis and model
├── CMSE_FinalProject.pptx            # Final presentation slides
└── README.md
```
 
---
 
## Reflection
 
Looking back at the project, there are a few things I would improve:
 
- **Overfitting**: The model achieved ~100% training accuracy, which is a red flag given the very small dataset (~30–40 rows after filtering to Silverstone only). A cross-validation step would give a more honest picture of model performance.
- **Data leakage**: `Finish_Position` was used as both a feature and the basis for the `Team_Podium` label, meaning the model essentially already "knew" the answer. A stronger approach would use only `Starting_Grid` and `Fastest_Lap` count as features.
- **Model interpretability**: Adding a confusion matrix would make the results clearer and more meaningful to viewers unfamiliar with accuracy scores alone.
---
 
## Course
 
CMSE 201 — Introduction to Computational Modeling, Michigan State University
 
