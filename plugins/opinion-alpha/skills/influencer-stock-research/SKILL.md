---
name: influencer-stock-research
description: Research what finance influencers say about a stock, a sector or the market, and how reliable they have been, using the Opinion Alpha MCP tools. Use when the user asks what finance influencers, creators, "finfluencers" or analysts on social media think about a ticker, an upcoming earnings report or a market move; whether a particular influencer is worth following; or who has called a stock best.
---

# Influencer stock research with Opinion Alpha

Opinion Alpha tracks finance influencers and extracts every stock call they make (ticker, bullish or bearish, horizon, strength and the exact quote) with a link to the moment in the source. It also simulates how following each influencer would have performed. These steps need the `opinion-alpha` MCP server (https://api.opinionalpha.app/mcp); a free Opinion Alpha account is enough, and Pro adds the full history.

## Ground rules

- **Cite every claim.** Each opinion comes with a source link; put it next to the claim it supports. Never attribute a view to someone without one.
- **Quote sparingly.** A short phrase in quotation marks, otherwise paraphrase.
- **Simulations, not advice.** Performance figures are backtests of public statements, not anyone's real returns. Do not tell the user to buy or sell; end with a one-line reminder that this summarises public opinions and is not investment advice.
- **Say what is missing.** If a stock or person is not tracked, say so plainly (and offer `suggest_influencer` for a person, after confirming the link with the user).
- **Mind the window.** Free accounts see recent history; if results stop at a date (`historyFrom`), say that older calls may exist.

## What influencers say about a stock

1. `search` the company name if the ticker is unclear (non-US tickers carry their exchange suffix, e.g. `000660.KS`, `600938.SS`).
2. `stock_opinions` for the ticker: the calls, newest first.
3. Summarise in this order:
   - the split: how many bullish vs bearish calls, and from how many influencers;
   - the main arguments on each side, grouped (valuation, growth, technicals, macro), each with its influencer and source;
   - where they disagree on timing (short-term caution vs long-term conviction is common);
   - what changed recently (someone who flipped, a burst of calls after news).
4. For context, `stock_prices` since the earliest call you cite, and say what the price did after the calls.
5. If the user wants to know whom to trust on this stock, `stock_overview` gives each influencer's simulated win rate on it; mention the sample size, since a 100% win rate on two calls means little.

The `stock_brief` prompt runs a compact version of this.

## Before an earnings report

1. `stock_opinions` for the ticker, focusing on calls from the last 30 days.
2. Separate what was said **before** the last report from what was said after it, if the user is looking back at a report that just happened.
3. Point out expectations that the report will test: numbers or thresholds influencers named (price levels, growth rates, margins, guidance).
4. The full earnings calendar with each report's influencer calls is on https://opinionalpha.app/earnings; link to it rather than guessing report dates.

## Is this influencer worth following?

1. `search` the name, then `influencer` for the profile and latest calls.
2. `influencer_performance` for the simulated record: return, excess return vs SPY, Sharpe ratio, max drawdown and win rate. Compare periods (e.g. 1Y vs 2Y) before drawing conclusions, and note the mode used (long-only, conviction-weighted or long-short).
3. Look at concentration: a record driven by one or two stocks is fragile.
4. `rank_influencers` puts the record in context against everyone tracked.

The `influencer_checkup` prompt runs a compact version of this.

## Beyond stock calls

- `search_transcripts` searches the full text of what influencers said, for sectors, indexes, macro and rates, or a stock mentioned in passing. Matches are literal, so pass every form the words may take in one call: tickers and short names, English and Chinese (Simplified and Traditional) wording.
- `latest_opinions` and `day_summary` give the overall flow: what is being discussed today or this week.
- `followed_stocks` shows the stocks the user follows on Opinion Alpha with the last 7 days of calls. `follow_stock` follows or unfollows one; confirm with the user first.

## Answer shape

Lead with a two- or three-sentence answer to the question. Then the grouped detail with sources, then prices or records if relevant, then the not-investment-advice line. Keep influencer names as they appear (many write in Chinese); add the stock's name the first time you use a ticker.
