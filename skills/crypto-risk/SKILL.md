---
name: market-risk
description: Get real-time risk levels for crypto (BTC, ETH, ADA, SOL, BNB, LINK) and stock indices (DJIA, S&P 500, NASDAQ) from CycleBottom. Use when the user asks about crypto risk, stock market risk, index risk, whether it's a good time to buy, or cycle position. Triggers on "crypto risk", "BTC risk", "ETH risk", "SOL risk", "market risk", "S&P 500 risk", "NASDAQ risk", "DJIA risk", "risk level", "cycle position", "is it safe to buy", "market temperature".
allowed-tools: Bash, WebFetch
---

# Market Risk Skill

Fetch real-time risk metrics for crypto and stock indices from the CycleBottom API.

## How to use

Fetch both endpoints and present the results:

```bash
curl -s https://cyclebottom.com/api/risk/crypto
curl -s https://cyclebottom.com/api/risk/indices
```

### Crypto response

The `/api/risk/crypto` response contains `btc`, `eth`, `ada`, `sol`, `bnb`, and `link` objects.

### Indices response

The `/api/risk/indices` response contains `djia`, `sp500`, and `nasdaq` objects.

Each object has:
- `price` — current price in USD
- `risk` — normalized risk score from 0 (lowest) to 1 (highest)
- `label` — human-readable risk assessment
- `ma365` — 365-day moving average price
- `priceToMA` — ratio of current price to MA (>1 = above average)
- `date` — date of the data point

## Risk scale

| Range | Meaning |
|-------|---------|
| 0.00 - 0.15 | Extreme low risk — Strong accumulation zone |
| 0.15 - 0.30 | Low risk — Good accumulation opportunity |
| 0.30 - 0.45 | Moderate-low risk — Reasonable entry |
| 0.45 - 0.55 | Neutral — Fair value range |
| 0.55 - 0.70 | Moderate-high risk — Consider caution |
| 0.70 - 0.85 | High risk — Distribution zone |
| 0.85 - 1.00 | Extreme high risk — Historically overvalued |

## Presentation

After fetching the data, present it concisely. Group by asset class:

**Crypto:**
**BTC** — $XX,XXX | Risk: X.XXX (label) | MA365: $XX,XXX | Price/MA: X.XXx
**ETH** — $X,XXX | Risk: X.XXX (label) | MA365: $X,XXX | Price/MA: X.XXx
**SOL** — $XXX | Risk: X.XXX (label) | MA365: $XXX | Price/MA: X.XXx
**ADA** — $X.XX | Risk: X.XXX (label) | MA365: $X.XX | Price/MA: X.XXx
**BNB** — $XXX | Risk: X.XXX (label) | MA365: $XXX | Price/MA: X.XXx
**LINK** — $XX.XX | Risk: X.XXX (label) | MA365: $XX.XX | Price/MA: X.XXx

**Indices:**
**DJIA** — XX,XXX | Risk: X.XXX (label) | MA365: XX,XXX | Price/MA: X.XXx
**S&P 500** — X,XXX | Risk: X.XXX (label) | MA365: X,XXX | Price/MA: X.XXx
**NASDAQ** — XX,XXX | Risk: X.XXX (label) | MA365: XX,XXX | Price/MA: X.XXx

If the user asks only about crypto or only about indices, fetch and show only the relevant endpoint.
If sending via Telegram, use plain text (no markdown tables).
