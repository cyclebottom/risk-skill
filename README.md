# market-risk

A Claude Code plugin that fetches real-time risk levels for crypto and stock indices from [CycleBottom](https://cyclebottom.com).

## What it does

Returns a normalized 0-1 risk metric based on logarithmic deviation from the 365-day moving average, adjusted for diminishing returns.

- Risk near 0 = historically cheap (accumulation zone)
- Risk near 1 = historically overvalued (distribution zone)

### Supported assets

| Asset Class | Assets | Data since |
|-------------|--------|------------|
| Crypto | BTC, ETH, ADA, SOL, BNB, LINK | 2010-2020 |
| Indices | Dow Jones, S&P 500, NASDAQ | 1927-1985 |

## Install

```
/plugin install cyclebottom/risk-skill
```

## Usage

```
/crypto-risk:market-risk
```

Or just ask naturally: "What's the BTC risk level?", "crypto risk", "is the S&P 500 overvalued?", "market temperature" — the skill auto-triggers.

## Response example

**Crypto:**
```
BTC  — $67,326 | Risk: 0.176 (Low risk)           | MA365: $58,241 | Price/MA: 1.156x
ETH  — $2,056  | Risk: 0.313 (Moderate-low risk)   | MA365: $1,842  | Price/MA: 1.116x
SOL  — $135    | Risk: 0.421 (Moderate-low risk)   | MA365: $112    | Price/MA: 1.205x
ADA  — $0.72   | Risk: 0.385 (Moderate-low risk)   | MA365: $0.58   | Price/MA: 1.241x
BNB  — $612    | Risk: 0.502 (Neutral)             | MA365: $548    | Price/MA: 1.117x
LINK — $15.20  | Risk: 0.344 (Moderate-low risk)   | MA365: $12.80  | Price/MA: 1.188x
```

**Indices:**
```
DJIA    — 42,150 | Risk: 0.612 (Moderate-high risk) | MA365: 39,820 | Price/MA: 1.059x
S&P 500 — 5,680  | Risk: 0.598 (Moderate-high risk) | MA365: 5,320  | Price/MA: 1.068x
NASDAQ  — 17,850 | Risk: 0.571 (Moderate-high risk) | MA365: 16,540 | Price/MA: 1.079x
```

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

## API

| Endpoint | Assets |
|----------|--------|
| `GET https://cyclebottom.com/api/risk/crypto` | btc, eth, ada, sol, bnb, link |
| `GET https://cyclebottom.com/api/risk/indices` | djia, sp500, nasdaq |

Each object returns `price`, `risk`, `label`, `ma365`, `priceToMA`, and `date`.

## License

MIT
