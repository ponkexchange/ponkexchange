<p align="center">
  <img src="https://ponk.exchange/brand/ponk-wordmark.png" alt="ponk.exchange" width="300">
</p>

<h3 align="center">Autonomous Liquidity Management &middot; Built on Solana</h3>

<p align="center">
  <a href="https://ponk.exchange"><b>ponk.exchange</b></a> &middot;
  <a href="https://ponk.exchange/docs">Docs</a> &middot;
  <a href="https://ponk.exchange/docs/developers/agents-api">API</a> &middot;
  <a href="https://ponk.exchange/docs/audits">Audits</a> &middot;
  <a href="https://ponk.exchange/start">Start earning</a>
</p>

---

An agent opens a concentrated LP position, collects the fees, compounds them, and
moves the range when the price does. Across **Meteora DLMM**, **Orca Whirlpools**,
**Raydium CLMM** and **Ponk Clouds**.

Live on mainnet with real funds. Non-custodial by default: you sign every action
unless you explicitly grant a scoped, expiring mandate.

### Why ranges are the whole game

Concentrated liquidity earns fees only while price is inside your range. Too tight
and you are out of range earning nothing; too wide and your capital is spread so
thin the fees do not cover divergence. The job is choosing a range, knowing when it
stopped being right, and moving it **only when moving it is worth more than it costs**.

That last clause is where most automation goes wrong. A rebalance is not free: gas,
a balancing swap, rent, and a performance fee. An agent that rebalances on every
wobble loses to one that holds.

### A bin position has a hard range ceiling, and it is a storage limit

A DLMM position stores per-bin shares in a fixed-size account. Meteora caps a
position at 70 bins. On the deepest SOL/USDC pool, bin step 4 bps:

```
69 usable bins x 4 bps  ->  +/-1.37%
```

No configuration raises it. If you have been asked for a +/-5% range on that pool,
it cannot be built there, and an interface offering it is quietly clamping you.

A **CLMM** stores one liquidity value for the whole range instead of per-tick
shares, so it has no equivalent ceiling:

```
+/-1.37%  ->  136 ticks each side
+/-3%     ->  296
+/-5%     ->  488
+/-6%     ->  583
```

Same fee tier, no cap. That is a property of the venue, not a feature one team
shipped and another did not.

### Verify the chain, not the docs

Published program source is not the deployed program. Before encoding a single
Raydium CLMM instruction we checked the layouts against mainnet, and two things did
not match the repository:

- `protocol_position` is marked non-writable and "deprecated" in current source.
  On the deployed program it is **writable**. Encoding it read-only fails.
- `DecreaseLiquidityV2` declares 16 accounts. The real instruction carries **17**:
  a writable `pool_tick_array_bitmap_extension` PDA appended as a remaining account.

We also confirmed the `PersonalPositionState` discriminator against 176,001 live
accounts before trusting our decoder.

If you are integrating a Solana AMM: decode a real account and read a real
transaction before you ship an encoder. The cost of being wrong is not a failed
build, it is a transaction that addresses the wrong account.

### How the decision engine thinks

The objective is **not** "maximize fees", which is pathological: tighter ranges
capture more fees right up until divergence and churn destroy the advantage. It is
*maximize incremental net value versus an appropriate control, subject to an
explicit risk mandate*.

**HOLD is a real candidate.** It competes on expected value like any action, and it
has to be beaten by a margin rather than by a cent, because an `argmax` over a
noisy estimator is a machine that turns noise into transaction fees.

**Safety constraints live outside the optimizer.** Cooldowns, anti-thrash floors and
the per-pool re-entry rule each exist because something went wrong once. They are
applied before expected value is ever compared, so no estimator can discover that
overriding one looks profitable.

**A recenter is one transaction.** Remove, close and re-open land together or not at
all. A remove that lands without its re-open leaves a user in cash and out of range.

### Security

The web application, the public API and the MCP server were assessed by **zauth
(Vector)** on 29 September 2026: a deep scan across 51 endpoints, 5 subdomains,
4 forms and 58 input vectors, run over 389 turns, with findings verified by
browser-based proof of concept.

**12 findings: 3 high, 5 medium, 1 low, 3 informational. No critical.**

- [**Read the report (PDF)**](https://ponk.exchange/audits/zauth-ponk-exchange-2026-09-29.pdf)
- [**Audits**](https://ponk.exchange/docs/audits) in the docs, with the scope and
  coverage tables

To report something, see
[SECURITY.md](https://github.com/ponkexchange/ponkexchange/blob/main/SECURITY.md).

### Principles

**Numbers a user might act on are never fabricated.** A value we cannot compute
renders as a dash and says why.

**Activity is not the product. Selectivity is.** An agent that fires all day is not
working harder than one that holds. `evaluated 357 times, acted 0 times` is a good
day when nothing was worth paying for, and the product says so.

<p align="center">
  <sub><a href="https://ponk.exchange">ponk.exchange</a> &middot; Solana</sub>
</p>
