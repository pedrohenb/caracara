# Handoff: Caracara studio site (caracara.games)

## Overview
A small static site for Caracara, an independent game studio. It has two pages:
1. **Studio page** (`/`): hero with the logo, a games list, about, contact, and a footer with social links.
2. **Hex & Hearth game page** (`/games/hex-and-hearth/`): a hero with the Wishlist button and capsule, plus a trailer. It uses the game's own parchment art style.

Hosting target: **GitHub Pages**. Plain HTML + CSS, no framework, no build step. The only JS is a small inline theme toggle.

## About the design files
The files in `site/` are HTML design references, and they are also written as deployable static code. The target stack is plain static HTML/CSS, so Claude Code can **use `site/` as the starting implementation**: tidy it, fill in the placeholders, and deploy it. If the site later moves to a framework or static generator (Astro, Eleventy, etc.), recreate these pages there and keep every value listed below.

## Fidelity
**High-fidelity.** The colours, type, spacing, shapes and copy are final. The only exceptions are the placeholders marked `SWAP:`.

---

## Page 1: Studio (`site/index.html`, `site/styles.css`)

### Art direction
Everything comes from the logo: cream paper, black ink and caracará orange, with angular cut shapes and crest-like jagged edges. It follows the spirit of Northeastern Brazilian woodcut (xilogravura) and cordel prints. There are no gradients and no rounded corners. Shadows are hard offset "print" shadows.

### Layout (top to bottom)
Content width: `min(1160px, 100% - 2.5rem)`, centred.

1. **Plate (header + hero)**. It stays **cream `#FDE8C8` with ink `#15110D` in both themes**, like the printed logo.
   - Header: 1rem vertical padding, flex with space-between.
     - Left: a home link with the 42px mark image and the text "caracara" (Big Shoulders Display 800, 24px, lowercase).
     - Right: the nav links "games", "about" and "contact" (Big Shoulders 700, 20px, lowercase, gap 1.4rem; "about" is hidden below 800px), then the theme toggle (a 44×44 icon button with sun and moon icons).
   - Hero: a 2-column grid `1fr / 1.1fr`, gap `1rem 2rem`, top padding `clamp(1.5rem, 5vw, 3.5rem)`.
     - Left: an `h1` holding the wordmark image (max 440px wide), vertically centred, bottom padding `clamp(3rem, 8vw, 6rem)`. There's no tagline.
     - Right: the bird mark, max 620px, aligned to the bottom-right so the neck strokes run into the section edge below. It has `margin-bottom: -4px`.
   - Below 800px: a single column, with the bird centred at `min(460px, 92%)`.

2. **Games band** (`#games`). Background **`#000`** in both themes, text cream.
   - Jagged top edge (see Shapes). Section padding `clamp(3rem, 7vw, 5rem)`.
   - Section title: "games" (see Section title).
   - The game list is a `<ul>` with one `<li class="game-item">` per game: a 2-column grid `1.15fr / 1fr`, gap `clamp(1.5rem, 4vw, 3rem)`, stacked below 800px.
     - Capsule: a 616×353 image (aspect ratio kept) with a 3px cream border and a `10px 10px 0 #EB7932` hard shadow. It links to the game page.
     - Eyebrow: "Our first game" (Big Shoulders 700, 16.8px, letter-spacing .16em, uppercase, `#D9C6A5`).
     - Title `h3`: "Hex & Hearth" (Big Shoulders 800, `clamp(2rem, 4.5vw, 3rem)`, line-height .95, margin-bottom 1.5rem). There's no description paragraph.
     - Actions (flex, gap `1rem 1.25rem`, wrapping):
       - Primary stamp button "Wishlist on Steam".
       - Text link "Game page →" (Big Shoulders 800, 21.6px, 3px orange underline).

