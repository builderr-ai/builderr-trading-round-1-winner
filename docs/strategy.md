# Strategy notes

## The short version

The winning agent looks for market leaders, but only takes its most aggressive position when the
broad market is healthy. When the trend breaks, it reduces risk instead of continuing to chase winners.

## States

- **CASH**: market-wide trend or volatility signals are poor; target risk is removed.
- **NEUTRAL**: the market is tradable, but the evidence is not strong enough for the aggressive
  sleeve.
- **FULL**: SPY and QQQ clear the trend filters, breadth is healthy, and QQQ volatility is within
  the limit. The measured QLD/SSO sleeve is allowed only here.

## Leader selection

The agent scores a fixed pool of liquid stocks, broad ETFs, and sector ETFs using:

- 42-day return
- 21-day return
- distance above the 50-day moving average

It keeps up to five positive-score names and sizes them by rank, subject to the position cap.

## Risk controls

- SPY/QQQ trend breaks trigger a move toward cash.
- A sharp QQQ decline or high short-term volatility triggers a brake.
- After a cash exit, hysteresis and cooldowns prevent immediate whipsaw re-entry.
- Drawdown tapering reduces target exposure around 6% and 10% drawdown levels.
- An 8% trailing stop blocks a damaged position and imposes a short cooldown.
- The agent sells stale or oversized positions before buying new targets.
- The strategy is long-only, deterministic, standard-library Python, and makes no network or LLM
  calls.

## What to study

The interesting design choice is not simply “buy momentum.” It is the boundary around aggression:

> When should the agent press leaders, and what forces it to stop?

That is also the main opening for a competing agent: improve regime detection, sizing, recovery
after drawdowns, or behavior in choppy markets without violating the challenge limits.
