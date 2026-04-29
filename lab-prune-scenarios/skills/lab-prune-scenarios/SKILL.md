---
description: Soft-delete auto-generated backtest scenario runs older than N days. Keeps YAML files on disk — Joe can re-run. Dry-run by default. Use when the scenario list is getting crowded or Joe says "clean up old experiments".
argument-hint: [--category auto|ported|canonical] [--older-than 30d] [--dry-run | --apply]
allowed-tools: Bash
---

Run the prune-scenarios script and summarize the results for Joe.

Output from the script:

!`/Volumes/4TB-990/dev/files/analysis/skills/lab-prune-scenarios/scripts/prune.sh $ARGUMENTS`

Read the JSON output above and give Joe a concise report:

1. **Mode**: Dry run (no deletions) or live apply.
2. **Criteria**: Category pruned, age threshold used.
3. **Candidates**: How many runs matched.
4. **Deleted**: How many were actually removed (0 for dry run).
5. **Names**: List the scenario names that were (or would be) removed — keep it brief if > 10, show first 10 then "and N more…".

If `candidates` is 0, say "Nothing to prune — no auto scenarios older than the threshold."

Safety reminders (include in every response):
- YAML files in `scenarios_v2/auto/` are NOT deleted — re-run anytime with lab-create-scenario.
- Canonical and ported scenarios are never pruned unless Joe explicitly passes `--category canonical` or `--category ported`.
- Always show dry-run first and ask Joe to confirm before running `--apply`.

Usage examples:
- `/lab-prune-scenarios:lab-prune-scenarios`  (dry run, auto category, 30d default)
- `/lab-prune-scenarios:lab-prune-scenarios --older-than 7d`
- `/lab-prune-scenarios:lab-prune-scenarios --apply`  (actually delete)
- `/lab-prune-scenarios:lab-prune-scenarios --category auto --older-than 14d --apply`
