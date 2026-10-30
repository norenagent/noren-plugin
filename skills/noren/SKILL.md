---
name: noren
description: Check a wallet's settled-payment record and verify a payment on Robinhood Chain before paying or delegating, using Noren's read-only MCP tools.
---

# Noren checks

Use this when an agent is about to pay, delegate to, or hand access to another wallet or service on Robinhood Chain (eip155:4663), and you want evidence instead of a claim.

Noren serves read-only tools over a remote MCP at `https://mcp.usenoren.xyz/mcp`:

- `noren_reputation(address)`: score and tier for a wallet, computed only from payments that settled through the Noren x402 gateway. The response includes the transaction hashes behind the number.
- `noren_verify_payment(tx_hash)`: reads the transaction from the chain RPC and returns its USDG transfers, so a claimed payment can be checked without trusting anyone.
- `noren_leaderboard()`: the top paying wallets.
- `noren_gateway_stats()`: paid APIs, 402 challenges and settled payments.
- `noren_list_apis()`: the pay-per-call APIs, with slug, path and price in USDG.

## How to use it

1. Call `noren_reputation` on the counterparty. A wallet with no payments through the gateway has no score. Treat that as unproven.
2. If someone says they paid, ask for the transaction hash and run `noren_verify_payment` on it.
3. Gate on what you got. For anything with real funds, do not treat an empty record as a pass.

## Limits

- The record only covers payments through the Noren gateway, not all activity on the chain. Some of the early payments come from Noren's own test wallets.
- The hosted endpoint has no payment tool. To let an agent pay for a gateway API, run the local server with your own key and spending caps: `npx -y noren-mcp`.
- Do not invent a score or a verdict. If a tool returns nothing, say so.
