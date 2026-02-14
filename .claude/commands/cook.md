---
description: "Generate a full recipe with science notes"
argument-hint: "<ingredients, method, constraints — be casual>"
---

Read `food-knowledge.md` into context first — it contains the book-sourced science that makes your output excellent.

Then read `CLAUDE.md` for the recipe output format and rules.

Parse the user's input for: ingredients (preserve exact quantities), cooking method, flavor direction, constraints (dietary, timing, equipment), and serving count. Default to 2 servings if not specified.

Generate a full recipe following the format in CLAUDE.md. Include:
- Precise ingredient table in grams
- Numbered steps with temperatures and times
- Brief inline science notes (1 sentence each, only where it matters)
- Quick Rationale section (3 sentences: why this technique, why these ratios, what makes it work)

Save the recipe to `recipes/YYYY-MM-DD-slug.md` where the slug describes the dish.

Tell the user the file path. This is now the active recipe — future `/adjust` commands will update it.

User wants: $ARGUMENTS
