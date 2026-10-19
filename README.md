# NBA PPG Predictor

Predicting how a player's points per game (PPG) will change from one NBA
season to the next, using data from many players.

This is a learning project on applied machine learning. The goal is to
understand each step (data, features, validation, evaluation), not only to
get a number.

## Approach

- **Unit of analysis:** one row per player-season. The target is
  `PPG(next season) - PPG(this season)`.
- **Features:** age, minutes, games played, shooting volume and efficiency,
  usage rate, and PPG from previous seasons.
- **Baselines:** last season's PPG, and the average of the last 3 seasons.
  Any model has to beat both.
- **Validation:** temporal, not random. Train on older seasons, tune on a
  validation set, and use the test set once at the end.
- **Evaluation:** overall error and error by group (young players, veterans).
- **Final step:** predict the 2026-27 season and compare against reality
  when it ends.

## Status

- [x] 1. Data download and merge (2013-14 to 2025-26)
- [ ] 2. Cleaning and feature construction (in progress)
- [ ] 3. Baselines
- [ ] 4. First model
- [ ] 5. Evaluation and tuning
- [ ] 6. 2026-27 predictions

## Data

Season stats come from NBA.com through the
[`nba_api`](https://github.com/swar/nba_api) package. The data is not
included in this repository: run `01_download.ipynb` to download it.
Please respect NBA.com's terms of use.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Then run the notebooks in order, from the project root.

## Structure

```
01_download.ipynb   # download and merge season stats
02_features.ipynb   # cleaning, target and lag features
data/               # generated locally, not tracked
```

## Known limitations

- Players traded mid-season appear as a single row with full-season stats.
- Players who retire have no next-season target, which can bias training.
