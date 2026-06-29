# Presentation Builder

Generate polished, self-contained HTML5 slide decks for technical and academic presentations — research paper talks, engineering demos, 20-minute project showcases, and business-technical pitches. Powered by Claude Code + `SKILL.md`.

---

## Prerequisites

- [Claude Code](https://claude.ai/code) installed
- Python 3.9+ (for PPTX export only)

---

## Project Structure

```
presentation_builder/
├── SKILL.md                    # The skill — Claude's full instruction set
├── assets/                     # Drop images here for use in slides
├── scripts/                    # Drop your notes, abstracts, or write-ups here
├── styles/                     # 44 style templates (32 visual + 12 brand)
│   └── <name>/
│       ├── style.md            # Design tokens: colors, fonts, spacing
│       └── style.html          # Live demo of the style (open in browser)
├── principles/
│   ├── design-principles.md   # 20 codified design rules with research citations
│   └── images/                 # Illustrated rule reference plates
├── template_creation/
│   ├── README.md               # How to create a new style from any website
│   ├── extract-brand.md        # Firecrawl brand extraction recipe
│   └── _style-template.md      # Blank schema for a new style
├── tools/
│   ├── html_to_pptx.py         # Convert HTML slides → PPTX
│   └── requirements.txt        # Python deps for the converter
└── final_slides/               # All generated presentations land here
```

---

## End-to-End Workflow

### Step 1 — Browse the styles

Open any `styles/<name>/style.html` in your browser to preview a style before committing. Visual styles have a full 4-slide demo. Brand styles show the design language of real companies (Stripe, Apple, Linear, etc.).

**Visual styles** — presentation aesthetics not tied to a brand:
`apple-keynote` · `apple-keynote-light` · `apple-minimal` · `minimalist-clean` · `swiss-design` · `editorial-magazine` · `dark-mode-pro` · `modern-saas-dark` · `modern-tech-startup` · `dark-glow` · `glassmorphism` · `cluely` · `cluely-3d` · `terminal-code` · `retro-synthwave` · `retro-game` · `retro-game-2` · `cyberpunk-neon` · `brutalist` · `isometric-3d` · `liquid-metal` · `animated-gradients` · `neumorphism` · `memphis-design` · `hand-drawn-sketch` · `simple-colors` · `white-pops-of-color` · `art-deco-luxury` · `black-neon-glow` · `blue-background-modal` · `modern-modal` · `cluely-v2`

**Brand styles** — use the visual identity of a real product:
`stripe` · `apple` · `linear` · `notion` · `vercel` · `figma` · `cursor` · `claude` · `spotify` · `airbnb` · `nvidia` · `ebay`

**Or extract any brand live** — paste a URL and Claude will use Firecrawl to pull the brand DNA and save a new style automatically.

---

### Step 2 — Provide your content

You have three options — tell Claude which to use:

**(a) Script or notes file**
Drop a `.txt` or `.md` file into `scripts/`. This can be a paper abstract, project description, bullet-point notes, or a full write-up. Claude reads it in full before generating.

```
scripts/
└── my-research-paper.md
```

**(b) Codebase exploration**
For software projects, Claude can explore your project directory to extract the architecture, tech stack, data flow, and key design decisions — producing more accurate diagrams. Claude will ask before doing this (it uses extra tokens).

**(c) Both**
Codebase exploration for structure + a script file for narrative context. Best for engineering showcases where you want accurate diagrams AND a written story.

---

### Step 3 — Add images (optional)

Drop any images into `assets/`. Claude will ask which ones to include and reference them in the slides as `../assets/<filename>`.

```
assets/
├── architecture-diagram.png
└── results-chart.png
```

---

### Step 4 — Invoke the skill

Open Claude Code in this project directory and give the instruction. Examples:

```
Use the presentation builder skill.
Style: apple-keynote
Content: scripts/my-paper.md
```

```
Use the presentation builder skill.
Style: stripe brand
Content: explore the codebase to understand the architecture
```

```
Use the presentation builder skill.
Style: minimalist-clean
Content: both — explore the codebase and also read scripts/project-notes.txt
```

Claude will ask three questions (style, content, images) and then generate.

---

### Step 5 — Review in the browser

Claude saves the output to `final_slides/<name>-slides.html` and opens it automatically.

**Keyboard controls:**

| Key | Action |
|---|---|
| `Space` or `→` | Next animation step, then advance to next slide |
| `←` | Previous slide |

Review the deck, then tell Claude what to change. Iterate in plain conversation — no need to restart.

---

### Step 6 — Export to PPTX (optional)

Once you're happy with the HTML version, convert it to PPTX for sharing or uploading to Google Slides / PowerPoint.

**One-time setup:**
```bash
pip install -r tools/requirements.txt
playwright install chromium
```

**Convert:**
```bash
python3 tools/html_to_pptx.py final_slides/my-slides.html
# Output: final_slides/my-slides.pptx
```

The converter opens the HTML in a headless browser, screenshots each slide at 1920×1080, and assembles a 16:9 PPTX. Every font, gradient, and layout detail is preserved exactly as rendered.

---

## Use Cases

### Research paper talk *(conference, seminar, group talk)*

Point Claude at your abstract + contributions. Structure:
**Hook → Problem Formulation → Proposed Method → Experiments → Ablations → Conclusion**

- 12–15 slides for 15-min talk; 25–35 slides for 30–45 min seminar
- Recommended styles: `minimalist-clean`, `swiss-design`, `apple-minimal`, `dark-mode-pro`

---

### Engineering demo *(10 min)*

Describe your system and outcomes. Structure:
**Motivation → System Overview → Key Decision → Demo / Results → Next Steps**

- 8–12 slides
- Recommended styles: `modern-saas-dark`, `terminal-code`, `dark-glow`

---

### Engineering showcase *(20 min — comprehensive)*

For faculty reviews, internship interviews, hackathon demos, or capstone presentations. Structure:
**Problem → Overview → Tech Stack → Architecture Deep Dive → Key Decisions → Implementation Challenges → Demo / Results → Lessons Learned → Next Steps → Closing**

- 20–25 slides; up to 30 for complex systems
- Claude will ask whether to explore the codebase for accurate architecture diagrams
- Recommended styles: `cluely`, `dark-mode-pro`, `modern-saas-dark`, `modern-tech-startup`

---

### Business-technical presentation

Mixed technical/non-technical audience. Structure:
**Problem → Gaps in Existing Solutions → Your Solution → Evidence → Plan → Ask**

- 15–20 slides for a 20-min presentation
- Recommended styles: `apple-keynote-light`, `stripe`, `notion`

---

## Creating a Custom Style

See `template_creation/README.md` for the full pipeline. Quick version:

1. Paste a URL — Claude uses Firecrawl to extract brand DNA (colors, fonts, components)
2. Saves the result as `styles/<slug>/style.md`
3. Optionally generates a `style.html` demo
4. Reference the new style by its slug in future presentations

---

## Design Principles

Every generated presentation is validated against 20 research-backed rules from Tufte, Bringhurst, Reynolds, Duarte, WCAG, Miller's Law, and Gestalt theory. The full field manual with numeric thresholds is at `principles/design-principles.md`.

Key rules applied to every slide:
- One idea per slide (max 10-word headline + one supporting block)
- ≥40% whitespace on content slides, ≥60% on hero slides
- Body ≥24px, title ≥48px — readable on projector at distance
- 8pt spacing grid — all margins and gaps are multiples of 8
- 60-30-10 color split — one accent color per slide, never two
- WCAG 7:1 contrast target for projector resilience

---

## Cloning & Reuse

`scripts/`, `assets/`, and `final_slides/` are gitignored — they stay local to each user. Clone the repo into any project directory, add your content to `scripts/`, and generate.

```bash
git clone <repo-url> presentation_builder
cd presentation_builder
# Add scripts/my-notes.md
# Open Claude Code and invoke the skill
```
