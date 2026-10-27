---
name: ucp
description: "Shop Blanq's catalog across its merchants and check out in the shopping widget, with Blanq Pay or at the merchant's own checkout."
---

# Blanq shop

## Connect

If the Blanq tools aren't available, or a Blanq tool fails because the user isn't signed in, Blanq isn't connected yet. Installing the Blanq plugin doesn't connect it: ask the user to connect Blanq in their plugin or connector settings and sign in to their Blanq wallet there, then retry the request. Never answer wallet questions without the tools.

## Searching

Call `blanq_shop` for anything the user wants to buy, whether or not they name a store.

- When the user names a brand, pass it as `brand`, so the results come from that brand's own store rather than resellers.
- Results are scoped to where the user lives, so a delivery location must be on file. If it returns `locationRequired`, ask the user for the recipient's first and last name, street address, city, state or region, postal code and country. Save them with `blanq_shop_location`, then run the same search again.
- If the widget doesn't appear, list the products as markdown links with their price, merchant and rating.

## Checkout

The user opens a product in the shopping widget, picks its options and checks out there, paying with Blanq Pay from their wallet when the merchant takes it, or at the merchant's own checkout otherwise. There is no order or payment step for you to run, so point the user to the widget.

## Security

Never ask for, repeat or store passkeys, PINs or recovery details. The user signs in to Blanq directly, never through you.
