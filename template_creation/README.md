# Template Creation Pipeline

This folder contains everything you need to create a new style and add it to the `styles/` library.

---

## What is a "style"?

A style is a subfolder inside `styles/` that contains:
- `style.md` — the design system document (colors, fonts, spacing, voice, CSS tokens)
- `style.html` — a reference HTML presentation showing the style in action (optional but recommended)

Once a style exists in `styles/`, you can use it in any presentation by saying:
> "Make slides in the style of **glassmorphism**" or "Use the **stripe** brand style"

---

## How to create a new style

### Option A — Extract from a website (Firecrawl)

The fastest way. Works for any brand or product with a public website.

1. Read `extract-brand.md` — it has the exact Firecrawl API call and conversion steps
2. Run the scrape against the target URL
3. Fill in `_style-template.md` with the extracted data
4. Save as `styles/<slug>/style.md`
5. Optionally generate a sample HTML deck to save as `styles/<slug>/style.html`

### Option B — Manual design system

For custom visual styles (not tied to a real brand):

1. Copy `_style-template.md` to `styles/<slug>/style.md`
2. Fill in every section: atmosphere, colors, typography, spacing, voice, CSS quick-reference
3. Optionally create a demo HTML file as `styles/<slug>/style.html`

---

## Files in this folder

| File | Purpose |
|---|---|
| `extract-brand.md` | Firecrawl recipe for extracting brand DNA from any URL |
| `_style-template.md` | Blank template schema for a new `style.md` |

---

## Naming conventions

- Slugs: lowercase, hyphenated, no spaces → `my-new-style`
- Visual styles: descriptive name → `glassmorphism`, `dark-glow`, `retro-synthwave`
- Brand styles: brand name → `stripe`, `notion`, `ebay`

---

## After creating a style

Tell Claude: "Save this style to `styles/<slug>/`" and it will write both files.
Future presentations can reference it by slug name.
