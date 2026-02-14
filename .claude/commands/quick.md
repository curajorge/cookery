---
description: "Generate a terse recipe — no explanations"
argument-hint: "<ingredients, method, constraints>"
---

Read `food-knowledge.md` into context — same knowledge, minimal output.

Read `CLAUDE.md` for rules (exact quantities, salt by weight, internal temps).

Parse the user's input. Default to 2 servings if not specified.

Output ONLY:
1. Recipe name
2. Ingredient table (grams)
3. Numbered steps (temps, times, no science explanation)

No rationale, no notes section, no prose. Just the recipe.

Save to `recipes/YYYY-MM-DD-slug.md`. Tell the user the file path.

User wants: $ARGUMENTS
