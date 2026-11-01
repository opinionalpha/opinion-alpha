# Opinion Alpha for AI assistants

**Every stock call from finance influencers, extracted, linked to its source and scored.**

[Opinion Alpha](https://opinionalpha.app) tracks finance influencers and pulls out each stock call they make: the ticker, bullish or bearish, the time horizon and the exact quote, with a link to the moment it was said. It then simulates how following each influencer would have performed.

This repository connects that data to your AI assistant:

- **An MCP server** (hosted, nothing to install) for Claude, ChatGPT, Cursor, Codex and any MCP client.
- **A research skill** that teaches the assistant to answer well: cite every claim, separate the bull and bear cases, check track records before trusting anyone.
- **A Claude Code plugin** that installs both at once.

Free with an [Opinion Alpha account](https://opinionalpha.app/auth/sign-up). [Pro](https://opinionalpha.app/pricing) adds the full history and longer simulations, in the assistant as on the site.

## Ask things like

- "What are influencers saying about NVDA this week? Who is bearish, and why?"
- "AMD reports on Tuesday. What did influencers expect going in?"
- "Is this influencer worth following? How has their record held up over two years?"
- "Who has called MU best?"
- "What did influencers say about the Philadelphia Semiconductor Index?"

Every answer links to the original video or post.

## Connect

The server address is `https://api.opinionalpha.app/mcp` (Streamable HTTP). You sign in with your Opinion Alpha account (OAuth); there is no API key.

**Claude (claude.ai, desktop, mobile)**: add Opinion Alpha from the [Claude connector directory](https://claude.ai/directory/opinion-alpha), or Settings › Connectors › Add custom connector with the address above.

**Claude Code**: install the plugin (MCP server + skill):

```
/plugin marketplace add opinionalpha/opinion-alpha
/plugin install opinion-alpha@opinionalpha
```

or only the server: `claude mcp add --transport http opinion-alpha https://api.opinionalpha.app/mcp`

**ChatGPT**: add a custom connector (app) with the address above.

**Cursor**: install from the [Cursor directory](https://cursor.directory/plugins/opinion-alpha), or add to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "opinion-alpha": { "url": "https://api.opinionalpha.app/mcp" } } }
```

**Other clients**: any client that supports remote MCP servers with OAuth; point it at the address above.

The full guide, with screenshots: [Opinion Alpha in your AI assistant](https://opinionalpha.app/blog/opinion-alpha-in-your-ai-assistant).

## The skill

[`influencer-stock-research`](plugins/opinion-alpha/skills/influencer-stock-research/SKILL.md) covers what influencers say about a stock, what they expected before an earnings report, whether an influencer is worth following, and searching everything they said. Claude Code loads it with the plugin; for other skill-aware assistants, copy the folder into your skills directory.

## Tools

| Tool | What it does |
|---|---|
| `search` | Find tracked influencers and stocks by name or ticker |
| `stock_opinions` | Influencer calls on one stock, newest first, with sources |
| `stock_overview` | Each influencer's simulated win rate on one stock |
| `latest_opinions` | The newest calls across all influencers |
| `day_summary` | One day's calls: bullish vs bearish, most-discussed stocks |
| `influencer` | One influencer's profile and latest calls |
| `influencer_performance` | Simulated record: return, excess vs SPY, Sharpe, drawdown, win rate |
| `rank_influencers` | Influencers ranked by simulated return |
| `stock_prices` | Daily prices, to set calls against what the stock did |
| `search_transcripts` | Full-text search of what influencers said, beyond stock calls |
| `followed_stocks` | The stocks you follow on Opinion Alpha, with the week's calls |
| `follow_stock` | Follow or unfollow a stock (asks you first) |
| `suggest_influencer` | Suggest an influencer for Opinion Alpha to track |

Two prompts, `stock_brief` and `influencer_checkup`, run the common questions in one step, and the `methodology` resource explains how calls are extracted and simulated.

## More from Opinion Alpha

- [Weekly review](https://opinionalpha.app/weekly): what influencers argued about this week, and what they expect from next week's earnings
- [Earnings calendar](https://opinionalpha.app/earnings) with the influencer calls before each report
- [Leaderboard](https://opinionalpha.app/leaderboard) of influencers by simulated performance

## Notes

Performance figures are simulations based on public statements, not anyone's real returns, and nothing here is investment advice. This repository holds the plugin, skill and listing files; the service itself is hosted at opinionalpha.app. Questions: support@opinionalpha.app.
