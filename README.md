# Cookery

![Cookery](assets/cover.png)

A food science knowledge base powered by Claude Code. Type casual descriptions, get Michelin-caliber recipes back — precise to the gram, grounded in real food science from 30+ books.

No code, no dependencies. Just markdown files + Claude Code slash commands + git.

## How It Works

![Architecture](assets/architecture.png)

One file (`food-knowledge.md`) contains distilled food science from books like Lopez-Alt's *The Food Lab*, McGee's *On Food and Cooking*, Nosrat's *Salt Fat Acid Heat*, and 25+ others. When you run a command, Claude reads this file into context — it activates deep knowledge that produces much better output than a generic "make me a recipe" request.

Recipes are saved as `.md` files. You iterate on them in conversation. Git tracks everything.

## Commands

| Command | Example | What it does |
|---|---|---|
| `/cook` | `/cook chicken thighs 1.52 lbs, brine, pan cook, simple spices` | Full recipe with science notes. Saves to `recipes/` |
| `/quick` | `/quick cucumber salad with dill` | Terse recipe — ingredient table + steps, nothing else |
| `/adjust` | `/adjust swap pine nuts for walnuts, scale to 4 servings` | Edit the active recipe file in place |
| `/save-recipe` | `/save-recipe` | Mark recipe as final, git commit |
| `/find-recipe` | `/find-recipe carbonara` | Search saved recipes by name, ingredient, or technique |
| `/cook-view` | `/cook-view` | Generate a standalone HTML cooking guide with phased mise en place |
| `/save` | `/save` | Git add + commit + push everything |

## Typical Workflow

```
> /cook dry-aged NY strip 500g, cast iron, butter baste, garlic thyme

  → Claude reads food-knowledge.md
  → Generates recipe with precise temps, times, grams
  → Saves to recipes/2026-02-14-butter-basted-ny-strip.md

> /adjust add a pan sauce with shallot and red wine

  → Updates the same file with a new sauce section

> /adjust scale to 4 people

  → Recalculates all quantities in the file

> /save-recipe

  → Marks as Final, commits to git
```

## Cook View — HTML Cooking Guides

`/cook-view` turns any recipe into a standalone, dark-themed HTML cooking guide designed for a kitchen screen or TV. No JS, no build step — just a single `.html` file you can open in any browser.

**What it generates:**
- Phased mise en place — ingredients grouped by when you need them, not dumped in one list
- Side-by-side cards for parallel tasks (e.g., "salt the steak" + "make pasta dough" at the same time)
- Time badges on each phase so you know where you are in the cook
- Callout boxes for food safety warnings, technique tips, and phase completion markers
- Temperature badges inline with instructions

**Example:** See [`guides/valentines-dinner-for-two-guide.html`](guides/valentines-dinner-for-two-guide.html) — a 4-course dinner broken into 5 timed phases.

![Cook View Example](assets/cook-view-example.png)

## Project Structure

```
cookery/
├── CLAUDE.md              # Agent personality, rules, recipe format
├── food-knowledge.md      # The brain — 30+ books, 10 food science categories
├── .claude/
│   ├── settings.local.json
│   └── commands/          # 7 slash commands
├── recipes/               # Saved recipes (YYYY-MM-DD-slug.md)
├── guides/                # Generated HTML cooking guides
└── README.md
```

## Knowledge Categories

The knowledge file covers:

1. **Cooking science** — heat transfer, Maillard, thermodynamics
2. **Protein mastery** — meat, poultry, fish, eggs
3. **Seasoning & spice** — salt by weight, bloom timing, blending
4. **Salads & dressings** — vinaigrettes, emulsions, raw prep
5. **Brining & marinating** — wet/dry brine, salt penetration rates
6. **Fermentation** — lacto, koji, miso, vinegar
7. **Baking science** — flour, gluten, leavening, dough
8. **Fresh pasta** — ratios, kneading, rolling, shape-to-sauce pairing
9. **Food safety** — temps, danger zone, pasteurization tables
10. **Flavor pairing** — volatile compounds, bridging, contrast
11. **Sauce architecture** — mother sauces, pan sauces, emulsions
12. **Steak science** — dry-aging, reverse sear, butter baste

## Setup

1. Clone this repo
2. Open the folder in Claude Code
3. Run `/cook` with whatever you want to make
