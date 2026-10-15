# FiveM Harbour — Plattenbau

> Category: Themed & Unique
> Variant B of the `fivem-harbour-ui` series. A north-German harbour town at night, seen from between the concrete housing blocks: asphalt-grey panels, sodium-lamp yellow, container blue, rust and signal red. Hard edges, opaque plates, texture only as a hint. Built to stay readable over the game world in FiveM NUI (CEF/Chromium, offline).

## 1. Direction and atmosphere

**Who it is for.** Players on a GTA V roleplay server (FiveM) set in a north-German harbour town: harbour crime (smuggling, container yard, docks at night) and everyday life in the prefab housing estates (Neubaublocks / Plattenbau). The UI sits on top of a moving 3D world. It is read in a glance while driving, in a firefight or during roleplay, and must never fight the scene for attention.

**The picture.** Night at the docks. Concrete slabs with visible joints, house numbers painted on the entrance ("Block 7, Aufgang B"), shipping containers with corrugated sides, rust stains, chain-link fence, wet asphalt under orange sodium street lamps. Grit comes from colour and from hints of texture, never from clutter: no graffiti, no torn paper, no distressed fonts, no parody of East-German aesthetics.

**Series anchor.** Yellow, grey and blue lead all three variants (A "Maritim", B "Plattenbau", C "Kiez"). In Plattenbau the yellow is the sodium lamp (`accent-primary` `#F2B53A`), grey is concrete and asphalt (`bg-*`, `border`), blue is the container (`accent-secondary` `#2C68A0`). Rust (`warning`) and signal red (`danger`) carry state.

**Three signature details.** Use them consistently and sparingly:

1. **The house-number plate (`.code`).** Every panel header opens with a square plate outlined in `accent-primary`, holding a short code: a block number ("7"), a slot ("P1"), a station ("K1"), a count ("48") or an icon. It is the painted entrance number of a Plattenbau block.
2. **The lamp line.** Every panel carries a 2px `accent-primary` top edge, the only warm light in an otherwise cold surface. Danger panels (confirm-destroy, admin) swap it for `danger`.
3. **Slab bars.** Every quantity bar (vitals, fuel, progress, weight, loading) is cut into ten equal slabs with 2px joints, like a prefab facade.

**What it is not.** Not futuristic: no neon glows, no glassmorphism, no sci-fi brackets, no gradients on surfaces. Not cosy: no rounded pills, no soft drop shadows as decoration. Not loud: one accent per view, colour only where it means something.

## 2. Colour tokens

All colours are opaque except `bg-overlay`. Contrast follows WCAG 2.x (relative luminance). Text pairs need 4.5:1 (3:1 at 18.66px bold / 24px regular and up); non-text UI parts need 3:1.

HUD colours are measured against the **worst case** a HUD plate meets: `bg-overlay` (88 % `#0D0F11`) composited over pure white, which yields `#2A2C2E`. Over a black scene the same plate yields `#0B0D0F`, so every HUD figure only improves at night.

### Surfaces and lines

| Token | Hex | Usage | Contrast | Measured against |
|---|---|---|---|---|
| `bg-base` | `#111315` | Full-screen backgrounds, input wells, panel footers, empty inventory slots | 15.36:1 | `text-primary` on it |
| `bg-surface` | `#1A1D20` | Panels, cards, dialogs, menus, tablets | 13.96:1 | `text-primary` on it |
| `bg-elevated` | `#24282C` | Hover, selected row, filled slot, chips, tiles | 12.24:1 | `text-primary` on it |
| `bg-overlay` | `#0D0F11E0` = `rgba(13,15,17,0.88)` | Every HUD plate and toast over the game world | 11.56:1 / 16.06:1 | `text-primary` on it, over white / over black |
| `border` | `#3B4045` | Slab joints: dividers, panel and card outlines, row separators (decorative only) | 1.62:1 | `bg-surface` |

`border` is deliberately quiet and is never the only thing that identifies a control. Interactive edges (inputs, steppers, ghost buttons, segmented controls, toggles) use `text-muted` as their outline: 6.17:1 against `bg-surface`.

### Text

| Token | Hex | Usage | Contrast | Measured against |
|---|---|---|---|---|
| `text-primary` | `#ECE9E2` | Body text, values, numbers, titles: warm off-white, concrete under a lamp | 13.96:1 | `bg-surface` |
| `text-secondary` | `#B3B5B2` | Descriptions, labels, secondary values, toast body | 8.20:1 | `bg-surface` |
| `text-muted` | `#989D9F` | Meta, timestamps, placeholders, disabled labels, edges of inputs | 6.17:1 (5.41:1 on `bg-elevated`, 5.11:1 on overlay over white) | `bg-surface` |
| `text-on-accent` | `#14130F` | Text and icons on yellow and on every coloured fill (keycaps, danger button, status-colour keys) | 10.13:1 | `accent-primary` |

### Accents and states

| Token | Hex | Usage | Contrast | Measured against |
|---|---|---|---|---|
| `accent-primary` | `#F2B53A` | Sodium yellow: the one primary action per view, focus ring, keycaps, active tab underline, lamp line, house-number plate | 9.23:1 | `bg-surface` |
| `accent-secondary` | `#2C68A0` | Container blue: selected fill in segmented controls and camera presets, secondary action buttons, EU strip on number plates. A fill, never text on dark | 4.82:1 | `text-primary` on it |
| `success` | `#6CC08B` | Stairwell green: paid, done, on duty, materials complete, indicators | 7.70:1 | `bg-surface` |
| `warning` | `#EE8A34` | Rust orange: running low, due, caution, low ammo, seatbelt off, overweight | 6.71:1 | `bg-surface` |
| `danger` | `#EA5D47` | Signal red: errors, destructive actions, warrants, critical health. On `bg-elevated` it drops to 4.35:1, so danger text there is ≥ 18.66px bold or sits on `bg-surface`/`bg-base` | 4.96:1 | `bg-surface` |
| `info` | `#6AAEE8` | Notices, "open", "new", info toasts, links | 7.12:1 | `bg-surface` |

On coloured fills, text is `text-on-accent`: 8.45:1 on `success`, 7.36:1 on `warning`, 5.45:1 on `danger`, 7.82:1 on `info`.

### Jobs

| Token | Hex | Usage | Contrast | Measured against |
|---|---|---|---|---|
| `job-police` | `#5C9AE6` | Police: job chip square, MDT house-number plate, unit identity | 5.82:1 | `bg-surface` |
| `job-ems` | `#EF6476` | Ambulance service: chip, EMS tablet plate. Cooler and pinker than `danger` so the two never read as one | 5.44:1 | `bg-surface` |
| `job-mechanic` | `#3FBFAE` | Garage/mechanic: chip, company plate (oil-blue overalls) | 7.48:1 | `bg-surface` |
| `job-civil` | `#A9AEB2` | Civilian / unemployed | 7.56:1 | `bg-surface` |

A job colour appears only as an 8px square inside a chip, as a house-number plate outline, or as a dot. It never fills a panel.

### HUD

| Token | Hex | Usage | Contrast over white | Contrast over black |
|---|---|---|---|---|
| `hud-health` | `#EE6A5E` | Health ("Leben") | 4.58:1 | 6.36:1 |
| `hud-armor` | `#5DA2E8` | Armour ("Panzerung") | 5.21:1 | 7.23:1 |
| `hud-hunger` | `#E39A3B` | Hunger | 5.97:1 | 8.30:1 |
| `hud-thirst` | `#46C0DB` | Thirst ("Durst") | 6.56:1 | 9.11:1 |
| `hud-stamina` | `#8BCB6A` | Stamina ("Ausdauer") | 7.24:1 | 10.06:1 |
| `hud-stress` | `#B596E3` | Stress | 5.63:1 | 7.82:1 |
| `hud-voice` | `#F5C64C` | Voice indicator while speaking | 8.72:1 | 12.11:1 |
| `hud-radio` | `#4FD3B5` | Radio channel while transmitting ("Sendet") | 7.55:1 | 10.49:1 |
| `hud-fuel` | `#A9BFCF` | Fuel ("Tank") | 7.37:1 | 10.23:1 |

Columns: measured against `bg-overlay` composited over white (`#2A2C2E`) and over black (`#0B0D0F`). HUD numbers themselves are always `text-primary`; the HUD colour marks the icon and the bar fill. Each vital is told apart by its icon as well as its hue, so the HUD still works for colour-blind players.

## 3. Typography

Three open-licence families (SIL OFL 1.1), shipped as woff2 in `fonts/` and declared in `manifest.json`. FiveM NUI runs offline in CEF, so there is no CDN, no Google Fonts URL and no runtime download: copy `fonts/` into the resource, list the files under `files {}` in `fxmanifest.lua`, reference them with relative `url()`s, and use `font-display: block` so the HUD never flashes a fallback.

| Role | Family | Weights | Files | Used for |
|---|---|---|---|---|
| Display (`--fh-font-display`) | Barlow Condensed | 500, 600, 700 | `barlow-condensed-{latin,latin-ext}-{500,600,700}-normal.woff2` | Panel titles, labels, buttons, tabs, HUD values, money, speed, keycaps. Compressed, DIN-like, the letterforms of house numbers and road signs |
| Sans (`--fh-font-sans`) | Inter (variable) | 400, 500, 600 used | `inter-{latin,latin-ext}-wght-normal.woff2` | Body text, form input, chat, descriptions, toast bodies, table cells |
| Mono (`--fh-font-mono`) | JetBrains Mono | 400, 500, 700 | `jetbrains-mono-{latin,latin-ext}-{400,500,700}-normal.woff2` | IDs, record numbers, account numbers, timestamps, timers, licence strings, MRZ line |

