---
description: Check channel credibility — how well do a provider's claimed SL/TP levels match what candles actually did. Use when Joe asks about channel accuracy, L2 vs L3 agreement, or whether GS/Ceddi's levels are trustworthy.
argument-hint: --provider gs|ceddi
allowed-tools: Bash
---

Run the channel credibility query and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-query-channel-credibility/scripts/query.sh $ARGUMENTS`

Read the JSON output above and give Joe a 3-line summary:

1. **Headline**: Provider, total signals, L2 coverage rate (% of signals that have L2 parsed data)
2. **Agreement rates**: SL agreement %, TP1–TP5 agreement % — which levels match candle truth and which diverge
3. **Verdict**: Is this provider's level-setting reliable? Flag any agreement rate below 70% as a concern.

If `l2_coverage_rate` is 0 or null, say "L2 data not yet backfilled — credibility view is empty."

Usage examples:
- `/lab-query-channel-credibility:lab-query-channel-credibility --provider gs`
- `/lab-query-channel-credibility:lab-query-channel-credibility --provider ceddi`
