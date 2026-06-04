# cairn-marketplace

Claude Code plugin marketplace for [Cairn](https://github.com/cairnscore/cairn-score-skill) — a trust + reputation service for AI agents.

## What this is

A catalog repo: one `.claude-plugin/marketplace.json` file that points Claude Code at the `cairn` plugin in [`cairnscore/cairn-score-skill`](https://github.com/cairnscore/cairn-score-skill). Nothing else lives here.

The plugin itself — skill, MCP server, hooks, scripts — lives in the main repo. This marketplace just makes it installable via the standard `/plugin marketplace add` flow.

## Install

In a Claude Code session:

```
/plugin marketplace add cairnscore/cairn-marketplace
/plugin install cairn@cairn-marketplace
```

Then **start a fresh Claude Code session** — hooks load at session start.

A one-line status banner prints to stderr at every session start (resolves rater backend, checks `uv` on PATH, reports queue depth, warns if a legacy `install.sh` install is still registered alongside the plugin).

## What you get

- 10 MCP tools (`score`, `profile`, `rate`, `retrieve`, `rank`, `discover`, `capabilities`, `score_batch`, `score_history`, `get_rubric`)
- Background rating hooks on `WebFetch | WebSearch | Bash | mcp__.*`
- Stop-hook queue flush to `api.cairnscore.ai`
- Per-host denylist + global opt-out env vars

See the main repo's [README](https://github.com/cairnscore/cairn-score-skill#readme) for the cost story, data-flow / privacy details, and configuration.

## Updating

```
/plugin marketplace update cairn-marketplace
```

The pinned SHA is bumped on each cairn-score-skill release (via `scripts/release.sh`). Claude Code auto-updates community marketplaces by default — toggle in `/plugin` → Marketplaces tab.

## Uninstall

```
/plugin uninstall cairn@cairn-marketplace
/plugin marketplace remove cairn-marketplace   # optional
rm -rf ~/.cairn                                # if you want to wipe runtime state
```

## License

MIT — see [LICENSE](LICENSE).
