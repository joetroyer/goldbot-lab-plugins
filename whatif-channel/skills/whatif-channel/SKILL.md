---
description: Counterfactual — if channel X had been live with $Y starting balance and Z% risk across the lab's full L1 history, what would the equity curve look like?
argument-hint: <channel_marker> <starting_balance> <risk_pct>
allowed-tools: Bash
---

Run whatif-channel and summarize for Joe.

!`/Volumes/4TB-990/dev/files/analysis/skills/whatif-channel/scripts/query.sh $ARGUMENTS`

Output the engine's verdict as Telegram-friendly:
```
What-if: <CHANNEL> (<provider>) — full lab history at $<balance> @ <risk>% risk
  Source scenario:  <name> (<canonical|synthetic>, N trades)
  Trades:           N (W / L · WR%)
  Profit factor:    PF
  Final balance:    $X  (+$Y / -$Y, +Z% / -Z%)
  Max drawdown:     X%
```

No period argument — scenarios run on full history. Examples:
- `/whatif-channel:whatif-channel CT 50000 1.5`
- `/whatif-channel:whatif-channel GS 25000 2.0 --min-trades 50`
