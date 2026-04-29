---
description: Get drawdown profile from lab backtest — max drawdown %, SL streak distribution, and Markov P(SL|SL). Use when Joe asks about worst-case drawdown, losing streaks, consecutive stops, or whether SL clustering is random.
argument-hint: --provider gs|ceddi [--window 7d|30d|90d|full] [--scenario-name NAME]
disable-model-invocation: true
allowed-tools: Bash
---

Run the drawdown profile query and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-query-drawdown-profile/scripts/query.sh $ARGUMENTS`

Read the JSON output above and give Joe a 3-line summary:

1. **Drawdown**: Max drawdown % across all scenarios, avg max drawdown, max drawdown duration. Flag if max DD > 15%.
2. **Streaks**: Worst losing streak (max_loss_streak), distribution of 1/2/3+ consecutive SLs. How bad can it get?
3. **Markov**: P(SL after SL) — is this persistent clustering (> 0.35 = danger zone) or relatively independent? Quote the note from the JSON.

If `n_scenarios` is 0, say "No backtest scenarios found — run lab-create-scenario first."

Usage examples:
- `/lab-query-drawdown-profile:lab-query-drawdown-profile --provider gs`
- `/lab-query-drawdown-profile:lab-query-drawdown-profile --provider ceddi --window 30d`
- `/lab-query-drawdown-profile:lab-query-drawdown-profile --provider gs --scenario-name gs_30_70_vantage_realistic_full`
