# Event Study: Dividend Announcements & Abnormal Returns

> Empirical finance project measuring the stock market reaction to dividend announcements using the market model and cumulative abnormal returns (CARs).

## Overview

This project implements a full **event study methodology** on US equity data to test whether dividend announcements generate statistically significant abnormal returns. We follow the standard Brown & Warner (1985) framework: estimate normal returns using the market model, compute abnormal returns around the event date, and test for significance across multiple event windows.

## Research Question

*Do dividend announcements generate statistically significant abnormal returns, and over what horizon does the market react?*

## Dataset

- **Returns data:** CRSP daily stock returns (`daily_returns_new.dta`)
- **Events data:** Dividend announcement dates (`dividend_events.csv`)
- **Coverage:** US equities identified by PERMNO
- **Note:** CRSP data requires a subscription. The code is fully replicable with any dataset matching the required format (columns: `PERMNO`, `date`, `DlyRet`, `DlyCap`).

## Methodology

**1. Estimation window:** (-250, -30) trading days relative to event date
- OLS market model: `R_it = α + β · R_mt + ε_it`
- Market return = equal-weighted average across all firms on each date

**2. Event windows tested:**
| Window | Description |
|---|---|
| (-1, +1) | Immediate reaction |
| (-5, +5) | Short-term reaction |
| (-10, +10) | Medium-term reaction |

**3. Statistical tests:**
- Daily abnormal return t-tests (AR_t)
- CAR t-tests for each event window
- Results reported with mean CAR, t-statistic, sample size and significance stars (*, **, ***)

## Key Results

- Statistically significant **positive CARs** detected around dividend announcement dates
- Effect strongest in the (-1, +1) window, consistent with semi-strong market efficiency
- Full results reproducible by running the notebook

## Repository Structure

```
├── Group_2_assignment_1.ipynb    # Full pipeline: data loading, market model, AR/CAR computation, t-tests
├── daily_returns_new.dta         # CRSP daily returns (not included — requires CRSP subscription)
├── dividend_events.csv           # Dividend announcement events
└── README.md
```

## Requirements

```
pandas
numpy
matplotlib
scipy
statsmodels
tqdm
```

Install with:
```bash
pip install -r requirements.txt
```

## References

- Brown, S. J., & Warner, J. B. (1985). *Using daily stock returns: The case of event studies.* Journal of Financial Economics, 14(1), 3–31.

## Author

Leonardo Trapani — *Empirical Methods for Finance*, Erasmus School of Economics, 2025
