---
description: Compare lab perfect-sim results vs bot execution — execution rate, average P&L, average R-multiple. Use when Joe asks about execution gaps, how many signals the bot actually traded, or lab vs live comparison.
argument-hint: --provider gs|ceddi [--window 7d|30d|90d|full]
disable-model-invocation: true
allowed-tools: Bash
---

Run the execution gap query and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-query-execution-gaps/scripts/query.sh $ARGUMENTS`

Read the JSON output above and give Joe a 3-line summary:

1. **Headline**: Provider, window, N signals total, execution rate (% the bot actually traded)
2. **Performance**: Average bot P&L per signal (USD) vs average lab R-multiple — is the bot capturing lab's expected return?
3. **Multi-timeframe trend**: 24h / 7d / 30d / 90d execution rates and P&L — any deterioration or improvement?
4. **Flag**: Signals with no bot execution (missed signals), and any large gap between lab R and bot P&L

If `n_signals` is 0, say "No signal data for this window — analysis tables not yet backfilled."

Usage examples:
- `/lab-query-execution-gaps:lab-query-execution-gaps --provider gs --window 30d`
- `/lab-query-execution-gaps:lab-query-execution-gaps --provider ceddi --window full`
