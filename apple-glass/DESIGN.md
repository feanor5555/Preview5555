# FiveM Apple Glass

> Category: Themed & Unique
> Variant D for a FiveM roleplay server UI: dark tinted liquid glass, continuous rounded corners, generous spacing, quiet hierarchy and one restrained blue accent, readable over bright and dark game scenes.

## 1. Direction and audience

**For whom.** Players of a German-speaking FiveM roleplay server set in a north-German harbour town (docks, container yard, fish market, ferries, a red-light district). They look at the HUD for hours while driving, talking and roleplaying; they open menus briefly, mostly with mouse and keyboard, sometimes with a controller. Job players (police, EMS, mechanics, company bosses) and staff (admins) use dense tools — MDT, EMS tablet, boss menu, admin panel — for several minutes at a time. All in-game copy is German; this document is English.

**Direction.** Modern, futuristic and minimal, in the spirit of current Apple design language (iOS 26 / visionOS "Liquid Glass" materials) without any Apple trademark, logo, product name or SF Pro font:

- Dark, tinted, translucent glass surfaces with a soft specular top edge. Legibility comes from the tint; the HUD carries no blur, full-screen menus sit on the game's own screen blur.
- Continuous (squircle-like) rounded corners, concentric radii: an inner radius equals the outer radius minus the padding.
- Generous spacing, quiet hierarchy: one semibold title, everything else regular or medium; colour is information, not decoration.
- One restrained accent (`accent-primary` blue) for the single primary action and the selected state; all other colour is semantic (status, job, vital).
- Subtle depth: three shadow levels and one accent glow; nothing neon.
- The centre of the screen stays free during gameplay. HUD lives in the corners inside the safe zone.

**Server identity placeholder.** The server name is shown as the wordmark "HARBOUR" with the subline "Roleplay". It is a placeholder that the server replaces; it is typeset in Inter, never drawn as a logo.

**Reference files.**

| File | Role |
| --- | --- |
| `design-systems/fivem-apple-glass/DESIGN.md` | This artefact: tokens, rules, every screen with states and interactions, long copy |
| `design-systems/fivem-apple-glass/tokens.css` | Shared Open Design schema bound to this palette (px at the 1080p reference) |
| `design-systems/fivem-apple-glass/components.html` | Compact fixture of the core primitives |
| `design-systems/fivem-apple-glass/fonts/` | Self-hosted Inter (variable, `opsz` + `wght`) and JetBrains Mono, with OFL licences |
| `work/fivem-harbour-designsystem/apple-glass-preview.html` | Full drawing of every element and state over stand-in game scenes |

## 2. Colour palette

Every token exists as `--fh-<token-name>`. Contrast ratios are WCAG 2.x relative-luminance ratios, computed, not estimated.

**How the backgrounds were measured.** Glass in FiveM cannot rely on blur: the NUI page is a transparent browser layer composited over the game, CSS `backdrop-filter` cannot see the game picture, and the HUD carries no blur at all (section 3). Legibility therefore comes from tint alone. Two reference backgrounds are used:

- **Surface** — solid `bg-surface` `#13161D` (what a panel looks like over a dark scene, and the floor for all panel text).
- **HUD worst case** — `material-thick` (`bg-surface` at 88 %) composited over pure white `#FFFFFF`, i.e. a HUD widget in front of a sunlit white wall or overexposed sky. The composite is `#2F3238`. Every real scene is darker than this, so every ratio in that column is a lower bound.

### Neutrals and surfaces

| Token | Hex | Usage | Contrast |
| --- | --- | --- | --- |
| `bg-base` | `#0A0C10` | Opaque full-screen canvases: loading screen, character selection, spawn selector backdrop, phone screen | `text-primary` on it 18.24:1 |
| `bg-surface` | `#13161D` | Tint of every glass material and the solid fallback of every panel | `text-primary` on it 16.87:1 |
| `bg-elevated` | `#1E222B` | Raised blocks inside a panel: input fields, selected rows, cards, tooltips, segmented track | `text-primary` on it 14.84:1 |
| `bg-overlay` | `#05070A8F` (`rgba(5,7,10,0.56)`) | Scrim behind every modal panel and the death screen; text never sits on the scrim alone | Over white it yields `#606163`; `text-primary` 4.35:1 there, which is why text always sits on a panel above the scrim |
| `border` | `#FFFFFF24` (`rgba(255,255,255,0.14)`) | Hairline edge of glass, row separators, keycaps | Composite `#34373D` vs `bg-surface` 1.52:1 — decorative edge; controls are identified by fill and label, never by the hairline alone |

### Text

| Token | Hex | Usage | Contrast (surface / HUD worst case) |
| --- | --- | --- | --- |
| `text-primary` | `#F5F7FA` | Titles, values, body copy, HUD numerals | 16.87:1 / 11.97:1 |
| `text-secondary` | `#BCC3CE` | Labels, descriptions, secondary values; the minimum for any text on the HUD | 10.20:1 / 7.24:1 |
| `text-muted` | `#9AA2AE` | Metadata, timestamps, placeholders, disabled labels | 7.03:1 / 4.99:1 |
| `text-on-accent` | `#FFFFFF` | Label on `accent-primary` fills | 4.65:1 on `accent-primary` |

### Accent

| Token | Hex | Usage | Contrast |
| --- | --- | --- | --- |
| `accent-primary` | `#2B6FE6` | The one primary button per view, selected tab/segment fill, toggles on, slider fill. Fill only, never text | 3.90:1 vs `bg-surface` (non-text ≥ 3:1); `text-on-accent` on it 4.65:1 |
| `accent-secondary` | `#8CB9FF` | Accent as text and line: links, focus ring, selected-row indicator, progress fill, radial hover edge | 9.05:1 surface / 6.42:1 HUD worst case |

### Status

| Token | Hex | Usage | Contrast (surface / HUD worst case) |
| --- | --- | --- | --- |
| `success` | `#3CD68A` | Confirmed, paid, on duty, ingredient available, indicator lamps | 9.63:1 / 6.84:1 |
| `warning` | `#FFC53D` | Attention needed: low fuel, overdue invoice, engine damaged, expiring licence | 11.47:1 / 8.14:1 |
| `danger` | `#FF5F57` | Errors, destructive actions, seatbelt open, warrants, critical vitals | 6.06:1 / 4.30:1 — as text only inside panels; on the HUD as icon, bar or dot (non-text ≥ 3:1) |
| `info` | `#6CC4FF` | Neutral information notifications, hints, dispatch info | 9.46:1 / 6.71:1 |

Status fills with dark text (badges): `bg-base` on `success` 10.42:1, on `warning` 12.40:1, on `danger` 6.55:1, on `info` 10.23:1.

### Jobs

Job colours mark a job in a dot, a badge, a scoreboard count and the top edge of a job tool. Job text in a job colour is allowed inside panels (all ≥ 4.5:1 on surface); on the HUD the job name stays `text-primary` and the colour is a dot.

| Token | Hex | Usage | Contrast (surface / HUD worst case) |
| --- | --- | --- | --- |
| `job-police` | `#7D8CFF` | Police (LSPD / harbour police): job dot, MDT top edge, scoreboard count | 6.09:1 / 4.32:1 |
| `job-ems` | `#FF6E85` | Rescue service: job dot, EMS tablet top edge | 6.74:1 / 4.78:1 |
| `job-mechanic` | `#FFA040` | Mechanics and towing: job dot, workshop invoices | 8.92:1 / 6.33:1 |
| `job-civil` | `#AAB3C0` | Civilians and every unlisted job: neutral job dot | 8.55:1 / 6.07:1 |

### HUD vitals and signals

Each vital colour is used for its ring arc, its icon and its warning tint. A vital is never identified by colour alone: every one has its own glyph.

| Token | Hex | Usage | Contrast (surface / HUD worst case) |
| --- | --- | --- | --- |
| `hud-health` | `#FF4F6D` | Health ring and heart glyph | 5.68:1 / 4.03:1 |
| `hud-armor` | `#AEBFD4` | Armour ring and shield glyph (steel, deliberately not blue) | 9.66:1 / 6.85:1 |
| `hud-hunger` | `#FF8F52` | Hunger ring and fork-and-knife glyph | 8.02:1 / 5.69:1 |
| `hud-thirst` | `#4CC4F5` | Thirst ring and drop glyph | 9.07:1 / 6.43:1 |
| `hud-stamina` | `#B6E35C` | Stamina ring and running glyph | 12.18:1 / 8.64:1 |
| `hud-stress` | `#B78DFF` | Stress ring and wave glyph | 7.13:1 / 5.06:1 |
| `hud-voice` | `#5FE3C4` | Proximity voice: mic glyph and range bars while talking | 11.44:1 / 8.12:1 |
| `hud-radio` | `#F28BE6` | Radio: channel glyph while connected, pill edge while transmitting | 8.28:1 / 5.88:1 |
| `hud-fuel` | `#F6BB3F` | Fuel bar and pump glyph in the vehicle HUD | 10.43:1 / 7.40:1 |

**Overlaps that are intended.** Fuel, hunger and warning share the amber–orange range; health, EMS and danger share red. They never mean the same thing in the same place: fuel lives only in the vehicle cluster, hunger only in the vitals row, warning only in notifications and badges, each with its own glyph.

## 3. Glass materials, blur and runtime constraints

**Runtime facts that shape the material.**
- The NUI page is a transparent browser layer composited over the game. CSS `backdrop-filter` cannot see the game picture behind the page, and on the current client it flickers. Glass in this system is therefore **tint, not blur**.
- **HUD widgets carry no `backdrop-filter` at all.** Their legibility comes from `material-thick` alone (88 % opaque), so every HUD colour keeps ≥ 4.0:1 even in front of pure white (section 2).
- **Full-screen menus** (every panel, dialog, tablet, death screen) ask the game for its own screen blur — `TriggerScreenblurFadeIn(duration)` when the menu opens and `TriggerScreenblurFadeOut(duration)` when the last menu closes, both with `duration-enter` / `duration-exit` — and lay the `bg-overlay` scrim plus a `material-regular` panel on top. The game blur is atmosphere; the scrim and the material carry the contrast.
- `--fh-blur-*` stay defined for one case only: **NUI over NUI**, where the backdrop is our own page (a context menu over the inventory, notifications over the phone wallpaper, the phone dock). Nothing may depend on them for legibility.
- Release builds run **Chromium 103**. Not available there and therefore not used in runtime CSS: `color-mix()`, `:has()`, container queries, CSS nesting, `corner-shape`. Tints are written as `rgba()` values or as a `::before` layer with `background: var(--c); opacity: 0.18` under the content.

Three materials, all built from `bg-surface`:

| Token | Value | Where | Rule |
| --- | --- | --- | --- |
| `material-thin` | `rgba(19,22,29,0.72)` | Nested surfaces inside a panel, glass over `bg-base` (loading screen, character selection) | Never directly over the game world with text on it |
| `material-regular` | `rgba(19,22,29,0.82)` | Every panel, dialog, menu, tablet; always above the `bg-overlay` scrim and the game screen blur | Worst-case composite (white world, scrim, panel) `#24272D` |
| `material-thick` | `rgba(19,22,29,0.88)` | Every HUD widget, notifications, interaction hint, progress bar, radial menu ring | Worst-case composite over white `#2F3238` — the reference of the contrast tables |

| Token | Value | Use (NUI over NUI only) |
| --- | --- | --- |
| `blur-thin` | `1.2rem` | Phone dock, keycaps over a panel |
| `blur-regular` | `2.4rem` | Context menu or notification over a panel or the phone |
| `blur-thick` | `4rem` | Dialog over a tablet or panel |

