# Blanq.dev

Blanq wallet is the first AI-native secure, self-custodial wallet for tokenized assets. Assets are always in the user's control, while the signing keys stay secure in Blanq's Trusted Execution Environment (TEE).

This plugin connects Claude to your Blanq wallet, so you can check your balances and open your wallet in the conversation, where you manage it yourself.

## Use it

1. Install the plugin, then connect Blanq and sign in to your Blanq wallet when Claude asks.
2. Ask Claude things like:

   - "What's my Blanq balance?"
   - "Open my Blanq wallet."
   - "How much do I hold in euros?"

## Data

The plugin runs no code on your device. It reaches Blanq's MCP server at the URL in its MCP configuration, signed in as you through OAuth. It returns your balance in each currency, an estimated total, and a link to your wallet.

Privacy policy: <https://www-dev.blanq.ai/legal/privacy>