The `latin` subset covers German (ä ö ü ß, €, „ “). `latin-ext` carries player names from Polish, Czech, Turkish, Hungarian and similar languages; keep it, chat and scoreboard show such names.

**Scale.** Sizes are in rem; under the series root rule 1rem = 10px at 1080p.

| Token | rem | px @1080p | Face, weight | Use |
|---|---|---|---|---|
| `--fh-text-4xl` | 7.2 | 72 | Display 700 | Speedometer, loading wordmark, death title |
| `--fh-text-3xl` | 4.8 | 48 | Display 700 | Magazine count, death timer (mono 500), large balances |
| `--fh-text-2xl` | 3.4 | 34 | Display 700 | Totals, stat values, vehicle name in detail |
| `--fh-text-xl` | 2.6 | 26 | Display 600 | Panel titles, wallet amounts |
| `--fh-text-lg` | 2.0 | 20 | Display 600 | HUD street name, interaction hint, radio frequency, progress label |
| `--fh-text-md` | 1.6 | 16 | Sans 400 / Display 600 | Body, inputs, list rows; buttons and tabs in display |
| `--fh-text-sm` | 1.4 | 14 | Sans 400 | Descriptions, toast body, table cells |
| `--fh-text-xs` | 1.2 | 12 | Sans 500 / Display 600 caps | Meta, timestamps, help text; uppercase labels |
| `--fh-text-2xs` | 1.1 | 11 | Display 600–700 caps only | Slot numbers, duty tag, tiny keycaps. Never sentence text |

**Weights.** `--fh-weight-regular` 400 (sans body), `--fh-weight-medium` 500 (sans emphasis, display small), `--fh-weight-semibold` 600 (display default: titles, labels, buttons), `--fh-weight-bold` 700 (display numbers, keycaps, house-number plates).

**Rules.**
- Display text is uppercase only for titles, labels, buttons, tabs and chips, with 0.04–0.08em tracking (labels 0.08em, buttons/tabs 0.06em, titles 0.04em). Names, values, sentences and German nouns keep their case.
- Every number that changes (money, speed, ammo, vitals, timers, percentages) uses `font-variant-numeric: tabular-nums` so it does not jitter.
- German number format throughout: `18.730 €`, `23,4 kg`, `64 %`, `22:47`, `15.10.`. The euro sign follows the amount with a space.
- Line height: 1.45 for sans text, 1.0–1.1 for display.
- Minimum on the HUD is 1.2rem (12px at 1080p, 9.6px at 720p clamp 8px → ~9.6px). Anything a player must read while moving is ≥ 1.6rem.

## 4. Spacing, layout and scaling

**Root rule (whole series).** `html { font-size: clamp(8px, calc(100vh / 108), 16px) }`. 1rem = 10px at 1080p, 8px at 720p (clamped, so the UI is slightly larger relative to a small screen), 13.33px at 1440p, capped at 16px from 1728p up. Every size, gap, radius and offset is in rem; there is no scale token and no JS scaling.

**Spacing scale.** A 4px base:

| Token | rem | px @1080p | Typical use |
|---|---|---|---|
| `--fh-space-0_5` | 0.2 | 2 | Slab joints, hairline offsets |
| `--fh-space-1` | 0.4 | 4 | Gap between HUD plates, icon–label in chips |
| `--fh-space-2` | 0.8 | 8 | Inside HUD plates, between related controls |
| `--fh-space-3` | 1.2 | 12 | Row padding, panel header gap |
| `--fh-space-4` | 1.6 | 16 | Card padding, field gap |
| `--fh-space-5` | 2.0 | 20 | Panel body padding |
| `--fh-space-6` | 2.4 | 24 | Section gap inside panels |
| `--fh-space-8` | 3.2 | 32 | HUD safe margin from screen edges; gap between side-by-side panels |
| `--fh-space-10` | 4.0 | 40 | Large group separation |
| `--fh-space-12` | 4.8 | 48 | Full-screen menu margin from screen edge |
| `--fh-space-16` | 6.4 | 64 | Loading screen gutters |

**HUD layout (1920×1080 reference, all anchored to edges, centre stays free).**

| Zone | Anchor | Contents |
|---|---|---|
| Top-left | 3.2rem / 3.2rem | Voice range plate, radio plate |
| Top-right | 3.2rem / 3.2rem, column 38rem wide | Wallet (cash, bank), job plate, notification stack |
| Bottom-left | 3.2rem / 3.2rem | Street plate, compass strip, minimap frame (31×19.5rem); vitals column (21rem) to its right |
| Bottom-centre | centred, 9.6rem from bottom | Interaction hint, progress bar |
| Bottom-right | 3.2rem / 3.2rem | Ammo plate above the vehicle plate (39rem) |

The minimap itself is drawn by the game. The NUI frame must sit on the native minimap rectangle: read its anchor in Lua (safe-zone size and aspect ratio, the common `GetMinimapAnchor` routine) and send `{x, y, w, h}` to NUI when the resolution or safe-zone changes. The frame then positions itself with those values instead of the reference offsets above.

**Full-screen menus.** Centred panels are at most 150rem × 84rem so they fit 1280×720 (160rem × 90rem at the 8px clamp). Side panels (character select, creator, clothing) hug the left edge at 4.8rem and leave the right 45 % to the game camera.

**Grids.** Inventory slots 8.8rem square with 0.6rem gaps, 5 columns. List rows ≥ 4.4rem tall. Tablet shells (MDT, EMS) are 150 × 84rem with a 22rem navigation rail.

## 5. Shape: radii, borders, shadows, glow, materials, textures

**Radii (hard edges).**

| Token | Value | Use |
|---|---|---|
| `--fh-radius-xs` | 0 | HUD plates, bars, slots, chips' dots, house-number plate, minimap frame |
| `--fh-radius-sm` | 0.2rem (2px) | Buttons, inputs, keycaps, chips, steppers |
| `--fh-radius-md` | 0.3rem (3px) | Panels, cards, dialogs, app tiles |
| `--fh-radius-lg` | 0.4rem (4px) | ID card and licence, phone screen, tablet screen |
| `--fh-radius-xl` | 0.8rem (8px) | Hardware shells only: phone and tablet body |
| `--fh-radius-pill` | 999rem | Reserved for round things that are round in reality (radial menu ring, hub). No pill buttons |

**Borders.** `--fh-border-width: max(1px, 0.1rem)` for joints and outlines; `--fh-border-width-strong: max(2px, 0.2rem)` for the lamp line, house-number plate, selected-row marker, active tab, slot drop target. The `max()` keeps lines crisp at 720p.

**Shadows.**

| Token | Value | Use |
|---|---|---|
| `--fh-shadow-1` | `0 0.1rem 0.2rem rgba(0,0,0,0.7)` | HUD plates: separates the plate edge from a bright world |
| `--fh-shadow-2` | `0 0.1rem 0 rgba(0,0,0,0.6), 0 0.6rem 1.6rem rgba(0,0,0,0.45)` | Toasts, context menus, tooltips, dragged item |
| `--fh-shadow-3` | `0 0.2rem 0 rgba(0,0,0,0.5), 0 2.4rem 6.4rem rgba(0,0,0,0.6)` | Panels, dialogs, devices |

**Glow.** `--fh-glow-accent: 0 0 2.4rem rgba(242,181,58,0.3)`, the sodium lamp. Use at most once per view, on the one selected thing that the camera or the world reacts to (selected spawn marker). Never on text, never on HUD plates.

**Materials and blur.** Plattenbau is opaque concrete. Backdrop blur is not used (it also costs frame time in CEF over a 3D game):

| Token | Value | Use |
|---|---|---|
| `--fh-blur-thin`, `--fh-blur-regular`, `--fh-blur-thick` | `0px` | Defined for series swap-compatibility; no blur in this variant |
| `--fh-material-thin` | `rgba(13,15,17,0.72)` | Large scrims only (never under small text) |
| `--fh-material-regular` | `rgba(13,15,17,0.88)` = `bg-overlay` | HUD plates, toasts, chat log, hints |
| `--fh-material-thick` | `rgba(17,19,21,0.96)` | Full-screen menu backgrounds over the world |

**Focus ring.** `--fh-focus-ring: 0 0 0 max(2px,0.2rem) var(--fh-bg-base), 0 0 0 max(4px,0.4rem) var(--fh-accent-primary)`: a dark gap then a yellow ring, visible on any fill including yellow buttons.

**Textures (hints only).** All CSS, no image files, never under text that must be read at speed:

