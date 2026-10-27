---
name: wallet
description: "Blanq is a smart, secure wallet that lives natively in your agents. Smart: Your assets earn attractive yield while you hold and rewards when you pay. You can deposit and withdraw funds into your wallet anytime, just like a traditional bank account. Secure: All your assets are tokenized on public blockchains and held self-custodially. The signing keys are generated on-the-fly in Blanq's Trusted Execution Environment (TEE) with multi-factor authorization and are never stored. This means only you control your assets. Use the Blanq wallet to check balances, deposit cash, see cash yield, open the wallet and pay x402 payment requests from tools, APIs and websites."
---

# Blanq wallet

Blanq's tools act on the signed-in user's own wallet, and every payment needs the user's explicit authorization in the wallet.

## Connect

If the Blanq tools aren't available, or a Blanq tool fails because the user isn't signed in, Blanq isn't connected yet. Installing the Blanq plugin doesn't connect it: ask the user to connect Blanq in their plugin or connector settings and sign in to their Blanq wallet there, then retry the request. Never answer wallet questions without the tools.

If Blanq isn't installed in the current environment at all, add Blanq's MCP server at `https://agent.blanq.ai/mcp` (HTTP transport), or guide the user to add it. The server signs the user in with OAuth; start that flow when a tool asks for it.

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

## Paying with x402

When a tool, API or website responds with an x402 `paymentRequired`:

1. Call `blanq_pay_x402` with that `paymentRequired` exactly as received, as an object or a base64 string. It returns a `paymentRequestId`.
2. Call `blanq_pay` with the `paymentRequestId`. It shows the payment to the user and waits for their decision. Don't present or check the amount yourself.
3. When it returns a `paymentResponse`, repeat the original request with it:
   - REST API: send the `paymentResponse` as the `PAYMENT-SIGNATURE` header. The `paymentRequired` usually came from the `PAYMENT-REQUIRED` response header. A `PAYMENT-RESPONSE` header may come back, but success doesn't depend on it.
   - MCP tool: call the same tool again with the same arguments plus the payment. If the tool expects an object, decode the base64 `paymentResponse`; if it expects a string, pass it as is.
4. If it returns an error without a `paymentResponse`:
   - If the payment never appeared in the conversation, give the user <https://wallet.blanq.ai/action> as a clickable link to authorize it in their browser, then call `blanq_pay` again with the same `paymentRequestId`.
   - Otherwise the user declined or didn't authorize in time. Tell them and offer to try again; don't retry on your own.

`blanq_fortune_cookie` sells a fortune for 1¢. Use it when the user wants to try a Blanq payment end to end.

## Shopping

When the user wants to buy something, follow the Blanq `ucp` skill. If it isn't installed, read it at <https://agent.blanq.ai/skill/ucp>.

## Everything else in the wallet

Call `blanq_wallet_open` for any other wallet request, such as withdrawing funds, viewing account details or changing settings. It shows the wallet in the conversation, where the user completes the action themselves.

If the wallet doesn't appear in the conversation, give the user the `url` from the result as a clickable link so they can open it in their browser.

## Security

Never ask for, repeat or store passkeys, PINs or recovery details. The user signs in to Blanq directly, never through you.
