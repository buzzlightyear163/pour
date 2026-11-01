# POUR ($POUR): Pour SOL in. Launch on Hyperliquid.

Landing page and launch desk for POUR. You pay in SOL from Phantom, and your coin goes live on HyperEVM (chain 999) with its LP burned. No HYPE to buy, no bridge to touch, and no treasury holding your SOL.

One file (`index.html`) with its own WebGL raymarch engine. It has no build step and no API keys.

## What's real and what's preview

| Part | Status |
|---|---|
| HYPE/SOL prices (Hyperliquid `api.hyperliquid.xyz/info`, allMids) | Live, refreshes every 12 s |
| HyperEVM block + gas price (`rpc.hyperliquid.xyz/evm`) | Live, refreshes every 4 s |
| Itemized quote (seed, first buy, gas, Relay est., POUR fee, Solana fee) | Live math on live prices. The Relay line is an estimate |
| HyperEVM wallet created in the browser (secp256k1 + keccak, EIP-55) | Real. Verified against ethers.js (45/45) |
| Phantom connect | Real (connects only, signs nothing) |
| Image crop/resize, share card, Copy text | Real |
| The pour itself (Relay route → ERC-20 deploy → pool → LP burn) | **Dry run.** The button says so and the receipt is stamped "Dry run · no SOL moved" |

If the live feeds can't be reached, the page falls back to preview prices and labels them "Preview".

## Fill in CONFIG (top of the `<script>`)

```js
ca: "",            // $POUR mint. Empty shows "Posted here and on X at launch"
x: "",             // https://x.com/yourhandle (shows X links when set)
dexscreener: "",   // chart link (shows Chart button when set)
site: "",          // your domain, used in the share text
fees: { launchSol: 0.02, burnPct: 50, floatPct: 50 },
seedHype: 0.25,    // HYPE seeded per pool (quote line)
gasUnits: 3200000, // HyperEVM gas estimate (quote line)
relayFeePct: 0.3, relayFeeUsd: 0.05,
launcher: ""       // leave empty = dry-run mode
```

Once `ca` is set, every "Buy $POUR" button goes to `https://pump.fun/coin/<ca>`.

## Deploy

GitHub → Vercel → New Project → Framework: **Other**, no build command, output = root. Keep `og.jpg` next to `index.html`.

## Check after deploy

- The intro plays and the 3D runs smoothly on a real GPU (the sandbox renders on CPU).
- Fonts load: Fraunces, Schibsted Grotesk and Spline Sans Mono from Google Fonts.
- The lamp in the header turns green and HYPE/SOL/block/gas show numbers.
- The X card preview shows `og.jpg` (use the X post composer or opengraph.xyz).
- On mobile, the pinned "Route" and "How" sections scroll smoothly.
