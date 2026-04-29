---
description: Clone an existing backtest scenario with overrides — tweak risk_pct, friction, split, or entry timeout without rebuilding from scratch. Use when Joe wants to run a variation of a scenario he already has.
argument-hint: --source PATH --override key=value [--override key=value ...] [--name NAME] [--window WINDOW] [--no-persist]
allowed-tools: Bash
---

Run the clone-scenario script and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-clone-scenario/scripts/clone.sh $ARGUMENTS`

Read the JSON output above and give Joe a clear summary:

1. **Cloned from**: Source scenario path, overrides applied
2. **New scenario**: Name, YAML path, provider, window
3. **Results**: N signals input, N trades placed, win rate %, profit factor, max drawdown %
4. **Comparison prompt**: Tell Joe to compare this against the source using lab-fetch-scenarios.

If the JSON contains `"error"` or a runner error, report it clearly. Pre-backfill errors are expected — the YAML is still written.

Override examples (use `--override key=value`, repeat for multiple):
- `--override risk_pct=3.0`
- `--override friction=zero`
- `--override tp_exit.partial_split=[30,70]`
- `--override entry.entry_timeout_min=60`

Source paths can be absolute or relative to project root. Scenario YAMLs live in:
`/Volumes/4TB-990/dev/files/scenarios_v2/auto/`

Usage examples:
- `/lab-clone-scenario:lab-clone-scenario --source /Volumes/4TB-990/dev/files/scenarios_v2/auto/gs_30_70_vantage_realistic_full.yml --override risk_pct=3.0`
- `/lab-clone-scenario:lab-clone-scenario --source scenarios_v2/auto/gs_30_70_vantage_realistic_full.yml --override friction=zero --override tp_exit.partial_split=[20,80]`
- `/lab-clone-scenario:lab-clone-scenario --source scenarios_v2/auto/gs_30_70_vantage_realistic_full.yml --override risk_pct=1.5 --name conservative_test --no-persist`
