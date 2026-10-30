# Noren plugin

Let your agent look at a wallet's record and verify a payment on Robinhood Chain before it pays or trusts a counterparty.

This plugin adds Noren's read-only tools over a remote MCP. Nothing runs locally and no key is needed.

## Install

Remote MCP:

```
https://mcp.usenoren.xyz/mcp
```

- Cursor: add it from this plugin, or add an MCP server with the URL above.
- Claude Code: `claude mcp add --transport http noren https://mcp.usenoren.xyz/mcp`

## Tools

| Tool | What it does |
| --- | --- |
| `noren_reputation` | Score and tier of a wallet, from settled payments only, with the transactions behind it |
| `noren_verify_payment` | Reads a transaction from the chain RPC and returns its USDG transfers |
| `noren_leaderboard` | Top paying wallets |
| `noren_gateway_stats` | Paid APIs, 402 challenges, settled payments |
| `noren_list_apis` | Pay-per-call APIs with their prices |

The hosted endpoint is read-only and allows 60 requests per minute per address. To let an agent pay for a gateway API, run the local server (`npx -y noren-mcp`) with your own key and caps. See the [MCP docs](https://docs.usenoren.xyz/mcp-server).

## What is in here

- `.mcp.json`: the Noren MCP (remote).
- `rules/noren.mdc`: a rule that has the agent check a counterparty before paying or delegating.
- `skills/noren/SKILL.md`: how to run the checks and gate on them.

## Origin

Derived from `open-covenant/covenant-plugin` (Apache-2.0); see [NOTICE.md](./NOTICE.md). The tools and text were rewritten for Noren, because the original checks were specific to another chain.

https://usenoren.xyz
