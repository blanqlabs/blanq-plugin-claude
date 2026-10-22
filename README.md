# Blanq.open-dev

Blanq wallet is the first AI-native secure, self-custodial wallet for tokenized assets. Assets are always in the user's control, while the signing keys stay secure in Blanq's Trusted Execution Environment (TEE).

This plugin connects Claude to your Blanq wallet, so you can check your balances, open your wallet, pay for things with x402 once you authorize each payment, and shop Blanq's catalog.

## Use it

1. Install the plugin, then connect Blanq and sign in to your Blanq wallet when Claude asks.
2. Ask Claude things like:

   - "What's my Blanq balance?"
   - "Find me trail running shoes."
   - "Buy a fortune cookie with Blanq."

## Data

The plugin runs no code on your device. It reaches Blanq's MCP server at the URL in its MCP configuration, signed in as you through OAuth. It receives the searches, delivery location and payment requests you ask for, and returns your balances, product results, payment confirmations and a link to your wallet. Every payment needs your authorization in the wallet.

Privacy policy: <https://www-dev.blanq.ai/legal/privacy>