3. **About** (`#about`). Page background.
   - A grid `1fr / 1.4fr`, gap `1.5rem 3rem`, stacked below 800px.
   - Left: the title "about", followed by three feather streaks.
   - Right: one paragraph at `clamp(1.15rem, 2vw, 1.3rem)`, max 58ch: "Independent game studio. We make small, handcrafted games with care."

4. **Contact band** (`#contact`). Background **orange `#EB7932`**, text ink `#15110D`, jagged top edge.
   - Title "contact", with an ink-coloured shard.
   - One item:
     - Label "Email" (Big Shoulders 700, 17.6px, .16em tracking, uppercase).
     - Link `hello@caracara.games` (Big Shoulders 800, `clamp(1.6rem, 4vw, 2.4rem)`, with an ink underline).
   - The press kit block is commented out in the source, so it can be restored later.

5. **Footer**. Background `#000`, text cream, jagged top edge, padding `2.25rem 0 2.5rem`.
   - Flex with space-between, wrapping.
   - Left: "© {year} Caracara" (16px). The year is set by JS.
   - Right: social icons: Bluesky, Discord, YouTube, X and Steam, from Simple Icons, inlined as SVG with `fill: currentColor`.
     - Each is a 46×46 square with a 2px cream border and a 20px icon.
     - Hover and focus: orange background, ink icon, orange border.
     - Each has a visually hidden label (`.sr-only`, inside the positioned `<a>`).

### Shapes and components
- **Jagged edge** (`.jag::before`): a 28px strip above the section, using the section's own background (`background: inherit`), masked with this repeating 240×28 SVG path:
  `M0 28V14L22 4l8 12L58 0l6 18 32-12 8 14L140 2l6 14 30-8 10 14 30-18 10 14 14-4v14z`
  It sits at `bottom: calc(100% - 1px)` to avoid a seam.
- **Shard** (`.shard`): a 0.55em square in orange, clipped to `polygon(0 22%, 74% 0, 100% 62%, 28% 100%)`, echoing the orange patch on the bird's face. It's placed before each section title.
- **Section title**: flex with gap .9rem; Big Shoulders 800, `clamp(2.25rem, 6vw, 3.5rem)`, line-height .9, lowercase; margin-bottom `clamp(2rem, 5vw, 3rem)`.
- **Feather streaks** (after "about"): three bars 8px tall, 42, 30 and 18px wide, gap 6px, `skewX(-28deg)`, colour `#4B453D` at 80% opacity. They echo the trails behind the wordmark.
- **Stamp button** (`.btn`):
  - Size and type: minimum height 50px, padding `.6rem 1.3rem`, Big Shoulders 800 at 21.6px.
  - Colours: ink text on orange, 3px ink border, `5px 5px 0` cream hard shadow, no radius.
  - Hover: `translate(-2px, -2px)` and a 7px shadow.
  - Active: `translate(3px, 3px)` and a 2px shadow.
  - Transition: 120ms ease.

### Theme
The site follows `prefers-color-scheme`. A `data-theme="light|dark"` attribute on `<html>` overrides it. The choice is stored in `localStorage` under `caracara-theme`, and a small inline script in `<head>` applies it before first paint to avoid a flash.

| Token | Light | Dark |
|---|---|---|
| `--bg` page | `#FDE8C8` | `#000` |
| `--fg` text | `#15110D` | `#FDE8C8` |
| `--muted` | `#4B453D` | `#D9C6A5` |
| `--band` games | `#000` | `#000` |
| `--band-fg` | `#FDE8C8` | `#FDE8C8` |
| `--band-muted` | `#D9C6A5` | `#D9C6A5` |
| `--foot` footer | `#000` | `#000` |

The hero plate and the orange contact band look the same in both themes.

---

## Page 2: Hex & Hearth (`site/games/hex-and-hearth/index.html`, `game.css`)

This page uses the game's UI style, not the studio's.

- **Colours:**
  - Light: parchment `#F7EEDC`, ink `#4A3724`, gold `#B8911F` / `#DEA03A`, leaf green `#6E9F43` with a `#4C7430` lip.
  - Dark: leather `#2E251A`, ink `#EFE6D2`, gold rims.
