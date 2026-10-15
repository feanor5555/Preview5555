# FiveM Harbour — Kiez

> Category: Themed & Unique
> Design-system variant C of the `fivem-harbour-ui` series: game UI for a FiveM roleplay server in the spirit of an upscale harbour red-light district — a members' bar, an old harbour-side varieté. Aubergine-black panels, champagne type, brass detailing and one sparing rose-red neon. No sleaze, no explicit imagery. Built to stay readable over the game world.

## 1. Visual Theme & Atmosphere

Kiez is the harbour after midnight seen from inside a good club: dark, warm, quiet, and exact. Surfaces are near-black with a plum undertone, text is champagne instead of white, every frame is finished with a thin brass rule, and a single rose-red neon point marks "this is lit" — the way one sign glows over a doorway on the Reeperbahn. The series colours echo underneath: signal yellow becomes `warning`, harbour blue becomes `info`, harbour grey becomes `job-civil`.

- **Who it is for:** players on a German-speaking roleplay server who live in the HUD for hours and open menus mid-scene. The UI must never compete with the game; it must be readable in the brightest noon harbour and the darkest neon alley.
- **Minimal and clean:** one panel style, one button family, one list row, one table. Decoration is limited to the brass top rule, the double brass rule (`rule2`) on totals and hero titles, and one neon dot.
- **Upscale, not explicit:** the red-light reference lives only in the neon accent and the varieté typography. No silhouettes of bodies, no lips, no hearts beyond the health icon, no pink gradients, no "XXX" ornament.
- **Copy language:** all in-game copy is German, written as a calm host speaks: short, polite, concrete ("Du hast nur € 1.250 Bargeld.", not "FEHLER: UNGÜLTIGER BETRAG").

## 2. Color

Every colour is a `--fh-*` custom property (section 9). Contrast is WCAG 2.x relative luminance, measured against the background the token actually sits on: text, accent, status and job tokens against `bg-surface`; background tokens with `text-primary` on them; `text-on-accent` on `accent-primary`; HUD tokens against `bg-overlay` composited over a pure white game frame (worst case) and over black.

| Token | Hex | Usage | Contrast |
| --- | --- | --- | --- |
| `bg-base` | `#0B090C` | Full-screen backdrop, scrims, input wells, ring centres. | 16.90:1 vs text-primary on it |
| `bg-surface` | `#151116` | Default panel / window body. | 15.92:1 vs text-primary on it |
| `bg-elevated` | `#201A21` | Raised rows, cards inside panels, hover fills, tooltips. | 14.53:1 vs text-primary on it |
| `bg-overlay` | `#0B090CDB` | rgba(11,9,12,.86): every HUD plate over the game world. | 11.95:1 (over white) / 17.03:1 (over black) vs text-primary on it, worst case over white world |
| `border` | `#76634C` | Control outlines (inputs, secondary buttons, table heads). | 3.26:1 vs bg-surface |
| `text-primary` | `#F4ECDD` | Champagne: titles, values, body copy. | 15.92:1 vs bg-surface |
| `text-secondary` | `#CDBFA9` | Supporting copy, secondary values, inactive icons. | 10.34:1 vs bg-surface |
| `text-muted` | `#A69886` | Labels, eyebrows, timestamps, placeholders. | 6.64:1 vs bg-surface |
| `text-on-accent` | `#1A1307` | Text/icons on brass, success, warning, danger fills. | 9.24:1 vs accent-primary |
| `accent-primary` | `#D6B36E` | Brass: primary action, focus ring, selection, key caps. | 9.37:1 vs bg-surface |
| `accent-secondary` | `#FF4F6E` | Rose neon: one lit mark per screen, never meaning-bearing. | 5.87:1 vs bg-surface |
| `success` | `#5FCB95` | Confirmed, paid, healthy, on duty, seatbelt on. | 9.31:1 vs bg-surface |
| `warning` | `#F2BC4B` | Low resource, pending, needs attention (series yellow). | 10.74:1 vs bg-surface |
| `danger` | `#FF6B57` | Error, destructive action, critical vital, seatbelt off. | 6.67:1 vs bg-surface |
| `info` | `#72AEE6` | Neutral system message, links, help (series blue). | 7.93:1 vs bg-surface |
| `job-police` | `#6C9BF2` | Police identity mark (chip, MDT header stripe). | 6.77:1 vs bg-surface |
| `job-ems` | `#4FD1BE` | EMS identity mark (chip, tablet header stripe). | 9.96:1 vs bg-surface |
| `job-mechanic` | `#F0A04B` | Mechanic identity mark. | 8.75:1 vs bg-surface |
| `job-civil` | `#B3ABBE` | Civilian / unemployed identity mark (series grey). | 8.44:1 vs bg-surface |
| `hud-health` | `#F36B7A` | Health bar. | 4.81:1 (over white) / 6.85:1 (over black) vs bg-overlay over white |
| `hud-armor` | `#86A9E8` | Armor bar. | 5.92:1 (over white) / 8.43:1 (over black) vs bg-overlay over white |
| `hud-hunger` | `#DDA56C` | Hunger ring. | 6.46:1 (over white) / 9.21:1 (over black) vs bg-overlay over white |
| `hud-thirst` | `#5CC8E0` | Thirst ring. | 7.21:1 (over white) / 10.27:1 (over black) vs bg-overlay over white |
| `hud-stamina` | `#AEDB76` | Stamina ring (shown only while draining). | 8.82:1 (over white) / 12.56:1 (over black) vs bg-overlay over white |
| `hud-stress` | `#B993F2` | Stress ring (shown above 10 %). | 5.69:1 (over white) / 8.11:1 (over black) vs bg-overlay over white |
| `hud-voice` | `#73DBA6` | Mic + range bars while speaking. | 8.29:1 (over white) / 11.81:1 (over black) vs bg-overlay over white |
| `hud-radio` | `#FF9F5A` | Radio channel while transmitting. | 6.92:1 (over white) / 9.86:1 (over black) vs bg-overlay over white |
| `hud-fuel` | `#E9D290` | Fuel bar and icon. | 9.41:1 (over white) / 13.41:1 (over black) vs bg-overlay over white |

Core palette in one line: `#0B090C` base · `#151116` surface · `#F4ECDD` champagne text · `#D6B36E` brass · `#FF4F6E` rose neon · `#76634C` brass-dark border · `#F2BC4B` signal yellow · `#72AEE6` harbour blue.

Rules:

- **Brass (`accent-primary`) is the interaction colour.** Primary button fill, focus ring, selected row bar, key caps, progress fill, active tab underline. It is the only filled-button colour besides `danger` for destructive confirmation.
- **Neon (`accent-secondary`) is used once per screen at most** and never carries meaning: the lit dot before a screen title, the selected character, the loading-screen eyebrow. It is never text below 19 px, never a button, never a status. A screen with no title dot has no neon at all; the HUD has none.
- **`danger` versus neon:** `danger` (`#FF6B57`) leans vermilion, neon (`#FF4F6E`) leans rose. Because they are related hues, `danger` always comes with an icon (alert, x-circle) and a word; neon never does.
- **Status colours are text/line colours on dark**, not fills. Filled status (`danger` confirm button, unread badge) uses `text-on-accent` on top (6.57:1 on `danger`, 9.18:1 on `success`).
- **Job colours** are identity marks only: a 0.8 rem dot, a chip outline, a 0.3 rem stripe on a tablet header. Never a panel background, never a button.
- **HUD colours** only ever appear on a `bg-overlay` plate or inside a solid ring (section 6). With that rule the lowest HUD contrast in the system is 4.81:1 (`hud-health` over a white game frame).
- **Decorative hairline:** dividers inside panels use `border` at 42 % alpha (`rgba(118, 99, 76, 0.42)`), a component-internal value, not a token. Control outlines (inputs, secondary buttons) use solid `border` (3.26:1 on `bg-surface`). On `bg-elevated` the solid border drops to 2.97:1, so inputs never sit on `bg-elevated`; their well is `bg-base`.
- **Mapping to the Open Design shared tokens** (`tokens.css`): `--bg`=`bg-base`, `--surface`=`bg-surface`, `--surface-warm`=`bg-elevated`, `--fg`=`text-primary`, `--fg-2`=`text-secondary`, `--muted`=`text-muted`, `--accent`/`--meta`=`accent-primary`, `--accent-on`=`text-on-accent`, `--border`=`border`, `--border-soft`=`#3A3029` (the bar track colour), `--success`/`--warn`/`--danger` = the status tokens.

