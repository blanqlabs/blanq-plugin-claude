# Blanq.dev

Blanq is a smart, secure wallet that lives natively in your agents. 
Smart: Your assets earn attractive yield while you hold and rewards when you pay. You can deposit and withdraw funds into your wallet anytime, just like a traditional bank account. 
Secure: All your assets are tokenized on public blockchains and held self-custodially. The signing keys are generated on-the-fly in Blanq's Trusted Execution Environment (TEE) with multi-factor authorization and are never stored. This means only you control your assets. 
This server lets chat agents connect to users' Blanq wallet and interact with it in-chat.
The user can check balance, see how to deposit assets and enquire what their cash earns.

This plugin connects Claude to your Blanq wallet. Interact with your Blanq wallet in the conversation - eg. open wallet widgets, check balances, get deposit instructions and yield information.

## Use it

1. Install the plugin, then connect Blanq in Claude's plugin or connector settings and sign in to your Blanq wallet.
2. Ask Claude things like:

   - "Open my wallet."
   - "What's my wallet balance?"
   - "How do I deposit cash?"

## Data

The plugin runs no code on your device. It reaches Blanq's MCP server at the URL in its MCP configuration, signed in as you through OAuth and lets you interact with your wallet from your chat.

Privacy policy: <https://www-dev.blanq.ai/legal/privacy>
