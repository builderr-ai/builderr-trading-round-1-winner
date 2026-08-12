# Builderr Trading Round 1 winner

The public Builderr archive for the winning Trading Agent Round 1 submission.

This repository is for **reading, running, and reproducing the local preview**. It is not a
promise of future returns and it is not investment advice.

## Result

| Item | Recorded result |
| --- | --- |
| Challenge | Builderr Trading Agent Round 1 |
| Result | Round 1 winning agent |
| Rank | 1 |
| Window | 16 live market days, closed July 2, 2026 |
| Return | +5.91% |
| Final paper account | $105,911 |
| Trades | 37 |

The result is a dated challenge result, not a live trading track record. The original market
data, fills, and private evaluator are not included here, so the local preview does not reproduce
the official +5.91% result.

## Run it

Requirements: Python 3.10+ and no third-party packages.

```bash
python preview.py round_1_winner_agent.py
```

The preview runs the agent on three public sample market windows and checks that it emits valid
orders, stays within the published safety limits, and does not crash. It is a local smoke test,
not the official leaderboard evaluation.

The challenge interface is one function:

```python
decide(market_state, portfolio_state, cash) -> list[dict]
```

The returned orders use `ticker`, `side` (`buy` or `sell`), and positive `quantity` fields.

## What the agent does

1. It ranks liquid stocks and ETFs by medium- and short-term momentum plus distance above a
   50-day moving average.
2. It holds up to five positive-momentum leaders, with a per-name target below the 30% limit.
3. It switches between `CASH`, `NEUTRAL`, and `FULL` depending on SPY/QQQ trend, breadth, and
   volatility.
4. It uses QLD/SSO only in the strongest state and keeps beta-adjusted exposure below the
   challenge cap.
5. It reduces exposure through drawdown tapering, trailing stops, cooldowns, and a market brake.

The full explanation is in [`docs/strategy.md`](docs/strategy.md). The dated evidence and claim
limits are in [`docs/result.md`](docs/result.md).

## Files

- [`round_1_winner_agent.py`](round_1_winner_agent.py) — submitted agent source, kept unchanged
- [`preview.py`](preview.py) — public local preview harness
- [`sample_regimes.json.gz`](sample_regimes.json.gz) — public preview windows
- [`docs/strategy.md`](docs/strategy.md) — plain-English strategy walkthrough
- [`docs/result.md`](docs/result.md) — result, evaluation boundary, and limitations
- [`NOTICE.md`](NOTICE.md) — attribution and reuse status

## Why this is public

Builderr publishes winning implementations so builders can inspect what worked, test it locally,
and try to beat the benchmark. The canonical challenge result page is:

https://builderr.ai/trading-v0/winners/arnav

The current challenge is a separate forward test. Start here:

https://builderr.ai/trading-v0

If this project is useful, use it first. A GitHub star is optional and is secondary to running the
code, opening a useful issue, or building a better agent.