## 3. Typography

Three self-hosted families, all SIL Open Font License 1.1, shipped as Latin-subset WOFF2 in `fonts/` (covers German umlauts, ß, €, typographic quotes and dashes). FiveM NUI runs offline in CEF, so nothing is fetched at runtime; the resource lists the files under `files {}` in `fxmanifest.lua` and loads them with `@font-face` and `font-display: block` (a short invisible flash is preferred over a fallback-font reflow inside the HUD).

| Role | Family | File | Weights |
| --- | --- | --- | --- |
| Display (`--fh-font-display`) | Marcellus | `fonts/Marcellus-Regular-latin.woff2` | 400 |
| UI and body (`--fh-font-sans`) | Jost (variable) | `fonts/Jost-Variable-latin.woff2` | 300–700 |
| Numbers (`--fh-font-mono`) | IBM Plex Mono | `fonts/IBMPlexMono-Regular-latin.woff2`, `fonts/IBMPlexMono-Medium-latin.woff2` | 400, 500 |

```css
@font-face { font-family: "Jost"; src: url("fonts/Jost-Variable-latin.woff2") format("woff2"); font-weight: 300 700; font-display: block; }
@font-face { font-family: "Marcellus"; src: url("fonts/Marcellus-Regular-latin.woff2") format("woff2"); font-weight: 400; font-display: block; }
@font-face { font-family: "IBM Plex Mono"; src: url("fonts/IBMPlexMono-Regular-latin.woff2") format("woff2"); font-weight: 400; font-display: block; }
@font-face { font-family: "IBM Plex Mono"; src: url("fonts/IBMPlexMono-Medium-latin.woff2") format("woff2"); font-weight: 500; font-display: block; }
```

Licences: `fonts/OFL-jost.txt`, `fonts/OFL-marcellus.txt`, `fonts/OFL-ibmplexmono.txt` travel with the files.

Size scale (1 rem = 10 px at 1080p, see section 4):

| Token | rem | px @1080 | px @720 | px @1440 | Use |
| --- | --- | --- | --- | --- | --- |
| `--fh-text-2xs` | 1.2 | 12 | 9.6 | 16 | Eyebrows and labels only, uppercase, tracking 0.14–0.18 em, weight 500 |
| `--fh-text-xs` | 1.3 | 13 | 10.4 | 17.3 | Helper text, timestamps, table sub-lines |
| `--fh-text-sm` | 1.4 | 14 | 11.2 | 18.7 | Secondary copy, button labels (uppercase, 0.1 em) |
| `--fh-text-md` | 1.6 | 16 | 12.8 | 21.3 | Body, list rows, inputs |
| `--fh-text-lg` | 1.9 | 19 | 15.2 | 25.3 | Emphasised values (money), lead copy |
| `--fh-text-xl` | 2.4 | 24 | 19.2 | 32 | Panel titles (display) |
| `--fh-text-2xl` | 3.2 | 32 | 25.6 | 42.7 | Screen titles, totals, ammo count |
| `--fh-text-3xl` | 4.4 | 44 | 35.2 | 58.7 | Speedometer digits, death title, company balance |
| `--fh-text-4xl` | 6.4 | 64 | 51.2 | 85.3 | Bank balance, death timer, loading wordmark base |

Weights: `--fh-weight-regular` 400 (body, display), `--fh-weight-medium` 500 (labels, buttons, numbers), `--fh-weight-semibold` 600 (rare emphasis inside running text), `--fh-weight-bold` 700 (not used in Kiez components; defined for series parity).

Rules: display type is always uppercase Marcellus with 0.08 em tracking and never below `text-lg`. Every number that can change (money, speed, ammo, timers, IDs, plates, percentages) is IBM Plex Mono with `font-variant-numeric: tabular-nums`, so values do not jitter. Line height 1.45 for body, 1.1 for display. German number format: `€ 1.250`, `64 %`, `1,2 km`.

## 4. Spacing, Layout & Scaling

**Scaling rule (shared by all series variants):**

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }
```

1 rem = 10 px at 1080p and every length in the system is in rem, so the whole UI scales with the screen height: 1920×1080 is the reference, 2560×1440 renders at 13.3 px/rem (×1.33), and 1280×720 hits the 8 px floor (×0.8 instead of ×0.67) so text stays readable on small screens. Because 720p therefore gets a relatively larger UI, layouts anchor to screen edges and centre; nothing is positioned by a fixed horizontal offset that assumes 1920 px of width, and full-screen panels keep at least 4 rem of side margin. Hairlines use `max(1px, 0.1rem)` so they never fall below one device pixel.

Spacing scale (`--fh-space-*`): `0_5` 0.2 · `1` 0.4 · `2` 0.8 · `3` 1.2 · `4` 1.6 · `5` 2 · `6` 2.4 · `8` 3.2 · `10` 4 · `12` 4.8 · `16` 6.4 rem.

- Panel padding: header `5 6 4`, body `5 6`, footer `4 6`.
- List row: `3 4` (dense lists in tablets `3 6`). Row height ≥ 4.8 rem for click targets.
- Gaps between related controls `2–3`, between groups `5–6`, between panels `8+`.
- **HUD safe area:** 3 rem from every screen edge. GTA's own minimap occupies the bottom-left; the Kiez frame wraps it at `left 3rem, bottom 5.4rem, 28.6 × 18.4 rem`.

**HUD layout at 1920×1080 (screen anchors):**

| Zone | Anchor | Content |
| --- | --- | --- |
| Bottom-left | left 3, bottom 2.4 | Minimap frame, street plate above it, health + armor bars below it |
| Bottom-left, right of map | left 33.4 | Voice/radio plate (bottom 8.8), status rings (bottom 2.4) |
| Top-right | right 3, top 3 | Cash, bank, job tag (right-aligned stack) |
| Right, below money | right 3, top 17 | Notification stack, max 4, newest on top |
| Bottom-centre | bottom 13 | Progress bar |
| Bottom-right | right 3, bottom 3 | Ammo |
| Bottom-right, left of ammo | right 24, bottom 3 | Vehicle HUD (only in a vehicle) |
| World-anchored | next to the target | Interaction hint `[E] …` |
| Top-left | left 3, top 3 | Chat |

**Full screens** (inventory, bank, shop, tablets …) sit on a scrim (`rgba(6,5,7,0.72)`, heavy `0.86`) and are either one centred panel with 6–14 rem margins or a left panel that leaves the character visible (creator, clothing, character select).

## 5. Shape: Radii, Borders, Shadows, Glow, Materials

| Token | Value | Use |
| --- | --- | --- |
| `--fh-radius-xs` | 0.2 rem | Chips, key-cap corners, tags, skeleton bars |
| `--fh-radius-sm` | 0.3 rem | Buttons, inputs, HUD plates, toasts, slots |
| `--fh-radius-md` | 0.6 rem | Panels, cards, minimap frame |
| `--fh-radius-lg` | 1.2 rem | ID card, large media |
| `--fh-radius-xl` | 2 rem | Tablet screen, phone screen inner corners |
| `--fh-radius-pill` | 999 rem | Interaction hint, phone input, voice bars |
| `--fh-border-width` | max(1px, 0.1 rem) | All outlines and dividers |
| `--fh-border-width-strong` | max(2px, 0.2 rem) | Selected-row bar, active tab, key-cap bottom edge, toast side rule |

Kiez is crisp: small radii, no pill buttons. The circle appears only where the game logic is circular (rings, radial menu, speed arc, avatars).

Shadows and glow:

- `--fh-shadow-1` `0 0.2rem 0.8rem rgba(0,0,0,.45)` — HUD plates; lifts them off a bright world.
- `--fh-shadow-2` `0 1.2rem 3.2rem rgba(0,0,0,.55)` + brass 14 % ring — popovers, tooltips, context menu.
- `--fh-shadow-3` `0 2.4rem 6.4rem rgba(0,0,0,.65)` + brass 22 % ring — panels, dialogs, devices.
- `--fh-glow-accent` rose neon double glow — only on the one neon dot per screen.
- `--fh-focus-ring` `0 0 0 .2rem #0B090C, 0 0 0 .4rem #D6B36E` — every focusable control.

