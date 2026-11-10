# Day Trading Toolkit

Eight Claude skills that take a day trade from idea to order: find the setup, check the news, time the entry, plan the exit, simulate the outcomes, size the position, check the risk and send the order.

Plain Python (standard library only, Python 3.8+), free public data (Yahoo Finance, Nasdaq Trader, SEC EDGAR), no API key. Paper trading by default, and no order is ever placed without an explicit yes.

## The skills

| Command | What it does |
| --- | --- |
| `/trader-scanner` | Scans around 5,900 US stocks for opening-range breakouts, flags and oversold bounces |
| `/trader-news` | Pulls recent headlines and SEC 8-K filings for each ticker on the watchlist |
| `/trader-entry` | Watches a setup bar by bar and flags the moment it triggers |
| `/trader-exit` | Sets the stop, the target and the flat-by time before entry |
| `/trader-timemachine` | Replays the rest of the session 10,000 times from the stock's own recent bars, plus every past day the setup fired |
| `/trader-budget` | Sizes the position to the account and the maximum loss per trade |
| `/trader-risk` | Checks every order against daily loss, trade count, reward to risk and position limits: PASS or BLOCK |
| `/trader-broker` | Sends approved orders to Alpaca (paper by default) or Interactive Brokers, one explicit yes per order |

## Workflow

```
scanner -> news -> entry -> exit -> timemachine -> budget -> risk -> broker
```

Each skill writes its output to a `trader/` folder in the project, and the next one reads it.

## Install

In Claude Code:

```
/plugin marketplace add antonriahi/day-trading-toolkit
/plugin install day-trading-toolkit@day-trading-toolkit
```

Or copy the skill folders into `~/.claude/skills/`.

The news tool asks for an SEC user agent: set `SEC_USER_AGENT="Your Name you@example.com"`.

## Tests

```bash
python3 -m unittest discover -s tests -v
```

245 tests, run offline on fixtures cut from real market data.

## Disclaimer

Not financial advice. This is software that reads public data and does arithmetic: it cannot predict the market, and most day traders lose money. Start in paper trading. Stops can fill worse than planned in fast markets. Free data can lag or change. Simulations are a reality check, not a forecast.

## Licence

MIT. See [LICENSE](LICENSE).