**Glass recipe.**

```css
/* every glass surface — no backdrop-filter */
.fh-glass {
  background-color: var(--fh-material-regular);
  background-image: linear-gradient(180deg, rgba(255,255,255,0.06), rgba(255,255,255,0) 40%);
  border: var(--fh-border-width) solid var(--fh-border);
  border-radius: var(--fh-radius-lg);
  box-shadow: var(--fh-shadow-2);
}
.fh-glass--hud { background-color: var(--fh-material-thick); border-radius: var(--fh-radius-md); }
.fh-glass--panel { box-shadow: var(--fh-shadow-3); }

/* only where the layer below is our own NUI page */
.fh-glass--over-nui {
  -webkit-backdrop-filter: blur(var(--fh-blur-regular)) saturate(160%);
  backdrop-filter: blur(var(--fh-blur-regular)) saturate(160%);
}

/* colour tint without color-mix(): Chromium 103 safe */
.fh-tint { position: relative; color: var(--c); }
.fh-tint::before { content: ""; position: absolute; inset: 0; border-radius: inherit; background: var(--c); opacity: 0.18; }
.fh-tint > * { position: relative; }
```

- The top-to-transparent sheen and the inset highlight in the shadow tokens are the specular edge; nothing else is "shiny".
- Continuous corners: Chromium 103 draws circular radii; the concentric-radius rule (inner = outer − padding) is what keeps the shapes calm. A later client may add `@supports (corner-shape: squircle) { border-radius: calc(radius × 1.6) }` as enhancement; the preview, rendered in a current Chrome, shows that enhancement.
- Tint values used across the system (all `rgba`, alpha in brackets): status badges and notification icon circles (0.18), inline error banner `danger` (0.14) over `bg-elevated`, warning banner `warning` (0.12), destructive button `danger` (0.18) over `bg-elevated` with a `danger` (0.40) border, critical vital `danger` (0.22) over `material-thick`, talking pill border `hud-voice` (0.45).

## 4. Typography

**Families.** Inter is the self-hostable stand-in for a neo-grotesk system face; its `opsz` axis gives text optics at small sizes and display optics at large sizes automatically (`font-optical-sizing: auto`). JetBrains Mono is used only for identifiers that must be read character by character (plates, ID numbers, case numbers, radio frequency in the MDT, admin console).

**Font files** — in `design-systems/fivem-apple-glass/fonts/`, shipped inside the NUI resource and referenced relatively; nothing is loaded from a CDN at runtime because FiveM NUI runs offline in CEF/Chromium:

| File | Family | Axes / weight | Unicode range |
| --- | --- | --- | --- |
| `Inter-Variable-latin.woff2` | Inter | `opsz` 14–32, `wght` 100–900 | Latin incl. German umlauts and ß, € |
| `Inter-Variable-latin-ext.woff2` | Inter | same | Latin Extended (Polish, Turkish, Czech names) |
| `JetBrainsMono-Regular-latin.woff2` | JetBrains Mono | 400 | Latin |
| `JetBrainsMono-Medium-latin.woff2` | JetBrains Mono | 500 | Latin |
| `OFL-inter.txt`, `OFL-jetbrainsmono.txt` | — | SIL Open Font License 1.1 | — |

```css
@font-face { font-family: "Inter"; font-style: normal; font-weight: 100 900; font-display: block;
  src: url("fonts/Inter-Variable-latin.woff2") format("woff2-variations");
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+0304, U+0308, U+0329, U+2000-206F, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD; }
@font-face { font-family: "Inter"; font-style: normal; font-weight: 100 900; font-display: block;
  src: url("fonts/Inter-Variable-latin-ext.woff2") format("woff2-variations");
  unicode-range: U+0100-02BA, U+02BD-02C5, U+02C7-02CC, U+02CE-02D7, U+02DD-02FF, U+1D00-1DBF, U+1E00-1E9F, U+1EF2-1EFF, U+2020, U+20A0-20AB, U+20AD-20C0, U+2113, U+2C60-2C7F, U+A720-A7FF; }
@font-face { font-family: "JetBrains Mono"; font-style: normal; font-weight: 400; font-display: block;
  src: url("fonts/JetBrainsMono-Regular-latin.woff2") format("woff2"); }
@font-face { font-family: "JetBrains Mono"; font-style: normal; font-weight: 500; font-display: block;
  src: url("fonts/JetBrainsMono-Medium-latin.woff2") format("woff2"); }
```

`font-display: block` because the files are local: a fallback flash would be the only visible effect of `swap`.

**Scale** (rem; 1rem = 10px at 1080p, see section 9):

| Token | rem | px @1080p | px @720p | px @1440p | Use | Weight | Leading | Tracking |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `text-2xs` | 1.2 | 12 | 9.6 | 16 | Keycap letters, units, chart axes | 600 | 1.2 | +0.02em |
| `text-xs` | 1.3 | 13 | 10.4 | 17.3 | Metadata, timestamps, table headers | 500 | 1.3 | +0.01em |
| `text-sm` | 1.5 | 15 | 12 | 20 | HUD labels, list rows, body in dense tools | 400/500 | 1.4 | 0 |
| `text-md` | 1.7 | 17 | 13.6 | 22.7 | Body, buttons, inputs | 400/600 | 1.45 | -0.005em |
| `text-lg` | 2.0 | 20 | 16 | 26.7 | Panel titles, money values | 600 | 1.25 | -0.01em |
| `text-xl` | 2.4 | 24 | 19.2 | 32 | Screen titles, dialog titles | 600 | 1.2 | -0.015em |
| `text-2xl` | 3.2 | 32 | 25.6 | 42.7 | Bank balance, character names | 600 | 1.1 | -0.02em |
| `text-3xl` | 4.8 | 48 | 38.4 | 64 | Loading wordmark, death-screen title | 600 | 1.05 | -0.022em |
| `text-4xl` | 7.2 | 72 | 57.6 | 96 | Speedometer numerals | 600 | 1.0 | -0.03em |

**Weights:** `weight-regular` 400, `weight-medium` 500, `weight-semibold` 600, `weight-bold` 700 (bold is reserved for the speedometer and the loading wordmark; hierarchy otherwise comes from size and colour).

**Rules.**
- All numbers that change (money, vitals, speed, ammo, timers, prices) use `font-variant-numeric: tabular-nums` so they do not jitter.
- German number format everywhere: thousands with a dot, decimals with a comma, currency after the value with a narrow space — `4.250 €`, `24,5 kg`, `Funk 101,5`.
- Sentence case for all labels and titles (German nouns stay capitalised); no all-caps except keycaps and three-letter codes (`LSPD`, `EMS`).
- Minimum HUD text size is `text-sm`; `text-2xs` only inside keycaps and as units next to a larger value.

## 5. Spacing, radii, borders, shadows and glow

**Spacing** (4-point base, rem):

| Token | rem | px @1080p | Typical use |
| --- | --- | --- | --- |
| `space-0_5` | 0.2 | 2 | Ring stroke gaps, keycap inner offset |
| `space-1` | 0.4 | 4 | Icon to text in chips |
| `space-2` | 0.8 | 8 | Gap inside HUD pills, between vitals |
| `space-3` | 1.2 | 12 | Row padding (vertical), gap between buttons |
| `space-4` | 1.6 | 16 | Padding of HUD widgets, list row padding (horizontal) |
| `space-5` | 2.0 | 20 | Card padding |
| `space-6` | 2.4 | 24 | Panel padding, gap between panel columns |
| `space-8` | 3.2 | 32 | Screen safe margin, section gaps |
| `space-10` | 4.0 | 40 | Dialog padding on large dialogs |
| `space-12` | 4.8 | 48 | Gap between major regions on full-screen views |
| `space-16` | 6.4 | 64 | Loading screen and character-selection outer padding |

**Radii** (concentric: inner = outer − padding):

| Token | rem | Use |
| --- | --- | --- |
| `radius-xs` | 0.6 | Keycaps, small badges, inventory slot inner image |
| `radius-sm` | 1.0 | Inputs, buttons in dense tools, list rows, slots |
| `radius-md` | 1.4 | HUD widgets, cards, notifications, context menu |
| `radius-lg` | 2.2 | Panels, dialogs, chat, scoreboard |
| `radius-xl` | 3.2 | Tablets (MDT, EMS), phone screen, loading cards |
| `radius-pill` | 999 | Primary buttons, HUD pills, chips, progress bar, search fields |

**Borders.** `border-width` = `max(1px, 0.1rem)` for every hairline; `border-width-strong` = `max(2px, 0.2rem)` for focus outlines, the selected inventory slot and the active radial segment. Inputs use `border-width` in `border`, `border-width-strong` in `accent-secondary` on focus and in `danger` on error.

**Shadows and glow.**

| Token | Value | Use |
| --- | --- | --- |
| `shadow-1` | `0 0.1rem 0.3rem rgba(0,0,0,0.28), inset 0 0.1rem 0 rgba(255,255,255,0.08)` | Keycaps, chips, slots, buttons |
| `shadow-2` | `0 0.8rem 2.4rem rgba(0,0,0,0.36), inset 0 0.1rem 0 rgba(255,255,255,0.10)` | HUD widgets, menus, notifications |
| `shadow-3` | `0 2.4rem 6.4rem rgba(0,0,0,0.50), inset 0 0.1rem 0 rgba(255,255,255,0.12)` | Panels, dialogs, tablets, phone |
| `glow-accent` | `0 0 0 0.1rem rgba(140,185,255,0.40), 0 0 2.4rem rgba(43,111,230,0.45)` | Exactly one element at a time: the hovered radial segment, the selected character, the active speed arc tip |
| `focus-ring` | `0 0 0 0.2rem var(--fh-bg-surface), 0 0 0 0.4rem var(--fh-accent-secondary)` | `:focus-visible` on every control |

## 6. Motion

| Token | Value | Use |
| --- | --- | --- |
| `duration-fast` | `120ms` | Hover, press, toggle, segment change |
| `duration-enter` | `220ms` | Panels, menus, notifications, hints appearing |
| `duration-exit` | `140ms` | Everything leaving; exits are shorter than entries |
| `duration-slow` | `420ms` | Screen-to-screen transitions (loading → character select → spawn), camera-linked moves |
| `ease-standard` | `cubic-bezier(0.23, 1, 0.32, 1)` | Default for every transition |
| `ease-spring` | `cubic-bezier(0.34, 1.4, 0.64, 1)` | Radial menu open, toggle knob, new notification settle — small overshoot only |

- Enter: `opacity 0 → 1` plus `translateY(0.8rem) → 0` or `scale(0.96) → 1`. Never from `scale(0)`; never `ease-in`.
- Panels mount once and toggle a class (`.is-open`) so the exit transition runs.
- Value changes on the HUD animate the ring arc over `duration-enter`; money deltas count up over `duration-slow`.
- Loops: talking bars (600ms), indicator lamps (1s, 50 % duty), seatbelt warning pulse (1.2s), low-vital pulse (1.6s), loading shimmer (1.4s linear).
- `prefers-reduced-motion: reduce` (and the server setting "Bewegung reduzieren"): translations and scale removed, fades kept at `duration-fast`, loops replaced by a steady state (indicators stay lit, shimmer becomes a static `bg-elevated` block, pulses become a steady `danger` outline).

## 7. Iconography