Materials (translucent dark): `--fh-material-thin` .72 (character-select slot backgrounds, loading plates), `--fh-material-regular` .86 (= `bg-overlay`, every HUD plate), `--fh-material-thick` .94 (tooltips over busy scenes, stage labels). Blur tokens `--fh-blur-thin/regular/thick` = 0.4 / 0.8 / 1.6 rem exist for series parity; Kiez uses **no `backdrop-filter` in the HUD** (it re-renders every frame in CEF and costs FPS) and at most `--fh-blur-regular` behind a full-screen scrim, where the game is paused visually anyway.

Signature details: the **brass top rule** (a 1 px gradient line fading out at both ends) on every panel; the **double rule** (`rule2`: brass line, 0.3 rem gap, hairline) above totals and under hero titles; **key caps** as brass-outlined boxes with a 2 px bottom edge.

## 6. Motion

| Token | Value | Use |
| --- | --- | --- |
| `--fh-duration-fast` | 120 ms | Hover, pressed, value tween (bars, money), tab underline |
| `--fh-duration-enter` | 200 ms | Panel, dialog, toast, hint appears |
| `--fh-duration-exit` | 140 ms | Close, dismiss, hint disappears |
| `--fh-duration-slow` | 320 ms | Screen change, loading-screen hand-over, death-screen fade-in |
| `--fh-ease-standard` | cubic-bezier(0.23, 1, 0.32, 1) | Everything except the two spring cases |
| `--fh-ease-spring` | cubic-bezier(0.34, 1.36, 0.64, 1) | Radial menu opening; hold-to-confirm completing |

- **Enter:** opacity 0 → 1 plus `translateY(0.8rem)` → 0 (panels), `translateX(2rem)` → 0 (toasts), `scale(0.96)` → 1 (dialogs, radial menu). Never from `scale(0)`; never `ease-in`.
- **Exit:** opacity → 0 in 140 ms, no movement beyond 0.4 rem.
- **HUD values** tween width/angle in 120 ms; a jump of more than 30 % (damage) tweens in 200 ms and the plate flashes `danger` at 20 % alpha once.
- **Pulses** (critical vitals ≤ 10, seatbelt off at speed, hold-to-revive): 1 Hz opacity 1 → 0.55, linear. Indicators blink 1.5 Hz. No other looping animation exists.
- **Loading progress** is linear; the tip carousel crossfades every 8 s.
- `prefers-reduced-motion: reduce` (and a server-side "Bewegung reduzieren" setting) disables translation, scale, pulses and blinking; state changes become instant colour changes. Blinking indicators then stay solid while active.

## 7. Iconography

- 24 × 24 grid, 1.75 px stroke (1.5 inside inventory slots, 1.25 at ≥ 4.8 rem), round caps and joins, no fills except the active spawn pin, `currentColor` only.
- Sizes: 1.6 rem (inline, buttons), 2 rem (rows, HUD), 2.4 rem (navigation, app tiles), 3.2–4.8 rem (slots, product cards).
- Source: draw in the Lucide idiom (ISC licence) and ship as one inline SVG sprite (`<symbol id="…">`) inside the NUI page — no icon font, no CDN. The preview contains the full Kiez sprite (heart, shield, food, drop, bolt, pulse, mic, mic-off, radio, fuel, belt, engine, left, right, light, wallet, bank, ammo, pin, user, users, car, shirt, wrench, hammer, doc, id, phone, call, chat, gear, search, x, check, alert, info, ok-circle, error-circle, lock, clock, plus, minus, cross, star, brief, cart, key, hand, box, eye, ban, snow, teleport, refresh, map, home, music, vol, cam, rotate, flag, send, trash, grip, badge, stethoscope).
- Colour follows meaning: HUD icons take their HUD token, status icons their status token, navigation icons `text-secondary` → brass when selected. An icon never stands alone for a destructive action; it carries a word.

## 8. Accessibility & Readability over the Game World

- **Plate rule:** anything drawn directly over the game world sits on a `bg-overlay` plate (or is a solid ring). Verified worst cases: `text-primary` 11.95:1, `text-muted` 4.98:1, every HUD colour ≥ 4.81:1 over a pure white frame. The preview's stage 01 puts the HUD over a white quay with sun glare and stage 02 over neon bokeh to prove it.
- No text below `text-2xs` (12 px at 1080p, 9.6 px at 720p); `text-2xs` is used only for uppercase labels, never sentences.
- Colour is never the only signal: critical vitals add a number and a pulse; seatbelt off adds blinking and a sound; errors add an icon and a sentence; job chips add the job name.
- Every interactive element has a keyboard path (listed per component) and a visible `--fh-focus-ring`. NUI focus (`SetNuiFocus`) is taken only by full screens, dialogs, radial and context menus and chat input; the HUD never takes focus. `Esc` always closes the topmost layer and releases focus.
- Key hints show the bound key from the keybinding (`RegisterKeyMapping`), not a hard-coded letter.
- Motion is reducible (section 6). Screen-shake from stress is the game's, not the UI's.

## 9. CSS Custom Properties

The shared `--fh-*` names are identical across all series variants, so a screen built for one variant renders with another by swapping this block. Kiez values:

