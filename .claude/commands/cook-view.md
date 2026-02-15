---
description: "Generate a standalone HTML cooking guide with phased mise en place"
argument-hint: "<optional: path to recipe file>"
---

Generate a dark-themed, standalone HTML cooking guide from a recipe. The output is a single `.html` file with all CSS embedded — no JS, no images, no external dependencies except Google Fonts.

## Step 1: Find the recipe

If `$ARGUMENTS` is a file path, use that. Otherwise, find the most recently modified `.md` file in `recipes/`. That's the active recipe.

Read the recipe file completely. Also read `food-knowledge.md` for science context you'll weave into callouts and technique notes.

## Step 2: Analyze structure

Determine recipe type:

- **Multi-course with timeline:** The recipe has multiple courses AND an "Execution Timeline" or sequenced cooking order. Timeline drives phase creation — parallel tasks become side-by-side cards in the same grid.
- **Single-course with stages:** One dish but clear prep/cook/rest stages. Phases follow: Prep → Cook → Rest/Cool → Finish.
- **Basic recipe:** Simple dish. Phases: Mise en Place → Cook.

Target 2–6 phases. Each phase gets a descriptive name and a time badge.

## Step 3: Generate the HTML

Create `guides/` directory if it doesn't exist. Save to `guides/{slug}-guide.html` where `{slug}` matches the recipe filename slug (e.g., `2026-02-14-valentines-dinner-for-two` → `valentines-dinner-for-two-guide.html`).

### Required HTML structure

