---
description: P&L view from dispatch_records — what the bot's pipeline THINKS happened. Diff vs pnl-broker catches recording bugs.
argument-hint: <last4_or_full_login> [period] [filter]
allowed-tools: Bash
---

Run pnl-dispatch and summarize for Joe.

!`/Volumes/4TB-990/dev/files/analysis/skills/pnl-dispatch/scripts/query.sh $ARGUMENTS`

Output as Telegram-friendly one-liner:
`Account <last4> (<name>) <period_label> [DISPATCH VIEW]: bot <±$X> · book <±$X> (N rows)`

If null final_pnl rows present, append `(W of N null — backfill pending)`.

Examples:
- `/pnl-dispatch:pnl-dispatch 9306 today`
- `/pnl-dispatch:pnl-dispatch 24759593 today bot-ceddi` (then compare vs pnl-broker — diff is the recording bug)