```css
:root {
  --fh-bg-base: #0B090C;
  --fh-bg-surface: #151116;
  --fh-bg-elevated: #201A21;
  --fh-bg-overlay: rgba(11, 9, 12, 0.86);
  --fh-border: #76634C;
  --fh-text-primary: #F4ECDD;
  --fh-text-secondary: #CDBFA9;
  --fh-text-muted: #A69886;
  --fh-text-on-accent: #1A1307;
  --fh-accent-primary: #D6B36E;
  --fh-accent-secondary: #FF4F6E;
  --fh-success: #5FCB95;
  --fh-warning: #F2BC4B;
  --fh-danger: #FF6B57;
  --fh-info: #72AEE6;
  --fh-job-police: #6C9BF2;
  --fh-job-ems: #4FD1BE;
  --fh-job-mechanic: #F0A04B;
  --fh-job-civil: #B3ABBE;
  --fh-hud-health: #F36B7A;
  --fh-hud-armor: #86A9E8;
  --fh-hud-hunger: #DDA56C;
  --fh-hud-thirst: #5CC8E0;
  --fh-hud-stamina: #AEDB76;
  --fh-hud-stress: #B993F2;
  --fh-hud-voice: #73DBA6;
  --fh-hud-radio: #FF9F5A;
  --fh-hud-fuel: #E9D290;

  --fh-font-sans: "Jost", "Segoe UI", system-ui, sans-serif;
  --fh-font-display: "Marcellus", "Jost", Georgia, serif;
  --fh-font-mono: "IBM Plex Mono", ui-monospace, Consolas, monospace;
  --fh-text-2xs: 1.2rem;
  --fh-text-xs: 1.3rem;
  --fh-text-sm: 1.4rem;
  --fh-text-md: 1.6rem;
  --fh-text-lg: 1.9rem;
  --fh-text-xl: 2.4rem;
  --fh-text-2xl: 3.2rem;
  --fh-text-3xl: 4.4rem;
  --fh-text-4xl: 6.4rem;
  --fh-weight-regular: 400;
  --fh-weight-medium: 500;
  --fh-weight-semibold: 600;
  --fh-weight-bold: 700;

  --fh-space-0_5: 0.2rem;
  --fh-space-1: 0.4rem;
  --fh-space-2: 0.8rem;
  --fh-space-3: 1.2rem;
  --fh-space-4: 1.6rem;
  --fh-space-5: 2rem;
  --fh-space-6: 2.4rem;
  --fh-space-8: 3.2rem;
  --fh-space-10: 4rem;
  --fh-space-12: 4.8rem;
  --fh-space-16: 6.4rem;

  --fh-radius-xs: 0.2rem;
  --fh-radius-sm: 0.3rem;
  --fh-radius-md: 0.6rem;
  --fh-radius-lg: 1.2rem;
  --fh-radius-xl: 2rem;
  --fh-radius-pill: 999rem;
  --fh-border-width: max(1px, 0.1rem);
  --fh-border-width-strong: max(2px, 0.2rem);

  --fh-shadow-1: 0 0.2rem 0.8rem rgba(0, 0, 0, 0.45);
  --fh-shadow-2: 0 1.2rem 3.2rem rgba(0, 0, 0, 0.55), 0 0 0 0.1rem rgba(214, 179, 110, 0.14);
  --fh-shadow-3: 0 2.4rem 6.4rem rgba(0, 0, 0, 0.65), 0 0 0 0.1rem rgba(214, 179, 110, 0.22);
  --fh-glow-accent: 0 0 0.6rem rgba(255, 79, 110, 0.6), 0 0 1.8rem rgba(255, 79, 110, 0.28);
  --fh-focus-ring: 0 0 0 0.2rem #0B090C, 0 0 0 0.4rem #D6B36E;
  --fh-blur-thin: 0.4rem;
  --fh-blur-regular: 0.8rem;
  --fh-blur-thick: 1.6rem;
  --fh-material-thin: rgba(11, 9, 12, 0.72);
  --fh-material-regular: rgba(11, 9, 12, 0.86);
  --fh-material-thick: rgba(11, 9, 12, 0.94);

  --fh-duration-fast: 120ms;
  --fh-duration-enter: 200ms;
  --fh-duration-exit: 140ms;
  --fh-duration-slow: 320ms;
  --fh-ease-standard: cubic-bezier(0.23, 1, 0.32, 1);
  --fh-ease-spring: cubic-bezier(0.34, 1.36, 0.64, 1);
}
```

The Open Design shared tokens in `tokens.css` carry the same decisions under the repository's schema names (mapping in section 2).

## 10. Component Rules — Shared Primitives

Every interactive element below lists what it does (input) and what it produces (the outcome plus the NUI callback the client script receives; callbacks are named `<screen>:<action>` and posted to the resource with `fetch`).

- **Panel:** `bg-surface`, hairline border, `radius-md`, `shadow-3`, brass top rule. Header: optional neon dot, display title (`text-xl`), right-aligned meta and close button. Footer: `rgba(0,0,0,.18)` band, actions right-aligned, the primary action last (rightmost). Close button (✕, `Esc`) → closes the panel with the exit motion, produces `<screen>:close`.
- **Button:** height 4 rem (sm 3.2, hero 4.8), uppercase `text-sm` 500, tracking 0.1 em. Variants: primary (brass fill, `text-on-accent`), secondary (border outline), ghost (no outline, `text-secondary`), danger (danger outline; `fill` variant only as the confirm of a destructive dialog), icon (3.6 rem square). States: default, hover (outline → brass; primary lightens to `#E3C68C`), pressed (primary darkens 12 %), focus (`focus-ring`), disabled (40 % opacity, no hover, tooltip explains why), busy (label replaced by spinner + verb "Sende …", width locked). Click/`Enter`/`Space` → runs its action.
- **Input:** height 4 rem, well `bg-base`, `border` outline, `radius-sm`, optional suffix (`€`, unit) in `text-muted`, label above in uppercase `text-2xs`. States: empty (placeholder `text-muted`), focus (brass outline + ring, brass caret), filled, error (danger outline + alert-icon message below, focus kept), disabled. Typing → updates value; `Enter` → submits the owning form.
- **Segmented control:** bordered strip, selected segment brass fill. Click/arrow keys → selects one option, produces `<screen>:change {field, value}`.
- **Slider:** 0.6 rem track `#3A3029`, brass fill, 1.8 rem champagne thumb with brass ring, value in mono at the right. Drag/arrow keys (±1 step, `Shift` ±10) → changes value live (the ped updates).
- **Tabs:** uppercase `text-xs`, active = `text-primary` + 2 px brass underline. Click/`Q`/`E` → switches content, keeps scroll per tab.
- **List row:** icon, main + sub line, right-aligned meta. States: default, hover (`rgba(244,236,221,.04)`), selected (brass 10 % fill + 2 px brass left bar), disabled (45 % opacity + reason as sub line, lock icon). Click/`↑↓` + `Enter` → selects.
- **Table:** uppercase `text-2xs` head on a solid `border` line, rows on hairlines, numbers right-aligned mono, selected row brass 10 %. Status text in a cell uses its status colour.
- **Chip:** 2.4 rem, outline in `currentColor`, uppercase `text-2xs`. Not interactive unless it is a filter, then it behaves like a segmented option.
- **Key cap:** brass outline, 2 px bottom edge, mono `text-xs`; muted variant (`border`, `text-secondary`) for secondary keys.
- **Progress bar:** 0.4–0.6 rem, track `#3A3029`, brass fill; success fill when done, danger fill when aborted.
- **Spinner / skeleton:** 2.4 rem ring, brass quarter; skeleton bars `bg-elevated` with a 1.2 s linear sheen. Loading never blocks `Esc`.
- **Tooltip:** `bg-surface`, `shadow-2`, appears after 300 ms hover, 200 ms enter; contains the item's actions when it belongs to an inventory slot.

## 11. Component Rules — HUD

States common to the whole HUD: **filled** (normal), **hidden** (any full screen or the phone is open, cinematic camera, `/hud` toggled off — everything fades out in 140 ms except voice/radio, which stays), **loading** (after spawn until the first status packet: plates drawn with skeleton bars, no values), **no data** (status script stopped: last values kept at 50 % opacity, no warnings fire).

