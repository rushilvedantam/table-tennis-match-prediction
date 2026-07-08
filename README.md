# Table Tennis Match Outcome Prediction

A logistic regression model that predicts the winner of a professional table tennis match using in-match scoring data. Built for CIS 406 (AI Foundations in Business) at Arizona State University, April 2026.

## Overview

Using a dataset of ~4,275 professional matches, this project explores whether a match's outcome can be predicted from early scoring patterns and player identity — before the match is finished. The motivation ties back to my own experience coaching competitive table tennis: early-game momentum is something coaches talk about anecdotally, and I wanted to see if it held up statistically.

## Data

- **Source:** `LigaProTableTennis.csv` — professional match records including per-game scores (up to 5 games), player names, and match outcome
- **Size:** ~4,275 matches after cleaning
- **Cleaning:** converted score columns to numeric, dropped incomplete records, parsed match dates

## Approach

1. **Feature engineering** — created `g1_margin` and `g2_margin` (point differential in the first two games) and a `p1_games_won_first2` feature capturing early momentum
2. **Baseline model** — logistic regression using only first-two-game margins
3. **Improved model** — added player identity (one-hot encoded) to capture consistent skill differences between players
4. **Model iteration** — added match timing features (hour, day of week) to test for scheduling effects

## Results

| Model | Accuracy | ROC AUC |
|---|---|---|
| Baseline (game margins only) | 75.3% | 0.837 |
| + Player identity | 77.0% | 0.840 |
| + Match timing | 77.1% | 0.840 |

## Key Takeaways

- Performance in the first two games is a strong predictor of final match outcome — a player who wins both early games or has a strong point margin is substantially more likely to win overall
- Adding player identity improved predictions, suggesting some players are consistently stronger regardless of early-game momentum — skill and momentum both matter
- Match timing features (hour, day of week) added negligible predictive value

## Potential Applications

Live match win-probability estimates, sports commentary/broadcast graphics, and performance tracking for coaches and players.

## Tools

Python, pandas, scikit-learn (Logistic Regression, ColumnTransformer, OneHotEncoder), matplotlib, seaborn
