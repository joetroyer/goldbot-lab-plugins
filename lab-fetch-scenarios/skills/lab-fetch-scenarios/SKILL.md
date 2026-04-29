---
description: List all backtest scenarios with their headline stats — win rate, profit factor, max drawdown. Use when Joe asks which scenario performed best, wants to compare splits, or needs a leaderboard of backtest results.
argument-hint: [--provider gs|ceddi] [--sort-by win_rate|profit_factor|max_drawdown_pct|trades_total]
disable-model-invocation: true
allowed-tools: Bash
---

Run the fetch-scenarios query and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-fetch-scenarios/scripts/query.sh $ARGUMENTS`

Read the JSON output above and give Joe a concise summary:

1. **Count**: Total scenarios found (and provider filter if applied)
2. **Top 3**: The three best scenarios by the sort field — scenario name, win rate, profit factor, max drawdown %, trade count
3. **Bottom**: Any scenario with profit factor < 1.0 or max drawdown > 20% — flag these as underperformers
4. **Pattern**: Is there a clear winner split (e.g. 30_70 consistently beats 20_80)? State it if visible.

Format the top-3 as a compact table. If `total` is 0, say "No scenarios found — run lab-create-scenario to build your first one."

Usage examples:
- `/lab-fetch-scenarios:lab-fetch-scenarios`
- `/lab-fetch-scenarios:lab-fetch-scenarios --provider gs --sort-by profit_factor`
- `/lab-fetch-scenarios:lab-fetch-scenarios --sort-by win_rate`
- `/lab-fetch-scenarios:lab-fetch-scenarios --provider ceddi --sort-by max_drawdown_pct`
