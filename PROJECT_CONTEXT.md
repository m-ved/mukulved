# Project Context & Development Log

**Project:** Mukul Ved — Data & ML Engineer Portfolio
**Stack:** Pure HTML, CSS (Vanilla), and JavaScript.
**Design System:** Neo-brutalist (high contrast, thick borders, sharp shadows, monospaced typography).

## 1. Core Architecture
- **Single Page Application:** The entire portfolio lives in `index.html` and is styled by `style.css`.
- **Dark/Light Mode:** Managed via a JavaScript toggle that sets `data-theme="dark"` on the `<html>` tag. A pre-paint script inside the `<head>` prevents theme-flashing on load by checking `localStorage`.
- **Accessibility:** Respects OS-level accessibility settings via `window.matchMedia('(prefers-reduced-motion: reduce)')`. Heavy animations are skipped if this is true.

## 2. Interactive Features Implemented
- **Interactive Network Background:**
  - A `<canvas id="network-bg">` element sits at `z-index: 0`.
  - Particles drift and connect with lines when close. The particles dynamically avoid the user's mouse cursor.
  - Theme-aware: Renders blue lines/black nodes in light mode, and lilac lines/mint nodes in dark mode.
  - Performance: Scales down from 60 to 30 particles on mobile screens (width < 768px).
- **Hacker Text Scramble (`.scramble-on-scroll`):**
  - Section eyebrow tags (`about_me`, `projects`, etc.) decode themselves character-by-character when scrolled into view using an `IntersectionObserver`.
- **Magnetic Buttons (`.magnetic`):**
  - Interactive elements (like the 'View my work' button and the moon/sun toggle) track the mouse and pull slightly toward the cursor on hover. 
  - Automatically disabled on mobile devices where hover is not supported.
- **3D Tilt Cards (`.tilt-card`):**
  - Project and experience cards tilt dynamically in 3D space based on mouse cursor position.
- **Infinite Marquee (`.marquee-wrap`):**
  - A ticker-tape banner that smoothly scrolls infinitely. Uses `flex-shrink: 0` to prevent mobile WebKit browsers from aggressively crushing the text layout.
- **Scroll Progress Bar (`.scroll-progress`):**
  - Attached to the bottom of the sticky `<header>` (using `position: fixed; top: 70px;`). This prevents the bar from being hidden under mobile browser address bars/status notches.

## 3. Notable CSS & Quirks Resolved
- **Mobile Stacking Contexts:** Mobile browsers can sometimes hide `z-index: -1` elements behind the `<body>` background color. To fix this, the network canvas runs at `z-index: 0`, while all foreground content sections (`.hero`, `.section`, `.manifesto`, etc.) are explicitly elevated using `position: relative; z-index: 1;`.
- **Dark Mode Contrast in Cards:** The Neo-Brutalist cards (`.card`) are designed to remain stark white in both Light and Dark modes. A bug caused dark-mode text variables (like light gray text) to bleed into the white cards, rendering text invisible. This was fixed by explicitly locking text CSS variables (like `--text-body`, `--text-exp`) to dark hexadecimal values inside the `.card` scope.
- **Hardware Acceleration:** Heavy animations (like the marquee and hero text) use `will-change: transform` and `transform: translateZ(0)` to force mobile browsers to hand rendering over to the GPU, guaranteeing 60fps scrolling.

## 4. Current State
The website is fully responsive, highly interactive, performant on mobile, and seamlessly handles light/dark mode transitions without sacrificing the stark neo-brutalist aesthetic.
