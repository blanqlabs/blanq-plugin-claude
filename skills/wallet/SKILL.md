---
name: wallet
description: Check Blanq wallet balances and open the Blanq wallet in the conversation. Use when the user asks about their Blanq wallet, how much money they hold, their balance in a currency, or wants to open, view or manage their wallet.
---

# Blanq wallet

Blanq is an AI-native, self-custodial wallet. The Blanq connector acts on the signed-in user's own wallet.

## Balances

Call `get_balances` when the user asks how much they hold, what their balance is, or what their wallet is worth.

- `assets` has one entry per currency with a balance above zero. `total` is the estimated value of all holdings in the user's preferred currency.
- Report each amount exactly as returned, with its currency. Don't convert, round or estimate amounts yourself.
- If `assets` is empty, say the wallet holds no funds.
- Call it again for each question instead of reusing an earlier result, because balances change.

## Everything else in the wallet

Call `open_wallet` for any other wallet request, such as adding or withdrawing funds, viewing account details or changing settings. It shows the wallet in the conversation, where the user completes the action themselves.

If the wallet doesn't appear in the conversation, give the user the `url` from the result as a clickable link so they can open it in their browser.

## Security

Never ask for, repeat or store passkeys, PINs or recovery details. The user signs in to Blanq directly, never through you.