Use this exact template. The CSS below must be embedded verbatim — do not modify it.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=3840, initial-scale=1.0">
<title>{Recipe Name} — Full Guide</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&family=DM+Serif+Display&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html {
    font-size: clamp(22px, 1.3vw, 34px);
    background: #0d0d0d;
    color: #e8e0d8;
  }

  body {
    font-family: 'DM Sans', 'Helvetica Neue', Arial, sans-serif;
    padding: 60px 100px;
    max-width: 3840px;
    margin: 0 auto;
    line-height: 1.5;
  }

  h1 {
    font-family: 'DM Serif Display', Georgia, 'Times New Roman', serif;
    font-size: 3rem;
    color: #fff;
    margin-bottom: 0.15em;
    letter-spacing: -0.02em;
  }

  .subtitle {
    font-size: 1.1rem;
    color: #b8756d;
    margin-bottom: 2rem;
    font-weight: 500;
  }

  .phase {
    margin: 50px 0 24px;
    display: flex;
    align-items: center;
    gap: 20px;
  }

  .phase h2 {
    font-family: 'DM Serif Display', Georgia, 'Times New Roman', serif;
    font-size: 2rem;
    color: #fff;
    white-space: nowrap;
  }

  .phase .time-badge {
    font-family: 'DM Sans', 'Helvetica Neue', Arial, sans-serif;
    font-size: 0.7rem;
    background: #b8756d;
    color: #0d0d0d;
    padding: 6px 18px;
    border-radius: 8px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    white-space: nowrap;
  }

  .phase-line {
    flex: 1;
    height: 1px;
    background: #2a2622;
  }

  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    margin-bottom: 20px;
  }

  .card {
    background: #1a1816;
    border: 1px solid #2a2622;
    border-radius: 18px;
    padding: 36px 40px;
  }

  .card.full {
    grid-column: 1 / -1;
  }

  .card h3 {
    font-family: 'DM Serif Display', Georgia, 'Times New Roman', serif;
    font-size: 1.5rem;
    color: #e8c8a0;
    margin-bottom: 0.4em;
    display: flex;
    align-items: center;
    gap: 14px;
  }

  .card h3 .tag {
    font-family: 'DM Sans', 'Helvetica Neue', Arial, sans-serif;
    font-size: 0.5rem;
    background: #3a2a22;
    color: #e8c8a0;
    padding: 3px 12px;
    border-radius: 5px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
  }

  .card h4 {
    font-size: 0.85rem;
    color: #7a7068;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin: 1.2em 0 0.4em;
    padding-bottom: 6px;
    border-bottom: 1px solid #2a2622;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin: 0.5em 0;
  }

  thead th {
    text-align: left;
    font-size: 0.65rem;
    color: #7a7068;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    padding: 6px 14px 10px;
    border-bottom: 1px solid #2a2622;
  }

  tbody td {
    padding: 10px 14px;
    font-size: 0.9rem;
    border-bottom: 1px solid #1f1d1a;
    vertical-align: top;
  }

  tbody tr:last-child td {
    border-bottom: none;
  }

  .amount {
    color: #e8c8a0;
    font-weight: 700;
    white-space: nowrap;
  }

  ol {
    padding-left: 1.4em;
    margin: 0.5em 0;
  }

  ol li {
    margin-bottom: 0.45em;
    font-size: 0.9rem;
    line-height: 1.5;
  }

  ol li strong {
    color: #e8c8a0;
  }

  .highlight {
    color: #b8756d;
    font-weight: 700;
  }

  .note {
    color: #8a8078;
    font-size: 0.8rem;
  }

  .callout {
    background: #22201c;
    border-radius: 10px;
    padding: 14px 20px;
    margin-top: 10px;
    font-size: 0.85rem;
    color: #c9a87c;
    font-weight: 500;
    border-left: 3px solid #b8756d;
  }

  .callout.warn {
    border-left-color: #d4443e;
    color: #e8a8a4;
  }

  .callout.go {
    border-left-color: #6daa6d;
    color: #a8d4a8;
  }

  .temp {
    display: inline-block;
    background: #3a2a22;
    color: #e8c8a0;
    padding: 2px 10px;
    border-radius: 5px;
    font-weight: 700;
    font-size: 0.85rem;
  }

  .divider {
    text-align: center;
    color: #2a2622;
    font-size: 1.5rem;
    margin: 30px 0 10px;
    letter-spacing: 0.5em;
  }

  .timeline-card {
    background: linear-gradient(135deg, #1a1816 0%, #1e1510 100%);
    border: 1px solid #3a2a22;
  }

  footer {
    text-align: center;
    color: #3a3632;
    font-size: 0.65rem;
    margin-top: 50px;
    padding-top: 30px;
    border-top: 1px solid #1a1816;
  }
</style>
</head>
<body>
<!-- CONTENT HERE -->
<footer>Cookery &mdash; {Recipe Name} &mdash; {Date}</footer>
</body>
</html>
```

### Component patterns

Use these HTML patterns to build the guide body:

**Page header:**
```html
<h1>{Recipe Name}</h1>
<p class="subtitle">{Course list or dish summary} &mdash; {Date}</p>
```

**Phase header** (one per phase):
```html
<div class="phase">
  <h2>Phase {N}: {Phase Name}</h2>
  <span class="time-badge">{Timing info}</span>
  <span class="phase-line"></span>
</div>
```

**Grid with cards** (after each phase header):
```html
<div class="grid">
  <!-- 1 card = half width, use class="card full" for full width -->
  <div class="card">...</div>
</div>
```

**Card with mise en place table + instructions:**
```html
<div class="card">
  <h3>{Card Title} <span class="tag">{Optional Tag}</span></h3>
  <h4>Mise en Place</h4>
  <table>
    <thead><tr><th>Item</th><th>Amount</th><th>Prep</th></tr></thead>
    <tbody>
      <tr><td>{ingredient}</td><td class="amount">{weight}</td><td>{prep note}</td></tr>
    </tbody>
  </table>
  <h4>Instructions</h4>
  <ol>
    <li><strong>{Key action}</strong> — {detail with <span class="highlight">critical values</span>}</li>
  </ol>
  <div class="callout">{Technique tip}</div>
</div>
```

**Temperature badge** (inline in instructions):
```html
<span class="temp">200°F</span>
```

**Callout variants:**
```html
<div class="callout">Neutral technique tip</div>
<div class="callout warn">Food safety warning or critical timing</div>
<div class="callout go">Phase complete / ready to move on</div>
```

**Timeline card** (for time-critical steps):
```html
<div class="card timeline-card">...</div>
```

## Phase design rules

1. **Multi-course with timeline:** The execution timeline from the recipe drives phases. Group parallel tasks into the same phase as side-by-side cards. Sequential steps that happen together (e.g., "sear steak while pasta water boils") share a phase. Use `.timeline-card` for time-critical steps.

2. **Single-course with stages:** Break into Prep → Cook → Rest/Cool → Finish. Merge or skip phases if the recipe doesn't warrant them (e.g., no rest phase for a salad).

3. **Basic recipe:** Mise en Place → Cook. Two phases is fine.

**For all recipes:**
- Every ingredient appears in a mise en place table in the phase where it's first used
- Use `.callout.warn` for food safety (temps, cross-contamination, timing windows that cause failure)
- Use `.callout.go` when a phase is complete and the cook can pause or move on
- Use neutral `.callout` for technique tips from food-knowledge.md
- Use `<strong>` for key actions and `<span class="highlight">` for critical measurements
- Use `<span class="temp">` for all temperatures
- Tags on card h3 (like "Do First") help the cook prioritize within a phase
- Use `.card.full` for steps that need wide layout (complex tables, many instructions)
- Use `.card` (half-width) when two tasks happen in parallel or are independent

## Step 4: Write the file

Use the Write tool to save the complete HTML to `guides/{slug}-guide.html`.

Tell the user the file path so they can open it in a browser.
