<p align="center">
  <img src="./banner.png" alt="ponk x GitHub" width="100%">
</p>

## Ponk ☁️

**Autonomous liquidity on six chains.** LP agents that open, rebalance, compound and exit concentrated positions on Solana, Ethereum, Arbitrum, Base, BNB Chain and Robinhood Chain, plus swap, trackers and a launchpad.

[ponk.exchange](https://ponk.exchange) · [Docs](https://ponk.exchange/docs) · [X](https://x.com/ponkexchange) · [Telegram](https://t.me/ponkexchange) · [Status](https://ponk.exchange/status)

## Chains and venues

| Chain | Venues | What an agent does there |
|---|---|---|
| Solana | Meteora DLMM, Orca Whirlpools, Raydium CLMM, Meteora DAMM v2 | Opens a range, recenters it when price leaves, compounds the fees, exits on your stops. On DAMM v2 it holds a share of the pool and compounds. |
| Ethereum | Uniswap v2, v3, v4 | Runs a range on v3 and v4 and recenters it; holds full range on v2. Compounds the fees. |
| Arbitrum | Uniswap v2, v3, v4 | The same, at Arbitrum gas. |
| Base | Aerodrome Slipstream, Aerodrome Classic | Runs a range on Slipstream and full range on Classic. Staked in the pool's gauge, the position farms AERO, which the agent harvests and compounds; a staked position earns AERO in place of swap fees, and staking is your choice per agent. |
| BNB Chain | PancakeSwap v2, v3, Infinity CL | Runs a range on v3 and Infinity CL, full range on v2. A staked v3 position farms CAKE on top of its swap fees, which the agent harvests and compounds. |
| Robinhood Chain | Uniswap v2, v3, v4 | Runs the same strategies on Robinhood Chain pools, stock token pools included, around the clock. |

You hold your own funds on every chain. An agent has its own wallet, acts only inside the mandate you sign, and pays out only to the address that mandate proved. Nothing is bridged: an agent on BNB Chain is funded with BNB, on the other EVM chains with ETH, on Solana with SOL.

## Documentation

- [Getting started](https://ponk.exchange/docs)
- [Create an agent](https://ponk.exchange/docs/agents/create-agent)
- [Ponk Copilot](https://ponk.exchange/docs/agents/copilot)
- [Strategies](https://ponk.exchange/docs/agents/strategies)
- [Venues](https://ponk.exchange/docs/agents/venues)
- [Risk controls](https://ponk.exchange/docs/agents/risk-controls)
- [Fees and referrals](https://ponk.exchange/docs/agents/fees-referrals)

## Products

- [LP Agents](https://ponk.exchange/agents): autonomous concentrated liquidity on Meteora, Orca and Raydium on Solana, Uniswap on Ethereum, Arbitrum and Robinhood Chain, PancakeSwap on BNB Chain and Aerodrome on Base, with CAKE and AERO farming where the venue pays it
- [Ponk Copilot](https://ponk.exchange/docs/agents/copilot): one sentence to a planned fleet of agents on one chain or several, "I have $200, put it in the top 5 BNB pools"
- [Swap](https://ponk.exchange): market, limit, DCA and TP/SL
- [Discover](https://ponk.exchange/discover): LP opportunities, the [X Tracker](https://ponk.exchange/docs/trackers/x) and the [Wallet Tracker](https://ponk.exchange/docs/trackers/wallets)
- [Plot](https://ponk.exchange/plot): backtest a range on a pool's real history
- [Top Ponkillionaires](https://ponk.exchange/ponkillionaires): the public agent leaderboard
- [Launchpad](https://ponk.exchange/docs/dex/launch-a-token)
- [Telegram bot](https://t.me/Ponkexchangebot): trade, run agents and get alerts from Telegram

## Build on Ponk

### SDKs

- Python: [`ponk`](https://pypi.org/project/ponk/) on PyPI ([source](https://github.com/ponkexchange/ponk-sdk))
- Rust: [`ponk`](https://crates.io/crates/ponk) on crates.io ([source](https://github.com/ponkexchange/ponk-sdk/tree/main/rust))
- Command line: [`ponk-cli`](https://crates.io/crates/ponk-cli), `cargo install ponk-cli`

All three cover every chain: list an EVM chain's pools, create an agent on one, read its wallet, position and farm rewards, and get the link where your own wallets fund it and sign.
- TypeScript launch kit: [`@ponkrain/sdk`](https://github.com/ponkexchange/ponk-rain)

### APIs

- [Agents API](https://ponk.exchange/docs/developers/agents-api): `/v1`, API keys, every site action including fleets, on every chain
- [Public API](https://ponk.exchange/docs/developers/public-api): pools, quotes, prices, no key needed, including the pool boards of the five EVM chains

### AI and MCP

- MCP server: `https://ponk.exchange/mcp` for Claude, ChatGPT, Cursor and any MCP client, with wallet sign-in ([guide](https://ponk.exchange/docs/developers))

  ```
  claude mcp add --transport http ponk https://ponk.exchange/mcp
  ```

  Then ask in one line: "I have $100, put me in one ETH pool on Base." The answer is the pool, the amount in ETH and in dollars, the gas and Ponk's fees, and the link where your own wallet funds the agent and signs.
- [`llms.txt`](https://ponk.exchange/llms.txt)

## Research

- [Ponk's Law](https://github.com/ponkexchange/ponks-law): the survival-weighted value model the agents run on

## Security

- [Audits](https://ponk.exchange/docs/audits) · [Report (PDF)](https://ponk.exchange/audits/zauth-ponk-exchange-2026-09-29.pdf)
- [Report a vulnerability](./SECURITY.md)
