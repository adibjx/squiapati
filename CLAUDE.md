# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static landing page for **Squiapati Romano Chagas & Afonso Neto Advocacia**, a Brazilian law firm marketing a legal service for ITCMD tax restitution on inherited private pension plans (PGBL/VGBL), based on a unanimous STF ruling (Tema 1.214, RE 1363013, December 2024).

**Live domain:** `https://squiapatiromanochagas.com.br`

**WhatsApp contact:** +55 34 997391342 → `https://wa.me/5534997391342`

**Instagram:** `@tributario.sa` → `https://instagram.com/tributario.sa`

## Development

No build system or dependencies. Open HTML files directly in a browser, or serve with any static server:

```bash
python -m http.server 8080
# or
npx http-server .
```

## File Structure

- `index.html` — Main landing page (all CSS and JS embedded). Renamed from `landing-page-previdencia.html`.
- `obrigado.html` — Post-form-submission thank you page. Has WhatsApp CTA and Instagram follow link.
- `email-confirmacao.html` — HTML email template sent to leads after form submission. Table-based layout for email client compatibility.
- `assets/Logo (3).png` — Company logo (white, transparent background). Used in all pages and email.
- `assets/Logo (2).png` — Alternative logo asset (unused).
- `assets/os 3.jpg` — Team photo (Manoel Squiapati, Bruno Chagas, Victor Romano). Used in "Quem Somos" section.
- `assets/os 3 sem fundo.png` — Team photo with transparent background.
- `assets/favicon.svg` — SVG favicon: italic "S" in gold (#C9A84C) on navy (#0A1628) background.

## Architecture

All pages are **self-contained HTML files** with all CSS and JavaScript inlined — no external stylesheets or script files.

### index.html (main landing page)

Sections (in order): fixed header → hero → disclaimer strip → context (`#entenda`) → eligibility cards → process steps → FAQ → contact form (`#contato`) → "Quem Somos" → footer.

**JavaScript** (bottom of file, ~50 lines):
- `toggleFaq(btn)` — accordion behavior, one item open at a time
- Intersection Observer — adds `.visible` class to `.reveal` elements at 12% threshold
- `handleSubmit(e)` — POSTs form data to Google Sheets via Apps Script, redirects to `obrigado.html`
- Stagger delays on cards (`i * 0.12s`) and steps (`i * 0.1s`)

**Form fields:** `nome`, `whatsapp`, `email`, `periodo`, `valor_plano`

**Google Sheets endpoint:** `https://script.google.com/macros/s/AKfycbxnNVsVYeSNhMW40ewX-gZReZVGACth0CdP3gkF2MjdvB-pA9hLx4Rx_w938Yco4RZnjA/exec`

**Analytics:** Google Tag Manager (ID: `GTM-W3DJ8WQ6`) injected in `<head>` and `<noscript>` fallback.

### email-confirmacao.html

Table-based HTML email (600px max-width) compatible with major email clients (Gmail, Outlook, Apple Mail).

Sections: header (logo) → hero (confirmation) → STF ruling detail → what it means for the lead → 4-step process + fee transparency note → WhatsApp CTA → "Quem Somos" with lawyers → footer + OAB disclaimer.

**Important:** images in the email use absolute URLs (`https://squiapatiromanochagas.com.br/assets/...`) — required for email clients.

Personalization variables (replace with platform tokens when configuring dispatch):
- Lead name: add before hero title (e.g. `{{contact.firstname}}` in Brevo, `*|FNAME|*` in Mailchimp)

### Design Tokens (CSS variables)

| Variable | Value | Usage |
|---|---|---|
| `--navy` | `#0A1628` | Primary background |
| `--navy-mid` | `#112240` | Secondary background |
| `--gold` | `#C9A84C` | Accent color |
| `--gold-light` | `#E8C96A` | Hover/highlight accents |
| `--gold-pale` | `#F5E6B8` | Light gold tint |
| `--cream` | `#F8F4EC` | Light backgrounds |
| `--text-muted` | `#8A9BB5` | Muted text |

**Fonts:** `Cormorant Garamond` (headings, serif, italic for accents) + `DM Sans` (body), loaded from Google Fonts.

**Breakpoints:** 900px and 600px.

## SEO & Meta

- `index.html`: `robots: index, follow` + canonical `https://squiapatiromanochagas.com.br/` + full OG + Twitter Card
- `obrigado.html`: `robots: noindex, nofollow` (conversion page, should not be indexed)
- `og:image` uses absolute URL: `https://squiapatiromanochagas.com.br/assets/Logo%20(3).png`

## Lawyers

- Manoel Squiapati — Sócio Fundador
- Bruno Chagas — Sócio
- Victor Romano — Sócio

## Fees (as displayed on site)

- Initial analysis: free
- Process opening: 1 salário mínimo
- Success fee: 20% of recovered amount
