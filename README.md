# Gold Mine Lab Plugins — Claude Code Desktop Marketplace

7 plugins that wire Joe's lab analysis scripts directly into Claude Code Desktop.
Voice or text → script → JSON → AI summary. No MCP. No extra services.

---

## Install

### Step 1 — Add the marketplace

```
/plugin marketplace add /Volumes/4TB-990/dev/files/plugins
```

This registers the `goldbot-lab` marketplace. You only do this once.

### Step 2 — Install all 7 plugins

Run each of these (or say "install all goldbot-lab plugins"):

```
/plugin install lab-query-signal-performance@goldbot-lab
/plugin install lab-query-channel-credibility@goldbot-lab
/plugin install lab-query-execution-gaps@goldbot-lab
/plugin install lab-query-drawdown-profile@goldbot-lab
/plugin install lab-fetch-scenarios@goldbot-lab
/plugin install lab-create-scenario@goldbot-lab
/plugin install lab-clone-scenario@goldbot-lab
```

### Step 3 — Reload if needed

If skills don't appear immediately:

```
/reload-plugins
```

---

## Commands

Each plugin installs one skill. Skills are namespaced as `/<plugin-name>:<plugin-name>`.

### Signal performance
```
/lab-query-signal-performance:lab-query-signal-performance --provider gs --window 30d
/lab-query-signal-performance:lab-query-signal-performance --provider ceddi --window 90d
/lab-query-signal-performance:lab-query-signal-performance --provider gs --window full
```
Win rate, TP1–5 hit rates, multi-timeframe 24h/7d/30d/90d breakdown.

### Channel credibility
```
/lab-query-channel-credibility:lab-query-channel-credibility --provider gs
/lab-query-channel-credibility:lab-query-channel-credibility --provider ceddi
```
L2 claimed vs L3 candle-truth agreement — are the channel's levels trustworthy?

### Execution gaps
```
/lab-query-execution-gaps:lab-query-execution-gaps --provider gs --window 30d
/lab-query-execution-gaps:lab-query-execution-gaps --provider ceddi --window full
```
Lab perfect-sim vs bot execution — execution rate, avg P&L, avg lab R-multiple.

### Drawdown profile
```
/lab-query-drawdown-profile:lab-query-drawdown-profile --provider gs
/lab-query-drawdown-profile:lab-query-drawdown-profile --provider ceddi --window 30d
/lab-query-drawdown-profile:lab-query-drawdown-profile --provider gs --scenario-name gs_30_70_vantage_realistic_full
```
Max drawdown %, SL streak distribution, Markov P(SL after SL).

### Fetch scenarios (leaderboard)
```
/lab-fetch-scenarios:lab-fetch-scenarios
/lab-fetch-scenarios:lab-fetch-scenarios --provider gs --sort-by profit_factor
/lab-fetch-scenarios:lab-fetch-scenarios --sort-by win_rate
/lab-fetch-scenarios:lab-fetch-scenarios --sort-by max_drawdown_pct
```
All backtest results sorted by the metric you care about.

### Create scenario
```
/lab-create-scenario:lab-create-scenario --provider gs --strategy 30_70 --friction vantage_realistic
/lab-create-scenario:lab-create-scenario --provider ceddi --strategy 40_30_15_10_5 --friction zero_commission --window 30d
/lab-create-scenario:lab-create-scenario --provider gs --strategy 50_50 --friction fxify --name my_test
```

Strategy format: underscore-separated percentages summing to 100.
- GS (2 TPs): `20_80`, `30_70`, `25_75`, `50_50`
- Ceddi (5 TPs): `40_30_15_10_5`, `30_25_20_15_10`

Friction presets: `zero`, `zero_commission`, `vantage_realistic`, `fxify`, `brightfunded`

### Clone scenario
```
/lab-clone-scenario:lab-clone-scenario --source /Volumes/4TB-990/dev/files/scenarios_v2/auto/gs_30_70_vantage_realistic_full.yml --override risk_pct=3.0
/lab-clone-scenario:lab-clone-scenario --source scenarios_v2/auto/gs_30_70_vantage_realistic_full.yml --override friction=zero --override tp_exit.partial_split=[20,80]
```

Override syntax: `--override key=value` (dot-notation for nested keys, repeat for multiple overrides).

---

## How it works

Each skill uses the `!` bash-injection pattern in its SKILL.md. When you invoke a skill:

1. Claude Code runs the shell command embedded in the skill content (the `!` backtick line)
2. The script's JSON stdout replaces the placeholder
3. Claude receives the fully-rendered prompt with real data and summarizes it

The scripts are pinned to the Mac Mini's venv and project root — they read `.env` for DB credentials.
No files move on install; the skills reference the scripts at their absolute paths.

---

## Structure

```
plugins/
├── .claude-plugin/marketplace.json          ← goldbot-lab marketplace
├── lab-query-signal-performance/
│   ├── .claude-plugin/plugin.json
│   └── skills/lab-query-signal-performance/SKILL.md
├── lab-query-channel-credibility/
│   ├── .claude-plugin/plugin.json
│   └── skills/lab-query-channel-credibility/SKILL.md
├── lab-query-execution-gaps/
│   ├── .claude-plugin/plugin.json
│   └── skills/lab-query-execution-gaps/SKILL.md
├── lab-query-drawdown-profile/
│   ├── .claude-plugin/plugin.json
│   └── skills/lab-query-drawdown-profile/SKILL.md
├── lab-fetch-scenarios/
│   ├── .claude-plugin/plugin.json
│   └── skills/lab-fetch-scenarios/SKILL.md
├── lab-create-scenario/
│   ├── .claude-plugin/plugin.json
│   └── skills/lab-create-scenario/SKILL.md
└── lab-clone-scenario/
    ├── .claude-plugin/plugin.json
    └── skills/lab-clone-scenario/SKILL.md
```

---

## Verification (smoke test)

After install, run this to confirm one script is callable:

```bash
/Volumes/4TB-990/dev/files/analysis/skills/lab-query-signal-performance/scripts/query.sh --provider gs --window 7d
```

If it returns JSON (even `{"n": 0, ...}` for pre-backfill), the backend is healthy.
Then invoke the skill in Claude Code and confirm it summarizes the JSON.

---

## Updating

After editing a skill's SKILL.md, run `/reload-plugins` in Claude Code.
After bumping `version` in a plugin.json, run `/plugin update <name>@goldbot-lab`.
