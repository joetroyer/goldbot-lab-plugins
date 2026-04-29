---
description: Create a new backtest scenario — generates a YAML, runs the backtest, and returns results. Use when Joe wants to test a new split strategy, friction preset, or time window.
argument-hint: --provider gs|ceddi --strategy SPLIT --friction PRESET [--window WINDOW] [--name NAME] [--no-persist]
allowed-tools: Bash
---

Run the create-scenario script and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-create-scenario/scripts/create.sh $ARGUMENTS`

Read the JSON output above and give Joe a clear summary:

1. **Created**: Scenario name, provider, window, YAML path
2. **Results**: N signals input, N trades placed, win rate %, profit factor, max drawdown %
3. **Verdict**: Is this a viable scenario? Flag if profit factor < 1.0 or max drawdown > 20%.
4. **Next step**: Suggest running lab-fetch-scenarios to compare against existing scenarios.

If the JSON contains `"error"` or a runner error, report it clearly. Pre-backfill errors (empty L1 tables) are expected — the YAML is still written and valid.

Strategy format: underscore-separated percentages summing to 100.
- GS (2 TPs): `20_80`, `30_70`, `25_75`, `50_50`
- Ceddi (5 TPs): `40_30_15_10_5`, `30_25_20_15_10`

Friction presets: `zero`, `zero_commission`, `vantage_realistic`, `fxify`, `brightfunded`

Window options: `full_history` (default), `last_7d`, `last_30d`, `last_90d` (or short forms: `7d`, `30d`, `90d`, `full`)

Usage examples:
- `/lab-create-scenario:lab-create-scenario --provider gs --strategy 30_70 --friction vantage_realistic`
- `/lab-create-scenario:lab-create-scenario --provider ceddi --strategy 40_30_15_10_5 --friction zero_commission --window 30d`
- `/lab-create-scenario:lab-create-scenario --provider gs --strategy 50_50 --friction fxify --name my_gs_5050_fxify`
- `/lab-create-scenario:lab-create-scenario --provider gs --strategy 30_70 --friction vantage_realistic --no-persist`
