# FIFA Players Market Value — Exploratory Data Analysis

Exploratory data analysis on the [FIFA Players Dataset](https://www.kaggle.com/datasets/luisfucros/fifa-players-dataset) (17,954 players) to understand what drives a football player's market value.

## Research Questions

1. Does a higher overall rating necessarily mean a higher market value?
2. Which skill groups (attacking, playmaking, athletic, defending) have the strongest relationship with market value?
3. How does age affect a player's market value?
4. How does growth potential relate to the current market value of young players?

## Data Preparation

- Removed irrelevant columns (personal info, national team stats, etc.) and rows with missing `value_euro`.
- Excluded goalkeepers from the skill-based analysis, since the skill framework was built for outfield players.
- Engineered four aggregated skill scores from 29 individual attributes: `attacking_score`, `playmaking_score`, `athletic_score`, `defending_score`.
- Applied a log transform (`log_value_euro`) to reduce skew in market value.
- Created `growth_potential` (`potential - overall_rating`) and `age_group` (4 bins) as additional features.
- Kept outliers — extreme valuations reflect real football superstars, not data errors.
- Final dataset: **15,675 outfield players, 20 columns**, no missing values or duplicates.

## Key Findings

- **Overall rating** has a very strong relationship with market value — correlation of **0.949** with log market value (≈90% of variance explained, R²).
- Among skill groups, **playmaking** correlates most strongly with value (**0.679**), followed by attacking (0.577) and athletic (0.560). **Defending** has the weakest relationship (0.238) — though that doesn't make it unimportant on the pitch.
- Market value rises from the **Young Talent** stage through **Peak** and **Experienced**, then declines in the **Veteran** stage (34+).
- For young players, higher **growth potential does not mean higher current value** — there's actually a weak-to-moderate negative correlation (**-0.269**). The highest current valuations belong to players with already-high current ability, not the highest potential ceiling.

## Conclusion

Current ability (overall rating) is a far stronger driver of market value than future potential. Skill profile matters too — playmaking ability stands out among the four skill groups. But no single factor fully explains a player's price: age, current ability, skill composition, and potential interact together.

## Tools

Python, Pandas, NumPy, Matplotlib, Seaborn

## Project Structure

```
├── players.ipynb          # full analysis notebook
├── Data/
│   ├── fifa_players.csv       # original dataset (Kaggle)
│   └── raw_skills_data.csv    # backup of the 29 raw skill attributes before aggregation
└── charts/                # exported chart images from the analysis
```