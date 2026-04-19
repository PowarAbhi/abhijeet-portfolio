# Abhijeet Powar – Portfolio (Static HTML/CSS/JS)

## Problem Statement
Full-stack UI refactor of `index.html` and `styles.css` into a Bento Grid system using CSS Grid and Flexbox. Implements a "Doodle/Brutalist" design language with custom Frame borders (corner nodes), infinite marquee loops, Pinterest-style Masonry gallery, contextual chat bubbles, and an interactive Jiji-cat SVG with eye-tracking.

## Tech Stack
- Vanilla HTML / CSS / JavaScript
- CSS Grid + Flexbox (no frameworks)
- SVG manipulation (Jiji cat), `Math.atan2` for eye-tracking
- IntersectionObserver for section-aware chat bubbles
- No backend / No DB (static portfolio deployed from GitHub)

## File Architecture
```
/app/
├── index.html               # Markup + inline JS (cursor, chat, eye-tracking)
├── styles.css               # Desktop brutalist styles & bento grid
├── mobile-styles.css        # Responsive breakpoints (<980px + <480px + 768-980px tablet)
├── assets/
│   └── uploads/
│       ├── HOMEBG.mp4       # Full-background Home video (user-hosted)
│       ├── CATLOOP.mp4      # Cat loop video (user-hosted)
│       ├── *.svg            # Icons (EMAIL, LOCATION, INSTA, Adobe apps)
│       ├── INTROMESSAGE.txt
│       ├── ABOUTMEMESSAGE.txt
│       ├── WORKSMESSAGE.txt
│       └── LETSCONNECTMESSAGE.txt
```

## Implemented Features
- **Doodle/Brutalist design** with node-cornered frame borders
- **Infinite gapless marquee** loops (CSS keyframe)
- **Contextual chat bubble** fetches from 4 local `.txt` files via IntersectionObserver
- **Fixed-offset 1:1 cursor follow** (velocity-based elastic physics removed per user)
- **Interactive Jiji-cat SVG** with `Math.atan2` eye-tracking
- **Sticky navigation** with active-section highlighting
- **Pinterest-style Masonry** gallery with category filter chips
- **Home Section:** Full-background `HOMEBG.mp4` video with overlapping "PORTFOLIO" + "GRAPHIC DESIGN" text
- **Top marquee relocated** directly below nav (above Home section)
- **About Me:** 2×2 Bento Grid (About / Education / Experience / Skills) with large centered Jiji cat and right-aligned software icons

## Mobile Responsive Rules (< 980px)
- 2×2 About grid stacks to single column
- Jiji cat hidden (`display: none`)
- Software icons remain visible but reflow horizontally (flex-wrap)
- Home section uses full-bg video at 100vh
- Masonry gallery switches to 1 column (< 768px) or 2 columns (768-980px tablet)
- Frame midpoint nodes hidden below 480px for cleaner look

## Completed Changelog

### 2026-02 (Current Session)
- ✅ Swapped Home video: `.home-video` (CATLOOP.mp4) → `.home-bg-video` (HOMEBG.mp4, full-bg)
- ✅ Wrapped Home title + subtitle in `.home-content` overlay on top of video
- ✅ Relocated PORTFOLIO marquee from below Home to directly below nav
- ✅ Implemented 2×2 Bento Grid for About section with centered Jiji cat
- ✅ Updated `mobile-styles.css`:
  - About container stacks to 1 column on mobile
  - Jiji cat `display: none` on mobile and tablet (<980px)
  - Software icons reflow horizontally (kept visible per user request)
  - Home section kept at full viewport with cover background video
  - Tablet breakpoint (768-980px) preserves 2×2 cards but hides Jiji
- ✅ Verified via Playwright screenshots at desktop (1920px) and mobile (390px) viewports

### Previous Sessions
- ✅ Brutalist node-border frames
- ✅ Infinite marquee loops (gap-less)
- ✅ Contextual chat bubble (4 text file data source)
- ✅ 1:1 cursor-follow refactor (elastic physics removed)
- ✅ Jiji Cat SVG with `Math.atan2` eye-tracking
- ✅ Masonry gallery + filter chips
- ✅ Sticky navigation

## Backlog / Potential Enhancements
- Add subtle dark-overlay/gradient on `.home-bg-video` for improved text readability (only if HOMEBG.mp4 has bright frames)
- Add lazy-loading + `srcset` for Masonry images (performance)
- Add `prefers-reduced-motion` media query to disable marquee animation for a11y
- Optional: add a micro-interaction to the software icon column on hover
