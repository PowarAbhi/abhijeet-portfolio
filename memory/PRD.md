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
- ✅ **Home Section WebGL Shader** — Replaced HOMEBG.mp4 with Three.js r128 purple liquid glow shader
  - `#shader-container` with `position: absolute; inset: 0; z-index: 0`
  - Desktop: `pointermove` drives `u_mouse` uniform with coords relative to the home section
  - Mobile: `touchstart` + `touchmove` mapped to same uniforms; `touch-action: none` enabled
  - Smooth mouse-follow interpolation (divisor = 1/10) + feedback buffer swap for trail
  - `#home` reduced to `min-height: 80vh`, black background
  - PORTFOLIO + GRAPHIC DESIGN centered in white `#FFFFFF` with subtle text-shadow
- ✅ **About Me refinement**
  - Restructured to 4-column grid: `1fr 320px 1fr 80px` (Card | Jiji | Card | Icons)
  - Zero overlap between Jiji character and software icons (each in dedicated column)
  - Added `#fbb03b` circular backdrop behind Jiji cat via `::before` pseudo element with black border
  - Removed drop-shadow / glow from `.jiji-cat` for clean Doodle look
  - Cropped Jiji SVG viewBox to `720 300 490 520` to fit cleanly inside the circular frame
  - Software icons moved to absolute far-right grid column (`justify-self: end`)
- ✅ **Mobile responsive fixes**
  - Reset grid-column for cards + icons in mobile breakpoint (single-column stack)
  - Tablet breakpoint (768-980px): 2×2 cards + icons in full-width row at bottom, Jiji hidden
  - Jiji fully hidden on mobile (<980px) per user spec
  - Software icons remain visible on mobile, reflow horizontally

### 2026-02 (Earlier in this session)

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
