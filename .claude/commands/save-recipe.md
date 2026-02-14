---
description: "Finalize and commit the active recipe to git"
---

Find the most recently modified `.md` file in `recipes/`. That's the active recipe.

Read it. Update its **Status** from `Draft` to `Final`.

Then:
1. `git add` the recipe file
2. `git commit` with message format: `"recipe: slug-name"` (e.g., `"recipe: valentines-dinner-for-two"`)
3. `git push`

Confirm to the user: file path, recipe name, commit done.
