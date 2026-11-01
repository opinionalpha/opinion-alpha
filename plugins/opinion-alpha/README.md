# Opinion Alpha plugin

Connects Claude Code to [Opinion Alpha](https://opinionalpha.app): finance influencers' stock calls, extracted with the exact quote, linked to their source and scored by simulating how following each influencer would have performed.

It installs two things:

- **The Opinion Alpha MCP server** (`https://api.opinionalpha.app/mcp`, hosted). On first use Claude Code opens a browser to sign in with your Opinion Alpha account (OAuth, no API key). A free account is enough; Pro adds the full history and longer simulations.
- **The `influencer-stock-research` skill**, which tells Claude how to answer questions such as "what are influencers saying about NVDA?", "what did they expect before AMD's earnings?" or "is this influencer worth following?": cite every claim with its source, separate the bull and bear cases, check track records and sample sizes, and never give investment advice.

Install:

```
/plugin marketplace add opinionalpha/opinion-alpha
/plugin install opinion-alpha@opinionalpha
```

Performance figures are simulations of public statements, not real returns and not investment advice. Privacy: https://opinionalpha.app/privacy. Support: support@opinionalpha.app.
