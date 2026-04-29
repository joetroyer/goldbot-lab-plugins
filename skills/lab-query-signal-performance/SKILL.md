---
description: Query GS or Ceddi signal performance — TP hit rates, win rate, multi-timeframe breakdown. Use when Joe asks about signal performance, win rate, how many TPs are hitting, or provider comparison.
argument-hint: --provider gs|ceddi [--window 7d|30d|90d|full]
disable-model-invocation: true
allowed-tools: Bash
---

Run the signal performance query and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-query-signal-performance/scripts/query.sh $ARGUMENTS`

Read the JSON output above and give Joe a 3-line summary:

1. **Headline**: Provider, window, N signals, win rate as a percentage (e.g. "GS 30d: 73% win rate, N=314")
2. **TP breakdown**: Which TPs are hitting and which are not (tp1 through tp5 hit rates as percentages)
3. **Multi-timeframe**: 24h / 7d / 30d / 90d win rate trend — flag any significant drops or spikes
4. **Flag**: SL rate and anything anomalous (unresolved %, large divergence between timeframes)

If the JSON contains `"error"` or `"n": 0`, say so plainly and explain it means the analysis tables are not yet backfilled.

Usage examples:
- `/lab-query-signal-performance:lab-query-signal-performance --provider gs --window 30d`
- `/lab-query-signal-performance:lab-query-signal-performance --provider ceddi --window 90d`
- `/lab-query-signal-performance:lab-query-signal-performance --provider gs --window full`
