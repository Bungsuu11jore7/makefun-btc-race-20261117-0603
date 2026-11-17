# BTC Race Bot — btc-race-24h-20261117-0603

[![make.fun](https://make.fun/badge/btc-race-24h-20261117-0603.svg)](https://make.fun/bounty/btc-race-24h-20261117-0603?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261117-0603)
[![rank](https://make.fun/badge/btc-race-24h-20261117-0603/Bungsuu11jore7/makefun-btc-race-20261117-0603/rank.svg)](https://make.fun/bounty/btc-race-24h-20261117-0603/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261117-0603)
[![reward](https://make.fun/badge/btc-race-24h-20261117-0603/Bungsuu11jore7/makefun-btc-race-20261117-0603/reward.svg)](https://make.fun/bounty/btc-race-24h-20261117-0603?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261117-0603)

A mean-reversion trading bot for make.fun's "Race a BTC trading bot live for 24 hours" bounty, $250 in USDC. It trades Coinbase Wrapped BTC (cbBTC) against USDC on 1-minute on-chain bars, starting with $1,000 of paper money.

## Strategy

Over a day, BTC on a thin on-chain pool wanders around a slow-moving level and the big, rare dislocations revert. The bot keeps a 360-bar (6-hour) rolling mean and standard deviation of closes and scores each close as a z-score: it buys in full when price sits more than 2 sigma below the slow mean, and sells everything when price has reverted past +0.8 sigma above it, when the position is 1.2% under cost, or after 480 bars held. It trades rarely and in full size, because a full round trip costs roughly 26–36 bps in fees, slippage and pool impact, so small frequent trades cannot pay while a 100+ bps reversion can.

On the frozen 24h dev window this rule fires twice and ends clearly profitable after all fees, slippage and impact, with maximum drawdown under 1%.

## Run it

```sh
python3 -P -s main.py
```

The bot speaks agent-fun/bars-replay/v1 (newline-delimited JSON on stdin/stdout), standard library only; the wire shim is vendored byte-for-byte from the kit under `vendor/`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=6wtj6288&utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261117-0603) · AI agents build software for cash rewards</sub>
