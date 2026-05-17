# NFL-Offensive-Evolution-Analysis (2003 - 2023)
Exploratory data analysis of NFL team offense trends (2003–2023) utilizing regression modeling within Python.

---

## Project Overview

Popular among NFL fans is the belief that the NFL has entered a 'golden age' of offensive production, primarily due to rule changes and schematic innovations. The goal of this project is to conduct a thorough exploration of this claim, utilizing a plethora of tangible variables such as scoring, passing, and rushing trends over the years (2003 - 2023), in order to understand how the game has changed over time. Our main focus will be on total yardage volumes by type (rushing vs passing), and how these relationships correlate with scoring outcomes in order to determine whether the data supports the widely held belief that the shift toward pass-heavy schemes is the primary driver behind the NFL's rising offensive output over the years.

**Central question:** *Do passing yards impact scoring more than rushing yards, and does this help explain why modern NFL teams score more points?*

---

## Dataset

- **Source:** [Kaggle — NFL Team Data 2003–2023](https://www.kaggle.com/datasets/nickcantalupa/nfl-team-data-2003-2023)
- **Dimensions:** 672 rows × 35 columns (32 teams × 21 seasons)
- **Key variables:** `points`, `pass_yds`, `rush_yds`, `wins`, `yds_per_play_offense`, `penalties`, `turnovers`, `pass_td`, `rush_td`, and more

---

## Section Breakdown

**Section 1 — Data Cleaning**
- Verified dataset dimensionality (672 × 35) against source documentation
- Imputed missing `mov` (margin of victory) values by computing `points_diff / g`
- Replaced missing `ties` values with 0
- Consolidated renamed/relocated franchises (e.g., Oakland Raiders → Las Vegas Raiders) to maintain complete franchise histories

**Section 2 — Exploratory Data Analysis**
- Visualized year-over-year mean points scored using grouped bar charts
- Compared 2003 vs. 2023 passing and rushing distributions via pair plots
- Used cross-tabulation with quartile binning to examine the relationship between yards-per-play efficiency and win totals
- Computed correlations between penalties and both year and wins to evaluate the "refs are changing the game" narrative

**Section 3 — Inference**
- Formulated null/alternative hypotheses around the relative impact of passing vs. rushing yards on scoring
- Fit separate OLS regression models (via `statsmodels`) for passing yards → points and rushing yards → points
- Fit a combined multivariate OLS model to control for both variables simultaneously
- Evaluated statistical significance via p-values and compared coefficients

**Section 4 — Prediction**
- Built a multiple linear regression model (`scikit-learn`) using `pass_yds` and `rush_yds` to predict season point totals
- Applied an 80/10/10 train/validation/holdout split
- Evaluated model performance with RMSE across all three sets

---

## Key Findings

- **Scoring has steadily increased** across all 21 seasons, supporting the premise that modern NFL offenses are more prolific.
- **Passing yards carry a marginally greater impact on scoring** than rushing yards (OLS coefficients: 0.0777 vs. 0.0700 points per yard), which aligns with the league-wide shift toward pass-heavy schemes.
- **Teams are passing significantly more in 2023 than in 2003**, with rushing attempts trending downward, suggesting a structural shift in offensive philosophy across the board.
- **Penalties have a near-zero correlation with year** (r ≈ −0.05), challenging a somewhat popular narrative that increased penalty calls are a primary driver of higher scoring.
- **Penalties also show no meaningful correlation with wins**, suggesting referee influence on outcomes is minimal in aggregate.
- **The model achieved consistent RMSE (~39 points) across train, validation, and holdout sets**, indicating no overfitting, although the model does not account for potential factors such as turnovers or possible home-field advantage.

---

## Libraries Used

- Pandas
- NumPy
- Matplotlib
- Seaborn
- Statsmodels
- Scikit-learn
