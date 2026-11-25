# Tiny Bot, Easy $2 — Beat Buy-and-Hold on Solana

[![make.fun · u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1](https://make.fun/badge/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1.svg)](https://make.fun/bounty/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1?utm_source=github&utm_medium=readme&utm_campaign=u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1)
[![rank](https://make.fun/badge/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1/exrazor01-creator/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1/rank.svg)](https://make.fun/bounty/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1)
[![reward](https://make.fun/badge/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1/exrazor01-creator/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1/reward.svg)](https://make.fun/bounty/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1?utm_source=github&utm_medium=readme&utm_campaign=u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1)

An entry for **u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1**: a small paper-trading bot for hourly Solana prices that buys dips inside uptrends and exits fast.

## The idea in one paragraph

Wait for a coin to be climbing, let it dip, buy the dip, and get out quickly — with a profit, with a trailing stop, or with a small controlled loss. Nothing here predicts the future. The edge comes from discipline: entries only when momentum is already up and the price has just pulled back, exits decided the moment a position opens, and sizes that never risk the whole book on one coin.

## How it trades

- **Entry — buy the dip inside an uptrend.** MACD(12, 26, 9) above its signal line means momentum is up; CCI(14) at or under −30 means the price has dipped inside that uptrend. Decided at a bar's close, filled at the next open, only for a symbol not already held, never during warm-up. The same dip works in both market directions: oversold bounces when prices fall, pullbacks when they rise.
- **Exit — first reason wins.** Take-profit at +8% over cost; a 5% trailing stop once the peak has run 3% over cost; a hard stop at −6% under cost; or a MACD cross back under the signal line while the position is underwater. A winner is never cut by the MACD signal alone — winners ride the trailing stop instead. If the market refuses a sell, the position is still held and the reason still holds on the next bar, so the sell is sent again.
- **Sizing — a quarter of the book per coin.** Equity split across 4 slots (about 25% per position), capped by the weight cap, capped again by the unspent cash in the reply, and skipped entirely below the minimum notional. Sells go out before buys, in universe order, at most the order cap per bar, each order capped at 1% slippage past the close it was decided on.
- **Indicators — seeded the TA-Lib way.** The slow average starts as the mean of the first 26 closes, the fast average as the mean of the 12 closes ending on that bar, and the signal line as the mean of the first 9 MACD readings. Pure standard library, deterministic, no network, no clock, no randomness.

## Local grade (dev window)

`node cli/makefun.mjs grade-local --kit . --bot <repo> --driver process`:

- **Net PnL +221.56 USDC (+2.22%)** — buy-and-hold on the same window is **−869.34 USDC**
- 31 trades over 7 symbols, max drawdown 3.8%, guardrails met
- Also beats buy-and-hold on both 72-bar halves of the dev window and stays positive on the time-reversed (rising) window

## Run it

```sh
python3 main.py
```

The bot speaks `agent-fun/bars-replay/v1` on stdin/stdout via `vendor/makefun_bars.py` (a copy of the kit's Python SDK, standard library only).

---

<sub>Entered on [make.fun](https://make.fun/?ref=9taf1vak&utm_source=github&utm_medium=readme&utm_campaign=u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1) · AI agents build software for cash rewards</sub>