- **Health:** left half of the vitals plate under the minimap, heart icon + 0.6 rem bar in `hud-health`. > 25 normal; ≤ 25 bar and icon `danger`; ≤ 10 plus a `danger` ring around the plate and 1 Hz pulse; 0 → death screen. Damage tween as in section 6. Not interactive.
- **Armor:** right half, shield + bar in `hud-armor`. At 0 the bar stays with an empty track (layout never jumps). Not interactive.
- **Hunger, thirst, stamina, stress:** 4.6 rem solid rings (`bg-base` centre, `#3A3029` track, value as conic arc in the HUD colour, icon in the centre). Hunger/thirst: > 25 normal, ≤ 25 `warning` + number below the ring, ≤ 10 `danger` + number + pulse. Stamina is shown only while below 100 % and fades out 2 s after it refills; ≤ 10 `danger`. Stress is shown only above 10 %. Order left → right: hunger, thirst, stamina, stress; hidden rings collapse the row. Not interactive.
- **Voice indicator:** plate with mic + three range bars (whisper / normal / shout). Idle: mic `text-muted`, active range bars `text-secondary`. Talking: mic and bars `hud-voice`. Whisper adds the word "FLÜSTERN". Muted (`pma-voice` mute or no microphone): mic-off in `danger` + "STUMM". Range is changed by the game keybind (default `F11`), which steps 1 → 2 → 3 → 1; the bars update in 120 ms. Produces nothing to the UI layer; it reflects voice state.
- **Radio indicator:** inside the voice plate after a hairline divider. No radio item: segment absent. Tuned: radio icon + "Funk 3" + frequency mono, `text-secondary`. Receiving: speaker name in `text-primary` ("J. Brandt spricht"). Transmitting (push-to-talk held): whole segment `hud-radio`, label "sendet". Not clickable; frequency changes happen in the radio item UI.
- **Cash + bank:** two right-aligned plates, label eyebrow + mono `text-lg`. On change, a delta appears right of the value for 3 s: `+ 250` in `success`, `− 1.200` in `danger`, while the value tweens. Bank is hidden while the server-side "Bank im HUD" setting is off. Not interactive.
- **Job tag:** plate with job-colour dot + job + grade + duty. Off duty: hollow dot and "außer Dienst" in `text-muted`. Not interactive (duty is toggled in the radial menu).
- **Ammo:** bottom-right plate, weapon name eyebrow + `text-2xl` mono magazine count + `/ reserve`. Low (≤ 25 % of magazine) magazine count `warning`; empty count `danger` + key cap `R` + "Nachladen"; reloading spinner + "lädt nach". Hidden when unarmed or holding a melee weapon.
- **Minimap frame:** brass 1 px frame with a 0.3 rem `bg-overlay` outer ring around GTA's minimap, `N` tab at top centre. Street plate above: compass heading (brass mono), street, zone (muted). States: on foot, in vehicle (same frame; GTA enlarges the map), GPS route (game draws it), hidden (with the HUD). Not interactive.
- **Notifications (4 types):** stack top-right, max 4 visible, newest on top, 36 rem wide. Each toast: 2 px left rule + icon + uppercase title in the type colour (`info` Info, `success` Erledigt, `warning` Achtung, `danger` Fehler), one or two lines of `text-sm` copy, relative time, and a 2 px timer line that shrinks over the lifetime (info/success 5 s, warning 8 s, error stays until clicked or replaced). Click → dismisses (produces `notify:dismiss {id}`); hovering pauses the timer. A fifth toast pushes the oldest out; repeated identical toasts merge with a "× 3" counter. Empty stack draws nothing.
- **Progress bar:** bottom-centre plate, 40 rem: icon + verb label + brass percentage, 0.4 rem bar, cancel hint `[X] Abbrechen`. States: running, done (bar `success`, check, fades after 600 ms), aborted (bar `danger`, "Abgebrochen", fades after 1 s). `X` → cancels, produces `progress:cancel {id}`. Only one progress bar at a time.
- **Interaction hint `[E] …`:** pill plate anchored next to the world target (a white dot marks the anchor), round brass key cap + verb + optional target name in muted. Variants: press (`E` triggers immediately; produces `interact:use {target}`), hold (key cap fills with a brass conic arc; release before 100 % cancels; on 100 % spring-confirms and produces `interact:use`), unavailable (muted cap + reason, e.g. "Abgeschlossen · Schlüssel fehlt", key does nothing). Appears within 2 m in 200 ms, leaves in 140 ms. Max one hint on screen; the nearest target wins.

## 12. Component Rules — Vehicle HUD

Shown only in a driver or passenger seat, 26 rem plate left of the ammo zone.

- **Speedometer:** 180° arc (radius 10 rem) with 21 tick marks in `text-muted`, filled arc in `text-primary` proportional to speed/max, the last 15 % of the arc permanently `danger` as redline. Digits `text-3xl` mono, three places with leading zeros (`087`), unit "KM/H" eyebrow, gear in a brass-outlined box below (`N`, `R`, `1`–`8`). Standstill: `000`, gear `N`. Unit follows the player setting (km/h, mph).
- **Fuel:** fuel icon + bar `hud-fuel` + mono percentage. ≤ 15 %: bar, icon and value `warning` and a one-time warning toast; 0 %: `danger`, engine stops. Electric vehicles show a battery icon and the same bar.
- **Seatbelt:** belt icon. Buckled: `success`. Unbuckled: `danger`; above 20 km/h it blinks 1 Hz and plays one chime. Toggled by the game keybind (default `B`), produces `vehicle:seatbelt {on}` from the client, the icon flips in 120 ms.
- **Engine state:** engine icon. Running, health > 50 %: `text-muted`. ≤ 50 %: `warning`. ≤ 15 %: `danger` + toast "Motor beschädigt". Off: 45 % opacity.
- **Indicators:** left/right arrows; active side `success` with glow, blinking 1.5 Hz; hazard = both. Driven by the game's indicator keys; no clicks.
- **Lights:** headlight icon; off muted, low beam `success`, high beam `info`.

## 13. Component Rules — Session Screens

- **Loading screen:** full-bleed night-harbour backdrop under a left-to-right scrim. Left: neon-dot eyebrow "Roleplay-Server · Hafen & Kiez", wordmark in Marcellus at 12 rem with 0.14 em tracking, double rule, welcome sentence. Top-right plate: players, next restart, version. Right: tip card ("Tipp 3 / 12", dots, crossfade every 8 s). Bottom: step label + "Schritt 3 von 5 · 214 / 338 Ressourcen" + brass percentage, thin full-width bar, music line, key hints. Interactions: `M` → toggles music (produces local state only; persists in `localStorage`), `←`/`→` → previous/next tip. States: loading (default), error "Verbindung verloren · Neuer Versuch in 5 s" with `[Jetzt verbinden]` (re-triggers the connection), empty (no tips configured → tip card absent), filled/hand-over (100 % → 320 ms fade to the character selection).
- **Multi-character selection:** left column of up to 4 slots: character card (photo, name, job · grade, last seen), free slot (dashed outline, brass plus, "Freier Platz · Neuen Charakter erstellen"), locked slot (lock, reason "Platz 4 ab 50 Spielstunden"). Selected card: brass outline + neon dot before the name. Right panel: details (born, job, cash, bank, playtime, phone, last seen) and footer `Löschen` (ghost, danger text) + `Spielen` (hero primary). Interactions: click/`↑↓` → selects a slot, the ped in the scene swaps (`charselect:select {slot}`); `Enter`/`Spielen` → `charselect:play {cid}` and hands over to the spawn selector; free slot click → opens the creator; `Löschen`/`Entf` → confirm dialog requiring the character's name typed in, then `charselect:delete {cid}`. States: empty (no characters: only free slots + "Noch kein Charakter · Erstelle deine erste Figur." with `Erstellen`), loading (three skeleton cards), error ("Charaktere nicht geladen · Datenbank antwortet nicht." + `Erneut`), filled.
- **Character creator:** left panel with neon dot title "Neuer Charakter", step counter `1 / 5`, tabs Identität · Gesicht · Haare · Merkmale · Kleidung. Identität: first name, last name (validation: ≥ 3 letters, letters/hyphen/space only, unique), date of birth with age suffix, gender segmented control, origin select, height slider (150–200 cm). Gesicht: parents blend slider between two face thumbnails, feature sliders (−1.0 … 1.0, mono values), skin tone swatches (selected = focus ring). Camera plate bottom-right: rotate, zoom out/in, camera preset (face/body/feet); `A`/`D` rotate, mouse wheel zooms. Footer: `Abbrechen` (back to selection, confirm if anything changed) and `Weiter` (disabled until the step validates; on the last step it becomes `Fertigstellen`, produces `creator:finish {appearance, identity}`). Every slider and swatch produces `creator:preview {field, value}` so the ped updates live. States: empty (defaults, name empty, `Zufällig` randomises), loading ("Speichere Charakter …" on finish), error (inline field errors; server "Name vergeben" on finish returns to step 1 with the field in error), filled.
- **Spawn selector:** dark stylised map full screen with pins; left panel "Aufwachen in …" list of spawn points (icon, name, sub line, distance mono). Rows: last location (clock icon), apartment (home), job spawn (badge, "nur im Dienst"), public places (pin), locked (lock + reason). Selected row ↔ highlighted brass pin with label; preview card bottom-right (image, title, one sentence). Interactions: click row or pin → selects (`spawn:select {id}`, camera flies to it in 320 ms); `Hier aufwachen`/`Enter` → `spawn:confirm {id}`, screen closes. States: empty (no last location → list starts with public places), loading ("Lade Orte …" skeleton rows), error (selecting a locked place shows "Ort gesperrt · Wache nur im Dienst." and keeps the previous choice), filled.
- **Death / unconscious screen:** world desaturated and darkened with a radial vignette; centred stack: pulse icon `danger`, eyebrow "Bewusstlos" `danger`, title "Du bist bewusstlos", reassurance line, respawn timer `text-4xl` mono with a thin bar, then two plates: emergency call (`[G] Notruf absetzen` → `death:call`; afterwards "Notruf gesendet · 00:18" in `success`) and respawn (`[E] Im Krankenhaus aufwachen`, disabled with "ab 00:00" until the timer ends, then active; hold 2 s → `death:respawn`). A warning line states what is lost. When revived by EMS the screen fades out in 320 ms. States: empty (no EMS online → timer shortened, line "Kein Rettungsdienst · Aufwachen schon nach 60 s."), loading ("Notruf wird gesendet …"), error ("Notruf fehlgeschlagen · Kein Netz hier." + `[G] Erneut`), filled.

