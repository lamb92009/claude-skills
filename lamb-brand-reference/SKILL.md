---
name: lamb-brand-reference
description: Use when creating emails, marketing materials, or designs for Lamb Screen Printing. Invoke for brand colors, typography, logos, social links, contact info, and EngineMailer email technical requirements.
---

# Lamb Screen Printing — Brand & Email Reference

## Company

| Field | Value |
|-------|-------|
| Company | Lamb Screen Printing |
| Website | https://lambca.com |
| Email | hello@lambca.com |
| Phone | (760) 754-5540 |
| Address | 804 N. Twin Oaks Valley Rd #122, San Marcos, CA 92069 |
| Business | Custom screen printing & promotional products |
| Heritage | Family-owned, 30+ years |
| Customers | ~1,600 contacts (EngineMailer) |

## Brand Tone

Warm, casual, quality-focused, family-oriented. "Our customers are like family." Emphasize quality over cheap. Avoid corporate/stiff language.

## Colors

| Role | Hex |
|------|-----|
| Primary (headers/text) | `#0F264D` Deep Navy |
| Secondary (links/accents) | `#2063B0` Medium Blue |
| Accent Orange | `#EC6425` |
| Accent Magenta | `#E91E8C` |
| Accent Gold | `#F1C40F` |
| Accent Green | `#1A7A3C` |
| Light background | `#F0F0F0` Soft Gray |
| Body background | `#FFFFFF` White |
| Muted text | `#666666` |
| Secondary muted | `#999999` |

## Typography

| Use | Font | Weight |
|-----|------|--------|
| Headlines | Exo | 900, uppercase |
| Body | Montserrat | 500-800 |
| Fallbacks | `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif` | |

## Design Patterns

- **CTA buttons:** Pill-shaped, 30px border-radius, orange `#EC6425` bg, white Exo uppercase text
- **Cards:** White bg, 8px border-radius, `box-shadow: 0 2px 8px rgba(0,0,0,0.08)`
- **Section dividers:** 3px accent line, orange `#EC6425`

## Social Links

| Platform | URL |
|----------|-----|
| Facebook | https://www.facebook.com/lambscreenprinting |
| Instagram | https://www.instagram.com/lambscreenprint/ |
| X (Twitter) | https://x.com/lambscreen |
| LinkedIn | https://www.linkedin.com/company/lambca/ |

## Hosted Assets

Base URL: `https://lambca.com/lspimages/enginemailer/`

| Asset | Path |
|-------|------|
| Header logo (full horizontal) | `logos/lamb-logo-main@4x.png` |
| Footer logo (light/white) | `logos/logo-light.png` |
| Square logo | `logos/lsp-square-logo.png` |

Social icon SVGs (white, single-color): `~/Documents/lamb-promo-email/icons/` — facebook.svg, instagram.svg, x-twitter.svg, linkedin.svg

## EngineMailer Technical Requirements

- **Layout:** Table-based (no flexbox/grid) — Outlook uses Word renderer
- **CSS:** All styles inlined — EngineMailer strips `<style>` blocks (keep `<style>` for mobile `@media` queries as progressive enhancement)
- **Images:** JPG for photos (80-85%, ~1000px), PNG for logos. **No WebP** (Outlook doesn't support it)
- **No CSS positioning** — Gmail strips `position:absolute/relative`
- **Max width:** 600px container, mobile breakpoint 480px (single-column stack)
- **Min font:** 14px body, 22px+ headings
- **Outlook buttons:** Use VML `<v:roundrect>` inside `<!--[if mso]>` for pill-shaped buttons
- **Unsubscribe:** `http://[globalunsubscribe]/`
- **CTA strategy:** `mailto:hello@lambca.com?subject=Promo%20Product%20Inquiry` — reply-to-email, not web links
- **Best send times:** Tuesday-Thursday, 10-11am PST
- **Footer text:** "You're receiving this because you're part of the Lamb family."

## Previous Emails

| Email | Date | Location |
|-------|------|----------|
| "Did You Know?" promo | Feb 2026 | `~/Documents/lamb-promo-email/` |
