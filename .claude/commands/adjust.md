---
description: "Modify the active recipe based on feedback"
argument-hint: "<what to change — swap ingredient, adjust quantity, add course>"
---

Find the most recently modified `.md` file in `recipes/`. That's the active recipe.

Read the active recipe file and `food-knowledge.md`.

Apply the user's requested changes directly to the file:
- Swap ingredients → recalculate affected quantities
- Change servings → scale everything proportionally
- Add/remove courses → update ingredient tables and method
- Adjust technique → rewrite relevant steps with correct science

Update the file in place using the Edit tool. Do NOT rewrite the entire file — make targeted edits.

After editing, show the user a brief summary of what changed (not the full recipe unless they ask).

User wants to change: $ARGUMENTS