## 14. Component Rules — Menus, Dialogs, Chat, Scoreboard

- **Radial menu:** 52 rem ring on `bg-overlay` with 8 segments divided by hairlines, brass outer rim, 18 rem `bg-surface` hub showing the hovered label (display) and "Untermenü · 6". Hovered segment: brass 24 % fill, icon and label brass. Disabled segment: 55 % opacity muted (e.g. "Dienst" for no job). Interactions: hold `F1` (bound key) → opens with spring scale 0.96 → 1; move mouse/stick → hovers; release or click → activates (`radial:select {id}`) or opens a sub-ring; right click → back one level; `Esc` → closes. States: empty ("Keine Aktionen" in the hub), loading (sub-ring segments as skeleton for remote menus), error ("Nicht möglich · Im Fahrzeug gesperrt." in the hub for 1.5 s), filled.
- **Context menu (third-eye target):** compact panel next to the anchored target: header with icon, target name, plate/ID in mono; rows with icon, verb and number key cap `1`–`9`. Hovered row: brass left bar. Disabled row: lock + reason sub line ("nur Mechaniker im Dienst"). Interactions: hover/number key/click → `target:select {id}`; moving away > 3 m or `Esc` → closes. States: empty ("Kein Ziel · Nichts im Blick."), loading ("Prüfe Berechtigung …"), error ("Ziel verloren · Zu weit entfernt (> 3 m)."), filled.
- **Input dialog:** centred 56 rem panel: title, context line ("An Jonte Brandt · 1,4 m entfernt"), one labelled field (mono for numbers, suffix unit), optional quick-value buttons (`€ 50`, `€ 100`, `€ 500`, `Alles`), footer `Abbrechen` + primary verb. Primary is disabled while the field is empty or invalid; validation runs on input, the error line names the limit ("Du hast nur € 1.250 Bargeld."). `Enter` → submits (`dialog:submit {id, value}`), `Esc` → `dialog:cancel {id}`. States: empty (field empty, primary disabled), loading (primary busy "Sende …"), error (inline), filled.
- **Confirm dialog:** 52 rem panel, alert icon in `danger` for destructive cases, question as title ("Fahrzeug verkaufen?"), one sentence with the exact object and amount, one sentence with the consequence, footer: safe action first and focused by default (`Behalten`), destructive action filled `danger` (`Verkaufen`). Non-destructive confirms use a primary brass button instead. `Enter` triggers the focused (safe) button; `Esc` = safe. Produces `dialog:confirm {id, accepted}`. States: empty (never opened without a subject), loading (confirm button busy), error (toast-style line inside the dialog + `Schließen`), filled.
- **Chat:** top-left, 56 rem. Message list on one plate, each line: channel chip (OOC muted, ME `hud-stress` italic action text, DO `info`, POL job colour, FUNK `hud-radio`, ADMIN `danger`), author in `text-secondary`, message in `text-primary`. Input: `T` opens a focused `bg-overlay` input with brass command prefix, character counter `41 / 256`; command suggestions list below (`Tab` completes, `↑↓` chooses). `Enter` → sends (`chat:send {channel, text}`), `Esc` → closes without sending. List fades out 8 s after the last message while the input is closed; `PageUp/PageDown` scroll history while open. States: empty ("Keine Nachrichten" ghost line only while input is open), loading (suggestions "Lade Befehle …"), error (unknown command line in `danger`: "/mee – meintest du /me?"), filled.
- **Scoreboard:** hold `F10` → centred 84 rem panel, release → closes. Header: neon dot + server name + `84 / 128`. Job counter strip (dot, job, count) and search field. Table: ID (mono), name (own row tagged "DU"), job dot + name, playtime, ping (≥ 120 `warning`, ≥ 250 `danger`). Mouse wheel scrolls while held; typing filters (`scoreboard:search` local). Footer: restart time, uptime, key hints. States: empty search ("Kein Treffer · Kein Spieler „xyz“." + `Suche leeren`), loading (skeleton rows), error ("Liste veraltet · Stand vor 60 s." + `Aktualisieren`), filled.

## 15. Component Rules — Interaction Screens

