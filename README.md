# monad-x402-map

A verified map of x402 on Monad: facilitators, payment rails, and actual sellers. Every entry
states how it was verified: probed over HTTP, checked on-chain, or actually paid (with the
transaction hash). Maintained by [ProofLines](https://prooflines.org/monad/); PRs welcome with
the same evidence standard.

Last sweep: 2026-08-09 (evening: Axil payability verified negative; glim.sh PAID over the mainnet USDC rail; our gate PAID on mainnet with real MON).

## Infrastructure (rails and facilitators)

| Project | Status | Evidence |
|---|---|---|
| [Official facilitator](https://x402-facilitator.molandak.org) (molandak) | LIVE, both networks | `/supported` returns `eip155:10143` and `eip155:143`, x402 v2 schemes incl. `upto`; facilitator address `0x7f6a2850...db86` |
| MetaMask Monad facilitator | announced | MetaMask ecosystem post in Monad Discord (June 2026); not probed yet |
| [MonX402](https://monx402.com) | site LIVE | responds to browser UAs, blocks bots; facilitator per its own description; not probed deeper |
| [m402.dev](https://www.m402.dev/) launchpad | unverified | aggressive rate limiting on fetch; retry pending |

## Sellers (endpoints you can actually pay)

| Project | What it sells | Rail | Status | Evidence |
|---|---|---|---|---|
| [ProofLines gate](https://prooflines.org/monad/x402-on-monad/) | Monad network concentration report | native MON, self-verified, testnet + mainnet | LIVE, PAID on BOTH networks | testnet tx [`0x372385ee...62ad3a`](https://testnet.monadexplorer.com/tx/0x372385ee8c03c6b93744cfa9a458dec45880ae653e0f60fb447f9bd65962ad3a) (block 51476148); MAINNET tx [`0x0d2792ef...52cc68`](https://monadexplorer.com/tx/0x0d2792ef5af187c943eeaa828e1b5d3d681ea924c2a64da1a8c850fa0c52cc68) (block 94492637, real MON, 2026-08-09); replay protection verified live |
| [glim.sh](https://glim.sh) | web/twitter/reddit/github data for agents | USDC on Monad MAINNET (`eip155:143`, asset `0x754704Bc...b603`), also Base + Solana | LIVE, PAID | paid 2026-08-09 over the mainnet USDC rail: EIP-3009 authorization signed, service returned 200 with results, settlement on-chain [`0x32b261b1...d37a2f`](https://monadexplorer.com/tx/0x32b261b1d700c73d6a511758b436e4f876e2b5b20a298d16755ae3a670d37a2f) (0.01 USDC, block 94493646) |
| [PayGate](https://paygatex402.vercel.app/) | micro-paywall platform (escrow, per-byte metering) | native MON via `PayGateRouter` contract | app LIVE, contract DEPLOYED, no public demo proxy | router `0x8197f76762F5b2cfeCbdfc1B90FBBAC3FC29b17C` has code on testnet (3,418 bytes); paying requires creating a proxy first |
| AxilProtocol | contract-based 402 with fee splits | native MON via contract | contract DEPLOYED, but NOT payable by outsiders | `0xB3A59e559B470Ce9Edc1Ccf70B912F8A021a4552` live on testnet, not paused, `totalExecutedIntents = 8`; source review 2026-08-09: `execute()` requires an EIP-712 signature from the protocol-configured `config.signerAddress`, and no public surface issues signed intents, so a buyer cannot pay without the operator; [GitHub](https://github.com/AxilProtocolV1/AxilProtocolV1) |

## Gone or dormant

| Project | Status |
|---|---|
| x402onmonad.com | 404 |
| daNomNoms (hackathon food-delivery demo, thirdweb x402) | app URL not found; [code](https://github.com/jayyu23/daNomNoms-monad) remains |

## Reading the map

- The rails are ready and healthy; the sellers are scarce. As of the last sweep, exactly two
  endpoints on this map can be paid by an agent without extra setup, and both are now verified
  PAID: ours (native MON, self-verified) and glim.sh (USDC via facilitator). Every other entry
  is infrastructure, gated, or gone.
- "PAID" means we sent the money and received the resource; nothing else earns that label.
- Related: the official [Monad x402 guide](https://docs.monad.xyz/guides/x402), our
  [engineering note](https://prooflines.org/monad/x402-on-monad/) on the facilitator-less native
  scheme, and [monad-x402-gate](https://github.com/ColinkaMir/monad-x402-gate) (MIT) if you want
  to become a seller yourself.

## License

MIT