- **Fonts:** Grenze 600/700 (display) and Vollkorn 400/600/italic (body).
- **Header:** a hex-framed mark plus "Caracara", linking back to `../../`; a "Trailer" nav link; the theme toggle (it shares the same localStorage key).
- **Hero:** a 2-column grid `1fr / 1.15fr`.
  - Left:
    - Eyebrow "Cozy hex tile-placer".
    - `h1` "Hex & Hearth" in Grenze 700 at `clamp(3.25rem, 9vw, 6rem)`.
    - Lede: "A cozy, no-fail hex tile-placer where you lay tiles and a village grows on them."
    - Green chamfered "Wishlist on Steam" button: 10px chamfer, 3px darker lip, cream text at 22px bold.
  - Right: the capsule inside a gilt chamfered-octagon panel.
  - Background: a subtle hex-outline pattern with a radial fade.
- **Trailer section:** a 16:9 slot with a 2px rim border. Code for a YouTube embed, a `<video>` or a GIF is commented in the source.
- **Footer:** © plus a "A game by Caracara" link home.
- **Chamfered-octagon panel:** two stacked pseudo-elements with a clip-path octagon (18px chamfer). The outer layer is the rim colour and the inner one is the panel fill, inset 2–3px.

---

## Interactions
- Anchor nav with `scroll-behavior: smooth` (disabled under `prefers-reduced-motion`, as are all transitions).
- Theme toggle: `aria-pressed` reflects the dark state.
- Skip link "Skip to content", visible on focus.
- Focus ring: a 3px orange outline with 3px offset (gold on the game page).
- No other JS, state or data fetching.

## Accessibility and performance
- Semantic landmarks, one `h1` per page, `aria-labelledby` on sections, decorative images with `alt=""`.
- Contrast:
  - Orange is never used as text on cream. Buttons and the contact band use ink on orange (about 7.9:1).
  - Cream on black is about 17:1.
  - The game page's green button uses large bold cream text, which meets the 3:1 large-text ratio.
- Images are served with `srcset` at 1×/2×/3×. The hero image has `fetchpriority="high"`; everything else is `loading="lazy"`.
- Google Fonts are loaded with `preconnect` and `display=swap`. Self-hosting them is optional.

## Assets (`site/assets/img/`)
| File | Use |
|---|---|
| `caracara-mark(.png, -2x, -3x)` | Bird mark, transparent background (684×521 at 1×) |
| `caracara-wordmark(.png, -2x, -3x)` | "cara" wordmark with feather trails, transparent background (325×90 at 1×) |
| `og-image.png` | Social share image (currently the square lockup; 1200×630 recommended) |
| `hex-and-hearth-capsule.svg` | **Placeholder**: replace with the 616×353 Steam main capsule |
| `hex-and-hearth-trailer-poster.svg` | **Placeholder**: replace with the trailer, video or GIF |

Social icons come from Simple Icons (CC0) and are inlined in the HTML.

## Placeholders to fill (search `SWAP:`)
- Steam `APPID` (used on both pages)
- Capsule image, trailer
- Email address
- Social URLs (delete any you don't use)
- Game share image (`og:image` on the game page)

## Deploy
- Push the contents of `site/` to the repo root, or to `/docs`, and enable GitHub Pages.
- `CNAME` already contains `caracara.games`. Point DNS at GitHub Pages as described in GitHub's docs.
- To add a game: copy `games/hex-and-hearth/`, then duplicate the `<li class="game-item">` on the studio page.

## Files
- `site/index.html`: studio page
- `site/styles.css`: studio styles and tokens
- `site/games/hex-and-hearth/index.html`: game page
- `site/games/hex-and-hearth/game.css`: game styles
- `site/assets/`: images and icons
- `site/CNAME`, `site/README.md`
