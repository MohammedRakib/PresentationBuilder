---
brand: eBay
slug: ebay
website: https://www.ebay.com
extracted_via: Firecrawl
---

# eBay — Brand Style

## Visual Theme & Atmosphere
eBay is bright, open, and high-energy — a light-mode marketplace that feels like a digital bazaar. The design is clean white with bold pops of the four signature brand colors (red, blue, yellow, green). The overall mood is democratic and accessible: modern without being cold, lively without being cluttered.

## Colors
| Role | Hex | Notes |
|---|---|---|
| Background | `#FFFFFF` | Clean white — the dominant canvas |
| Red (e) | `#F02D2D` | eBay's "e" — used for urgency, sale, primary actions |
| Blue (B) | `#0968F6` | eBay's "B" — primary CTAs, links, interactive elements |
| Yellow (a) | `#FFBD14` | eBay's "a" — alerts, highlights, secondary accents |
| Green (y) | `#4CE160` | eBay's "y" — confirmations, deals, secondary buttons |
| Text Primary | `#191919` | Near-black for headings |
| Text Muted | `#666666` | Body copy, supporting text |
| Border | `#E0E0E0` | Subtle dividers, card borders |

**Color scheme:** light  
**Accent rule:** One accent per slide. eBay's multi-color identity is in the *logo* only — slide content uses a single accent (blue `#0968F6` is the safest default). Never scatter all four brand colors across slide content.

## Typography
- **Display:** Market Sans — eBay's proprietary typeface. Fallback: **Inter** (Google Fonts) or **DM Sans** (Fontshare)
- **Body:** Market Sans → Arial → Helvetica Neue → sans-serif

| Role | Size |
|---|---|
| H1 | 28 px |
| H2 | 36 px |
| Body | 20 px |
| Caption | 14 px |

**Weight:** Regular (400) for body; Semibold (600) for headings; Bold (700) for display callouts.

## Spacing & Shape
- Base grid: 4 px (multiples of 4)
- Slide-safe 8 pt grid: use 8, 16, 24, 32, 48, 64, 96 px
- Border radius (cards/containers): 16 px
- Border radius (pill buttons): 44 px
- Shadows: none — flat, clean surfaces throughout
- Framework hint: custom design system

## Logo
Inline SVG — four-color wordmark (e=red, B=blue, a=yellow, y=green):

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="117" height="48" viewBox="0 0 122 48.592" aria-label="eBay">
  <path fill="#F02D2D" d="M24.355 22.759c-.269-5.738-4.412-7.838-8.826-7.813-4.756.026-8.544 2.459-9.183 7.915zM6.234 26.93c.364 5.553 4.208 8.814 9.476 8.785 3.648-.021 6.885-1.524 7.952-4.763l6.306-.035c-1.187 6.568-8.151 8.834-14.145 8.866C4.911 39.844.043 33.865-.002 25.759c-.05-8.927 4.917-14.822 15.765-14.884 8.628-.048 14.978 4.433 15.033 14.291l.01 1.625z"/>
  <path fill="#0968F6" d="M46.544 35.429c5.688-.032 9.543-4.148 9.508-10.32s-3.947-10.246-9.622-10.214-9.543 4.148-9.509 10.32 3.974 10.245 9.623 10.214zM30.652.029l6.116-.034.085 15.369c2.978-3.588 7.1-4.65 11.167-4.674 6.817-.037 14.412 4.518 14.468 14.454.045 8.29-5.941 14.407-14.422 14.454-4.463.026-8.624-1.545-11.218-4.681a33.237 33.237 0 01-.19 3.731l-5.994.034c.09-1.915.185-4.364.174-6.322z"/>
  <path fill="#FFBD14" d="M77.282 25.724c-5.548.216-8.985 1.229-8.965 4.883.013 2.365 1.94 4.919 6.7 4.891 6.415-.035 9.826-3.556 9.794-9.289v-.637c-2.252.02-5.039.054-7.529.152zm13.683 7.506c.01 1.778.071 3.538.232 5.1l-5.688.032a33.381 33.381 0 01-.225-3.825c-3.052 3.8-6.708 4.909-11.783 4.938-7.532.042-11.585-3.915-11.611-8.518-.037-6.665 5.434-9.049 14.954-9.318 2.6-.072 5.529-.1 7.945-.116v-.637c-.026-4.463-2.9-6.285-7.854-6.257-3.68.021-6.368 1.561-6.653 4.2l-6.434.035c.645-6.566 7.53-8.269 13.595-8.3 7.263-.04 13.406 2.508 13.448 10.192z"/>
  <path fill="#92C821" d="M91.939 19.852l-4.5-8.362 7.154-.04 10.589 20.922 10.328-21.02 6.486-.048-18.707 37.251-6.85.039 5.382-10.348-9.887-18.393"/>
</svg>
```

**Logo placement (slides):** Bottom-left, ~24 px tall, inside 5% safe-zone. The SVG is self-colored — render it as-is on white or very light backgrounds. On dark/colored fills, use a white flat version or the wordmark in white text.

## Voice & Personality
- Tone: energetic, direct, democratic, human
- Energy: high
- Audience: general consumers — buyers and sellers across all demographics, comfortable with online transactions
- Brand promise: the world's marketplace — everything from everyday deals to rare collectibles

## Voice samples (real copy from the brand)
- "Buy & sell electronics, cars, clothes, collectibles & more on eBay, the world's online marketplace."
- "Top brands, low prices & free shipping on many items."
- "Tune in and shop curated experiences."
- "Shop the best deals on what you love."

## Quick Reference (for Claude)
```css
:root {
  --bg:          #FFFFFF;
  --fg:          #191919;
  --muted:       #666666;
  --accent:      #0968F6;   /* blue — primary CTA */
  --red:         #F02D2D;   /* urgency / sale */
  --yellow:      #FFBD14;   /* highlight */
  --green:       #4CE160;   /* confirm / deal */
  --radius-card: 16px;
  --radius-pill: 44px;
  --font:        "Market Sans", "Inter", Arial, sans-serif;
}
```

---

## Reference
**Website:** [https://www.ebay.com](https://www.ebay.com)  
**Favicon:** https://www.ebay.com/favicon.ico  
**OG Image:** https://ir.ebaystatic.com/cr/v/c1/ebay-logo-1-1200x630-margin.png
