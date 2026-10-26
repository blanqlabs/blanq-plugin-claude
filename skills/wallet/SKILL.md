---
name: wallet
description: Check Blanq wallet balances, deposit cash, see cash yield and open the Blanq wallet in the conversation. Use when the user asks about their Blanq wallet, how much money they hold, their balance in a currency, how to deposit, what their cash earns, or wants to open, view or manage their wallet.
---

# Blanq wallet

Blanq is an AI-native, self-custodial wallet. The Blanq connector acts on the signed-in user's own wallet.

## Connect

If the Blanq tools aren't available, or a Blanq tool fails because the user isn't signed in, Blanq isn't connected yet. Installing the Blanq plugin doesn't connect it: ask the user to connect Blanq in their plugin or connector settings and sign in to their Blanq wallet there, then retry the request. Never answer wallet questions without the tools.

## Balances

Call `blanq_wallet_balances` when the user asks how much they hold, what their balance is, or what their wallet is worth.

- `assets` has one entry per currency with a balance above zero. `total` is the estimated value of all holdings in the user's preferred currency.
- Report each amount exactly as returned, with its currency. Don't convert, round or estimate amounts yourself.
- If `assets` is empty, say the wallet holds no funds.
- Call it again for each question instead of reusing an earlier result, because balances change.

## Depositing cash

Call `blanq_cash_deposit` when the user wants to deposit, add funds or top up their wallet, or asks for their deposit account details.

- It takes no arguments, even when the user names a currency. The widget starts with the wallet's preferred currency, and the user picks the linked bank account they send from, which also sets the currency.
- When `status` is `ready`, the widget shows the bank details to send the transfer to. If the widget doesn't appear, list each of `fields` with its label and value exactly as returned, including any note. When a memo or reference is among them, the deposit only arrives if the user includes it.
- When `status` is `accountSelection`, the user picks the bank account they're sending from in the widget. If the widget doesn't appear, give them the `url` from the result as a clickable link to pick it in their wallet.
- For any other `status`, the user has to finish a step in their wallet first. Tell them what's missing and give them the `url` from the result as a clickable link.
- `accounts` lists the user's linked bank accounts in every currency they can deposit in. If the widget doesn't appear and the user wants another currency, give them the `url` from the result as a clickable link to deposit from their wallet.

## Yield

Call `blanq_cash_yield` when the user asks what their cash earns, or about yield, interest or rates.

- `rates` holds the current yield rate in percent for each currency. Report the rates exactly as returned. If `rates` is missing, the rates aren't available right now.
- `balances` holds the user's cash balance in each currency.
- Don't estimate or project earnings yourself.

## Everything else in the wallet

Call `blanq_wallet_open` for any other wallet request, such as withdrawing funds, viewing account details or changing settings. It shows the wallet in the conversation, where the user completes the action themselves.

If the wallet doesn't appear in the conversation, give the user the `url` from the result as a clickable link so they can open it in their browser.

## Security

Never ask for, repeat or store passkeys, PINs or recovery details. The user signs in to Blanq directly, never through you.