- Line icons on a 24-unit grid, 1.75-unit stroke, round caps and joins, drawn as inline SVG with `stroke="currentColor"` so they take the token colour of their context.
- Filled variant only for an active or critical state (heart fills when health is critical, mic fills while talking, seatbelt fills when open).
- Sizes: 1.6rem in rows and buttons, 2rem in HUD widgets, 2.4rem in notifications and empty states, 4rem in empty-state illustrations.
- Shapes are generic (heart, shield, drop, fork and knife, figure running, waves, microphone, radio tower, pump, belt buckle, engine block, arrows, wallet, columns building, briefcase, star badge, cross, wrench). No Apple glyph, no SF Symbols file, no third-party logo.
- Keycaps (`[E]`) are text, not icons: `bg-elevated`, `border`, `radius-xs`, `text-2xs` semibold, min width 2.4rem.

## 8. CSS custom properties

The complete `--fh-*` set. Colour tokens are shared by all six variants; the non-colour set is the fixed common set. No further `--fh-*` names exist.

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }

:root {
  /* surfaces */
  --fh-bg-base: #0A0C10;
  --fh-bg-surface: #13161D;
  --fh-bg-elevated: #1E222B;
  --fh-bg-overlay: rgba(5, 7, 10, 0.56);
  --fh-border: rgba(255, 255, 255, 0.14);
  /* text */
  --fh-text-primary: #F5F7FA;
  --fh-text-secondary: #BCC3CE;
  --fh-text-muted: #9AA2AE;
  --fh-text-on-accent: #FFFFFF;
  /* accent */
  --fh-accent-primary: #2B6FE6;
  --fh-accent-secondary: #8CB9FF;
  /* status */
  --fh-success: #3CD68A;
  --fh-warning: #FFC53D;
  --fh-danger: #FF5F57;
  --fh-info: #6CC4FF;
  /* jobs */
  --fh-job-police: #7D8CFF;
  --fh-job-ems: #FF6E85;
  --fh-job-mechanic: #FFA040;
  --fh-job-civil: #AAB3C0;
  /* hud */
  --fh-hud-health: #FF4F6D;
  --fh-hud-armor: #AEBFD4;
  --fh-hud-hunger: #FF8F52;
  --fh-hud-thirst: #4CC4F5;
  --fh-hud-stamina: #B6E35C;
  --fh-hud-stress: #B78DFF;
  --fh-hud-voice: #5FE3C4;
  --fh-hud-radio: #F28BE6;
  --fh-hud-fuel: #F6BB3F;

  /* type */
  --fh-font-sans: "Inter", system-ui, -apple-system, "Segoe UI", sans-serif;
  --fh-font-display: "Inter", system-ui, -apple-system, "Segoe UI", sans-serif;
  --fh-font-mono: "JetBrains Mono", ui-monospace, "SF Mono", Menlo, monospace;
  --fh-text-2xs: 1.2rem;
  --fh-text-xs: 1.3rem;
  --fh-text-sm: 1.5rem;
  --fh-text-md: 1.7rem;
  --fh-text-lg: 2rem;
  --fh-text-xl: 2.4rem;
  --fh-text-2xl: 3.2rem;
  --fh-text-3xl: 4.8rem;
  --fh-text-4xl: 7.2rem;
  --fh-weight-regular: 400;
  --fh-weight-medium: 500;
  --fh-weight-semibold: 600;
  --fh-weight-bold: 700;

  /* spacing */
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

  /* shape */
  --fh-radius-xs: 0.6rem;
  --fh-radius-sm: 1rem;
  --fh-radius-md: 1.4rem;
  --fh-radius-lg: 2.2rem;
  --fh-radius-xl: 3.2rem;
  --fh-radius-pill: 999rem;
  --fh-border-width: max(1px, 0.1rem);
  --fh-border-width-strong: max(2px, 0.2rem);

  /* depth */
  --fh-shadow-1: 0 0.1rem 0.3rem rgba(0, 0, 0, 0.28), inset 0 0.1rem 0 rgba(255, 255, 255, 0.08);
  --fh-shadow-2: 0 0.8rem 2.4rem rgba(0, 0, 0, 0.36), inset 0 0.1rem 0 rgba(255, 255, 255, 0.10);
  --fh-shadow-3: 0 2.4rem 6.4rem rgba(0, 0, 0, 0.50), inset 0 0.1rem 0 rgba(255, 255, 255, 0.12);
  --fh-glow-accent: 0 0 0 0.1rem rgba(140, 185, 255, 0.40), 0 0 2.4rem rgba(43, 111, 230, 0.45);
  --fh-focus-ring: 0 0 0 0.2rem var(--fh-bg-surface), 0 0 0 0.4rem var(--fh-accent-secondary);

  /* materials */
  --fh-blur-thin: 1.2rem;
  --fh-blur-regular: 2.4rem;
  --fh-blur-thick: 4rem;
  --fh-material-thin: rgba(19, 22, 29, 0.72);
  --fh-material-regular: rgba(19, 22, 29, 0.82);
  --fh-material-thick: rgba(19, 22, 29, 0.88);

  /* motion */
  --fh-duration-fast: 120ms;
  --fh-duration-enter: 220ms;
  --fh-duration-exit: 140ms;
  --fh-duration-slow: 420ms;
  --fh-ease-standard: cubic-bezier(0.23, 1, 0.32, 1);
  --fh-ease-spring: cubic-bezier(0.34, 1.4, 0.64, 1);
}
```

Mapping to the shared Open Design schema in `tokens.css` (px = rem × 10): `--bg` = `bg-base`, `--surface` = `bg-surface`, `--surface-warm` = `bg-elevated`, `--fg` / `--fg-2` / `--muted` = the three text tokens, `--accent` = `accent-primary`, `--accent-on` = `text-on-accent`, `--warn` = `warning`, `--text-xs…4xl` = `text-2xs, sm, md, lg, xl, 2xl, 3xl, 4xl`, `--radius-sm/md/lg` = `radius-sm/md/lg`, `--focus-ring` = `focus-ring`.

## 9. Layout, scaling and safe zones

**Scaling rule.** `html { font-size: clamp(8px, calc(100vh / 108), 16px) }`; every size is in rem. 1rem is 10px at 1080p, 13.33px at 1440p, 16px at 2160p and floors at 8px at 720p — so at 720p everything is 20 % larger than strict proportion, which keeps `text-sm` at 12px. Consequence for layout: the usable canvas is **192 × 108 rem** at 16:9 above 864p, but only **160 × 90 rem** at 1280 × 720. Every screen is designed to fit 156 × 84 rem; full-screen views centre their content and let the world or `bg-base` fill the rest. Ultrawide (21:9) widens the canvas; HUD anchors to the corners and panels stay centred.

**Safe zone.** HUD and edge-anchored elements keep `space-8` (3.2rem) from every screen edge. The centre ellipse (60 % width × 50 % height) holds nothing during gameplay except the interaction hint, the progress bar and the radial menu.

**HUD screen map (1080p reference, gameplay):**

| Region | Content |
| --- | --- |
| Top left | Chat (inactive messages fade) |
| Top right | Money (cash, bank), job chip, ammo when armed; notifications stack below |
| Bottom left | Minimap frame with street, zone and compass above it; voice/radio pill and vitals row to its right |
| Bottom centre | Progress bar (`bottom: 14rem`), interaction hint above it (`bottom: 22rem`) |
| Bottom right | Vehicle HUD while in a vehicle |

**Panel sizes:** dialog 52rem wide; standard panel 96 × 64rem; wide panel (inventory, shop, garage, crafting, bank) up to 140 × 76rem; tablet (MDT, EMS, admin) 148 × 82rem; phone 36 × 74rem anchored bottom right with `space-8` margin.

**Input model.** HUD is not focusable and has no cursor. Every panel, menu and dialog sets NUI focus with cursor when it opens and releases it when it closes. `Esc` closes the topmost layer (dialog → panel → nothing); `Tab` / `Shift+Tab` move focus; `Enter` activates the focused control; arrow keys move within lists, grids and segments. Every panel shows its close affordance as a 3.2rem round glass button with an × icon in the top-right corner, labelled "Schließen" for screen readers.

## 10. Shared primitives and state patterns

These primitives build every screen in sections 11–17. A screen section only names what differs.

**Buttons** (height 4.4rem, `text-md` semibold, `radius-pill`, padding 0 `space-6`):

| Variant | Look | Use |
| --- | --- | --- |
| Primary | `accent-primary` fill, `text-on-accent` | The one main action of a view |
| Secondary | `bg-elevated` fill, `text-primary`, `border` | Every other action |
| Plain | No fill, `accent-secondary` text | Inline and low-weight actions ("Alle anzeigen") |
| Destructive | `danger` at 18 % over `bg-elevated`, `danger` text, `danger` 40 % border | Delete, fire, ban, decline |
| Icon | 4.4rem circle, `bg-elevated`, icon `text-primary` | Close, back, steppers |

States for every button: default; hover (`hover` fill +6 % white, `duration-fast`); pressed (`scale(0.97)`, fill −8 %); focus-visible (`focus-ring`); disabled (opacity 0.4, no pointer, reason in a tooltip or helper line below); busy (label replaced by a 1.6rem spinner, width kept, control disabled). Dense tools use a 3.6rem compact height with `text-sm`.

**Inputs.** Height 4.4rem, `bg-elevated`, `border`, `radius-sm`, label above in `text-sm` medium `text-secondary`, helper below in `text-xs` `text-muted`. Focus: `border-width-strong` `accent-secondary`. Error: `border-width-strong` `danger`, helper replaced by the error in `danger` with a warning glyph. Disabled: opacity 0.5. Numeric fields have − / + steppers and accept arrow keys. Search fields are `radius-pill` with a magnifier glyph.

**Segmented control.** Track `material-thin` on `bg-elevated`, `radius-pill`; selected segment `accent-primary` fill with `text-on-accent`; switching slides the fill over `duration-fast`.

**Toggle.** 5.2 × 3.2rem; off = `bg-elevated` with `border`; on = `accent-primary`; knob white with `shadow-1`, moves with `ease-spring`.

**Rows.** Min height 5.2rem, padding `space-3` `space-4`, `radius-sm`. Hover `bg-elevated`; selected `bg-elevated` plus a 0.3rem `accent-secondary` bar at the leading edge; row separators `border` inset by `space-4`.

**Badges.** `text-xs` semibold, `radius-pill`, padding 0.2rem 0.8rem; tinted: colour at 18 % over the panel with the colour as text (panels only); solid: colour fill with `bg-base` text.

**Tabs.** Text tabs with a 0.3rem `accent-secondary` underline on the selected one; `text-md` medium; `text-secondary` → `text-primary` when selected.

**Scrim.** `bg-overlay` full screen under every modal panel, on top of the game screen blur (`TriggerScreenblurFadeIn`); both fade in over `duration-enter` and out over `duration-exit`.

### State patterns (used by every screen)

| State | Drawing | Copy pattern |
| --- | --- | --- |
| **Loading** | Skeleton shapes of the filled layout in `bg-elevated` with a 1.4s shimmer of white 6 %; after 8 s a line "Dauert länger als üblich …" in `text-muted` appears under the skeleton | No spinner-only screens; spinner only inside busy buttons |
| **Empty** | Centred in the content area: 4rem line icon in `text-muted`, title `text-lg` `text-primary`, one sentence `text-sm` `text-secondary`, optional secondary button | Title says what is missing, sentence says how it fills ("Noch keine Fahrzeuge" / "Kaufe ein Fahrzeug beim Händler am Hafen.") |
| **Error (blocking)** | Same position as empty: warning glyph in `danger`, title, sentence, primary "Erneut versuchen" and, where useful, a secondary "Schließen" | Title names the failure, sentence names the consequence, never a stack trace; an error code in `text-muted` mono at the bottom for support ("Fehlercode GAR-204") |
| **Error (inline)** | Banner at the top of the content: `danger` 14 % over `bg-elevated`, `danger` glyph, text `text-primary`, × to dismiss | For a failed action while the content stays usable |
| **Filled** | The normal layout | — |
| **Offline / no connection** | Inline banner in `warning` tint: "Verbindung zum Server unterbrochen – Änderungen werden nicht gespeichert." Actions that write are disabled | — |

Every screen section lists these four states (loading, empty, error, filled) with its own content, plus the extra states it has.

## 11. Session flow

### 11.1 Loading screen

**For whom:** every player while the client downloads resources (30 s to several minutes). **Canvas:** `bg-base` with a slow (60 s) cross-fade of three harbour artworks at 40 % opacity under a vertical gradient to `bg-base` at the bottom; no video audio by default.

**Layout.** Centre-left: wordmark "HARBOUR" `text-3xl` bold, tracking −0.022em, subline "Roleplay" `text-lg` `text-secondary`. Bottom (full width minus `space-16` margins): a `material-thin` glass card 8.8rem high holding the progress capsule (0.6rem high, `radius-pill`, track white 10 %, fill `accent-secondary`), the stage label left ("Ressourcen werden geladen · 312 von 486"), the percentage right in tabular numerals. Right column: glass card "Gut zu wissen" with the rotating tip (rotates every 9 s, cross-fade), below it "Neuigkeiten" with two short entries. Top right: a 4.4rem round glass button for music (speaker glyph) plus a volume slider that appears on hover.

**States.**
- Loading (the filled state of this screen): progress advances by stage — "Verbindung wird hergestellt", "Ressourcen werden geladen · n von m", "Karte wird vorbereitet", "Charaktere werden geladen".
- Stalled: no progress for 20 s → the stage label adds "· dauert länger als üblich" in `text-muted`; nothing turns red, the game is still loading.
- Error: the loading screen only shows the client's own connection errors when the server hands them over: the bottom card turns into an inline error banner "Verbindung fehlgeschlagen – Der Server antwortet nicht." with the error code; the game itself owns retry.
- Empty: not applicable (no news → the "Neuigkeiten" card is not drawn).

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Music button | Click / `Space` | Toggles music | Music muted or playing; icon switches speaker ↔ speaker-slash; choice remembered for next load |
| Volume slider | Drag / arrow keys | Sets music volume 0–100 % | Volume applied live and remembered |
| Tip card | none | Rotates automatically | — |

### 11.2 Multi-character selection

**For whom:** every player after loading. **Canvas:** the game camera shows the selected character standing in a harbour scene; NUI draws on top. A left-to-right gradient from `bg-base` 80 % to transparent keeps the left column readable.

**Layout.** Left column (44rem, `space-12` from the left edge): title "Wähle deinen Charakter" `text-xl`, subline "3 von 4 Plätzen belegt" `text-sm` `text-secondary`. Below, a vertical list of character cards (`material-regular`, `radius-lg`, 9.6rem high): name `text-lg`, job dot + job and rank `text-sm` `text-secondary`, last played and cash/bank in `text-xs` `text-muted`. Selected card: `bg-elevated` fill and `glow-accent`. Empty slot card: dashed `border`, plus glyph, "Neuen Charakter erstellen". Locked slot (supporter perk): lock glyph, "Platz gesperrt", `text-muted`. Bottom of the column: primary "Spielen" (full column width), secondary icon button "Löschen" (trash glyph) to its right.

**States.**
- Loading: three skeleton cards.
- Empty (first visit, no characters): the card list is replaced by an empty state "Noch kein Charakter" / "Erstelle deinen ersten Charakter, um die Stadt zu betreten." with primary "Charakter erstellen".
- Error: "Charaktere konnten nicht geladen werden" / "Deine Daten sind sicher. Versuche es in einem Moment erneut." + "Erneut versuchen".
- Filled: as drawn.
- Deleting: confirm dialog (section 15.4, destructive, the character's full name typed to confirm).

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Character card | Click / arrow keys | Selects the character | Camera cross-fades to that character's ped (`duration-slow`); "Spielen" now targets it |
| Character card | Double-click / `Enter` | Selects and plays | Same as "Spielen" |
| Empty slot | Click / `Enter` | Opens the character creator | Transition to 11.3 |
| "Spielen" | Click / `Enter` | Confirms the character | Hands over to the spawn selector (11.4) with this character |
| "Löschen" | Click | Opens the destructive confirm | On confirm: character removed, list refreshed, toast "Charakter gelöscht" |

### 11.3 Character creator

**For whom:** new players and players filling an empty slot. **Canvas:** the game shows the ped centred-right in front of a neutral studio; the NUI panel is a left glass column; camera controls float bottom centre.

**Layout.** Left panel 52rem × full safe height, `material-regular`, `radius-xl`. Top: step indicator "Schritt 2 von 4" with four segments (Identität, Herkunft, Aussehen, Kleidung). Content per step:
1. **Identität** — Vorname, Nachname (text inputs), Geburtsdatum (three numeric fields TT/MM/JJJJ), Geschlecht (segmented: Männlich / Weiblich), Größe (slider 150–210 cm, value right), Nationalität (select).
2. **Herkunft** — parent mix: two face pickers (horizontal strip of 6.4rem round portraits) and two sliders "Ähnlichkeit" and "Hautton" (0–100 %).
3. **Aussehen** — collapsible groups (accordion) Gesicht, Augen, Nase, Kiefer, Haare, Bart, Augenbrauen, Makeup; each feature is a slider −1…+1 with a centre tick or a stepper ‹ 12 / 38 › for styles plus a colour swatch row (12 swatches of 3.2rem).
4. **Kleidung** — the clothing controls of 16.6 in compact form, without prices.

Footer: secondary "Zurück", primary "Weiter" (last step: "Charakter erstellen"). Camera pill bottom centre: segmented "Gesicht / Körper / Füße", rotate left / right icon buttons, hint "Rechte Maustaste halten zum Drehen".

**States.**
- Loading: ped not yet streamed → the panel is interactive, the camera pill shows "Modell wird geladen …" and controls that change the ped are disabled.
- Empty: not applicable (every field starts with a default).
- Error (validation): field-level errors — "Bitte gib einen Vornamen ein.", "Namen dürfen nur Buchstaben, Bindestriche und Leerzeichen enthalten.", "Du musst mindestens 18 Jahre alt sein.", "Dieser Name ist bereits vergeben." "Weiter" stays enabled; pressing it focuses the first invalid field.
- Error (save failed): inline banner "Charakter konnte nicht gespeichert werden." with "Erneut versuchen"; entered data stays.
- Filled: as drawn; creating: primary button busy, panel locked.

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Step segments | Click a completed step | Jumps to that step | Content swaps (cross-fade `duration-fast`) |
| Text / numeric fields | Typing | Edits identity | Validated on blur |
| Sliders | Drag / arrows (Shift = ×10) | Changes a face or body value | Ped updates live |
| Style stepper | ‹ / › / arrows | Cycles styles | Ped updates live; counter "12 / 38" |
| Colour swatch | Click / arrows + `Enter` | Picks a colour | Ped updates live; selected swatch ringed with `border-width-strong` white |
| Camera segments / rotate | Click / hold right mouse | Moves the game camera | Camera transition `duration-slow` |
| "Weiter" | Click / `Enter` | Validates the step | Next step, or first invalid field focused |
| "Charakter erstellen" | Click | Saves | Character stored; hands over to the spawn selector with "Erster Tag" spawn |
| Close (×) / `Esc` | — | Asks before discarding | Confirm "Erstellung abbrechen?" → back to character selection |

### 11.4 Spawn selector

**For whom:** every player after choosing a character. **Canvas:** an aerial game camera over the town; NUI draws a list left and pins on the map.

**Layout.** Left glass panel 44rem: title "Wo möchtest du aufwachen?", list of spawn points as rows (glyph, name, district, distance-free): "Letzter Standort" (first, with time "vor 2 Std."), "Wohnung · Speicherstadt", "Hafen · Fischmarkt", "Bahnhof", "Motel · Reeperbahn", job spawn "Wache · Davidwache" (only for police, `job-police` dot). Selected row = selected-row pattern. Map pins: 3.2rem glass circles with glyph; selected pin `accent-primary` with `glow-accent` and a label capsule. Bottom of the panel: primary "Hier aufwachen".

**States.**
- Loading: skeleton rows; pins hidden.
- Empty: impossible by design (at least "Letzter Standort" or the public spawns exist); if the server returns none, show the blocking error.
- Error: "Spawnpunkte konnten nicht geladen werden" + "Erneut versuchen".
- Disabled point: row `text-muted` with reason ("Wohnung · noch nicht gekauft").
- First character: only "Erster Tag · Bahnhof" is offered, with the sentence "Neue Bürger kommen am Bahnhof an."
- Filled: as drawn; spawning: primary busy, then the screen fades to the game (`duration-slow`).

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Row / pin | Click / arrows | Selects a spawn | Camera flies to the spot (`duration-slow`); pin highlighted |
| "Hier aufwachen" | Click / `Enter` | Spawns | Player placed; NUI closes; HUD fades in |

## 12. HUD

All HUD widgets use `material-thick` without any `backdrop-filter`, `radius-md` (pills `radius-pill`), `shadow-2`, `space-8` from the edges. Nothing in the HUD takes focus. Global HUD states: **hidden** (pause menu, cinematic camera, screenshots — `opacity 0` over `duration-exit`), **data pending** (values shown as "–", rings empty, no shimmer — the HUD must never flicker), **filled**.

### 12.1 Vitals (health, armour, hunger, thirst, stamina, stress)

**Layout.** A row of six rings to the right of the minimap, aligned to its bottom edge, gap `space-2`, each ring 5.2rem in a 6.4rem glass circle. Ring stroke 0.4rem, track white 12 %, arc in the vital colour starting at 12 o'clock, glyph 2rem centred in the vital colour. The value number is not shown permanently; it appears for 2 s under the ring (`text-xs` tabular, `text-secondary`) when it changes by ≥ 5 points.

**States per vital.**
- Normal: as drawn.
- Low (≤ 30 %; stress: ≥ 70 %): the glass circle gains a 0.1rem ring in the vital colour that pulses (1.6s).
- Critical (≤ 10 %; stress: ≥ 90 %; health additionally at 0 = unconscious): circle background becomes `danger` 22 % over `material-thick`, glyph fills, steady `danger` ring.
- Hidden when idle (setting "Volle Werte ausblenden", default on): hunger, thirst and stamina at 100 %, stress at 0 % and armour at 0 % collapse (width → 0, `duration-exit`); health always stays.
- Data pending: empty rings.

**Interactions:** none (display only). The order is fixed: health, armour, hunger, thirst, stamina, stress.

### 12.2 Voice and radio indicator

**Layout.** A pill above the vitals row: mic glyph, three range bars (Flüstern / Normal / Rufen — 1, 2 or 3 bars lit), the range word in `text-sm` `text-secondary`; when a radio is connected a divider and "Funk 101,5" with the radio glyph follow.

**States.**
- Idle: mic glyph `text-secondary`, bars `text-muted` except the active range in `text-secondary`.
- Talking: mic glyph and lit bars `hud-voice`, bars animate (600ms); the pill gains `hud-voice` 40 % border.
- Range changed: the range word swaps and stays highlighted 1.5 s.
- Muted / voice disconnected: mic-slash glyph `danger`, text "Stumm" or "Sprachchat getrennt"; the latter adds a dot pulsing.
- Radio connected: radio glyph `hud-radio`, frequency `text-primary`.
- Radio transmitting: the whole pill border `hud-radio`, radio glyph filled, label "Funk 101,5 · sendet".
- Radio off: the radio part is not drawn.

**Interactions:** none in the HUD (range is cycled with the voice key; the radio has its own item UI).

### 12.3 Cash and bank

**Layout.** Top right, right-aligned stack without a panel background behind the numbers — each line is its own pill: wallet glyph + "4.250 €" (`text-lg` semibold tabular), below building glyph + "128.940 €" (`text-md`, `text-secondary`).

**States.**
- Filled: as drawn.
- Change: a delta pill slides in left of the line for 3 s — "+250 €" in `success`, "−80 €" in `danger` — while the value counts to the new total (`duration-slow`).
- Bank hidden (setting "Kontostand nur bei Änderung"): the bank line appears for 5 s after a change or while the scoreboard key is held.
- Negative bank balance: value in `danger` with a leading minus.
- Data pending: "– €".

### 12.4 Job

**Layout.** Under the money: pill with the job dot (job colour), "Polizei · Sergeant" in `text-sm` `text-primary`, and a duty word "Im Dienst" in `success` or "Außer Dienst" in `text-muted`.

**States:** on duty / off duty / unemployed ("Arbeitslos", `job-civil` dot) / multi-job (a small "2" badge, the active job shown).

### 12.5 Ammo

**Layout.** Under the job pill when a weapon is drawn: pill with the weapon name `text-sm` `text-secondary`, magazine "24" `text-lg` semibold tabular, "/ 120" `text-md` `text-muted`, and a 12-segment magazine bar.

**States.** Unarmed: hidden. Normal. Low magazine (≤ 25 %): magazine number `warning`. Empty magazine: number `danger`, label "Nachladen [R]". Reloading: the magazine bar fills over the reload time, label "Lädt nach …". No reserve: "/ 0" in `danger`. Melee or throwable: name only, count for throwables.

### 12.6 Minimap frame

**Layout.** The game draws the radar; NUI draws only a frame aligned to the radar's position: a `radius-lg` rounded rectangle 32 × 20.8rem with `border-width-strong` white 14 %, `shadow-2` outside, nothing inside (transparent). Above the frame, a glass pill: compass heading "NO 42°" (heading letters German: N, NO, O, SO, S, SW, W, NW), a divider, street "Kaistraße" `text-sm` `text-primary`, zone "Fischmarkt" `text-sm` `text-secondary`, postal "PLZ 2041" `text-xs` `text-muted` mono.

**States.** On foot (frame shown, radar small); in a vehicle (frame grows to the game's vehicle radar size over `duration-enter`); radar disabled (no frame, the location pill stays); no GPS signal (tunnel/interior: street "Kein GPS-Signal", heading hidden); waypoint set (a distance "1,2 km" in `accent-secondary` after the street).

## 13. Vehicle HUD

**Layout.** Bottom right cluster in one glass widget 36 × 17.6rem, `radius-lg`:
- Speed: "87" in `text-4xl` bold tabular `text-primary`, unit "km/h" `text-sm` `text-secondary` under it; a 270° arc gauge (0.4rem stroke, track white 12 %, arc `accent-secondary`, tip dot with `glow-accent`) around the numerals' left side; gear "3" in a keycap-style chip.
- Status row (icons 2rem, gap `space-3`): left indicator, seatbelt, engine, lights, right indicator.
- Fuel: pump glyph + bar 14rem × 0.6rem in `hud-fuel` + "62 %" tabular.

**States.**
- Not in a vehicle: hidden.
- Seatbelt fastened: glyph `text-muted`. Seatbelt open while moving > 20 km/h: glyph `danger` filled, pulsing 1.2 s, plus a short "Anschnallen [B]" label beside the speed for 4 s after starting. Vehicles without belts (bikes, boats): glyph not drawn.
- Engine running and healthy: glyph not coloured (`text-muted`). Engine off: glyph `text-muted` with a strike line, speed area shows "Motor aus" `text-sm`. Engine damaged (< 40 % health): glyph `warning`. Engine failing (< 15 %): glyph `danger`, pulsing.
- Indicators: left / right glyph `success`, blinking 1 s at 50 % duty; hazard lights both; off = `text-muted` at 50 %.
- Lights: off hidden, low beam `text-secondary`, high beam `info`.
- Fuel: normal `hud-fuel`; low (≤ 15 %) bar and value `warning` with "Tank fast leer"; empty (0 %) `danger`, engine stops; electric vehicles show a battery glyph and "Akku" — same colours.
- Speed limiter / cruise control: a chip "Tempomat 50" in `accent-secondary` above the speed.
- Boats and aircraft: unit "kn", altitude chip "ALT 320 m" for aircraft.

**Interactions:** none (display only).

## 14. Feedback

### 14.1 Notifications (four types)

**Layout.** Top right under the money/job stack, width 38rem, max four visible, newest on top, gap `space-2`. Card: `material-thick`, `radius-md`, padding `space-4`; leading 3.6rem circle in the type colour at 18 % with the type glyph in the type colour; title `text-md` semibold `text-primary`; body `text-sm` `text-secondary` (max three lines, then ellipsis); trailing timestamp "jetzt" `text-xs` `text-muted`; a 0.2rem bottom hairline in the type colour shrinking over the lifetime.

| Type | Colour | Glyph | Lifetime | Example |
| --- | --- | --- | --- | --- |
| Info | `info` | i in circle | 5 s | "Neue Nachricht" / "Jonas: Bin in 5 Minuten am Fischmarkt." |
| Success | `success` | check | 4 s | "Zahlung erfolgreich" / "Rechnung #2041 über 380 € bezahlt." |
| Warning | `warning` | triangle | 7 s | "Tank fast leer" / "Noch etwa 6 km Reichweite." |
| Error | `danger` | x in circle | 8 s | "Kauf fehlgeschlagen" / "Nicht genug Bargeld. Es fehlen 120 €." |

**States.** Entering (slide from `translateX(2.4rem)`, `duration-enter`, `ease-spring`); visible; leaving (fade + `translateX(1.2rem)`, `duration-exit`); stacked overflow (a fifth notification collapses the oldest into a "+2 weitere" pill); persistent (no hairline, stays until acted on: incoming call, dispatch assignment); grouped (same title within 3 s → count badge "×3" instead of a new card).

**Interactions.** In gameplay none (no cursor). When a panel gives the cursor: click a card → dismisses it, or opens its source when it has one (message → phone conversation); persistent cards have up to two compact buttons ("Annehmen" primary, "Ablehnen" secondary) that produce the corresponding answer to the source resource.

### 14.2 Progress bar

**Layout.** Bottom centre, 44rem glass capsule, `radius-pill`, padding `space-3` `space-5`: glyph of the action, label "Reifen wird gewechselt …" `text-sm` `text-primary`, percentage right tabular `text-secondary`, a 0.6rem bar under the text (`accent-secondary` fill on white 12 % track). Optional cancel hint right: keycap "X" + "Abbrechen".

**States.** Running; cancellable / not cancellable (no hint); cancelled (bar turns `danger`, label "Abgebrochen", leaves after 800 ms); done (bar full, glyph → check in `success`, leaves after 600 ms); failed (label replaced by reason "Werkzeug fehlt", `danger`).

**Interactions.** `X` (when cancellable) → cancels; produces the cancel event to the action owner; the action rolls back.

### 14.3 Interaction hint "[E] …"

**Layout.** Bottom centre above the progress-bar position, glass capsule `radius-pill`: keycap "E" + label "Kofferraum öffnen" `text-md` medium. Several options stack vertically, the primary one first: "[E] Kofferraum öffnen", "[G] Abschließen". Object hints (third-eye style) use the context menu (15.2) instead.

**States.** Available; hold-to-confirm ("[E] gedrückt halten · Tresor knacken": a ring around the keycap fills `accent-secondary` over the hold time; releasing early empties it over `duration-exit`); disabled (keycap and label `text-muted`, reason in `text-xs` after a dot: "Abgeschlossen"); appearing/leaving (fade + 0.8rem rise, `duration-enter` / `duration-exit`).

**Interactions.** The named key → runs the action; produces the action of the owning resource; the hint hides while the action's progress bar runs.

### 14.4 Death / unconscious screen

**Canvas.** The world stays visible under the game screen blur and `bg-overlay`; a vignette of `bg-base` 60 % at the edges.

**Layout.** Centred glass card 56rem, `material-regular`, `radius-xl`, padding `space-10`: heart-pulse glyph 4rem in `hud-health`; title "Du bist bewusstlos" `text-3xl`; sentence "Halte durch – Hilfe kann unterwegs sein." `text-md` `text-secondary`; a large timer "04:32" `text-2xl` tabular with the label "bis du im Krankenhaus aufwachen kannst"; two key rows: "[G] Notruf absetzen" and "[E] gedrückt halten · Im Krankenhaus aufwachen" (disabled until the timer ends); footer `text-xs` `text-muted`: "Wenn du im Krankenhaus aufwachst, verlierst du Bargeld und mitgeführte Gegenstände."

**States.**
- Unconscious, timer running: as drawn, respawn row disabled.
- Emergency call sent: the G row becomes "Notruf abgesetzt · 2 Rettungskräfte im Dienst" in `success`, no longer interactive.
- No EMS on duty: sentence becomes "Gerade ist kein Rettungsdienst im Dienst." and the timer is shortened (server rule), G row disabled with "Kein Rettungsdienst verfügbar".
- Being treated: an EMS player starts treatment → card shows progress "Du wirst behandelt …" (progress-bar pattern), both key rows hidden.
- Respawn available: timer reads "00:00", E row enabled with hold ring.
- Revived: card leaves (`duration-slow`), HUD returns, notification success "Wiederbelebt".
- Dead (server ruling, permanent death): not drawn by this screen; staff tooling only.
- Loading / empty / error: loading = timer "–:–" while the server confirms the state; empty does not apply; error = the G row shows "Notruf konnte nicht gesendet werden · [G] erneut" in `danger`.

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| G row | `G` | Sends an emergency call | EMS dispatch call with location; row state "abgesetzt" |
| E row | Hold `E` 3 s (only after timer) | Respawns | Player teleported to hospital; items/cash rule applied; screen closes |

## 15. Menus, dialogs and social

### 15.1 Radial menu

**Layout.** Screen centre, 46rem ring of `material-thick` glass, inner hole 17rem (also glass, holds the label). Up to eight segments separated by 0.2rem gaps; each segment holds a 2.4rem glyph and a `text-xs` label. Centre: the hovered segment's title `text-lg` and one line `text-sm` `text-secondary`; when nothing is hovered "Schließen". Submenus replace the ring (scale 0.96 → 1, `ease-spring`); the first segment of a submenu is "Zurück".

Top-level segments: Fahrzeug, Begleiten, Interaktion, Animationen, Rechnung, Ausweis zeigen, Job (job colour dot), Notfall.

**States.** Open (`duration-enter`, `ease-spring` from `scale(0.92)`); hovered segment (fill `accent-primary` 28 %, edge `border-width-strong` `accent-secondary`, `glow-accent`); disabled segment (glyph and label `text-muted`; the centre shows the reason "Nur im Fahrzeug" on hover); empty (no actions: the ring shows a single centre message "Keine Aktionen verfügbar"); loading (actions resolved asynchronously: segments drawn as skeleton slices for ≤ 300 ms); error (action failed: the segment flashes `danger` once and a notification explains).

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Open | Hold `F1` (or controller: hold D-pad left) | Opens the ring, cursor centred | — |
| Segment | Move pointer / stick toward it | Hovers | Centre label updates |
| Segment | Release `F1` or click | Activates | Runs the action, or opens its submenu |
| "Zurück" | Click / right click | Up one level | Parent ring |
| Close | `Esc` / release `F1` in the centre | Closes | Nothing runs |

### 15.2 Context menu (target menu)

**Layout.** Anchored next to the target or cursor, 28rem wide, `material-thick`, `radius-md`, padding `space-2`. Header: target name "Karin Futo · HH-RP 4821" `text-sm` semibold, subline `text-xs` `text-muted`. Rows 4.4rem: glyph, label `text-md`, optional keycap or chevron for submenus. Destructive rows in `danger`. Separator: `border` hairline.

**States.** Open; hovered row (`bg-elevated`); disabled row (`text-muted`, reason on the right in `text-xs`: "Keine Schlüssel"); submenu open (second menu attached to the right, or left near the screen edge); empty (target without actions: "Keine Aktionen"); loading (two skeleton rows); error (row flashes `danger`, menu stays).

**Interactions.** Click / `Enter` on a row → runs its action and closes the menu (produces the action); hover or `→` on a chevron row → opens the submenu; `Esc` / click outside → closes without action; arrow keys move.

### 15.3 Input dialog

**Layout.** Centred on the scrim, 52rem, `material-regular`, `radius-lg`, padding `space-8`: title `text-xl`, description `text-sm` `text-secondary`, fields (section 10 inputs) stacked with `space-5` gap, footer right-aligned: secondary "Abbrechen", primary verb ("Überweisen", "Rechnung senden", "Einstellen").

Example drawn: "Geld überweisen" — Empfänger (Kontonummer, mono, placeholder "DE00 0000 0000"), Betrag (numeric with € suffix, helper "Verfügbar: 128.940 €"), Verwendungszweck (text, optional, 0/60 counter).

**States.** Default; focused field; validation error ("Betrag muss größer als 0 € sein.", "Nicht genug Guthaben.", "Konto nicht gefunden."); submitting (primary busy, fields disabled); submit failed (inline banner top of the dialog, fields kept); empty (fields at their defaults; primary disabled until required fields are filled); loading (dialog needs remote data — e.g. account list — fields shown as skeletons).

**Interactions.** `Enter` in the last field or primary click → validates and submits; produces the values to the caller and closes on success. "Abbrechen" / `Esc` / × → closes; produces "cancelled" to the caller.

### 15.4 Confirm dialog

**Layout.** Centred, 44rem, `material-regular`, `radius-lg`, padding `space-8`, text centred: glyph 4rem (warning glyph `warning` for caution, trash glyph `danger` for destructive), title `text-xl`, body `text-md` `text-secondary`, buttons full-width stacked: confirm first, cancel second (Apple alert order on narrow alerts).

**States.** Caution (primary = `accent-primary`); destructive (confirm = destructive button, `Enter` does not confirm — focus starts on "Abbrechen"); typed confirmation (for irreversible actions: field "Gib KARIN MÜLLER ein, um zu bestätigen"; confirm disabled until it matches); busy; failed (inline banner). Loading and empty do not apply; error = failed.

**Interactions.** Confirm → produces "confirmed" to the caller and closes after success; cancel / `Esc` → "cancelled".

### 15.5 Chat

**Layout.** Top left, 64rem wide, `space-8` margins. Inactive: the last 6 messages, each on its own `material-thick` row capsule (`radius-sm`, padding `space-1` `space-3`), fading out 8 s after arrival. Active (`T`): one glass panel `material-regular` `radius-lg`, 64 × 36rem, scrollable history, input row at the bottom (`radius-pill` field, placeholder "Nachricht oder /befehl …"), command suggestions appear as a menu above the input (command `text-sm` mono `text-primary`, arguments `text-muted`, description `text-xs`).

Message types (prefix chip + text):

| Type | Chip | Text style |
| --- | --- | --- |
| Local / OOC | "OOC" `bg-elevated` | `text-primary` |
| /me | none, name then action | italic `text-secondary` ("* Jonas zieht die Mütze tiefer ins Gesicht") |
| /do | "DO" `bg-elevated` | `text-secondary` |
| Twitter-style / news | "News" `info` tint | `text-primary` |
| Staff | "Team" `accent-primary` solid | `text-primary` |
| System | glyph `info` | `text-muted` |
| Error | glyph `danger` | `danger` text inside the panel |

**States.** Inactive (fading rows); active; empty ("Noch keine Nachrichten. Drücke T, um zu schreiben." in the active panel only); loading (history fetched after reconnect: skeleton rows); error (send failed: the own message row shows `danger` "Nicht gesendet · erneut" link); rate-limited ("Langsam – du kannst in 3 s wieder schreiben.", input disabled with countdown); unknown command ("Unbekannter Befehl /reprair – meintest du /repair?").

**Interactions.** `T` opens with focus in the input; typing `/` opens suggestions (arrows + `Tab` complete); `Enter` sends (produces the message or command to the server; field clears); `↑` recalls the last sent line; `PgUp/PgDn` and wheel scroll history; `Esc` closes without sending.

### 15.6 Scoreboard

**Layout.** Held `Home`/`Tab` (server setting): centred panel 96 × 64rem. Header: title "Spieler" with "48 / 128" `text-secondary`, server uptime "seit 6 Std. online" `text-xs` `text-muted`. Job strip: four counters with job dots — Polizei 6, Rettungsdienst 3, Mechaniker 2, Zivil 37. Search field. Table: ID (mono, `text-secondary`), name, Spielzeit, Ping (tabular; ≥ 150 ms `warning`, ≥ 300 ms `danger`), own row highlighted (`bg-elevated`, "Du" badge). Sort by ID / name / ping via column headers.

**States.** Loading (8 skeleton rows); empty search ("Kein Spieler mit „Kaltenb“ gefunden."); error ("Spielerliste nicht verfügbar"); filled; staff view (extra column "Meldungen" with a count badge).

**Interactions.** Hold key → shows, release → hides (no focus); with the cursor key (`Alt`) focus is given: search typing filters (produces the filtered list), header click sorts, row click for staff opens the admin panel on that player.

## 16. Economy and world screens

All are centred panels on the scrim with a header row: glyph, title `text-xl`, context subline `text-sm` `text-secondary`, close button. Concentric radii: panel `radius-lg` (2.2rem) with padding `space-6`, inner cards `radius-sm`.

### 16.1 Inventory

**Layout.** 140 × 76rem panel split in two columns + detail rail:
- Left "Taschen" — weight capsule "24,5 / 40 kg" (bar `accent-secondary`; ≥ 85 % `warning`; 100 % `danger`), grid 5 × 5 slots of 9.6rem (`bg-elevated`, `radius-sm`), item image centred, count bottom-right `text-xs` tabular, durability bar 0.3rem at the bottom in `success`/`warning`/`danger`. Slots 1–5 are the hotbar: number badge top-left.
- Right — the second container with its own header: "Boden", "Kofferraum · Karin Futo", "Handschuhfach", "Schrank", "Spieler durchsuchen", same grid and weight.
- Detail rail (30rem) — selected item: large image, name `text-lg`, description `text-sm` `text-secondary`, facts table (Gewicht, Haltbarkeit, Seriennummer mono), actions "Benutzen" primary, "Geben", "Teilen", "Wegwerfen" (destructive).

**States.** Loading (grid of skeleton slots); empty own inventory ("Deine Taschen sind leer."); empty container ("Hier liegt nichts."); error (transfer rejected: the dragged item returns to its slot with a 2-cycle shake, notification error with reason "Zu schwer – im Kofferraum sind noch 1,5 kg frei."); locked container ("Abgeschlossen · Schlüssel erforderlich" empty-state style with lock glyph); full; drag in progress (ghost item at 80 % opacity follows the cursor, target slot `border-width-strong` `accent-secondary`, invalid target `danger`); item selected (slot `border-width-strong` `accent-secondary`); offline banner.

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Slot | Click | Selects the item | Detail rail shows it |
| Slot | Drag to slot | Moves or swaps | Server move; on reject, item returns |
| Slot | Drag to other container | Transfers | Server transfer; weights update |
| Slot | `Shift`+click | Quick transfer whole stack | Same |
| Slot | `Ctrl`+drag | Splits | Input dialog "Menge teilen" (numeric) → split stack |
| Slot | Right click | Opens the context menu | Benutzen / Geben / Teilen / Wegwerfen |
| "Benutzen" | Click / `Enter` | Uses the item | Item effect; panel may close (e.g. eating starts a progress bar) |
| "Geben" | Click | Gives to nearest player | Picker of nearby players (context-menu style) → transfer |
| "Wegwerfen" | Click | Drops | Confirm for ≥ 1 valuable item; item moves to "Boden" |
| Hotbar `1–5` | Key in gameplay | Uses / equips the hotbar item | Same as "Benutzen" |

### 16.2 Phone

**Layout.** Bottom right, 36 × 74rem device: `bg-base` body with `radius-xl` (3.2rem) screen inset by 0.8rem, a small camera pill at the top (generic, unnamed), status bar (time "14:32", signal bars, battery). Home screen: 4-column grid of 6rem app tiles (`radius-md` squircles, each a flat colour from the palette at 22 % over `bg-elevated` with a white glyph), labels `text-xs`. Apps: Nachrichten, Telefon, Kontakte, Bank, Garage, Karte, Kamera, Rechnungen, Notizen, Einstellungen, Dispatch (job only), Inserate. Dock of four. Home indicator bar at the bottom.

App drawn: **Nachrichten → conversation** — header with back chevron and contact "Jonas Petersen", message bubbles (own: `accent-primary` with `text-on-accent`; other: `bg-elevated` with `text-primary`), timestamp separators, input pill + send button.

**States.** Opening (rises from `translateY(4rem)`, `duration-enter`); locked (lock screen: time `text-3xl`, notifications list, "Zum Entsperren tippen"); loading app (app header + skeleton content); empty (Nachrichten: "Keine Unterhaltungen" + "Neue Nachricht"); error ("Kein Netz" in the status bar, sending fails with a `danger` "!" next to the bubble and "Nicht zugestellt · Tippen zum Wiederholen"); no signal zone (status bar "Kein Netz", apps that need network show an empty-state "Kein Netz – im Tunnel oder Keller ist kein Empfang."); incoming call (full-screen call view: caller name `text-2xl`, "eingehender Anruf", two 7.2rem round buttons: decline `danger`, accept `success`); in call (timer, mute, speaker, hang up); low battery (battery `warning` ≤ 20 %, `danger` ≤ 5 %).

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Phone key | `M` (setting) | Opens / closes the phone | Focus to phone; character plays phone animation |
| App tile | Click | Opens the app | App view (zoom from tile, `duration-enter`) |
| Home indicator / back chevron | Click / `Backspace` | Back / home | Previous view |
| Send | Click / `Enter` | Sends message | Message to recipient; bubble state sent → delivered |
| Accept / decline | Click / `Enter` / `Esc` | Answers | Voice call starts / caller gets "abgelehnt" |
| `Esc` | — | Puts phone away | Phone slides down; call continues in a HUD pill if active |

### 16.3 Bank and ATM

**Bank (counter or app).** 132 × 76rem panel: left column of account cards (Girokonto, Sparkonto, Firmenkonto "Hafen Werkstatt GmbH" for bosses): name, IBAN-like number mono `text-xs`, balance `text-lg`; selected card `bg-elevated` + accent bar. Main: balance "128.940 €" `text-2xl` with "Verfügbar" label; actions row: "Einzahlen", "Abheben", "Überweisen" (primary), "Rechnungen"; a mini chart of the last 30 days (line `accent-secondary`, area 12 %); transaction list (date, counterparty, purpose `text-secondary`, amount right tabular: incoming `success` with "+", outgoing `text-primary` with "−").

**ATM.** 64 × 60rem panel with a stepped flow: PIN entry (4 masked dots, 3 × 4 keypad of 7.2rem round keys, "Korrektur", "Abbrechen") → amounts (quick tiles 50 / 100 / 200 / 500 € + "Anderer Betrag") → result. ATMs offer Abheben, Einzahlen and Kontostand only.

**States.** Loading (balance skeleton, list skeleton); empty transactions ("Noch keine Umsätze auf diesem Konto."); error ("Bank nicht erreichbar" blocking with retry); insufficient funds (field error "Nicht genug Guthaben. Verfügbar: 1.240 €."); PIN wrong ("PIN falsch · noch 2 Versuche", dots shake); card blocked ("Karte gesperrt – wende dich an einen Bankberater."); success (sheet "Abgehoben · 200 €", check `success`, auto-returns after 2 s); no card (ATM without card item: empty-state "Keine Bankkarte" / "Hol dir eine Karte in der Filiale am Rathausmarkt."); offline banner.

**Interactions.** Account card click → switches account (balance, chart, list update). "Einzahlen/Abheben/Überweisen" → input dialog (15.3) → on success: balance animates, transaction row inserted on top, success notification. Transaction row click → expands details (reference, time, account). ATM keypad: digits / `0–9` keys enter PIN; `Enter` confirms; after 3 wrong PINs the card is blocked.

### 16.4 Shop

**Layout.** 140 × 76rem: header "24/7 Supermarkt · Hafenstraße"; category tabs (Lebensmittel, Getränke, Werkzeug, Elektronik); product grid of cards 20 × 24rem (image on `bg-elevated`, name `text-md`, price `text-lg` tabular, stock `text-xs` `text-muted` "12 vorrätig", "+" icon button); cart rail 36rem: rows with name, stepper − 2 +, line price; summary: Zwischensumme, Steuer, Gesamt `text-xl`; payment segmented "Bar / Karte" with available amount under it; primary "Bezahlen · 46 €".

**States.** Loading (skeleton cards); empty category ("In dieser Kategorie gibt es gerade nichts."); empty cart ("Dein Warenkorb ist leer." + glyph, "Bezahlen" disabled); out of stock (card at 50 %, badge "Ausverkauft", "+" disabled); licence required (badge "Waffenschein nötig", "+" disabled, reason on hover); insufficient funds (payment line `danger` "Es fehlen 12 €", "Bezahlen" disabled); paying (busy); success (cart clears, success notification "Einkauf abgeschlossen · 46 €"); error ("Zahlung fehlgeschlagen" banner).

**Interactions.** "+" or card click → adds 1 (cart row animates in); stepper → changes quantity (to 0 removes); payment segment → switches method; "Bezahlen" → buys, produces items in the inventory and money deducted; `Esc` → closes, cart kept for 10 min at this shop.

### 16.5 Garage

**Layout.** 132 × 72rem: header "Garage · Speicherstadt"; filter tabs "Alle / Eingeparkt / Unterwegs / Abgeschleppt"; vehicle list left (rows: vehicle name `text-md`, plate chip mono "HH-RP 4821" on `bg-elevated`, state badge: Eingeparkt `success` tint, Unterwegs `info` tint, Abgeschleppt `warning` tint); detail right: large vehicle image on a soft floor gradient, name `text-2xl`, plate, three condition bars (Kraftstoff `hud-fuel`, Motor, Karosserie — `success` > 60 %, `warning` 25–60 %, `danger` < 25 %), facts (Kilometerstand, Garage, Versicherung), primary "Ausparken".

**States.** Loading (skeleton rows + image placeholder); empty ("Keine Fahrzeuge in dieser Garage" / "Fahrzeuge, die du hier einparkst, erscheinen in dieser Liste."); error ("Fahrzeuge konnten nicht geladen werden"); spawn blocked (banner "Ausfahrt blockiert – ein Fahrzeug steht im Weg."); vehicle out ("Unterwegs" → primary becomes secondary "Auf Karte zeigen"); impounded (primary "Auslösen · 500 €", destructive-free, opens confirm); job garage (header job colour edge, vehicles without ownership, primary "Dienstwagen nehmen").

**Interactions.** Row click / arrows → selects (detail updates, camera preview if the garage has a preview spot). "Ausparken" → spawns the vehicle at the exit, produces vehicle + keys, closes. "Auf Karte zeigen" → sets waypoint (produces GPS route, notification). "Auslösen" → confirm → pays fee, state → Eingeparkt.

### 16.6 Clothing store

**Layout.** Left glass panel 52rem (world and ped visible to the right): header "Kleidung · Hafen-Outlet"; category list (Oberteil, Unterhemd, Hose, Schuhe, Jacke, Kopfbedeckung, Brille, Uhr, Kette, Tasche) as rows with the current item number; open category shows two steppers: "Modell ‹ 12 / 186 ›" and "Variante ‹ 2 / 6 ›", price of the change `text-md`, "Zurücksetzen" plain button. Bottom: outfit section ("Outfit speichern" input + saved outfits list), total "Gesamt 240 €", primary "Kaufen". Camera pill bottom centre as in 11.3.

**States.** Loading (model streaming: "Kleidungsstück wird geladen …" in the camera pill, steppers locked); empty saved outfits ("Noch keine Outfits gespeichert"); unavailable item (number in `text-muted`, badge "Nicht verfügbar", skipped by the stepper unless selected directly); job-restricted ("Nur für Polizei"); insufficient funds; error (purchase failed banner, preview reverted on close); unsaved changes on close (confirm "Änderungen verwerfen?").

**Interactions.** Steppers / arrows → preview on ped live (produces nothing until bought); "Zurücksetzen" → reverts category; "Kaufen" → buys all changes, produces the outfit on the character and money deducted; "Outfit speichern" → stores the current look under the typed name (produces a saved outfit entry); saved outfit click → applies it as preview.

### 16.7 Crafting

**Layout.** 132 × 72rem: header "Werkbank · Container 14"; recipe list left (search, groups "Werkzeug / Teile / Munition", rows with output image, name, craft time); detail: output image + name `text-xl`, description; ingredients table (image, name, "vorhanden / benötigt" tabular — enough: `success` check, missing: `danger` and "fehlt 2"); quantity stepper; time "Dauer 0:45"; primary "Herstellen"; a queue strip at the bottom (up to 3 jobs, each with a small progress ring).

**States.** Loading; empty ("Noch keine Baupläne" / "Baupläne findest du bei Händlern oder als Belohnung."); missing ingredients (primary disabled, helper "Es fehlen 2 Zutaten."); skill too low (lock glyph, "Benötigt Handwerk Stufe 3"); crafting (queue job running, progress bar 14.2 also in the HUD when the panel closes); done (queue item shows check, "Abholen"); error ("Herstellung fehlgeschlagen – Zutaten wurden zurückgelegt."); inventory full ("Kein Platz im Inventar" on collect).

**Interactions.** Recipe click → detail; stepper → quantity (ingredients scale); "Herstellen" → consumes ingredients, produces a queue job; "Abholen" → moves the output to the inventory; queue item × → cancels (confirm), ingredients returned.

### 16.8 Invoice

**Recipient view.** Centred 56rem card styled as a document on glass: issuer block (job dot + "Hafen Werkstatt GmbH", address `text-sm` `text-secondary`), "Rechnung #2041" mono, date, due date; line items table (Position, Menge, Einzelpreis, Summe); totals (Netto, MwSt 19 %, Gesamt `text-2xl`); note; footer buttons "Ablehnen" (destructive secondary) and "Bezahlen · 380 €" (primary), payment source segmented "Bank / Bar".

**Issuer view.** Input dialog "Rechnung erstellen": Empfänger (nearby players picker), positions (add row button, each with text, quantity, price), note, total live; primary "Rechnung senden".

**States.** Loading; empty (issuer without positions: "Füge mindestens eine Position hinzu.", send disabled); open (default); paid (stamp-like badge "Bezahlt" in `success` solid, buttons removed); overdue (badge "Überfällig seit 3 Tagen" `warning`); declined (badge "Abgelehnt" `danger` tint); insufficient funds (payment error); error (send failed banner). The phone app "Rechnungen" lists invoices with these same badges.

**Interactions.** "Bezahlen" → pays from the chosen source (produces payment to the issuer's account, both get notifications); "Ablehnen" → confirm → declined (issuer notified); issuer "Rechnung senden" → recipient receives the invoice as a persistent notification with "Ansehen".

### 16.9 ID card

**Layout.** Card 54 × 34rem (ID-1 ratio), `material-regular` over a subtle vertical gradient of the card type colour at 10 %, `radius-md`: header "Personalausweis" `text-sm` semibold + "Freie und Hansestadt" `text-xs` `text-muted`; photo 12 × 15rem (`radius-sm`, the character mugshot); fields in two columns (label `text-xs` `text-muted`, value `text-md` `text-primary`): Name, Vorname, Geburtsdatum, Geburtsort, Staatsangehörigkeit, Größe, Gültig bis; ID number bottom mono "L01X 7K3P 9"; signature line with the name in an italic.

Types: Personalausweis (neutral), Führerschein (classes chips "A · B · C"), Waffenschein (`warning` edge), Dienstausweis (job colour edge, rank and service number).

**States.** Shown to someone (the viewer sees it bottom centre for 8 s with "von Karin Müller gezeigt" `text-xs`); own view (with buttons "Zeigen" and "Schließen"); expired (a band at the top "Abgelaufen seit 12.03." `warning` tint); revoked (Führerschein: band "Entzogen" `danger`); loading (photo skeleton); empty (no document: inventory shows nothing; not drawn); error ("Ausweis konnte nicht angezeigt werden").

**Interactions.** "Zeigen" → shows to the nearest player within 3 m (produces the card on their screen; if nobody is near: notification "Niemand in der Nähe"); `Esc` / "Schließen" → closes.

## 17. Job tools

Tablets share a frame: 148 × 82rem `material-regular`, `radius-xl`, `shadow-3`, a 0.3rem top edge in the job colour, sidebar 24rem with nav rows (glyph + label, selected = selected-row pattern), top bar with the signed-in person and status, content area with `space-6` padding. All tables: header `text-xs` medium `text-muted`, rows 4.8rem `text-sm`, zebra off, hover `bg-elevated`.

### 17.1 Police MDT

**Sidebar:** Übersicht, Personen, Fahrzeuge, Berichte, Haftbefehle, Einsätze, Beweismittel, Einheiten. **Top bar:** "Sgt. M. Petersen · 2-ADAM-12", unit status segmented "10-8 Frei / 10-6 Beschäftigt / 10-7 Außer Dienst", clock.

**Drawn view — Personen:** search field "Name, Telefonnummer oder Ausweis-ID"; results list (mugshot 4.8rem, name, DOB, flags badges: "Haftbefehl" `danger` solid, "Gefährlich" `warning`, "Waffenschein" `info` tint); profile pane: mugshot, facts grid, licences chips, linked vehicles (plate mono, model, status "Gestohlen" `danger`), records timeline (Berichte with case numbers mono "B-2025-0412"), notes field; actions "Bericht erstellen" (primary), "Haftbefehl ausstellen", "Bußgeld erteilen". Right rail: "Aktive Einsätze" cards (code "10-31 Einbruch", location, age "vor 3 Min.", assigned units chips, "Übernehmen").

**States.** Loading (list + profile skeleton); empty search ("Keine Person gefunden" / "Prüfe die Schreibweise oder suche nach der Ausweis-ID."); initial empty ("Suche nach einer Person, um ihre Akte zu öffnen."); no active calls ("Keine offenen Einsätze"); error ("Datenbank nicht erreichbar"); access denied (rank too low for Haftbefehle: lock state "Ab Rang Sergeant"); unsaved report (confirm on navigation); report saved (success notification + case number).

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Search | Type + `Enter` | Searches | Result list |
| Result row | Click / arrows | Opens profile | Profile pane |
| Status segment | Click | Sets unit status | Dispatch sees new status; top bar updates |
| "Übernehmen" | Click | Assigns own unit to the call | Waypoint set, unit chip added, call notification persistent |
| "Bericht erstellen" | Click | Opens the report editor (title, involved persons, charges multi-select with fine/jail totals, narrative textarea, evidence attach) | Saved report with case number |
| "Haftbefehl ausstellen" | Click | Opens input dialog (charges, reason) → confirm | Warrant flag on the person, visible to all officers |
| Vehicle plate | Click | Opens vehicle record | Vehicle view |

### 17.2 EMS tablet

**Sidebar:** Patienten, Einsätze, Behandlungen, Medikamente, Personal. **Top bar:** "Notärztin L. Brandt · RTW 3", status segmented as MDT.

**Drawn view — Patient:** patient header (name, age, blood type chip, allergies `warning` chip "Penicillin"); body diagram (front silhouette, eight zones: Kopf, Brust, Bauch, linker/rechter Arm, linkes/rechtes Bein, Rücken; zone fill by severity: none = white 8 %, leicht `warning` 40 %, schwer `danger` 60 %, behandelt `success` 40 %); vitals cards (Puls 112 bpm, Blutdruck 95/60, SpO₂ 93 %, Bewusstsein "somnolent") with trend arrows, out-of-range values in `danger`; treatment actions grid (Verband anlegen, Schiene, Infusion, Schmerzmittel, Defibrillator, Transport) each a compact secondary button with glyph; treatment log (time, action, by whom).

**States.** Loading; no patient selected ("Wähle einen Patienten in deiner Nähe oder aus einem Einsatz."); no patients nearby ("Kein Patient in Reichweite"); patient unconscious (header badge "Bewusstlos" `danger`, defibrillator action highlighted as primary); action in progress (progress bar 14.2); action unavailable (missing item: button disabled, "Kein Verbandsmaterial"); error ("Behandlung fehlgeschlagen"); patient stabilised (header badge "Stabil" `success`).

**Interactions.** Zone click → filters treatments to that zone and shows injuries ("Schussverletzung, schwer"); treatment button → plays animation + progress, produces the treatment on the patient and a log row; "Transport" → patient follows into vehicle (produces attach state); Einsätze tab rows → "Übernehmen" as in the MDT.

### 17.3 Boss menu

**Layout.** 132 × 76rem panel with the job edge: header "Hafen Werkstatt GmbH · Chefmenü"; KPI row of three cards (Firmenkonto "84.200 €", Mitarbeiter "12 · 5 im Dienst", Umsatz 7 Tage "+18.400 €" `success`); tabs Mitarbeiter / Ränge & Gehälter / Finanzen; Mitarbeiter table: name, rank (select inline), status dot (`success` im Dienst / `text-muted`), hired since, salary tabular, row actions (Befördern, Degradieren, Entlassen — destructive, in a row context menu); primary "Mitarbeiter einstellen". Finanzen: "Einzahlen", "Abheben", transaction list as 16.3. Ränge: editable table of ranks with salary per hour and permissions toggles.

**States.** Loading; empty employees ("Noch keine Mitarbeiter" / "Stelle Spieler in deiner Nähe ein."); error; no permission (rank without boss rights: blocking "Kein Zugriff – nur für Geschäftsführung."); hiring (input dialog with nearby players picker; success → row added); firing (confirm destructive "Jonas Petersen entlassen? Er verliert sofort Zugang zu Firmenfahrzeugen und Lager."); insufficient society funds (withdraw error); unsaved rank changes (sticky footer "Änderungen speichern / Verwerfen").

**Interactions.** Rank select → changes rank (produces new rank + salary, employee notified); "Entlassen" → confirm → removed; "Mitarbeiter einstellen" → dialog → hire (produces employee); Einzahlen/Abheben → input dialog → society balance updates; rank table edits → saved via the sticky footer.

### 17.4 Admin panel

**Layout.** Tablet frame without job edge, edge in `accent-secondary`. Sidebar: Spieler, Meldungen, Server, Ressourcen, Protokoll. Top bar: "Admin · Nordlicht", role badge "Superadmin", toggles "Unsichtbar", "Godmode" (each a toggle with label).

**Drawn view — Spieler:** search; table (ID mono, name, character name, ping, playtime, flags badges "Neu" `info`, "Gemeldet ×2" `warning`); player detail pane: identifiers list (mono, masked by default, "Anzeigen" plain), quick actions grid — Teleport zu, Zu mir holen, Zuschauen, Einfrieren, Heilen, Wiederbeleben (secondary), Kicken, Bannen (destructive); notes; recent log for this player. Server view: KPI cards (Spieler 48 / 128, Uptime 6:12 h, Server-FPS, Ressourcen 214 aktiv) and an announcement input ("Ankündigung senden").

**States.** Loading; empty search; empty reports ("Keine offenen Meldungen"); error ("Admin-API nicht erreichbar"); insufficient role (actions above the role disabled with "Nur für Superadmin"); player left (detail header "Offline seit 2 Min.", live actions disabled, ban still possible); action busy; action done (success notification "Spieler eingefroren").

**Interactions.**

| Element | Input | Does | Produces |
| --- | --- | --- | --- |
| Teleport zu / Zu mir holen | Click | Moves admin or target | Teleport; log entry |
| Zuschauen | Click | Spectates | Panel collapses to a pill "Zuschauen: ID 23 · [Esc] beenden" |
| Einfrieren / Heilen / Wiederbeleben | Click | Applies the state | State change; log entry; success notification |
| Kicken | Click | Opens input dialog (Grund, required) | Player kicked with reason; log entry |
| Bannen | Click | Opens input dialog (Grund, Dauer segmented 1 Tag / 7 Tage / 30 Tage / Dauerhaft) → typed confirm of the player name | Ban stored; player dropped; log entry |
| Meldung | Click "Übernehmen" | Claims a report | Report assigned; reporter notified |
| Ankündigung senden | Type + primary | Broadcasts | Persistent info notification to all players |

## 18. Copy

Voice: calm, direct, informal "du", short sentences, no exclamation marks except for genuine danger, no jokes in errors. Errors name what happened and what the player can do.

**Loading screen tips** (rotate in this order):
1. "Drücke T, um zu schreiben. Mit /me beschreibst du, was dein Charakter tut."
2. "Mit F1 öffnest du das Aktionsmenü – halte die Taste gedrückt und wähle mit der Maus."
3. "Schnall dich an: Mit B legst du den Gurt an. Ohne Gurt fliegst du bei einem Unfall aus dem Fahrzeug."
4. "Bargeld verlierst du, wenn du im Krankenhaus aufwachst. Dein Bankguthaben bleibt."
5. "Die Polizei erreichst du über das Telefon unter 110, den Rettungsdienst unter 112."
6. "Rechnungen kannst du in der Telefon-App „Rechnungen“ jederzeit nachsehen und bezahlen."
7. "Leise sprechen, normal sprechen, rufen: Mit der Sprachtaste wechselst du die Reichweite."
8. "Respektiere das Rollenspiel der anderen. Was im Spiel passiert, bleibt im Spiel."

**Loading screen news** (example entries, the server replaces them): "Neue Fähre zwischen Fischmarkt und Containerhafen – Abfahrt alle 20 Minuten." / "Die Werkstatt am Kai sucht Mechanikerinnen und Mechaniker. Bewerbungen im Rathaus."

**Death screen:** title "Du bist bewusstlos"; sentence "Halte durch – Hilfe kann unterwegs sein."; no EMS variant "Gerade ist kein Rettungsdienst im Dienst. Du kannst früher im Krankenhaus aufwachen."; footer "Wenn du im Krankenhaus aufwachst, verlierst du Bargeld und mitgeführte Gegenstände."

**Confirm dialogs:**
- Delete character: "Charakter löschen?" / "Karin Müller wird mit Inventar, Fahrzeugen, Wohnungen und Kontostand endgültig gelöscht. Das kann niemand rückgängig machen." / field "Gib KARIN MÜLLER ein, um zu bestätigen" / "Endgültig löschen" · "Abbrechen".
- Discard creator: "Erstellung abbrechen?" / "Alles, was du bisher eingestellt hast, geht verloren." / "Verwerfen" · "Weiter bearbeiten".
- Drop valuable: "Goldkette wegwerfen?" / "Sie bleibt hier auf dem Boden liegen. Andere können sie aufheben." / "Wegwerfen" · "Behalten".
- Fire employee: "Jonas Petersen entlassen?" / "Er verliert sofort Zugang zu Firmenfahrzeugen, Lager und Firmenkonto." / "Entlassen" · "Abbrechen".
- Ban: "Spieler bannen?" / "ID 23 · Jonas Petersen wird für 7 Tage gebannt. Grund: Metagaming. Die Entscheidung wird protokolliert." / "Bannen" · "Abbrechen".

**Generic errors:** "Das hat nicht geklappt. Versuche es gleich noch einmal." · "Verbindung zum Server unterbrochen – Änderungen werden nicht gespeichert." · "Dafür fehlt dir die Berechtigung." · "Zu weit entfernt – geh näher heran."

## 19. Accessibility and readability

- Text contrast floors: body and labels ≥ 4.5:1 against the HUD worst case (white world behind `material-thick`) — `text-primary` 11.97, `text-secondary` 7.24, `text-muted` 4.99. Non-text indicators ≥ 3:1 there (lowest: `accent-primary` is never used on the HUD; `hud-health` 4.03).
- Panels always sit on the `bg-overlay` scrim; text is never placed on the scrim alone.
- No information by colour alone: every vital, status and job colour pairs with a glyph, a word or a position.
- Focus: every interactive element shows `focus-ring` on `:focus-visible`; focus is trapped inside the topmost dialog and returned to the opener on close.
- Hit targets ≥ 4.4rem (44px at 1080p) for pointer; 3.6rem in dense tools with ≥ 0.8rem spacing.
- Keyboard and controller parity: every action reachable by keys listed in each screen; the radial menu supports stick input.
- Reduced motion per section 6. No flashing above 3 Hz (indicator blink is 1 Hz).
- Text size setting "Textgröße" (90 / 100 / 115 %) multiplies the root rule; layouts are rem-based so they grow with it.
- Colour-blind check: health (red-pink) vs stamina (lime) and success vs danger are also separated by glyph and position; protanopia renders `danger` dark but still ≥ 3:1 on surface.

## 20. Anti-patterns

- `backdrop-filter` on HUD widgets; blur as the legibility mechanism anywhere; glass thinner than `material-thick` on the HUD.
- `color-mix()`, `:has()`, container queries, CSS nesting or `corner-shape` in runtime CSS (Chromium 103).
- White or light glass; coloured glass tints (only the danger tint on critical vitals is allowed).
- More than one `accent-primary` element per view; accent as body text colour.
- Neon glows, scanlines, hexagon frames, angled "cyber" corners, gradient text.
- All-caps labels, letter-spaced headings, condensed fonts.
- Apple logos, product names, SF Pro or SF Symbols files, iPhone-identical device chrome.
- Sharp corners next to round ones; inner radii larger than outer radii.
- Spinners as the only loading feedback for a screen; empty screens without a sentence on how to fill them.
- HUD elements in the centre of the screen during gameplay; HUD widgets that take focus.
- CDN fonts or remote images at runtime.
