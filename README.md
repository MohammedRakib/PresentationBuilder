# Presentation Builder

Generate polished, self-contained HTML5 slide decks for technical and academic presentations — research paper talks, engineering demos, 20-minute project showcases, and business-technical pitches.

**Powered by** Claude Code + `SKILL.md`

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Project Structure](#project-structure)
3. [End-to-End Workflow](#end-to-end-workflow)
   - [Step 1 — Choose a style](#step-1--choose-a-style)
   - [Step 2 — Provide your content](#step-2--provide-your-content)
   - [Step 3 — Add images (optional)](#step-3--add-images-optional)
   - [Step 4 — Invoke the skill](#step-4--invoke-the-skill)
   - [Step 5 — Review and iterate](#step-5--review-and-iterate)
   - [Step 6 — Export to PPTX (optional)](#step-6--export-to-pptx-optional)
4. [Use Cases](#use-cases)
5. [Available Styles](#available-styles)
6. [Extract Any Brand Live (Firecrawl Setup)](#extract-any-brand-live-firecrawl-setup)
7. [Creating a Custom Style](#creating-a-custom-style)
8. [Design Principles](#design-principles)
9. [Cloning & Reuse](#cloning--reuse)

---

## Prerequisites

| Requirement | Purpose |
|---|---|
| [Claude Code](https://claude.ai/code) | Running the skill |
| Python 3.9+ | PPTX export only — skip if not needed |
| Firecrawl API key | Live brand extraction only — [see setup below](#extract-any-brand-live-firecrawl-setup) |

---

## Project Structure

```
presentation_builder/
├── SKILL.md                     # Claude's full instruction set — the brain
├── assets/                      # Drop your images here
├── scripts/                     # Drop your notes, abstracts, write-ups here
├── styles/                      # 44 style templates (32 visual + 12 brand)
│   └── <name>/
│       ├── style.md             # Design tokens: colors, fonts, spacing, voice
│       └── style.html           # Live 4-slide demo — open in browser to preview
├── principles/
│   ├── design-principles.md    # 20 codified design rules with research citations
│   └── images/                  # Illustrated rule reference plates (one per rule)
├── template_creation/
│   ├── README.md                # How to create a new style from any website
│   ├── extract-brand.md         # Firecrawl brand extraction recipe
│   └── _style-template.md       # Blank schema for a new style
├── tools/
│   ├── html_to_pptx.py          # Convert HTML slides → PPTX
│   └── requirements.txt         # Python deps for the converter
└── final_slides/                # All generated presentations saved here
```

---

## End-to-End Workflow

### Step 1 — Choose a style

Open any `styles/<name>/style.html` in your browser to preview it — every style has a live 4-slide demo showing its exact colors, typography, and component patterns.

Pick from three sources:

**A. Visual styles** — general presentation aesthetics, not tied to any real brand.
→ [See the full list below](#visual-styles)

**B. Pre-built brand styles** — design systems modelled on real products.
→ [See the full list below](#brand-styles)

**C. Extract any brand live** — paste any URL and Claude pulls the brand DNA automatically using Firecrawl.
→ [Firecrawl setup required — see below](#extract-any-brand-live-firecrawl-setup)

> **Not sure which to pick?** For academic talks and research, `minimalist-clean`, `swiss-design`, or `apple-keynote` are safe defaults. For engineering projects, `modern-saas-dark`, `cluely`, or `dark-mode-pro` work well.

---

### Step 2 — Provide your content

Tell Claude which input to use:

**Option A — Script or notes file**

Drop a `.txt` or `.md` file into `scripts/` — paper abstract, project description, bullet-point notes, or a full write-up. Claude reads it in full before generating.

```
scripts/
└── my-research-paper.md
```

**Option B — Explore the codebase**

For software projects, Claude can explore your project directory to extract architecture, tech stack, data flow, and key design decisions. This produces more accurate diagrams and component descriptions.

> Claude will ask before doing this since it uses extra tokens.

**Option C — Both**

Codebase exploration for structural accuracy + a script file for narrative framing. Best for engineering showcases.

---

### Step 3 — Add images (optional)

Drop any images into `assets/`. Claude checks this folder automatically and asks which ones to include.

```
assets/
├── architecture-diagram.png
└── results-chart.png
```

Images are referenced in the final HTML as `../assets/<filename>` — keep the folder alongside your generated presentation.

---

### Step 4 — Invoke the skill

Open Claude Code in this directory and describe what you want. Examples:

```
Use the presentation builder skill.
Style: apple-keynote
Content: scripts/my-paper.md
```

```
Use the presentation builder skill.
Style: stripe
Content: explore the codebase — this is an engineering showcase
```

```
Use the presentation builder skill.
Style: minimalist-clean
Content: both — explore the codebase and read scripts/project-notes.txt
```

```
Use the presentation builder skill.
Style: extract from https://mycompany.com
Content: scripts/pitch-notes.md
```

Claude will confirm style, content source, and images — then generate.

---

### Step 5 — Review and iterate

Claude saves the output to `final_slides/<name>-slides.html` and opens it in your browser automatically.

**Keyboard controls in the generated presentation:**

| Key | Action |
|---|---|
| `Space` or `→` | Next animation step, then next slide |
| `←` | Previous slide |

---

#### Editing slides after generation

You can edit the deck slide by slide — no need to regenerate from scratch. Just tell Claude which slide and what to change.

**Reference a slide by number:**
```
Slide 3: change the headline to "Memory-Efficient Attention"
```

**Reference a slide by its role:**
```
The motivation slide: add a second sentence explaining why existing methods fail
```

**Change content or data:**
```
Slide 6: update the accuracy from 87% to 94.2% and relabel the comparison bar
```

**Change layout or visual treatment:**
```
Slide 4: switch from three cards to a two-column comparison — left side old approach, right side ours
```

**Add a new slide:**
```
Add a slide after slide 3 showing the system architecture diagram from assets/arch.png
```

**Remove a slide:**
```
Remove slide 7 — it's redundant with slide 5
```

**Change animations:**
```
Slide 4: reveal each card one at a time instead of showing them all at once
```

**Apply multiple edits in one message:**
```
Slide 1: make the title larger and add more breathing room
Slide 3: the code block is too long — crop to just the forward pass, max 10 lines
Slide 5: replace "87%" with "94.2%" everywhere on this slide
```

> Claude applies only the changes you describe and preserves everything else. After each edit, refresh your browser to see the updated result.

---

### Step 6 — Export to PPTX (optional)

Convert your HTML presentation to PPTX for sharing via email, uploading to Google Slides, or presenting in PowerPoint.

**One-time setup:**

```bash
pip install -r tools/requirements.txt
playwright install chromium
```

**Convert any generated presentation:**

```bash
python3 tools/html_to_pptx.py final_slides/my-slides.html
# → final_slides/my-slides.pptx
```

> The converter opens the HTML in a headless browser, screenshots each slide at 1920×1080, and assembles a 16:9 PPTX. Every font, gradient, and layout is preserved exactly as rendered.

---

## Use Cases

### Research paper talk *(conference, seminar, group talk)*

**Slide structure:** Hook → Problem Formulation → Proposed Method → Experiments → Ablations → Conclusion

| Talk length | Target slides |
|---|---|
| 15 min (conference) | 12–15 |
| 30–45 min (seminar/thesis) | 25–35 |

Recommended styles: `minimalist-clean` · `swiss-design` · `apple-minimal` · `dark-mode-pro`

---

### Engineering demo *(10 min)*

**Slide structure:** Motivation → System Overview → Key Decision → Demo / Results → Next Steps

- **8–12 slides**
- Recommended styles: `modern-saas-dark` · `terminal-code` · `dark-glow`

---

### Engineering showcase *(20 min — comprehensive)*

For faculty reviews, internship/job interviews, hackathon demos, or capstone presentations.

**Slide structure:** Problem → Overview → Tech Stack → Architecture Deep Dive → Key Decisions → Implementation Challenges → Demo / Results → Lessons Learned → Next Steps → Closing

- **20–25 slides** (up to 30 for complex systems)
- Claude will offer to explore your codebase for accurate architecture diagrams
- Recommended styles: `cluely` · `dark-mode-pro` · `modern-saas-dark` · `modern-tech-startup`

---

### Business-technical presentation

Mixed technical/non-technical audience.

**Slide structure:** Problem → Gaps in Existing Solutions → Your Solution → Evidence → Plan → Ask

- **15–20 slides** for a 20-min presentation
- Recommended styles: `apple-keynote-light` · `stripe` · `notion`

---

## Available Styles

### Visual Styles

| Slug | Character |
|---|---|
| `apple-keynote` | Dark Apple keynote — black stage, white type, blue accent |
| `apple-keynote-light` | Light Apple keynote — clean, minimal, confident |
| `apple-minimal` | Ultra-sparse — maximum whitespace, one idea per frame |
| `minimalist-clean` | Swiss-influenced, nothing wasted |
| `swiss-design` | Grid-strict, Helvetica, authoritative |
| `editorial-magazine` | Serif editorial, ink-black contrast, red accent |
| `dark-mode-pro` | Professional dark — slate palette, sky-blue accent |
| `modern-saas-dark` | Zinc-black SaaS aesthetic (Vercel/Linear adjacent) |
| `modern-tech-startup` | Light startup — indigo accent, clean sans-serif |
| `dark-glow` | Dark with subtle radial glows and depth |
| `glassmorphism` | Frosted glass cards over vivid gradient |
| `cluely` | Deep purple + glass morphism |
| `cluely-3d` | Spatial depth + 3D perspective cards |
| `cluely-v2` | Cluely variant with alternate color treatment |
| `terminal-code` | CLI aesthetic — green-on-black monospace |
| `retro-synthwave` | 1980s synthwave grid — purple, pink, cyan |
| `retro-game` | 8-bit pixel art retro game |
| `retro-game-2` | Alternative pixel art, amber palette |
| `cyberpunk-neon` | Dark with neon magenta and cyan |
| `brutalist` | Raw, undecorated, deliberately confrontational |
| `isometric-3d` | Flat isometric depth and geometric shapes |
| `liquid-metal` | Chrome gradients, metallic surfaces |
| `animated-gradients` | Flowing vivid gradient backgrounds |
| `neumorphism` | Soft UI — extruded/indented surfaces |
| `memphis-design` | 1980s bold geometric shapes and primary colors |
| `hand-drawn-sketch` | Organic, chalk-on-paper warmth |
| `simple-colors` | Bold flat colors, no gradients, direct |
| `white-pops-of-color` | White base with selective bold accents |
| `art-deco-luxury` | Black + gold Art Deco, ornate geometry |
| `black-neon-glow` | Pure black + electric neon highlights |
| `blue-background-modal` | Deep blue with layered card UI |
| `modern-modal` | Light layered panels, subtle shadows |

### Brand Styles

| Slug | Character |
|---|---|
| `stripe` | White canvas, navy headings, purple accent, multi-layer shadows |
| `apple` | Black stage, blue CTA pills, SF Pro typography |
| `linear` | Near-black, lavender accent, dense dark panels |
| `notion` | White, purple CTA, pastel-tinted feature cards |
| `vercel` | Pure black/white monochrome, workflow accent badges |
| `figma` | White + black editorial with bold pastel color blocks |
| `cursor` | Warm cream, orange accent, editorial feel |
| `claude` | Warm cream, coral accent, serif display type |
| `spotify` | Near-black, Spotify green accent, pill-shaped everything |
| `airbnb` | White, coral accent, soft rounded cards |
| `nvidia` | Black, NVIDIA green, sharp zero-radius rectangles |
| `ebay` | White, blue primary, 4-color logo identity |

> Open `styles/<slug>/style.html` in your browser to see a live demo of any style before using it.

---

## Extract Any Brand Live (Firecrawl Setup)

Firecrawl is a web scraping API that Claude uses to pull a brand's design DNA — colors, fonts, logo, component styles — from any public URL in one call. You need this only if you want to create a slide deck using a brand that isn't already in `styles/`.

### 1. Create a free Firecrawl account

Go to **[firecrawl.dev](https://firecrawl.dev)** and sign up. The free tier gives you ~500 scrapes/month — more than enough for extracting brand styles.

### 2. Copy your API key

After signing in, go to your dashboard → **API Keys** → copy the key. It starts with `fc-`.

### 3. Add Firecrawl as an MCP to Claude Code

Run this command in your terminal. Replace `fc-YOUR_KEY_HERE` with your actual key:

```bash
claude mcp add --scope user firecrawl \
  -e FIRECRAWL_API_KEY=fc-YOUR_KEY_HERE \
  -- npx -y firecrawl-mcp
```

> **What `--scope user` does:** Adds the MCP to your global Claude Code config (`~/.claude/`), so it's available in every project — not just this one. You only need to run this once.

### 4. Verify it's connected

```bash
claude mcp list
```

You should see `firecrawl` in the list with status `connected`.

### 5. Use it

Now tell Claude:

```
Use the presentation builder skill.
Style: extract from https://stripe.com
Content: scripts/my-notes.md
```

Claude will scrape the URL, extract the brand DNA, save it as `styles/stripe/style.md`, and use it to generate your slides. The extracted style is saved permanently — next time you can just say `Style: stripe`.

> **Good URLs to scrape:** Marketing homepages and landing pages work best. Avoid dashboards or app interiors — those have less brand personality and more functional UI chrome.

---

## Creating a Custom Style

See `template_creation/README.md` for the full pipeline. The Firecrawl route above is the fastest — one URL → one saved style. Alternatively, you can manually fill in `template_creation/_style-template.md` with any colors and fonts you choose.

---

## Design Principles

Every generated presentation is validated against 20 research-backed design rules before any HTML is emitted. Sources include Tufte, Bringhurst, Reynolds, Duarte, WCAG 2.2, Miller's Law, and Gestalt theory.

The full field manual with numeric thresholds is at `principles/design-principles.md`. A few key rules:

- **One idea per slide** — max 10-word headline + one supporting block
- **≥40% whitespace** on content slides; ≥60% on hero/title slides
- **Body ≥24px, title ≥48px** — readable on a projector from row 10
- **8pt spacing grid** — every margin and gap is a multiple of 8px
- **One accent color per slide** — never two; multiple accents = no accent
- **WCAG 7:1 contrast target** — projectors wash out contrast by 30–50%

---

## Cloning & Reuse

`scripts/`, `assets/`, and `final_slides/` are gitignored — they stay local to each user. Clone anywhere, add your content, and generate.

```bash
git clone <repo-url> my-presentations
cd my-presentations

# Add your content
echo "My research abstract..." > scripts/my-paper.md

# Open Claude Code and invoke the skill
claude
```
