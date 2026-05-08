---
description: Broker-truth P&L for one account, broken out by bot vs scalps. Reads deals.bin (truth source).
argument-hint: <last4_or_full_login> [period] [filter]
allowed-tools: Bash
---

Run pnl-broker and summarize for Joe.

!`/Volumes/4TB-990/dev/files/analysis/skills/pnl-broker/scripts/query.sh $ARGUMENTS`

Output as Telegram-friendly one-liner:
`Account <last4> (<name>) <period_label>: bot <±$X> · scalps <±$X> (<label>) · book <±$X> (N deals)`

If a bucket is $0 with 0 deals, omit it. If `book` differs from sum-of-buckets, flag as parser bug.

Examples:
- `/pnl-broker:pnl-broker 9306 today`
- `/pnl-broker:pnl-broker 24759593 today bot-ceddi`
- `/pnl-broker:pnl-broker 9416 last7 bot`