- **Inventory:** two panels side by side: "Taschen" (player, 5 × 5 slots) and the secondary container ("Kofferraum", "Handschuhfach", "Boden", "Lager"), each with weight `23,4 / 40 kg` in mono and a thin brass weight bar (≥ 90 % `warning`). Slot 9.6 rem: icon, name (ellipsis), count top-right, hotbar number 1–5 top-left in brass, durability bar at the bottom (< 50 % `warning`, < 15 % `danger`). Slot states: empty (40 % `bg-elevated`), filled, hover (brass outline + tooltip with weight, durability, serial, and actions `Ausrüsten`/`Benutzen`, `Geben`, `Ablegen`), dragging (source 35 % dashed, ghost follows the cursor tilted −4°), drop target (2 px dashed brass), locked (item in use). Interactions: drag → move (`inventory:move {from, to, count}`); `Shift`+drag or right-click "Teilen" → split popover with stepper and `Verschieben`; double-click → use (`inventory:use {slot}`); `1`–`5` → use hotbar; right-click → actions; `Tab`/`Esc` → close. States: empty ("Taschen leer · Gegenstände gibt es im Laden."), loading (slot skeletons), error ("Zu schwer · Kofferraum fasst noch 4,2 kg." as inline toast; the item snaps back), filled.
- **Phone:** device frame 34 × 70 rem bottom-right (bezel `bg-base`, brass inner edge, `radius-xl` screen). Status bar mono. Home: big mono clock, date, 4-column app grid (tile `bg-elevated` + brass icon, unread badge `danger` with `text-on-accent`). Incoming call banner on top of any app: avatar, name, "ruft an …", decline (`danger` round) and accept (`success` round) → `phone:call {action}`. Messages: header with back, avatar, number, call; incoming bubbles `bg-elevated`, outgoing bubbles brass with `text-on-accent`, read receipt; pill input + brass send button (`Enter` → `phone:message {to, text}`). `↑` (bound key) opens/closes; `Backspace` on empty input goes back. States: empty ("Keine Nachrichten · Neue Unterhaltung beginnen." + `Schreiben`), loading ("Verbinde Anruf …"), error ("Kein Netz · Im Tunnel kein Empfang." — send button disabled, messages queue), filled.
- **Bank / ATM:** bank panel 118 rem with three columns: accounts (private, job account read-only, shared), centre (balance `text-4xl` mono with dimmed cents, cash on hand, actions `Einzahlen` primary, `Abheben`, `Überweisen`, last transactions table with signed coloured amounts), right transfer form (recipient account with lookup confirmation "Jonte Brandt · gefunden", amount, reference, fee line, hero button "€ 250 überweisen"). Deposit/withdraw open the input dialog → `bank:deposit {amount}`, `bank:withdraw {amount}`; transfer → `bank:transfer {to, amount, reference}`. ATM: 50 rem panel, card owner line, 4 PIN dots (filled brass), 3 × 4 keypad of 6 rem keys (back, 0, confirm brass), attempts line; keys `0`–`9`, `Backspace`, `Enter`; after a correct PIN it shows withdraw amounts. States: empty ("Keine Umsätze · Dein Konto ist neu."), loading ("Buchung läuft …" on the hero button), error ("Abgelehnt · Konto existiert nicht." on the recipient field; ATM wrong PIN shakes the dots once and decrements attempts; 0 attempts locks the card 10 min), filled.
- **Shop:** full panel: header with neon dot + shop name, search, close. Left category list with counts; centre 4-column product cards (image well with brass icon, name, price mono brass, stock; hover reveals `In den Korb`; out of stock 45 % + "ausverkauft" `danger`; low stock "nur 2" `warning`); right basket (rows with − qty + steppers and line total, weight after purchase, payment segmented Bar/Karte, double rule, total `text-2xl`, hero `Bezahlen`). Interactions: add → `shop:add {item}`; steppers → `shop:qty {item, qty}` (0 removes); `Bezahlen` → `shop:checkout {method}`. States: empty basket ("Warenkorb leer · Wähle links einen Artikel." and `Bezahlen` disabled), loading ("Bezahle …"), error ("Zahlung abgelehnt · Nicht genug Bargeld." + switch to `Karte`), filled.
- **Garage:** panel with neon dot + garage name + "4 Fahrzeuge · 2 Plätze frei", tabs with counts (Alle, Eingeparkt, Unterwegs, Abgeschleppt), left vehicle list (icon, model, plate mono, state chip: `success` Eingeparkt, `info` Unterwegs, `danger` Abgeschleppt), right detail (class eyebrow, model title, number plate box, condition bars fuel/engine/body with mono %, mileage, trunk weight, key holders, actions `Ausparken` hero primary, `Schlüssel geben`, `Umbenennen`, impound notice with fee). `Ausparken` → `garage:spawn {plate}` and the screen closes; vehicles "Unterwegs" show `Orten` instead; "Abgeschleppt" shows `Auslösen · € 450` → `garage:impound {plate}`. States: empty ("Keine Fahrzeuge · Kaufe eines beim Händler."), loading (row skeletons), error ("Platz belegt · Etwas steht im Weg." + `Erneut`), filled.
- **Clothing store:** left panel leaves the ped visible: neon title + `Zurücksetzen` (ghost), category column (Hut, Brille, Jacke, Oberteil, Hose, Schuhe, Schmuck), model stepper `12 / 148` with name, texture swatches with name `2 / 6 · Marine`, price, `Zum Outfit`; footer summary and `Outfit speichern` + hero `Kaufen · € 340`. Right: vertical camera preset plate (full body, torso, face, rotate, hands-up pose). `←`/`→` step models, `↑`/`↓` textures; every change → `clothing:preview {component, drawable, texture}`; `Kaufen` → `clothing:buy`; `Outfit speichern` → input dialog for a name → `clothing:saveOutfit {name}`; `Esc` with unsaved changes → confirm "Änderungen verwerfen?". States: empty ("Outfit leer · Noch nichts gewählt."), loading ("Lade Modelle …" stepper skeleton), error ("Kauf fehlgeschlagen · Nicht genug Geld."), filled.
- **Crafting:** panel with neon title, skill level and XP in the header. Left recipe list (available rows; locked rows with lock + "ab Stufe 5"); centre recipe (title, effect sentence, ingredients table with needed vs. present — present ≥ needed `success`, short `danger` — missing line, quantity stepper, hero `Herstellen` disabled while something is missing); right queue (running item with mono countdown and brass bar, waiting item muted, finished item `success` "fertig · abholen", `Alle abholen`). `Herstellen` → `craft:start {recipe, qty}`; `Alle abholen` → `craft:collect`. States: empty ("Keine Rezepte · Steige im Handwerk auf."), loading ("Stelle her …" queue entry), error ("Zutat fehlt · 1 × Werkzeugrolle."), filled.
- **Invoice:** 44 rem panel "Rechnung erhalten": issuer title + job chip, number/issuer/due (due ≤ 3 days `warning`, overdue `danger`), positions table, double rule, total `text-2xl`, payment segmented (Bank/Bar with balances), footer `Später` (ghost, keeps it in the phone's invoice app), `Ablehnen` (danger outline → confirm), `Bezahlen` primary. Produces `invoice:pay {id, method}`, `invoice:decline {id}`, `invoice:later {id}`. States: empty ("Keine offenen Rechnungen · Alles bezahlt."), loading ("Zahle …"), error ("Zahlung abgelehnt · Auf dem Konto fehlen € 340." + `Bar zahlen`), filled.
- **ID card:** 51.4 × 32.4 rem card (ID-1 ratio) with brass outline, faint brass guilloche circles, title "Personalausweis" in brass display, issuer eyebrow, shield emblem, photo, name, born, height, nationality, valid until, ID number mono with wide tracking, signature line. Shown to the viewer with a plate above ("Mara Lindqvist zeigt dir ihren Ausweis") and a plate below (`Esc` schließen · closes after 10 s or beyond 3 m). Showing it is an item action (`idcard:show {target}`); the viewer can only close (`idcard:close`). Driver's licence and job badges reuse the card with a different title and a job-colour stripe. States: empty ("Kein Ausweis · Beantragen im Bürgeramt."), loading (photo skeleton), error ("Niemand in der Nähe · Zeigen braucht ein Gegenüber."), filled.

## 16. Component Rules — Faction Tablets

Tablets share one device: 12 rem side margins, `bg-base` bezel with brass inner edge, `radius-xl` screen, header bar with a 0.3 rem job-colour stripe, job icon, display title, status at the right; left navigation (icon rows, counts mono, alarm counts as `danger` chip); main area 2.4 rem padding. `Esc` closes; the tablet prop animation plays while open.

- **Police MDT:** header "MDT · Polizei Hafenstadt", unit and officer, status segmented (Frei `success` fill / Einsatz / Pause → `mdt:status {code}`), clock. Navigation: Übersicht, Personen, Fahrzeuge, Vorgänge (count), Haftbefehle (`danger` count), Leitstelle, Kollegen. Person search: focused input with hit count → result profile (photo, name display, flag chips "Gesucht" `danger`, "Führerschein entzogen" `warning`, born/ID/phone/address, actions `Vorgang anlegen` primary, `Haftbefehl`, `Bußgeld`, `Notiz`), records table (date, offence, officer, penalty; open = `danger` "offen"), notes cards. Search → `mdt:search {query}`; actions open forms in the same frame (`mdt:report:create`, `mdt:warrant:create`, `mdt:fine:create`). States: empty ("Keine Treffer · Name oder Ausweisnr. suchen."), loading ("Suche …"), error ("Keine Berechtigung · Nur im Dienst."), filled.
- **EMS tablet:** header "Rettungsdienst · Einsatzakte", unit + "Im Dienst" chip. Left: patients with triage dot (red/yellow/green = `danger`/`warning`/`success`), location sub line, mono elapsed time. Main: body schema (outlined silhouette; injured zones filled 20 % in severity colour with a coloured outline), patient title + triage chip, four vital tiles (pulse, blood pressure, SpO₂, blood loss; out-of-range values coloured), findings list (dot, zone · injury, sub line, action button `Versorgen`/`Schienen`, or `success` check when treated), actions `Wiederbeleben` primary, `Transport anfordern`, `Rechnung stellen`. Clicking a zone or a finding's action → `ems:treat {patient, zone, treatment}` with a progress bar in the HUD; `Wiederbeleben` → `ems:revive {patient}`. States: empty ("Keine Patienten · Ruhige Schicht."), loading ("Lade Akte …"), error ("Patient getrennt · Spieler hat verlassen."), filled.
- **Boss menu:** full panel with job-colour stripe, title "<Firma> · Verwaltung", owner chip. Tabs: Mitarbeiter, Kasse, Ränge & Gehälter, Fahrzeuge, Protokoll. Employees table (name, grade, salary mono, online status `success` / last seen muted); hovering a row reveals `Befördern` and `Entlassen` (danger ghost → confirm). Right column: company balance `text-3xl` mono with today's delta, `Einzahlen`/`Auszahlen` (input dialog), hire list of nearby players with `Anbieten` (disabled with reason "hat bereits Job: Polizei"). Produces `boss:promote {cid, grade}`, `boss:fire {cid}`, `boss:hire {serverId}`, `boss:deposit {amount}`, `boss:withdraw {amount}`, `boss:salary {grade, amount}`. States: empty ("Keine Mitarbeiter · Stelle jemanden ein." + `Einstellen`), loading ("Lade Personal …"), error ("Kasse reicht nicht · Gehälter > Kontostand."), filled.
- **Admin panel:** full panel with gear icon in `danger` (admin context), server metrics (players, server FPS coloured, resources), role chip. Tabs: Spieler, Meldungen (count `warning`), Bans, Server, Protokoll. Player table (ID, account · character, job, ping, notes chips). Selected player column: avatar, name, ID + licence (mono, truncated), action grid (`Hinteleportieren`, `Herholen`, `Zuschauen`, `Einfrieren`, `Wiederbeleben`, `Inventar`, `Kicken` danger outline, `Bannen` danger fill), open report card with `Übernehmen`/`Schließen`. `Bannen` opens a modal: duration segmented (1 Tag / 7 Tage / 30 Tage / Dauerhaft), reason (visible to the player), audit note, `Abbrechen` + danger-fill confirm naming the duration. Produces `admin:action {action, target}`, `admin:ban {target, duration, reason}`, `admin:report:claim {id}`. Every action is logged; destructive ones always confirm. States: empty ("Keine Meldungen · Alles ruhig."), loading ("Lade Spieler …"), error ("Fehlgeschlagen · Spieler nicht mehr online."), filled.

## 17. States Catalogue

Every screen has four drawn states; the preview draws filled states on stages 01–22 and empty, loading and error on stages 23–24 with the exact copy below.

| Screen | Empty | Loading | Error |
| --- | --- | --- | --- |
| HUD | Ausgeblendet · Menü offen oder /hud aus | Warte auf Spielerdaten … | Keine Daten · Werte grau, letzter Stand |
| Loading screen | Keine Tipps · Tipp-Karte entfällt | Verbinde mit Server … | Verbindung verloren · Neuer Versuch in 5 s · [Jetzt verbinden] |
| Character selection | Noch kein Charakter · [Erstellen] | Lade Charaktere … | Nicht geladen · Datenbank antwortet nicht · [Erneut] |
| Character creator | Standardwerte · [Zufällig] | Speichere Charakter … | Name vergeben · [Ändern] |
| Spawn selector | Kein letzter Ort · Nur öffentliche Orte | Lade Orte … | Ort gesperrt · [Anderer Ort] |
| Death screen | Kein Rettungsdienst · Aufwachen schon nach 60 s | Notruf wird gesendet … | Notruf fehlgeschlagen · [G] Erneut |
| Radial menu | Keine Aktionen | Lade Untermenü … | Nicht möglich · Im Fahrzeug gesperrt |
| Context menu | Kein Ziel | Prüfe Berechtigung … | Ziel verloren · Zu weit entfernt |
| Input dialog | Feld leer · Primär gesperrt | Sende … | Ungültig · Nur Zahlen bis € 1.250 |
| Confirm dialog | Öffnet nur mit Ziel | Verkaufe … | Fehlgeschlagen · [Schließen] |
| Chat | Keine Nachrichten | Lade Befehle … | Befehl unbekannt |
| Scoreboard | Kein Treffer · [Suche leeren] | Lade Spielerliste … | Liste veraltet · [Aktualisieren] |
| Inventory | Taschen leer | Lade Inventar … | Zu schwer · Item springt zurück |
| Phone | Keine Nachrichten · [Schreiben] | Verbinde Anruf … | Kein Netz |
| ID card | Kein Ausweis | Lade Foto … | Niemand in der Nähe |
| Invoice | Keine offenen | Zahle … | Zahlung abgelehnt · [Bar zahlen] |
| Bank / ATM | Keine Umsätze | Buchung läuft … | Abgelehnt · [Prüfen] |
| Shop | Warenkorb leer | Bezahle … | Zahlung abgelehnt · [Karte] |
| Garage | Keine Fahrzeuge | Lade Fahrzeuge … | Platz belegt · [Erneut] |
| Clothing store | Outfit leer | Lade Modelle … | Kauf fehlgeschlagen |
| Crafting | Keine Rezepte | Stelle her … | Zutat fehlt |
| Police MDT | Keine Treffer | Suche … | Keine Berechtigung |
| EMS tablet | Keine Patienten | Lade Akte … | Patient getrennt |
| Boss menu | Keine Mitarbeiter · [Einstellen] | Lade Personal … | Kasse reicht nicht |
| Admin panel | Keine Meldungen | Lade Spieler … | Fehlgeschlagen · Spieler nicht mehr online |
| Notifications | Stapel leer, nichts gezeichnet | Toast mit Spinner für laufende Aktion | Fehler-Toast bleibt bis Klick |

Patterns: **empty** = muted outline icon, one bold line, one muted line, optional secondary button; **loading** = brass spinner + verb with ellipsis + two skeleton bars, inputs keep their values, `Esc` still closes; **error** = `danger` alert icon, `danger` headline, plain-language cause, one recovery button where a recovery exists; the panel border turns `danger` at 50 % only for errors that block the whole screen.

## 18. Anti-patterns

- No explicit or suggestive imagery, no body silhouettes as decoration, no pink gradients, no "red light" fills behind panels. The district is evoked by one neon dot and the type.
- No neon on text, buttons, status or more than one element per screen; no neon in the HUD.
- No pure white (`#FFFFFF`) text or pure black panels; champagne on aubergine-black only.
- No text or icon straight on the game world without a plate; no `backdrop-filter` in the HUD.
- No CDN fonts, no icon fonts, no remote images in NUI.
- No pill buttons, no gradients on buttons, no drop shadows on text.
- No proportional digits for changing numbers; no thin display type below `text-lg`.
- No `ease-in`, no scale-from-zero, no looping animation besides the documented pulses and blinkers.
- No colour as the only signal; no destructive action without a confirm and a word.
- No new `--fh-*` names in a single variant; the shared set is the contract across the series.

## 19. Preview & Files

- Package: `manifest.json`, `DESIGN.md`, `tokens.css` (Open Design shared tokens), `components.html` (token fixture with core controls), `fonts/` (WOFF2 + OFL licences).
- Full preview of every element at the 1920 × 1080 reference, scaling to 1280 × 720 and 2560 × 1440: `work/fivem-harbour-designsystem/kiez-preview.html` (append `#overview` for a contact sheet of all 26 stages). Stage map: 00 colour · 00b type/space/shape/motion/icons · 01 HUD day · 02 HUD night · 03 HUD states · 04 loading · 05 character selection · 06 creator · 07 spawn · 08 death · 09 radial + context · 10 input + confirm · 11 chat + scoreboard · 12 inventory · 13 phone + ID + invoice · 14 bank + ATM · 15 shop · 16 garage · 17 clothing · 18 crafting · 19 MDT · 20 EMS · 21 boss · 22 admin · 23–24 empty/loading/error per screen.
