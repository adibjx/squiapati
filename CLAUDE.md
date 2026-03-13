# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static landing page for **Squiapati Advocacia**, a Brazilian law firm marketing a legal service for ITCMD tax restitution on inherited private pension plans (PGBL/VGBL), based on an STF court ruling.

## Development

No build system or dependencies. Open HTML files directly in a browser, or serve with any static server:

```bash
python -m http.server 8080
# or
npx http-server .
```

## File Structure

- `landing-page-previdencia.html` — Main landing page (all CSS and JS embedded)
- `obrigado.html` — Post-form-submission thank you page
- `assets/Logo (2).png` — Company logo

## Architecture

Both pages are **self-contained HTML files** with all CSS and JavaScript inlined — no external stylesheets or script files.

### landing-page-previdencia.html

Sections (in order): fixed header → hero → disclaimer strip → context (`#entenda`) → eligibility cards → process steps → FAQ → contact form (`#contato`) → footer.

**JavaScript** (bottom of file, ~40 lines):
- `toggleFaq(btn)` — accordion behavior, one item open at a time
- Intersection Observer — adds `.visible` class to `.reveal` elements at 12% threshold
- `handleSubmit(e)` — disables button, waits 800ms, redirects to `obrigado.html`
- Stagger delays on cards (`i * 0.12s`) and steps (`i * 0.1s`)

**Analytics:** Google Tag Manager (ID: `GTM-W3DJ8WQ6`) injected in `<head>` and `<noscript>` fallback.

### Design Tokens (CSS variables)

| Variable | Value | Usage |
|---|---|---|
| `--navy` | `#0A1628` | Primary background |
| `--navy-mid` | `#112240` | Secondary background |
| `--gold` | `#C9A84C` | Accent color |
| `--gold-light` | `#E8C96A` | Hover accents |
| `--cream` | `#F8F4EC` | Light backgrounds |

**Fonts:** `Cormorant Garamond` (headings) + `DM Sans` (body), loaded from Google Fonts.

**Breakpoints:** 900px and 600px.
