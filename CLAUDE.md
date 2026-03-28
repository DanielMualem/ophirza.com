# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static HTML portfolio site for Ophir Zadicareo. No build system — files are ready to deploy as-is. The site was originally exported from Adobe Portfolio and has since been decoupled from that platform.

## Deployment

Deployed via Netlify. To preview locally, serve the root directory with any static server:

```bash
python3 -m http.server 8000
# or
npx serve .
```

## Architecture

### Page Structure
Each page is a standalone `.html` file at the root:
- `index.html` — homepage and portfolio gallery (the root page served by default)
- `about.html`, `contact.html` — standard pages
- `pocket.html`, `amdocs-go-store.html`, `amdocs-outages.html`, `onetwofree.html`, `mapping_app_case_study_v2.html` — project detail pages

Navigation between pages uses plain `<a href="page.html">` links.

### Assets
- `dist/css/main.css` — all styles
- `dist/js/main.js` — all JS (includes jQuery 2.2.4, lightbox, nav, form logic)
- `videos/` — MP4 files tracked with **Git LFS** (`.gitattributes` configures this)
- `mapping-pics/` — local images for the Compass Mapper case study
- Images are served from Adobe's CDN (`cdn.myportfolio.com`) with responsive `srcset`; Compass Mapper uses local images from `mapping-pics/`

### Contact Form
Handled by Formspree (`https://formspree.io/f/xkovlodk`) via a `fetch` POST in `contact.html`. The form uses `e2e-site-contact-form` as an identifier and manages its own submit state (Sending... / Thank you! messages).

### JS Conventions
Interactive elements are selected by class prefixes:
- `.js-hamburger`, `.js-responsive-nav` — mobile nav
- `.js-lightbox` — gallery lightbox
- `.js-back-to-top` — scroll-to-top button
- `.js-lazy` — lazy-loaded images

Avoid touching `dist/js/main.js` directly for behavior changes — it's a compiled bundle. Add page-specific `<script>` blocks in the relevant HTML file instead.
