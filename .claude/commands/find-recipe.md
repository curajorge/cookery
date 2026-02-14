---
description: "Search saved recipes"
argument-hint: "<ingredient, technique, dish name, or cuisine>"
---

Search `recipes/` directory:

1. Search filenames with Glob for matches
2. Search file contents with Grep for the query term
3. If multiple matches, list them with: filename, recipe name, date, key ingredients
4. If one match, show the full recipe
5. If no matches, say so and suggest what's available

User is looking for: $ARGUMENTS
