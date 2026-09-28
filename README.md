# Recipes

Machine-readable recipe index. Single source of truth is `recipes.yaml` —
any assistant (Muse, ChatGPT, Gemini, Claude) can read it directly, no
conversion needed.

## Format

```yaml
version: 1

recipes:
  - id: turkey-pesto-pasta
    title: Turkey Pesto Pasta

    yield:
      quantity: 1
      unit: batch

    time:
      prep: 15        # minutes, optional
      cook: 30        # minutes, optional

    meal: [dinner]    # dinner, breakfast, snack, etc.
    cuisine: [italian-american]   # optional
    tags: [turkey, pasta, stovetop]  # optional, freeform

    ingredients:
      - quantity: 400
        unit: g
        item: dry pasta
      - quantity: 18
        unit: g
        item: garlic
        note: minced          # optional
      - item: salt
        note: to taste         # no quantity = unmeasured

    instructions:
      - Boil pasta until just tender.

    notes:                    # optional
      - Weigh the finished batch and log grams on the plate.
```

Rules:
- One recipe = one block. `id` is a stable slug — other tooling keys off it,
  so don't rename it casually.
- Ingredients use `quantity` + `unit` + `item`, with optional `note`.
  Units are whatever the recipe author used (g, cups, tbsp, lb) — the
  grocery flow converts to purchasable products at cart time.
- Omit `quantity`/`unit` for unmeasured items (salt, pepper); use
  `note: to taste`.
- Keep block style (each key on its own line). It's what assistants edit
  most reliably.
- One file until ~100 recipes. A single file pastes straight into any chat.

## Workflow

`WORKFLOW.md` documents the dinner grocery flow that consumes this file:
request → match recipe → bulk pantry prompt → resolve products → cart → review.