| Texture | Recipe | Where |
|---|---|---|
| Concrete grain | SVG `feTurbulence` noise as data-URI, 6 % opacity | Full-screen backgrounds, large panel bodies |
| Slab joints | 1px lines in `text-primary` at 3.5 % every 24 × 13.5rem | Full-screen backgrounds, vehicle preview well |
| Chain-link | two 45° 1px line sets at 4.5 %, 2.6rem pitch | Loading screen, death screen |
| Container ribs | vertical 0.3rem ribs at 5 % every 1rem | Header of garage, shop, trunk, boss menu |
| Hazard band | `accent-primary` / `bg-base` 45° stripes, 0.7rem | Only: admin panel top edge, low-state bar fills (in the bar's own colour), locked slots (grey) |

## 6. Motion

| Token | Value | Use |
|---|---|---|
| `--fh-duration-fast` | 100ms | Hover, press, toggle, tab change |
| `--fh-duration-enter` | 200ms | Toasts, menus, panels, tooltips appearing |
| `--fh-duration-exit` | 140ms | Everything leaving; always shorter than enter |
| `--fh-duration-slow` | 320ms | Full-screen transitions: loading screen out, death screen in/out, character camera hand-off |
| `--fh-ease-standard` | `cubic-bezier(0.23, 1, 0.32, 1)` | Default for every UI transition (strong ease-out) |
| `--fh-ease-spring` | `cubic-bezier(0.3, 1.15, 0.5, 1)` | Only for snapping into place: radial-menu segment selection, hotbar slot pick |

**Patterns.**
- Panels enter with opacity 0 → 1 and `translateY(0.8rem)` → 0; exit with opacity only.
- Toasts slide in from the right by 2.4rem; leave with opacity and height collapse (`grid-template-rows: 1fr → 0fr`) so the stack closes up.
- Scale animations start at `scale(0.96)` or higher, never at 0. `ease-in` is not used.
- Bars animate width linearly over 300ms (data, not UI). Progress bars run linear over their real duration.
- **Step blink, 667ms period (1.5 Hz):** turn indicators, seatbelt warning, low-health icon (1 Hz). Below the 3-flashes-per-second threshold; it carries state, so it keeps blinking under reduced motion.
- **Reduced motion** (`prefers-reduced-motion: reduce`, or a server setting forwarded from Lua): no translations, no skeleton shimmer, no pulse; opacity fades of ≤ 140ms remain. Indicator and seatbelt blink stay.

## 7. Iconography

- Drawn on a 24-unit grid, 2-unit stroke (2px at 1080p), `stroke-linecap: square`, `stroke-linejoin: miter`, no fill. Shapes are built from straight segments and true arcs; rounded corners only where the object is round (drop, heart, clock).
- Square containers instead of circles where a frame is needed: the info and success icons are a square with a mark inside; the error icon is an octagon (stop sign).
- Colour is `currentColor`. Icons inherit text colour; state colour is set on the parent.
- Sizes: 1.6rem in buttons and dense rows, 1.8–2rem in HUD and menus, 2.4rem in tiles, 3.2–5rem as item art in slots and empty states (stroke drops to 1.6 at large sizes).
- One icon per meaning across the whole series: heart = health, shield = armour, fork/knife = hunger, drop = thirst, bolt = stamina, pulse line = stress, microphone = voice, handset with antenna = radio, banknote = cash, bank building = bank, case = job, cartridge = ammo, pump = fuel, figure with belt = seatbelt, engine block = engine, arrows = indicators, padlock = locked.
- Delivered as an inline SVG sprite (`<symbol id="i-…">`) inside the NUI page, so there are no network requests. The preview carries the full set (82 symbols).
- No emoji, no multicolour icons, no brand logos.

## 8. Token reference

Every token of the series schema, bound for Plattenbau. Paste this block into the NUI page; component CSS reads only these variables.

```css
:root {
  /* colour */
  --fh-bg-base: #111315;
  --fh-bg-surface: #1A1D20;
  --fh-bg-elevated: #24282C;
  --fh-bg-overlay: rgba(13, 15, 17, 0.88);
  --fh-border: #3B4045;
  --fh-text-primary: #ECE9E2;
  --fh-text-secondary: #B3B5B2;
  --fh-text-muted: #989D9F;
  --fh-text-on-accent: #14130F;
  --fh-accent-primary: #F2B53A;
  --fh-accent-secondary: #2C68A0;
  --fh-success: #6CC08B;
  --fh-warning: #EE8A34;
  --fh-danger: #EA5D47;
  --fh-info: #6AAEE8;
  --fh-job-police: #5C9AE6;
  --fh-job-ems: #EF6476;
  --fh-job-mechanic: #3FBFAE;
  --fh-job-civil: #A9AEB2;
  --fh-hud-health: #EE6A5E;
  --fh-hud-armor: #5DA2E8;
  --fh-hud-hunger: #E39A3B;
  --fh-hud-thirst: #46C0DB;
  --fh-hud-stamina: #8BCB6A;
  --fh-hud-stress: #B596E3;
  --fh-hud-voice: #F5C64C;
  --fh-hud-radio: #4FD3B5;
  --fh-hud-fuel: #A9BFCF;

  /* type */
  --fh-font-sans: "Inter", "Segoe UI", Arial, sans-serif;
  --fh-font-display: "Barlow Condensed", "Arial Narrow", "Inter", sans-serif;
  --fh-font-mono: "JetBrains Mono", Consolas, "Courier New", monospace;
  --fh-text-2xs: 1.1rem;
  --fh-text-xs: 1.2rem;
  --fh-text-sm: 1.4rem;
  --fh-text-md: 1.6rem;
  --fh-text-lg: 2rem;
  --fh-text-xl: 2.6rem;
  --fh-text-2xl: 3.4rem;
  --fh-text-3xl: 4.8rem;
  --fh-text-4xl: 7.2rem;
  --fh-weight-regular: 400;
  --fh-weight-medium: 500;
  --fh-weight-semibold: 600;
  --fh-weight-bold: 700;

  /* space */
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
  --fh-radius-xs: 0;
  --fh-radius-sm: 0.2rem;
  --fh-radius-md: 0.3rem;
  --fh-radius-lg: 0.4rem;
  --fh-radius-xl: 0.8rem;
  --fh-radius-pill: 999rem;
  --fh-border-width: max(1px, 0.1rem);
  --fh-border-width-strong: max(2px, 0.2rem);
  --fh-shadow-1: 0 0.1rem 0.2rem rgba(0, 0, 0, 0.7);
  --fh-shadow-2: 0 0.1rem 0 rgba(0, 0, 0, 0.6), 0 0.6rem 1.6rem rgba(0, 0, 0, 0.45);
  --fh-shadow-3: 0 0.2rem 0 rgba(0, 0, 0, 0.5), 0 2.4rem 6.4rem rgba(0, 0, 0, 0.6);
  --fh-glow-accent: 0 0 2.4rem rgba(242, 181, 58, 0.3);
  --fh-blur-thin: 0px;
  --fh-blur-regular: 0px;
  --fh-blur-thick: 0px;
  --fh-material-thin: rgba(13, 15, 17, 0.72);
  --fh-material-regular: rgba(13, 15, 17, 0.88);
  --fh-material-thick: rgba(17, 19, 21, 0.96);
  --fh-focus-ring: 0 0 0 max(2px, 0.2rem) var(--fh-bg-base), 0 0 0 max(4px, 0.4rem) var(--fh-accent-primary);

  /* motion */
  --fh-duration-fast: 100ms;
  --fh-duration-enter: 200ms;
  --fh-duration-exit: 140ms;
  --fh-duration-slow: 320ms;
  --fh-ease-standard: cubic-bezier(0.23, 1, 0.32, 1);
  --fh-ease-spring: cubic-bezier(0.3, 1.15, 0.5, 1);
}

html { font-size: clamp(8px, calc(100vh / 108), 16px); }
```

`tokens.css` in this package binds the repository's shared design-system schema (`--bg`, `--fg`, `--accent`, …) to the same values for Open Design artefacts; the `--fh-*` block above is the game-UI contract shared by the three `fivem-harbour-ui` variants.

## 9. Shared primitives

These primitives build every screen in section 10. A screen rule names only what differs.

**HUD plate.** `bg-overlay` fill, 1px `rgba(0,0,0,0.6)` outline, `shadow-1`, radius 0, display font, text shadow `0 0.1rem 0.2rem rgba(0,0,0,0.5)`. Never transparent text on the world.

**Panel.** `bg-surface`, 1px `border`, 2px `accent-primary` top edge (lamp line), radius md, `shadow-3`. Header: house-number plate, title (display 600, xl, uppercase), subtitle (sans sm, muted), optional right-aligned meta and close button. Body padding space-5. Footer: `bg-base`, top border, actions right-aligned, primary rightmost.

**Button.** Height 4rem (sm 3.2rem), radius sm, display 600 md uppercase 0.06em.

| Variant | Rest | Hover | Pressed | Focus | Disabled |
|---|---|---|---|---|---|
| Primary | `accent-primary` fill, `text-on-accent` | `#F4BF56` | `translateY(0.1rem)` | focus ring | `bg-elevated` fill, `text-muted` |
| Secondary | `accent-secondary` fill, `text-primary` | `#4177AA` | same | focus ring | same as primary |
| Ghost | transparent, `text-muted` outline | `bg-elevated`, `text-secondary` outline | same | focus ring | same |
| Danger | `danger` fill, `text-on-accent` | `#ED705D` | same | focus ring | same |
| Danger ghost | transparent, `danger` outline and text | `bg-elevated` | same | focus ring | same |

One primary button per view. A button that triggers with a key shows the key inside (`Enter`, `Esc`, `E`) as an outlined mini keycap. A disabled button always has its reason in text nearby (never a tooltip only).

**Keycap.** 2.8rem square minimum, `accent-primary` fill, `text-on-accent`, display 700, inset bottom shadow. Ghost keycap (outline `text-muted`, text `text-secondary`) for secondary keys and help lines. A keycap filled `success` means "already done" (death screen "Notruf gesendet").

**Input.** Height 4rem, `bg-base` well, 1px `text-muted` outline, radius sm, sans md. States: placeholder `text-muted`; focus `accent-primary` outline + focus ring + caret in `accent-primary`; error `danger` outline + message below with error icon (sans sm, `danger`), the field keeps focus; disabled `bg-elevated`, `border` outline, `text-muted`, reason as hint text below. Numbers align with suffix (`€`, `kg`) right inside the field. Live validation on input, submit blocked while an error stands.

**Tabs.** Display 600 md uppercase, `text-secondary`; active is `text-primary` with a 2px `accent-primary` underline; optional count in xs muted.

**Segmented control.** `text-muted` outline, segments separated by 1px; active segment `accent-secondary` fill with `text-primary`.

**Stepper, slider, toggle.** Stepper: outlined box with − and + (3.2rem), value in tabular display. Slider: 0.4rem track at 14 % `text-primary`, fill `accent-primary`, square 1.6rem thumb in `text-primary`; focus puts the focus ring on the thumb; arrow keys step 1 %, Shift+arrow 10 %. Toggle: square 4.4 × 2.4rem, off `bg-elevated` with `text-muted` knob, on `accent-primary` with `text-on-accent` knob.

**Chip.** 2.4rem tall, radius sm. Job chip: `bg-elevated` with 0.8rem colour square and display caps label. Status chip: text in the status colour on a tint of the same colour at 14 % opacity (an `::after` layer with `background: var(--c); opacity: 0.14`, so it works with any token).

**Slab bar.** Track `text-primary` at 12 %, fill in the meaning colour, masked into 10 slabs with 0.2rem joints. Low state (below the threshold named per element): the fill turns into 45° stripes, drawn as `repeating-linear-gradient(-45deg, transparent 0 0.5rem, rgba(0,0,0,0.45) 0.5rem 1rem), var(--c)` over its own colour.

**List row.** Min 4.4rem, 1px bottom joint. Hover `bg-elevated`. Selected `bg-elevated` + 2px `accent-primary` inset left edge. Disabled: all text `text-muted`, lock icon, reason in the row.

**Every data view has four states, and draws exactly one:**

| State | Drawing |
|---|---|
| Loading | Skeleton rows in `bg-elevated` with a 1.4s linear shimmer (static under reduced motion), same row height as filled rows; actions that need the data are disabled |
| Empty | Dashed `border` box, muted icon (3.2rem), title in display caps, one sentence saying what will appear here and, if possible, how to get it |
| Error | Error box: `rgba(234,93,71,0.12)` fill, 2px `danger` left edge, error icon, bold one-line cause, secondary detail, ghost button "Erneut versuchen" (or the key that retries) |
| Filled | Rows / tiles as specified per element |

**Toast.** See 10.6.

**Number plate (`.plate-de`).** Off-white `#F1EFE8` plate, black text and border, blue `accent-secondary` EU strip with "D". Shows the vehicle's plate in garage, context menu, dialogs, MDT.

## 10. Screens and elements

Each element lists purpose, anatomy, states and interactions. Interactions read **input → effect → output**; "callback" means an NUI `fetch` POST to the resource (`https://<resource>/<name>`), "message" means an NUI message the Lua side sends in. Copy is German as it appears in game.

### 10.1 Loading screen

- **Purpose.** Shown by FiveM while the client connects and streams. Non-interactive: the loading screen gets no mouse or keyboard focus.
- **Anatomy.** Night scene darkened from the left (94 % → 35 %), chain-link texture. Left column at 9.6rem: house-number plate "7" + label "Block 7 · Ostkai · Hafenstadt Roleplay"; wordmark "HAFENSTADT" (display 700, 12rem, server name placeholder); tagline "Zwischen Kai und Wohnblock. Nachts wird hier entschieden." Bottom-left: stage list (Verbindung, Ressourcen, Kartendaten, Fahrzeuge, Charaktere), current stage line "Lade Kartendaten …" with the resource being loaded in mono xs, percentage in `accent-primary` 2xl, full-width slab bar 1.6rem high. Bottom-right: tip card (yellow left edge, "Tipp 3 / 12"), server facts line (players, Discord name, version in mono).
- **States.** Loading: stages done in `success` with tick, current stage `text-primary` with pulsing yellow square, pending stages muted. Stalled (no progress for 60 s): a warning plate top-right "Dauert länger als üblich – Stufe Kartendaten". Done: the whole screen fades out over `duration-slow` when the game calls `ShutdownLoadingScreenNui`. Empty and error do not apply: connection errors are FiveM's own dialog.
- **Interactions.** None. Tips rotate every 8 s with a 140ms cross-fade (static under reduced motion). Progress comes from `loadProgress` messages FiveM posts to the loading screen.

### 10.2 Multi-character selection

- **Purpose.** Choose, create or delete a character after connecting.
- **Anatomy.** Left column 50rem at 4.8rem: header plate "7" + "Wer bist du heute?" + hint "Wähle einen Charakter · ↑ ↓ wechseln". Selected character expands into a panel: portrait, name (display 700 xl), job chip, job line, key-values (Bargeld, Bank, Wohnung, Zuletzt), footer with primary "Spielen [Enter]" and danger-ghost icon button (delete). Other characters collapse to one row (portrait, name, job · last played, job chip). Then the free-slot button "Neuen Charakter anlegen · Slot 4 von 5 frei" (dashed outline, opaque fill), then locked slots (hatched, lock, reason). Right: the game shows the selected character standing in the world; a camera help plate at the bottom.
- **States.** Filled (drawn). Loading: skeleton rows in place of characters, buttons disabled. Empty (new player): only the create button, enlarged, with the line "Noch kein Charakter. Leg deinen ersten an." Error: error box "Charaktere nicht geladen." with "[R] Erneut".
- **Interactions.**
  - Click row / ↑ ↓ → selects → callback `previewCharacter {cid}`; game swaps the ped; panel expands.
  - Spielen / Enter → callback `selectCharacter {cid}` → screen fades out; spawn selector opens (10.4) or the character spawns at the last location, as the server decides.
  - Delete icon → confirm dialog (10.14, danger) "Charakter löschen?" with typed name confirmation → callback `deleteCharacter {cid}` → row removed, toast success "Charakter gelöscht".
  - Neuen Charakter anlegen → callback `createCharacter {slot}` → character creator (10.3).
  - A / D rotate the camera, mouse wheel zooms (game side).

### 10.3 Character creator

- **Purpose.** Build a new character in six steps.
- **Anatomy.** Left panel 54rem, full height minus 4.8rem margins. Header plate shows the step number, title = step name, subtitle "Neuer Charakter · Schritt 3 von 6". Step rail: six segments (Herkunft, Merkmale, Gesicht, Haare, Kleidung, Daten); done steps `success` underline, current `accent-primary`, upcoming `border`. Body: sub-tabs (Nase, Augen, Kiefer, Lippen, Wangen), labelled sliders with signed value (−1.00 … +1.00, mono xs), swatch row (eye colour, 3.6rem squares, selected has a 3px yellow frame), template stepper "14 / 46" with "Zufällig" and "Zurücksetzen". Footer: ghost "Zurück [Q]", primary "Weiter [E]". Right side: camera panel (presets Kopf/Körper/Beine/Ganz as a segmented row, key help), and on step 6 the data form (Vorname, Nachname, Geburtsdatum, optional Geschlecht).
- **States.** Filled (drawn, slider in focus). Validation error on step 6: field error "Dieses Datum gibt es nicht." / "Name schon vergeben." and "Weiter" becomes "Fertig" disabled until valid. Saving: "Fertig" shows a spinner-free busy label "Speichert …", all inputs disabled. Error on save: error box above the footer "Speichern fehlgeschlagen. Deine Eingaben bleiben erhalten." Empty and loading do not apply (the creator opens with defaults).
- **Interactions.**
  - Slider drag / ← → → callback `setFeature {id, value}` at most every 50ms → ped updates live.
  - Swatch click → callback `setEyeColour {index}`.
  - Template stepper → callback `setFaceTemplate {index}`; Zufällig → `randomizeStep {step}`; Zurücksetzen → `resetStep {step}`.
  - Weiter / E → next step (local); on step 6 "Fertig" → callback `finishCharacter {data}` → creator closes, spawn selector opens.
  - Zurück / Q → previous step; on step 1 → confirm "Erstellung abbrechen?" → back to selection.
  - Camera presets → callback `setCamera {preset}`.

### 10.4 Spawn selector

- **Purpose.** Pick where the character wakes up.
- **Anatomy.** Centred panel 150 × 82rem. Header "Wo wachst du auf?" with character name and "Kamera fährt zum gewählten Ort", weather and time right. Left list 46rem: rows with numbered plate (0–5), name, address line; selected row yellow plate + home icon. Disabled locations show a lock and "nur im Dienst". Bottom: primary "Hier aufwachen [Enter]" at 5.6rem. Right: stylised map (water, quays, blocks) with markers: square numbered plate + label + stem; selected marker filled yellow with `glow-accent`; disabled marker at 60 % opacity.
- **States.** Filled (drawn). Loading: six skeleton rows; "Letzter Ort" stays usable once known. Error: error box "Orte nicht geladen." and only "Letzter Ort" selectable. Empty does not occur (the last location always exists).
- **Interactions.** Click row or marker / keys 0–5 → select → callback `previewSpawn {id}` → game camera flies there (320ms UI cross-fade). Enter / button → callback `spawn {id}` → screen fades out over `duration-slow`; HUD fades in. Mouse wheel zooms the map.

### 10.5 HUD

Always on during play, never takes focus. Every element is a HUD plate (section 9). All values arrive by message `hud:update {…}` (partial updates allowed); elements show or hide by message flags (`inVehicle`, `armed`, `radioOn`).

**Health, armour, hunger, thirst, stamina, stress (vitals column).** Six plates 21 × 3rem stacked with 0.4rem gaps, right of the minimap. Each: icon in its `hud-*` colour, slab bar in the same colour, value 0–100 in `text-primary` tabular. Order fixed: Leben, Panzerung, Hunger, Durst, Ausdauer, Stress.
- Low state (Leben < 25, Hunger < 20, Durst < 20; Stress inverted: > 80): striped fill, value in `danger`, 3px `danger` left edge, icon blinks at 1 Hz.
- Armour at 0 and Stress at 0 may hide (server setting); Ausdauer hides when 100 for 5 s and returns when it drops.
- Empty/loading/error: before the first `hud:update` the column is not drawn; a missing value keeps the last one.

**Voice indicator.** Plate top-left: microphone icon, three ascending pips for the range (Flüstern = 1, Normal = 2, Rufen = 3), range label in display caps. Idle: icon `text-secondary`, pips `text-primary`. Speaking: icon and pips `hud-voice`. Muted / not connected to voice: icon crossed, label "Stumm" in `text-muted`. Range changes by the voice resource's key (message `voice:range`).

**Radio indicator.** Plate under the voice plate, only when a radio is on: radio icon, frequency (display 700 lg), "Funk · 4 im Kanal" in sans xs. Transmitting: icon and frequency `hud-radio`, a solid `hud-radio` tag "Sendet" replaces the member count. Someone else talking on the channel: their name replaces the count for as long as they talk.

**Cash and bank.** Wallet plate top-right: rows "Bar" and "Bank", icon, label caps, amount display 600 xl tabular. A change shows a delta "+250" / "−74" in `success` / `danger` next to the amount for 3 s, then fades (140ms).

**Job.** Plate under the wallet: job colour square, company in display caps, grade in `text-secondary`, duty tag "Im Dienst" (`success`) or "Außer Dienst" (`text-muted`).

**Ammo.** Plate bottom-right, only while armed: weapon name caps, fire mode in muted xs caps, magazine count 3xl tabular, reserve "/ 48" lg `text-secondary`. Low (magazine ≤ 25 %): magazine count in `warning`. Empty magazine: "0" in `danger` and the hint "[R] Nachladen" appears below for 2 s. Melee weapons: plate hides.

**Minimap frame.** 31 × 19.5rem frame around the game minimap: 2px `bg-base` frame, 1px outer line `text-primary` at 45 %, yellow corner brackets (0.3rem). Above it, the street plate (street in display 700 lg, district in display 500 md `text-secondary`) and the compass strip (tick ruler, letters W NW N NO O S SW, heading tag in `accent-primary` with `text-on-accent`: "NO 042°"). German compass letters (O for Ost). Frame position follows the minimap anchor message (section 4). Big map open: frame and street plate hide.

### 10.6 Vehicle HUD

- **Visibility.** Only while seated in a vehicle (message `inVehicle: true`); enters with opacity + 0.8rem rise over 200ms, leaves over 140ms.
- **Anatomy.** Plate 39rem bottom-right, under the ammo plate. Top row: left indicator arrow, gear "GANG 3" (or "R", "N"), right indicator arrow. Main row: speed in display 700 4xl tabular right-aligned in a 12rem box + unit "KM/H"; status grid with four labelled icons: Gurt, Motor, Licht, Schloss ("Offen" / "Zu"). Speed slab bar (0–240 km/h, `text-primary` fill). Fuel row: pump icon, slab bar in `hud-fuel`, percentage.
- **States.**
  - Indicators: off at 22 % `text-primary`; on in `success`, step blink 667ms; hazard = both.
  - Seatbelt: on = icon `success`, label "Gurt"; off while moving > 20 km/h = icon and label `warning`, label "Gurt!", icon blinks; off while stopped = `text-muted`. Vehicles without belts (bikes, boats) hide the item.
  - Engine: running = `success` "Motor"; off = `text-muted` "Aus"; damaged (< 40 %) = `danger` "Motor 31%".
  - Lights: off muted, low beam `success`, high beam `info`.
  - Fuel: < 15 % turns the fill into `warning` stripes and the value `warning`; < 5 % `danger`. Electric vehicles relabel "Akku".
  - Boats and aircraft swap km/h for "KN" (knots) and hide the seatbelt.
- **Interactions.** None on the plate. Toggling the belt (B by default) is a game key; the plate reflects message `vehicle:update`.

### 10.7 Notifications (four types)

- **Placement.** Stack under the job plate, top-right, 38rem wide, newest on top, maximum four visible; a fifth pushes the oldest out.
- **Anatomy.** HUD plate with `shadow-2`, 0.4rem left edge and icon in the type colour, title display 700 md caps, timestamp mono xs muted right, body sans sm `text-secondary` (max two lines, ellipsis), 2px lifetime line at the bottom in the type colour, shrinking linearly.

| Type | Colour | Icon | Example title / body |
|---|---|---|---|
| Success | `success` | check square | "Zahlung erhalten" / "+250 € von Mira Hansen · Rechnung RE-0193" |
| Info | `info` | info square | "Neue Nachricht" / "Ole: „Komm runter zum Tor 3.“" |
| Warning | `warning` | triangle | "Tank fast leer" / "Noch etwa 6 km. Tankstelle Hafenstraße 400 m." |
| Error | `danger` | octagon | "Kein Platz" / "Inventar voll (39,6 / 40 kg). Lege erst etwas ab." |

- **Lifetime.** Success and info 5 s, warning 8 s, error 10 s; a hover is impossible in play, so durations are fixed. Message `notify {type, title, text, duration?}`.
- **Motion.** Enter from right 2.4rem over 200ms; exit opacity + height collapse over 140ms.

### 10.8 Progress bar

- **Placement.** Bottom-centre, 46rem wide, 9.6rem above the bottom edge.
- **Anatomy.** HUD plate: action label (display 600 lg), percentage in `accent-primary` right, slab bar 1.2rem in `accent-primary`, footer line with ghost keycap "X" "Abbrechen · noch 0:07".
- **States.** Running (drawn). Cancelled: bar fill turns `danger`, label "Abgebrochen", plate fades after 600ms. Completed: fill `success` for 300ms, then fades. Blocked start (e.g. no tool): no bar, an error toast instead.
- **Interactions.** X (or moving, if the action requires standing still) → callback `progress:cancel {id}` → game stops the animation. Completion is decided by the game; the bar only renders `progress {id, label, duration, canCancel}`.

### 10.9 Interaction hint "[E] …"

- **Placement.** Bottom-centre above the progress bar, or attached to a world point (3D-to-2D projection from Lua) when the server prefers that.
- **Anatomy.** HUD plate: yellow keycap with the key, label display 600 lg ("Rolltor öffnen", "Tür öffnen"), optional suffix in sans sm `text-secondary`.
- **States.** Tap: as drawn. Hold: the keycap gets a progress ring (0.25rem) that fills clockwise in `accent-primary`, suffix shows "· 40 %"; label starts with "Halten:". Unavailable: ghost keycap, label in `text-muted`, reason as suffix ("Abgeschlossen · Schlüssel fehlt"). Several options at one spot: up to three hints stacked, mouse wheel cycles the active one (only the active one has a solid keycap).
- **Interactions.** Key press → game action (the hint is information; the key is read in Lua). Hold release before 100 % → ring resets over 140ms.

### 10.10 Death / unconscious screen

- **Purpose.** Shown while the character is down. The game desaturates the world (timecycle modifier); NUI adds the radial dark vignette.
- **Anatomy.** Centred column: label "Schwer verletzt" in `hud-health` caps; title "BEWUSSTLOS" display 700 4xl with 0.12em tracking; one line of context ("Du liegst am Containerhof Süd. Ein Sanitäter kann dich wiederbeleben."); two figures: respawn countdown (mono 500 3xl "02:41") and "Rettungsdienst · 2 im Dienst" in `job-ems`; two hint plates.
- **States.**
  - Call open: "[G] Notruf senden" with yellow keycap.
  - Call sent: keycap `success`, "Notruf gesendet · 0:48 her · erneut ab 1:12".
  - No EMS on duty: figure reads "Kein Sanitäter im Dienst" in `warning`; countdown shortened by server rule.
  - Respawn locked: second hint dimmed, "Halten: im Krankenhaus aufwachen · ab 00:00".
  - Respawn available: second hint at full opacity, yellow keycap, hold ring 3 s.
  - Revived: whole screen fades out over 320ms.
- **Interactions.** G → callback `death:callEms` → server dispatch to EMS (10.25) → state "Notruf gesendet". Hold E (when available) → callback `death:respawn` → screen fades, hospital spawn.

### 10.11 Radial menu

- **Purpose.** Quick actions around the player; opened by holding F3 (server binding), released to close.
- **Anatomy.** 46rem ring: eight annular segments with 1.4° gaps, `bg-overlay` fill; icon (2.6rem) and caps label per segment; the hovered segment fills `accent-primary` with `text-on-accent` content and a yellow arc outside; locked segments darker with a lock icon and muted label. Hub (`bg-surface` disc): current label, count of sub-options, reason when the hovered item is locked ("Wohnung: zu weit weg"). Key help plate under the ring.
- **States.** Root level (drawn). Sub-level: hub shows a back arrow and parent name; segments are the children. Loading of dynamic items: segments show skeleton labels for ≤ 300ms. Empty sub-level: hub shows "Keine Optionen hier".
- **Interactions.** Mouse direction → highlights segment (snap with `ease-spring`). Click or release key on a segment → callback `radial:select {id}` → either opens the sub-level or runs the action and closes. Right-click → up one level. Release on the hub → closes without action. Locked segment click → no action, short shake-free flash of the reason in the hub.

### 10.12 Context menu

- **Purpose.** Actions on a targeted entity (vehicle, door, person) via third-eye/target or right-click in menus.
- **Anatomy.** `bg-surface` list 30rem, `shadow-2`. Header: entity icon in `accent-primary`, entity type caps, identifying detail (number plate, name). Items 3.8rem: icon, label (sans md), right side either a ghost keycap shortcut, a chevron (submenu) or a muted reason. Separator before destructive items. Danger item text and icon in `danger`.
- **States.** Hover: `bg-elevated` + yellow left edge. Disabled: muted with reason ("Werkzeugkasten fehlt"). Submenu: opens to the right, aligned to its parent row, same style without header. Loading (permissions resolving): items render disabled for ≤ 300ms. Empty: menu does not open; the hint shows "Hier gibt es nichts zu tun".
- **Interactions.** Click / Enter on item → callback `context:select {entity, action}` → menu closes. Hover chevron item or → → submenu. Esc or click outside → closes. Shortcut key while open → same as clicking that item.

### 10.13 Input dialog

- **Purpose.** Ask for one to four values (amount, text, choice), e.g. "Geld geben".
- **Anatomy.** Panel 56rem centred upper third over a 45 % dim: house-number plate with icon, title, subtitle with the recipient ("an Mira Hansen · ID 23 · 1,4 m entfernt"), close icon button. Body fields stacked: amount with € suffix, source as a segmented control showing both balances, optional note (textarea with counter "14 / 80"). Footer: help text left ("Eingabe prüft live · Enter sendet nur ohne Fehler"), ghost "Abbrechen [Esc]", primary "Geben [Enter]".
- **States.** Default: first field focused. Error: field error inline ("Du hast nur 4.250 € Bargeld."), primary disabled. Submitting: title becomes "Wird gesendet …", indeterminate thin bar under the header, all fields and primary disabled, Esc still cancels. Server error: error box above the footer with the cause; fields re-enabled with values kept. Success: dialog closes, the result arrives as a toast.
- **Interactions.** Enter → callback `input:submit {id, values}`; Esc / close / Abbrechen → callback `input:cancel {id}` → closes. Tab moves between fields in order.

### 10.14 Confirm dialog

- **Purpose.** Confirm an irreversible or costly action.
- **Anatomy.** Panel 52rem; for destructive actions the lamp line and house-number plate are `danger` with a warning icon. Title is the question ("Fahrzeug verschrotten?"); body names the object (number plate), the consequence ("wird endgültig gelöscht"), what the player gets or loses ("420 € Schrottwert") and "Das lässt sich nicht rückgängig machen." Footer: ghost "Abbrechen [Esc]" first and focused, then danger "Verschrotten" (verb, never "OK"/"Ja").
- **States.** Default focus on Abbrechen. Submitting: buttons disabled, label "Wird verschrottet …". Error: error box, buttons back. Very destructive actions (delete character, permanent ban) add a typed confirmation field; the danger button stays disabled until it matches.
- **Interactions.** Enter activates the focused button (so Enter alone cancels). Danger click → callback `confirm:accept {id}`; Esc / Abbrechen → `confirm:cancel {id}`.

### 10.15 Chat

- **Placement.** Top-left, 62rem wide, below the voice/radio plates when they are shown (the chat shifts down).
- **Anatomy.** Log on `material-regular`, up to 8 lines visible, sans md with a text shadow. Each line: channel tag (display 700 xs caps on its colour: OOC `text-muted`, Funk `hud-radio`, Polizei `job-police`, System `danger`; DO as a plain `bg-elevated` tag), author in 600, message. `/me` actions in italic `text-secondary` with a leading "*". Input line: `bg-surface`, 1px yellow outline, channel tag "LOKAL" in yellow, text with caret, help right "Tab Kanal · ↑ Verlauf". Command suggestions above the input: command in mono `accent-primary`, argument hint and description in `text-secondary`, hovered row `bg-elevated`.
- **States.** Closed: log fades to 0 after 10 s without new lines; new lines show the log again for 10 s. Open: log fully visible, scrollable with the mouse wheel. Empty log: nothing drawn. Unknown command: system line in `danger` tag ("Befehl unbekannt: /abschlep"). Rate-limited: input outline `warning`, hint "Langsamer – 2 s".
- **Interactions.** T opens the input (game key) and focuses it. Enter → callback `chat:send {channel, text}` → input closes. Esc → closes without sending. Tab → cycles channel (Lokal, OOC, Funk if available). ↑ ↓ → history. Click a suggestion → completes the command.

### 10.16 Scoreboard

- **Placement.** Right-centre panel 78 × 80rem while Tab (or the server key) is held.
- **Anatomy.** Header plate with the player count ("48"), server name, "48 / 64 Spieler · Uptime 6 h 12 min", ghost keycap "Tab". Job count chips (Polizei 6, Rettung 3, Werkstatt 2, Zivil 37). Table: ID (mono), Name, Beruf (job chip), Ping (mono; > 90 `warning`, > 150 `danger`). Own row selected style with "· du" in `accent-primary`. Bottom fades out when the list scrolls.
- **States.** Filled (drawn). Loading: header counts and skeleton rows. Error: error box "Spielerliste nicht verfügbar". Empty cannot occur (the player is always listed).
- **Interactions.** Release Tab → closes. Mouse wheel scrolls (only when the server grants focus). No actions on rows: player actions live in the admin panel.

### 10.17 Inventory

- **Anatomy.** Over a 60 % dim, three columns centred: player panel ("Taschen", 5 × 5 grid), middle column (item detail card and move controls), other-container panel ("Kofferraum" with number plate, "Handschuhfach", "Boden", "Kiste", 5 × 4 grid; container-rib header). Each panel: weight row (label, slab bar, "23,4 / 40 kg"); the bar turns `warning` above 85 %, `danger` above 100 %. Slots 1–5 of the player grid are the hotbar (slot number in `accent-primary`). Hotbar strip of five 7.2rem slots at the bottom centre while the inventory is open.
- **Slot states.** Empty (`bg-base`, number only). Filled (`bg-elevated`; count "×12" top-right; 3.4rem icon; name on a darker strip at the bottom, ellipsis). Durability (weapons, tools): 0.3rem bar above the name, `success`, `warning` under 40 %. Selected: yellow outline. Dragging origin: 35 % opacity. Drag ghost: follows the cursor, tilted −2°, `shadow-2`, yellow outline. Drop target: dashed 2px yellow outline, 8 % yellow fill. Invalid target (too heavy, wrong type): dashed `danger` outline. Locked slot: grey hazard hatch + lock.
- **Detail card.** Icon, name caps, slot; description; Gewicht, Haltbar; actions Benutzen (secondary), Geben, Teilen, Ablegen (ghost).
- **Container states.** Loading: grid of skeleton slots. Empty container: grid of empty slots + line "Leer" in the header subtitle. Error: error box in place of the grid ("Kofferraum ist gerade von jemand anderem geöffnet."). No second container: middle column and right panel are replaced by "Boden" (ground).
- **Interactions.**
  - Drag slot → slot → callback `inventory:move {from, to, amount}`; the move amount comes from the stepper (Alle / Hälfte presets). Shift+click → moves the whole stack to the other container. Drop onto an occupied same item → stacks; different item → swaps.
  - Right-click → item detail card for that slot. Benutzen / double-click → `inventory:use {slot}`. Geben → closest player picker → `inventory:give {slot, target, amount}`. Teilen → split into the first free slot. Ablegen → drops to ground container.
  - 1–5 (with or without the inventory) → `inventory:useHotbar {n}`; the HUD shows the hotbar strip for 2 s with the chosen slot selected.
  - Esc / Tab → closes → `inventory:close`.

### 10.18 Phone

- **Anatomy.** Device 36 × 74rem bottom-right: hardware shell (radius xl), screen (radius lg, `bg-base`). Status bar (time, carrier "HafenNetz · 4G", battery). Lock/home clock (display 700, 7.2rem) with date and weather. App grid 4 × 3: square tiles 5.6rem in `bg-elevated` with a 0.3rem coloured bottom edge for apps with an identity (Nachrichten `success`, Bank `accent-secondary`, Markt `accent-primary`, Dienste `danger`, Karte `info`, Rechnungen `warning`), unread badge in `danger`. Dock with four apps on `bg-surface`.
- **States.** Locked: clock only + "Hochwischen / Enter". Home (drawn). Incoming call: banner at the top (portrait, "Eingehender Anruf", caller name, red reject and green accept square buttons); full-screen call view when the phone is opened. In-call: green status bar with duration. No signal (tunnel, cellar): carrier reads "Kein Netz", messaging apps show the error state "Kein Netz – Nachricht wird gesendet, sobald du Empfang hast." App loading: skeleton list. Battery empty: black screen with "Akku leer".
- **Interactions.** F1 (server key) → phone slides up from the bottom over 200ms, callback `phone:open`. App tile → opens the app inside the screen (each app follows the panel primitives at phone scale). Accept → `phone:answer`; reject → `phone:decline`. Esc / Backspace → back one level, then closes.

### 10.19 Bank and ATM

- **Bank (branch counter).** Panel 84 × 76rem: header "Hafensparkasse · Filiale Ostkai". Left column: account cards (Girokonto with IBAN in mono, Bargeld, company account read-only when the rank only allows reading), Einzahlen / Abheben secondary buttons. Right: tabs Übersicht, Überweisen, Verlauf. Überweisen form: recipient (IBAN or name), amount, purpose, "Gebühr 0 € · sofort", primary "Überweisen". Verlauf table: date (mono), text, amount (positive `success`, negative `danger`, with sign).
- **ATM.** Panel 40rem: PIN entry with four 5.6 × 6.4rem cells, keypad 3 × 4 (ghost keys, OK primary). After PIN: quick amounts 50 · 100 · 200 · 500 € and "Anderer Betrag".
- **States.** Loading: account figures as skeletons, forms disabled. Recipient not found: field error "Konto nicht gefunden. Prüfe die letzten 4 Stellen." Insufficient funds: amount field error. PIN wrong: cells outlined `danger`, "PIN falsch · noch 2 Versuche"; after the last attempt "Karte gesperrt – bitte in der Filiale entsperren" and the keypad disables. Empty history: "Noch keine Buchungen". Success: toast + history row inserted at the top.
- **Interactions.** Einzahlen/Abheben → input dialog (10.13) → `bank:deposit` / `bank:withdraw {account, amount}`. Überweisen → `bank:transfer {iban, amount, purpose}`. Keypad keys and number keys → PIN digit; ← deletes; OK / Enter → `atm:pin {pin}`. Quick amount → `atm:withdraw {amount}`. Esc → closes.

### 10.20 Shop

- **Anatomy.** Panel 146 × 80rem, container-rib header with plate "7", shop name "Kiosk Block 7", subtitle "Späti · geöffnet bis 04:00", search field, close. Category tabs with count. Product grid 4 columns: card with icon well, name, price (display lg), stock ("24 da"), ghost "In den Korb". In-cart products carry a yellow quantity keycap on the icon well. Right column (46rem, `bg-base`): cart rows with stepper and line total; payment segmented control (Bar / Karte with balances); total (2xl); primary "Bezahlen [Enter]" 5.6rem.
- **States.** Product sold out: card 55 % opacity, "Ausverkauft" in `danger`, disabled button "Nicht da". Hover card: `bg-elevated` with `text-muted` outline. Empty cart: "Noch nichts im Korb", Bezahlen disabled. Not enough money for the selected method: error under the payment control "Zu wenig Bargeld – 3,20 € fehlen", Bezahlen disabled. Loading: skeleton cards. Error: error box in the grid "Ladenkasse nicht erreichbar". Search without results: empty state "Nichts gefunden für „…“".
- **Interactions.** In den Korb → adds 1 (local). Stepper → quantity; 0 removes the row. Bezahlen → `shop:checkout {shopId, items, method}` → success toast, cart clears, inventory updates. Search filters live. Esc → closes; cart is discarded.

### 10.21 Garage

- **Anatomy.** Panel 140 × 78rem, rib header with plate "P1", "Tiefgarage Block 7", "6 / 10 Stellplätze belegt". Left 58rem: tabs (Eigene, Job, Boote, Abschlepphof with counts), search + status filter, rows (vehicle icon, name, location, number plate, status chip: Eingeparkt `success`, Draußen `info`, Im Einsatz `warning`, Abgeschleppt `danger`). Right: preview well (slab-joint texture; the game renders the vehicle into it via a scripted camera, NUI only frames it), status chip, name (2xl caps), location line, large number plate, condition bars (Tank `hud-fuel`, Motor `success`, Karosserie; any value < 30 % turns `warning` stripes), notice box, action row.
- **States and actions by vehicle status.**

| Status | Primary | Secondary |
|---|---|---|
| Eingeparkt | "Ausparken [Enter]" | Markieren |
| Draußen | "Orten" (sets GPS) | — ; Ausparken disabled with "Fahrzeug ist draußen" |
| Abgeschleppt | "450 € zahlen & auslösen [Enter]" with warning notice of the fee and pickup place | Ausparken disabled |
| Im Einsatz (job) | none | "Von Kollege benutzt: P. Lorenzen" |

  Loading: skeleton rows. Empty tab: "Keine Fahrzeuge – hier parkst du, sobald du eins besitzt." Error: "Garage nicht erreichbar." + Erneut. Parking spot blocked when taking out: toast error "Ausfahrt blockiert".
- **Interactions.** Row click → select → `garage:preview {plate}` (camera shows vehicle). Ausparken → `garage:takeOut {plate}` → panel closes, vehicle spawns. Auslösen → confirm dialog with fee → `garage:release {plate, method}`. Markieren / Orten → `garage:waypoint {plate}`. Storing happens outside the menu via the interaction hint "[E] Einparken".

### 10.22 Clothing store

- **Anatomy.** Left panel 56rem full height: header "Klamottenladen", category list (Oberteil, Unterhemd, Hose, Schuhe, Kopf, Brille, Uhr, Tasche, Maske), editor: model stepper "14 / 212" with the item name, texture swatches (4.4rem squares numbered, selected yellow frame), price (2xl), "In den Korb" (secondary) and "Anprobe zurücksetzen" (ghost); cart rows with remove icon; footer "Outfit speichern" (ghost), sum, "Kaufen [Enter]". Bottom-centre camera plate: Kopf / Körper / Beine / Füße (segmented, current `accent-secondary`), key help "A D drehen · H Hände hoch". The character stands in the right half (game).
- **States.** Category not sold here: row disabled with lock ("nicht in diesem Laden"). Item already owned: price replaced by "Besitzt du", add button reads "Anziehen". Loading model list: stepper shows "– / –" and is disabled. Empty cart: Kaufen disabled, sum "0 €". Purchase error: error box above the footer. Leaving without buying: confirm "Anprobe verwerfen?" if the cart is not empty.
- **Interactions.** Stepper / ← → → `clothing:set {component, drawable}` (live try-on). Swatch → `clothing:set {component, texture}`. In den Korb → local cart. Kaufen → `clothing:buy {items}` → toast, outfit stays on. Outfit speichern → input dialog (name) → `clothing:saveOutfit`. Camera buttons → `clothing:camera {preset}`. Esc → closes; unbought try-ons revert.

### 10.23 Crafting

- **Anatomy.** Panel 132 × 74rem, header plate "K1", "Werkbank · Keller Block 7 · Fertigkeit Schlosser 3". Left 40rem: recipes grouped by category; row = icon, name, duration (mono), readiness dot (`success` craftable, `warning` material missing); recipes above the skill level locked with requirement ("Elektronik 2"). Middle: result slot (12rem) with name, quantity, weight, duration; "Benötigt" list (icon, material, have / need, tick `success` or cross `danger`; missing rows in `danger`); quantity stepper with "max. N mit aktuellem Material"; primary "Herstellen" (5.6rem) with the reason under it when disabled ("Es fehlt 1× Klebeband."). Right 34rem (`bg-base`): queue cards with progress slab bar and remaining time; finished item card with `success` outline and "Nehmen".
- **States.** Craftable: Herstellen enabled. Missing material: as drawn. Locked recipe: detail shows the requirement and how to raise it. Queue full (3): Herstellen disabled "Warteschlange voll". Inventory full on collect: error toast; item stays in the queue. Loading: skeleton recipe rows. Empty (no recipes at this bench): "An dieser Werkbank kannst du noch nichts bauen."
- **Interactions.** Recipe click → select. Stepper → quantity (bounded by max). Herstellen → `craft:start {recipe, amount}` → queue card appears, materials leave the inventory. Nehmen → `craft:collect {jobId}`. Closing the panel does not cancel; the queue keeps running while the player stays within 15 m (stated in the panel).

### 10.24 Invoice

- **Received invoice.** Panel 54rem: plate in the issuer's job colour, "Rechnung", number and date in mono (`RE-2025-0193 · 15.10. 22:41`), status chip (Offen `info`, Fällig `warning`, Bezahlt `success`, Abgelehnt `text-muted`). Key-values Von (job chip + company + person), An, Fällig ("in 3 Tagen · danach +10 % Mahngebühr"). Line items table, sum row (2xl). Footer: ghost "Ablehnen", primary "Vom Konto zahlen [Enter]".
- **Issue invoice.** Panel 54rem: recipient select (nearby players "ID 23 · Mira Hansen"), amount, reason, hint "Empfänger muss in 5 m Nähe sein", secondary "Senden".
- **States.** Paid: chip `success`, buttons replaced by "Bezahlt am 15.10. 22:44". Not enough on the account: error under the footer, pay disabled. Recipient out of range: field error "Mira Hansen ist zu weit weg". No nearby players: recipient select empty state "Niemand in der Nähe". Sending: secondary button busy label.
- **Interactions.** Zahlen → `invoice:pay {id}` → toast success for both parties (issuer sees "Zahlung erhalten"). Ablehnen → confirm → `invoice:decline {id}`. Senden → `invoice:create {target, amount, reason}` → recipient gets the received-invoice panel as a notification ("Neue Rechnung – [F1] Handy · Rechnungen").

### 10.25 ID card

- **Anatomy.** Card 64 × 40.4rem (ID-1 ratio), light warm-grey card stock (`#E9E6DE → #D9D6CC`), radius lg, `shadow-3`. Header strip `accent-secondary` with an "H" house-number plate in yellow and "Hafenstadt · Ausweis" caps; photo well (silhouette placeholder; the server provides a mugshot texture); fields in two columns (Name, Vorname, Geburtsdatum and Gültig bis in mono, Geschlecht, Wohnort); handwritten signature line; machine-readable line in mono on a darker strip. Driving licence card (40rem): classes as outlined boxes (granted solid, not granted dashed muted), points line. It is a fictional town ID; it must not reproduce the real German Personalausweis.
- **States.** Shown by someone: hint plate "[Esc] Schließen · gezeigt von ID 23 · schließt in 0:12". Own card: no countdown. Expired: "Gültig bis" in `danger` with "abgelaufen". Fake ID (server flag, police check): no visual tell on the card itself; the MDT search reveals it.
- **Interactions.** Show ID (radial menu "Ausweis zeigen") → `id:show {target|nearby}`; viewers receive the card. Esc → `id:close`. Auto-close after 15 s.

### 10.26 Police MDT

- **Anatomy.** Tablet shell 150 × 84rem. Top bar: police plate (star), "MDT · Polizei Hafenstadt", duty chip, officer and unit ("PK K. Brandt · 3214 · Streife Hafen 12"), clock, close. Rail (22rem): Übersicht, Personen, Fahrzeuge, Akten, Haftbefehle (count `danger`), Einsätze (count), Einheiten, and at the bottom Bußgeldkatalog; active item `bg-elevated` with a `job-police` left edge. Main (Personen view): search card (focused field, result count, results with portrait, name, DOB and ID in mono, "HB" warrant chip), record card (portrait, key-values, active-warrant error box, records table date / charge / fine / officer, actions: add entry icon, "Bußgeld" secondary, "Haftbefehl" danger-ghost), right column: active call card (`danger` outline, code, place, "Annehmen" primary, "GPS") and units list (BOS status number plates coloured by status: 1 Funk `info`, 2 Frei `success`, 3 Einsatz `warning`, 4 Vor Ort `danger`, 6 Außer Dienst `job-civil`).
- **States.** Search empty query: "Name, Geburtsdatum oder Ausweisnummer eingeben". Searching: skeleton result rows. No result: "Keine Person gefunden – Schreibweise prüfen". Database error: error box + "Erneut". No record selected: the record column shows an empty state "Person links auswählen". Off duty: MDT opens read-only with a `warning` bar "Außer Dienst – nur Lesen".
- **Interactions.** Typing (debounced 300ms) → `mdt:searchPerson {q}`. Result click → `mdt:getPerson {id}`. Bußgeld → input dialog (catalogue picker + amount) → `mdt:fine`. Haftbefehl → form panel → confirm → `mdt:warrant`. Eintrag (+) → note form → `mdt:addRecord`. Annehmen → `mdt:acceptCall {id}` → own unit status becomes 3, GPS set. Unit status keys 1–6 while the MDT is open → `mdt:setStatus {n}`. Esc / close → closes.

### 10.27 EMS tablet

- **Anatomy.** Same shell, `job-ems` identity. Rail: Patienten (count), Notrufe (count), Krankenhaus, Berichte, Kollegen, Bestand. Main: patient list sorted by triage (left colour bar and chip: Rot `danger`, Gelb `warning`, Grün `success`; line "bewusstlos · Containerhof Süd · 0,6 km"); patient card: header with name, age, state chip, "Route" and "Transport ins KH" actions; body diagram (front silhouette with square injury markers in triage colour); vitals tiles (Puls, Blutdruck, SpO₂ with values in display 2xl, abnormal in `warning`/`danger`); injuries list with state chips (blutet, versorgt, offen); treatment buttons (Druckverband secondary, Schmerzmittel, Infusion ghost, Wiederbeleben primary when unconscious); treatment log in mono, running treatment highlighted.
- **States.** No patients: "Keine Patienten – ruhige Schicht". Stale list (no update > 30 s): timestamp in `danger` and a retry button. Treatment needs an item not carried: button disabled with "Kein Verband im Inventar". Patient out of range for treatment (> 3 m): treatment buttons disabled with "Zu weit weg – näher heran". Patient revived: card status `success` "Ansprechbar", Wiederbeleben hides.
- **Interactions.** Patient click → `ems:getPatient {id}`. Route → `ems:waypoint {id}`. Treatment → `ems:treat {id, treatment}` → progress bar (10.8) on the HUD, log line added. Wiederbeleben → progress bar 10 s → `ems:revive`. Transport → confirm → `ems:transport {id}`. Notrufe list accepts calls like the MDT.

### 10.28 Boss menu

- **Anatomy.** Panel 146 × 80rem, rib header with the company plate in the job colour, "Werkstatt Ostkai · Chefmenü", "Inhaberin M. Hansen · Rang 4 · 7 Mitarbeiter, 3 im Dienst". Left 44rem: company account (3xl) with weekly change, amount field, Einzahlen (secondary) / Abheben (ghost); ranks and hourly wages list, the selected rank editable inline (input in the row). Right: tabs Mitarbeiter, Einstellen, Protokoll; search, hint "Einstellen: nur Spieler in 10 m", primary "Einstellen"; staff table: name ("· du" on own row), rank, since (mono), duty dot + text, actions (promote ↑, demote ↓ ghost icon buttons, dismiss danger-ghost icon). Footer note: dismiss and demote always confirm.
- **States.** Own row: no actions ("—"). Actions above own rank disabled. Withdraw above balance: field error. Nobody nearby to hire: Einstellen tab empty state "Niemand in der Nähe". Loading: skeleton rows; Error: error box. Protokoll empty: "Noch keine Einträge".
- **Interactions.** ↑ → `boss:promote {cid}`; ↓ → confirm → `boss:demote`; dismiss → confirm (danger) → `boss:fire`. Einstellen → nearby list → `boss:hire {target, grade}`. Wage edit → Enter saves `boss:setWage {grade, wage}`, Esc reverts. Einzahlen / Abheben → `boss:deposit` / `boss:withdraw {amount}`. Every action writes a Protokoll line and a toast.

### 10.29 Admin panel

- **Anatomy.** Panel 150 × 82rem with a `danger` lamp line and a thin hazard band across the top; plate "A" in `danger`; "Admin", "feanor · Rolle Superadmin · Aktionen werden protokolliert"; server chip "Server ok" (or `warning` "Last hoch", `danger` "Störung") and server facts in mono (players, resources, uptime, tick time). Left 46rem: player search ("ID, Name oder Lizenz") and list (ID plate, OOC name, job dot + label, ping coloured). Centre: selected player (big ID plate, character name, OOC name, playtime, warnings, job chip), identifiers masked in mono ("license:••••••••3f9a"), ping, location; action grid (Zu ihm, Holen, Zuschauen, Einfrieren, Heilen, Inventar, Nachricht, Verwarnen; ghost small); Kick/Bann card with `danger` outline: reason field (required), duration segmented (1 h, 24 h, 7 T, Dauerhaft), "Kick" danger-ghost, "Bannen" danger, disabled until a reason is given. Right 40rem: tabs Meldungen (count) / Log; report cards with a left edge in severity colour (`danger`, `warning`, `info`, `success` for closed), title, reporter, age, actions "Übernehmen" (secondary) and "Zu ID 31".
- **States.** No player selected: centre shows "Spieler links auswählen". Player left the server: centre header shows "Offline seit 2 min", live actions disabled, ban stays available. Missing permission: action button disabled with "Rolle Moderator: nicht erlaubt" under the grid. Frozen player: Einfrieren becomes "Auftauen" (secondary). No reports: "Keine offenen Meldungen". Loading and error: as section 9.
- **Interactions.** Each action → `admin:action {target, action}` and a Log line. Zuschauen → panel closes to a slim top bar "Zuschauen: ID 23 · [Esc] beenden". Bannen → confirm with typed ID → `admin:ban {target, reason, duration}`. Kick → confirm → `admin:kick {target, reason}`. Übernehmen → `admin:claimReport {id}` → card shows "übernommen: feanor". Esc → closes.

## 11. Readability and accessibility

- Text on the world always sits on a plate (`material-regular` or opaque). Measured worst case: `text-primary` on a plate over white is 11.56:1; `text-muted` on it is 5.11:1, so even meta text passes.
- Each HUD vital has an icon and a fixed position, so hue is never the only cue. Status chips carry words ("Abgeschleppt"), not only colours. Triage uses words (Rot/Gelb/Grün) next to colour.
- Every interactive element has a visible `:focus-visible` ring (`--fh-focus-ring`), works with Enter / Esc / Tab, and names its key where the game binds one.
- Disabled controls always state the reason in text near the control.
- No information only in motion: blinking items also change colour or label.
- Hit targets ≥ 3.2rem (32px at 1080p) in menus; HUD has no targets.
- Large-text rule for `danger` on `bg-elevated` (4.35:1): danger text there is display 700 ≥ 1.9rem or moves to `bg-surface`.

## 12. Do and don't

**Do**
- Keep the screen centre free during play; HUD lives in the corners.
- Use one yellow primary per view and one glow at most.
- Use slab bars for every quantity, tabular numerals for every changing number, German number formats.
- Open every panel with a house-number plate and the lamp line.
- Draw all four data states for every list, grid and table.
- Ship fonts and icons inside the resource.

**Don't**
- No graffiti, spray textures, torn paper, stencil fonts, Cyrillic jokes or GDR parody.
- No neon glow, no glassmorphism, no `backdrop-filter`, no gradients on surfaces.
- No pills or large radii on controls; no circular avatars.
- No text directly on the game world without a plate.
- No colour outside the token set; no new `--fh-*` names (the three variants must stay swappable).
- No CDN fonts, no remote images, no `ease-in`, no scale-from-zero.

## 13. NUI implementation notes

- **Offline assets.** List `html/fonts/*.woff2` and the page in `fxmanifest.lua` `files {}`; set `ui_page`. Fonts load with `font-display: block` and a `<link rel="preload" as="font" crossorigin>` for the two display weights used by the HUD (600, 700).
- **Chromium 103 baseline.** Release FiveM clients run Chromium 103. Do not use `color-mix()`, `:has()`, container queries, CSS nesting or unprefixed `mask` (use `-webkit-mask`); every tint in this document is written as a precomputed hex or `rgba()` value. `clamp()`, `max()`, `inset`, `gap`, `:focus-visible` and `font-variant-numeric` are safe.
- **No blur.** `backdrop-filter` cannot blur the game picture behind the NUI page and flickers on the current client; readability comes from the opaque `material-*` fills alone, which is why the three `--fh-blur-*` tokens are `0px`.
- **Performance in CEF.** No `backdrop-filter`, no large box-shadows on elements that update every frame (HUD values update text only), animate `opacity` and `transform` only, keep the HUD DOM static and update `textContent` and CSS custom properties (`--v` for bar fills).
- **Scaling.** The root rule in section 4 is the only scaling mechanism; do not use `zoom` or `transform: scale()` on the page.
- **Focus.** Only menus call `SetNuiFocus(true, true)`; HUD, hints, progress, toasts and the death screen never take focus. Every menu closes on Esc and returns focus.
- **Message contract.** Lua → NUI messages carry `{action, data}`; NUI → Lua callbacks are named in section 10 and always answer `{ok, error?}` so the UI can draw the error state.
- **Preview.** The full set of screens drawn from these rules, over bright and dark stand-in game worlds, is in `work/fivem-harbour-designsystem/plattenbau-preview.html` (screenshots under `work/fivem-harbour-designsystem/screenshots/`).
