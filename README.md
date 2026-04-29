# goldbot-lab plugins (marketplace moved)

⚠ **Active marketplace lives at: https://github.com/joetroyer/goldbot-lab-plugins**

This local `plugins/` directory is the source of truth that gets pushed to the
dedicated marketplace repo. To add the marketplace to Claude Code Desktop:

```
/plugin marketplace add joetroyer/goldbot-lab-plugins
```

Then install whichever plugins you want:

```
/plugin install lab-query-signal-performance@goldbot-lab
/plugin install lab-query-channel-credibility@goldbot-lab
/plugin install lab-query-execution-gaps@goldbot-lab
/plugin install lab-query-drawdown-profile@goldbot-lab
/plugin install lab-fetch-scenarios@goldbot-lab
/plugin install lab-create-scenario@goldbot-lab
/plugin install lab-clone-scenario@goldbot-lab
```

## To update plugins

1. Edit files under `plugins/` here in the goldbot repo
2. Sync to `goldbot-lab-plugins` repo and push:
   ```
   rsync -av --delete plugins/ /tmp/goldbot-lab-plugins/
   cd /tmp/goldbot-lab-plugins && git add . && git commit -m "..." && git push
   ```
3. In Claude Desktop, refresh the marketplace to pull updates.

Backend scripts live in `analysis/skills/lab-*/scripts/` — plugins are thin
slash-command wrappers that shell out to those scripts. .env stays on Mac Mini.
