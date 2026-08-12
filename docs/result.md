# Result and evidence

## Official result

The Round 1 result was finalized at the July 2, 2026 US market close:

- Rank: 1
- Return: +5.91%
- Final paper account: $105,911 from a $100,000 starting account
- Window: 16 live market days
- Trades: 37

Builderr's public result page contains the dated chart and the full method notes:

https://builderr.ai/trading-v0/winners/arnav

## What the local preview proves

The bundled preview uses public sample windows to check that the agent:

- loads and runs without crashing;
- returns orders in the challenge format;
- stays within the leverage and concentration safety checks; and
- avoids a catastrophic sample drawdown.

It does **not** reproduce the official result. The official run used the challenge engine, its
market data and fills, and the original 16-day window, which are not bundled in this repository.

## Claim boundary

This archive supports the claim that Arnav's agent won one dated Builderr paper-trading challenge
window. It does not support a claim of guaranteed returns, long-term alpha, or suitability for a
real brokerage account.

