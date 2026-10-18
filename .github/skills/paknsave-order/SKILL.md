---
name: paknsave-order
description: Shop for groceries on the PAK'nSAVE online store (Click & Collect) using the Playwright browser tools. Adds the requested items to the cart, verifies the cart with the user, shows available pickup dates/slots, and takes the user through to payment. Use when the user wants to order from Pak n Save, fill a cart, choose a pickup time, or pay a grocery bill.
---

# PAK'nSAVE order skill

Drive https://www.paknsave.co.nz with the Playwright browser tools (`playwright-browser_*`).
Work end to end: items -> cart check -> pickup slot -> payment. **Never skip a confirmation step.**

## Rules
1. Never type, store, or log card details or passwords. If login or payment details are needed, pause and ask the user to enter them in the browser themselves (or provide a saved-card choice on the page).
2. Never place the order or press the final "Pay"/"Place order" button without an explicit "yes, pay" from the user in the current conversation, after showing the final total.
3. Never substitute a product silently. If an item is unavailable or ambiguous, ask the user to choose.
4. Do not store personal data (address, card, account) anywhere.

## Workflow
1. **Collect the list.** Ask for items, quantities, brand/size preferences, budget, and the chosen store (Click & Collect store). Repeat the list back.
2. **Sign in / choose store.** Navigate to the site, select the pickup store, and let the user sign in themselves.
3. **Add to cart.** For each item: search, pick the best match (respect brand/size/price), set quantity, add to cart. Keep a running table of: item, size, unit price, qty, line total. Report any not found or out of stock.
4. **Verify the cart.** Open the cart and compare it with the requested list. Show the user a table (item, qty, price), the subtotal, any fees and the total. Flag mismatches, substitutions, and specials. Ask: "Is the cart correct? Change anything?" Fix and re-verify until the user approves.
5. **Pickup dates.** Proceed to checkout and read the available Click & Collect days and time slots (and any cut-off/ordering deadline and pickup fee). Present them as a list, e.g. "Mon 20 Oct: 10-11am, 11am-12pm ...". Let the user pick one; reserve the slot.
6. **Final confirmation.** Summarise: items, total, pickup store, date/slot, payment method. Ask for explicit approval to pay.
7. **Pay.** Only after approval, complete payment. If the page requires card entry or 3-D Secure/bank approval, hand control to the user for that step. Report the order number and confirmation, plus the pickup date/time and what to bring.

## Failure handling
- Page changes or captchas: take a snapshot, describe the problem, ask the user to help.
- Price changes between cart and checkout: stop and re-confirm with the user.
- Session timeout: re-open the cart and re-verify before continuing.
