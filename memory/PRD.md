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

### 2026-02-21 (Patch 6 — filter clip fix)
- ✅ **Works filter "ALL" button clipping fixed:**
  - Removed the `@media (min-width: 981px) { justify-content: center }` override that caused overflow clipping when chips exceeded container width
  - `.filters` now uses `padding: 10px 20px` (horizontal 20px breathing room so black borders never clip; vertical 10px so top/bottom borders aren't trimmed)
  - Added `scroll-padding-left: 20px` + `scroll-padding-right: 20px` so when users swipe back the ALL chip snaps with a consistent left margin
  - Chips already had `flex-shrink: 0` so they don't squash
  - Verified: the "ALL" chip's left edge sits exactly 20px from the filter container's left edge (no clipping on any viewport size)

### 2026-02-21 (Patch 5)
- ✅ **Expanding cards simplified:** Removed all `.info` divs (main + sub text) from the 4 cards; each card now displays only its FontAwesome icon inside the white circle. Icons (user, graduation-cap, briefcase, palette) remain on both active and collapsed states so the card identity stays clear.
- ✅ **Mobile software-icon row fix:** `.about-icons` → `display: flex; flex-wrap: nowrap; justify-content: center; gap: 6px`; `.software-icon` → `45×45` with `flex-shrink: 0`. All 6 icons (Ps, Ae, Pr, Ai, Blender, CorelDRAW) fit on one line at 390px (evenly spaced 51px apart).
- ✅ **Works Zomato-style filter slider:** `.filters` → `flex-wrap: nowrap; overflow-x: auto; scrollbar-width: none` with `::-webkit-scrollbar { display:none }`. Chips have `flex-shrink: 0; border-radius: 999px; white-space: nowrap; scroll-snap-align: start`. Desktop centers chips when they fit; mobile scrolls horizontally with hidden scrollbar and smooth scroll-snap.

### 2026-02-20 (Patch 4)
- ✅ **Home mobile height:** reduced to `min-height: 35vh; height: 35vh;` (was 60vh) — prevents excessive scrolling above fold.
- ✅ **Expanding card asset mapping:** mapped each card to its dedicated asset:
  - About Me → `assets/uploads/ABOUTME-CARD.png`
  - Education → `assets/uploads/EDUCATION-CARD.png`
  - Experience → `assets/uploads/EXPERIENCE-CARD.png`
  - Skills → `assets/uploads/SKILLS-CARD.png`
- ✅ **Background-pattern fix:** `.about .option` now uses `background-size: cover; background-repeat: no-repeat; background-position: center center;` and split into `background-image` + `background-color` so images never tile or stack when a card is collapsed.
- ✅ **Icon alignment fix:**
  - Collapsed cards: `.label` uses `top: 50%; left: 50%; transform: translate(-50%, -50%)` so the circular icon is perfectly centered on both axes (verified at 61/232 desktop and 179/30 mobile).
  - `.info` is now `display: none` on inactive cards (was `opacity: 0`), so it no longer steals flex space and pushes the icon off-center.
  - Active cards: `.label` stays at bottom-left (`bottom: 24px; left: 24px`) with icon + info side by side (flex-row, align-items: flex-end).
  - Added subtle box-shadow on `.icon` for better visibility over image backgrounds.

### 2026-02-19 (Patch 3)
- ✅ **Home mobile refinement:**
  - WebGL shader disabled on `window.innerWidth < 980` (JS early-return + CSS `display:none` on `#shader-container`)
  - Mobile `#home` → solid black `#000000`, `min-height: 60vh`
- ✅ **Cursor chatbox mobile-only migration:**
  - Removed `#mouse-keychain` DOM + all cursor-follow JS (Math.atan2 eye-tracking + 1:1 follow)
  - `#chat-bubble` DOM removed on desktop (JS `.remove()` if desktop); retained on mobile as fixed bottom-right toast
  - IntersectionObserver still drives section-based randomized messages from 4 `.txt` files
  - Cycle: 2s delay → show 5s → hide 3s → next random
- ✅ **About Me — Expanding Flex Cards refactor:**
  - Removed: Jiji cat SVG, eye-tracking logic, 2×2 grid, circular backdrop
  - 4 cards: About Me (profile.jpg), Education (Illustration3.jpg), Experience (Magzine Design2.jpg), Skills (photoshop5.jpg)
  - FontAwesome 6.5.1 CDN added for `.fas` icons on card labels
  - CSS: `flex-grow: 1` inactive, `flex-grow: 10000` + `max-width: 820px` active, smooth `cubic-bezier(0.05, 0.61, 0.41, 0.95)` transitions
  - Labels: 44px white circular icon + main title + sub description; info fades in only on active card
  - Vanilla JS click handler toggles `.active` class between cards (jQuery-free)
  - Software icons remain pinned to far-right flex edge — zero overlap with cards at any screen size
  - Mobile: cards stack vertically; inactive collapse to 60px min-height; active expands to 280px min-height
  - Tablet (768-980px): preserves horizontal expanding-row behavior

### 2026-02-18 (Patch 2)
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
