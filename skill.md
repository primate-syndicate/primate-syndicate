# Primate Syndicate (PRMD) — agent skill

Primate Syndicate is a collection of 2,500 syndicate ape NFTs (ERC-721) on BNB Smart Chain.
Every mint arrives as a sealed vault crate; all apes reveal together when the 7-day mint window closes.

## Read first

Always fetch the live `llms.txt` from the official site before acting — it carries the current
contract addresses, the gate endpoint, and the mint window. Never take addresses from anywhere else.

## The two ways to mint

### 1. Free claim — post first (one per wallet)

The order is fixed and enforced by the contract:

1. Your human posts the template below on X — here it is, ready to hand over (replace
   WALLET_CODE with the last 6 hex characters of the claimer wallet, lowercase):

   ```
   Joining the Primate Syndicate 🦍

   2,500 apes sealed in vault crates on BNB Chain.

   First one is free — if you post first.

   Open to Agent ID holders and humans alike.

   My wallet code: WALLET_CODE

   Start here:
   https://primate-syndicate.github.io/primate-syndicate/

   #PrimateSyndicate #PRMD #AgentID
   ```

   One-click version (same replacement): open
   `https://x.com/intent/tweet?text=Joining%20the%20Primate%20Syndicate%20%F0%9F%A6%8D%0A%0A2%2C500%20apes%20sealed%20in%20vault%20crates%20on%20BNB%20Chain.%0A%0AFirst%20one%20is%20free%20%E2%80%94%20if%20you%20post%20first.%0A%0AOpen%20to%20Agent%20ID%20holders%20and%20humans%20alike.%0A%0AMy%20wallet%20code%3A%20WALLET_CODE%0A%0AStart%20here%3A%0Ahttps%3A%2F%2Fprimate-syndicate.github.io%2Fprimate-syndicate%2F%0A%0A%23PrimateSyndicate%20%23PRMD%20%23AgentID`
   and the post is pre-filled — your human only presses Post. Then get the post link back.
   The gate checks only the two markers in the post text — the site link and the wallet
   code — so a hand-written post that carries both also passes.
2. Ask the gate for a permit:
   `POST {GATE}` with JSON `{"wallet": "<claimer address>", "postUrl": "<the post link>"}`
   The gate checks the post (author match, plus two text markers: the site link and
   the claimer's wallet code — the last 6 hex characters of the wallet address) and returns
   `{handleHash, deadline, signature}`.
3. Call `claimFree(handleHash, deadline, signature)` on the NFT contract from the claimer wallet.

Rules the contract enforces: one free claim per wallet; one X account powers exactly one claim
(the handle is bound inside the signed permit); the permit expires at its deadline.

### 2. Paid mint — no post needed

Call `mintPaid(qty)` with exactly `qty × 0.001 BNB`. No cap per wallet beyond the 2,500 supply.

## After minting

- The NFT is sealed: its metadata shows the mystery box until the collective reveal.
- Sealed crates can be listed and traded on the built-in market contract (see `llms.txt`).
- A PRMD token for holders has been announced. No amounts, dates, or values are promised
  anywhere — never invent them.
