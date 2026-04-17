# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static single-page website for **Guido Administración**, a property management company (administradora de consorcios) in Buenos Aires (CABA). The entire site is a single file: `index.html`.

## Development

No build step or local server required. Open `index.html` directly in a browser, or use any static file server:

```bash
npx serve .
# or
python -m http.server 8080
```

The only npm dependency (`jimp`) is for image processing scripts, not the website itself.

## Architecture

Everything lives in `index.html` (~2461 lines):

1. **CSS** (lines ~13–1487): All styles inline in `<style>`. Uses CSS custom properties for theming. Two themes: `light` (default) and `dark`, toggled via `data-theme` attribute on `<html>`.

2. **HTML sections** (lines ~1489–2163):
   - `#nav` — Fixed navbar with logo, links, theme toggle, hamburger menu
   - `#hero` — Full-screen image carousel (5 slides, auto-advance every 5.5s)
   - Stats strip — Animated counters triggered by IntersectionObserver
   - `#quienes` — About section
   - `#servicios` — Services cards grid
   - `#resenas` — Client reviews carousel (auto-advance every 4.5s)
   - `#mapa` — Leaflet.js map with 10 building markers across CABA
   - `#contacto` — Contact form (simulated submit, no backend)
   - Footer + floating WhatsApp button

3. **JavaScript** (lines ~2174–2459): All inline. Key systems:
   - Theme toggle (persisted in `localStorage`)
   - Hero carousel with touch swipe support
   - Reviews carousel with touch swipe and resize handling
   - Leaflet map initialized on `window.load`
   - Scroll reveal via IntersectionObserver
   - Stats counter animation via IntersectionObserver

## External Dependencies (CDN)

- **Fonts**: Google Fonts — Cormorant Garamond, DM Sans, Playfair Display
- **Map**: Leaflet 1.9.4 (CSS + JS from unpkg)

## Design Tokens

Primary colors defined as CSS variables:
- `--navy: #1C2D4F` — primary brand color
- `--gold: #B8962E` — accent color
- `--cream: #FAFAF7` — light background

## Images

All images are in `/images/`: `logo.png`, `logo.jfif`, `brand1.jfif`, `brand2.jfif`, `slide1–5.jpg` (hero carousel).

## Key Notes

- The contact form (`submitForm()`) is a UI-only simulation — it has no backend. To add real form submission, replace the `submitForm()` function with a fetch/POST call.
- The WhatsApp link (line 2166) uses a placeholder phone number (`5491100000000`) that must be updated with the real number.
- Building addresses/coordinates in the map (lines 2384–2395) are placeholder data.
- Dark mode applies a CSS `filter: invert(1) hue-rotate(180deg)` workaround on Leaflet map tiles to adapt the map for dark theme.
