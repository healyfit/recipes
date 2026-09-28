# Dinner grocery workflow

## The flow
1. Mark says what dinner needs ("turkey pesto pasta tonight", "salmon bowls for 4", or a freeform list).
2. Match to `recipes.yaml` (or take the freeform list as-is for new dishes).
3. Prompt the check items in bulk: one message listing every pantry-type
   ingredient (salt, pepper, oils, spices, sauces, etc.) with kitchen-unit
   amounts (tbsp/tsp/cups, converted from grams). Mark confirms what he has;
   only what's missing gets bought. No pantry inventory is tracked and
   nothing is assumed — the bulk prompt replaces it.
4. Resolve each remaining ingredient to a specific product via the shopping
   profile, then order history, then default + flag (see Troubleshooting).
5. Build the cart (browser, delivery/pickup) and present it for review.
6. Mark reviews/approves; corrections become standing preferences.
7. Checkout only after explicit approval.

## Troubleshooting / ambiguity resolution
Order of operations for "which brand/kind?":
1. **Profile first** — `~/memory/shopping/PROFILE.md` item and category rules.
2. **Order history** — what he actually bought before (70 orders on file).
3. **Default aggressively + flag at review** — pick the most likely option,
   mark it as a guess in the cart review. Silence = approval; corrections
   get written back to the profile. Never interrogate drip by drip.
4. **Ask once** — only for high-stakes ambiguity (e.g. kosher salt brand
   changes the food). The answer becomes a standing rule.

## Current limitations (2026-09-27)
- Aldi **in-store** shopping lists are native-app-only. Instacart web exposes
  no in-store mode and no lists page. Cannot read or write the in-store list
  from the browser; cannot drive the phone app.
- Delivery/pickup carts work via the browser (sign-in verified 2026-09-27:
  saved login + CAPTCHA preference + email code).
- No live price/inventory API. Price checks are minutes per lookup via browser.
  Mitigation planned: cached Aldi price book (assortment ~1,400 SKUs).
- Official Instacart connector for Muse announced 2026-09-22, not yet live.
  Revisit in-store automation when it ships.
