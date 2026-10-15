# FiveM Harbour — Maritim

> Category: Themed & Unique
> Surface: game NUI (FiveM, CEF/Chromium, offline), 1920×1080 reference

Variant A of the `fivem-harbour-ui` series. A bright, clean harbour-instrument interface for a north-German harbour-town roleplay server: foam-white surfaces like a chart table on a sunny day, deep harbour navy for everything that must be read, signal yellow for the one thing to press, sunny-water teal for what is selected. Variants B "Plattenbau" and C "Kiez" share every `--fh-*` token name, so any screen built on these tokens can be re-skinned by swapping the token block.

## Direction and audience

**Who it is for.** Players of a German-language FiveM roleplay server set in a north-German harbour town (docks, container yard, fish market, ferries, cranes, lighthouse, brick warehouses, a red-light quarter). They read the UI in short glances while driving, running or talking on voice, mostly at 1920×1080, often at 1280×720 on weaker machines and at 2560×1440 on strong ones. A second audience works inside the UI for minutes at a time: police officers (MDT), paramedics (EMS tablet), company owners (boss menu) and staff (admin panel).

**What it should feel like.** A modern harbour on a clear day: white hulls, painted steel, navy markings, a yellow bollard, sunlit water. Minimal and precise like a ship's instrument or a nautical chart. Bright and fresh, never cosy.

**What it must not be.** No anchors, ship's wheels, rope borders, wood grain, life rings, brick textures, enamel-sign rivets or seagull clip-art. No neon, no glow-heavy sci-fi, no heavy glassmorphism. The maritime reading comes from three quiet devices only:

1. **The instrument dial** — circular gauges with tick scales for vitals and speed, like ship instruments.
2. **The signal flag** — a solid 0.6rem colour bar at the leading edge of a notification, list row or badge; colour carries the meaning, the way signal flags do.
3. **The harbour mark** — a square split diagonally into navy and signal yellow, used as the series mark on the loading screen and the character selection header. Nowhere else.

**Readability over the game world.** Every text-bearing element sits on an opaque surface or on `--fh-material-thick`; text is never placed directly on the world. Contrast is therefore a property of the UI, not of the scene behind it, and holds in sun glare, at night and over water.

## Colour palette

The series colours map as: **yellow** → `accent-primary`; **grey** → the blue-tinted neutrals (`bg-*`, `border`, `text-*`, `job-civil`); **blue** → `text-primary` navy, `info`, `job-police`; **sunny water** → `accent-secondary` and its 12 % selection tint.

Contrast ratios are WCAG 2.x relative-luminance ratios. "on surface" means against `bg-surface` `#F7FAFB`; HUD chips and panels sit on `--fh-material-thick`, which is the opaque surface, so the listed ratios hold over any scene. Text needs 4.5:1 (3:1 at ≥ 2.4rem / ≥ 1.9rem semibold); graphics and state indicators need 3:1.

| Token | Hex | Usage | Contrast against its background |
| --- | --- | --- | --- |
| `bg-base` | `#E7F1F5` | Backdrop of full-screen menus (loading, selection, creator, spawn), input fills, table zebra rows. | `text-primary` on it 14.12:1 |
| `bg-surface` | `#F7FAFB` | Panels, cards, HUD chips (via material), list bodies. | `text-primary` on it 15.45:1 |
| `bg-elevated` | `#FFFFFF` | Dialogs, popovers, menus, the dial faces, anything raised above a panel; also the light text colour on dark fills. | `text-primary` on it 16.20:1 |
| `bg-overlay` | `rgba(8, 28, 46, 0.66)` | Scrim between game world and a modal or the death screen; bottom gradient of the loading screen. | `bg-elevated` text over scrim over a white scene 5.62:1; a `bg-surface` panel stands off it at 5.35:1 |
| `border` | `#B9C8D3` | Hairline dividers, panel edges, input frames, empty slot outlines. Decorative separation, never the only cue for state. | 1.63:1 on surface (non-text divider) |
| `text-primary` | `#0B2236` | Harbour navy. All primary text, numbers, icons, the speed arc, the outline of the speed pointer, the progress fill. | 15.45:1 on surface |
| `text-secondary` | `#3A5469` | Secondary lines, labels in tables, timestamps in chat. | 7.55:1 on surface |
| `text-muted` | `#5A6F81` | Placeholders, hints, disabled labels, units ("km/h", "€"). Only on opaque surfaces or thick material. | 4.97:1 on surface · 4.55:1 on base |
| `text-on-accent` | `#0B2236` | Text and icons on `accent-primary` fills. | 10.02:1 on `accent-primary` |
| `accent-primary` | `#FFC21F` | Signal yellow. Fill of the one primary action per view, hovered radial segment, speed pointer (navy-outlined), "[E]" key in interaction hints, selected step in steppers. Always a fill carrying navy content; never a thin line or text on a light surface. | `text-on-accent` on it 10.02:1 · as fill on surface 1.54:1 (fill only) |
| `accent-secondary` | `#0A7896` | Sunny-water teal. Selection (3 px leading bar + 12 % tint fill), links, active tab underline, toggles "on", secondary filled buttons with white text. | 4.84:1 on surface · white on it 5.07:1 |
| `success` | `#16815A` | Success notification flag, "Eingeparkt", paid invoices, sufficient materials. | 4.63:1 on surface · white on it 4.86:1 |
| `warning` | `#A95F00` | Warning notification flag, low fuel, overdue invoice, engine damaged. | 4.63:1 on surface · white on it 4.86:1 |
| `danger` | `#C42F3D` | Error notification flag, destructive actions, validation errors, warrants, critical health ring. | 5.24:1 on surface · white on it 5.50:1 |
| `info` | `#1F64C4` | Info notification flag, system chat lines, neutral status. | 5.44:1 on surface · white on it 5.71:1 |
| `job-police` | `#1E4B9B` | Police badge fill, MDT header bar, police chat channel. | white on it 8.28:1 · 7.90:1 on surface |
| `job-ems` | `#C83A24` | Rettungsdienst badge fill, EMS tablet header bar. | white on it 5.14:1 · 4.90:1 on surface |
| `job-mechanic` | `#6553B0` | Werkstatt badge fill (welding-arc violet). | white on it 6.14:1 · 5.86:1 on surface |
| `job-civil` | `#5A6E80` | Civilian and unemployed badge fill, any job without its own colour. | white on it 5.28:1 · 5.03:1 on surface |
| `hud-health` | `#D3334A` | Leben dial and bar. | 4.61:1 on surface |
| `hud-armor` | `#2A68D4` | Panzerung bar. | 4.97:1 on surface |
| `hud-hunger` | `#C27812` | Hunger dial. | 3.34:1 on surface |
| `hud-thirst` | `#138BBE` | Durst dial. | 3.66:1 on surface |
| `hud-stamina` | `#4F8E1A` | Ausdauer dial. | 3.84:1 on surface |
| `hud-stress` | `#8655C9` | Stress dial. | 4.82:1 on surface |
| `hud-voice` | `#0F9775` | Voice indicator while speaking (Sprechen). | 3.51:1 on surface |
| `hud-radio` | `#C43C86` | Voice indicator while transmitting on radio (Funk), radio channel chip. | 4.62:1 on surface |
| `hud-fuel` | `#C9600E` | Fuel arc in the vehicle dial. | 3.88:1 on surface |

Rules:

- One yellow primary action per view. Outside the primary button, yellow appears only as a live marker that carries navy content: the active interaction key cap, the speed pointer, the hovered radial segment, the selected spawn pin, the "Dienste" app tile. Two yellow buttons in one view are a design error.
- Selection is always `accent-secondary`: a 0.3rem leading bar plus a tint layer — an `::after` filled with `--fh-accent-secondary` at opacity 0.12 beneath the content (the element gets `position: relative; isolation: isolate`, the layer `z-index: -1`).
- State is never colour alone: every semantic colour travels with an icon or a word (notifications have an icon and a title; low vitals blink their icon; job badges carry the job name).
- HUD colours are graphic colours (≥ 3:1). Numbers inside dials and bars stay `text-primary`.
- Hover and pressed states are derived, not tokens: on `accent-primary` fills `filter: brightness(0.94)` (hover) and `0.88` (pressed); on light rows and buttons `bg-base` as hover fill; every tint (selection 12 %, status badges 12 %, banners and drop targets 8 %) is the tint layer above with the token colour and that opacity. No `color-mix()` — see Platform constraints.

## Materials and readability over the game world

| Token | Value | Use |
| --- | --- | --- |
| `--fh-material-thick` | `#F7FAFB` (opaque, equals `bg-surface`) | Every text-bearing HUD chip, notification, hint, chat when open, panel over the world. |
| `--fh-material-regular` | `rgba(247, 250, 251, 0.94)` | The idle chat panel and the phone dock. `text-primary` and `text-secondary` only (≥ 11.8:1 and ≥ 5.7:1 even over a black scene); `text-muted` is forbidden on it. |
| `--fh-material-thin` | `rgba(247, 250, 251, 0.86)` | Non-text fills only: minimap frame ring, radial menu ring background, vehicle dial outer bezel. |
| `--fh-blur-thin` / `regular` / `thick` | `0px` / `0px` / `0px` | Defined for series swappability and bound to zero: FiveM NUI cannot blur the game picture behind the page and `backdrop-filter` flickers on the current client. Readability comes from opaque fills, never from blur. |

The HUD keeps its edge against a bright scene through `--fh-shadow-1` (a 0.1rem navy hairline plus a soft drop), and against a dark scene through its own brightness. Both are proven in the preview's day and night frames.

## Typography

All fonts are self-hosted woff2 files under `fonts/` (Latin subset, covers German umlauts, ß and €), licensed under the SIL Open Font License 1.1 (licence texts beside the files). No CDN at runtime: FiveM NUI loads them from the resource with `nui://` paths.

| Token | Family | Files | Role |
| --- | --- | --- | --- |
| `--fh-font-sans` | Barlow | 400, 500, 600, 700 | Body, controls, table cells. A grotesk related to road and harbour signage; open at small sizes. |
| `--fh-font-display` | Barlow Semi Condensed | 500, 600, 700 | Headings, uppercase labels, every number in HUD and tables (tabular figures), the speedometer. |
| `--fh-font-mono` | JetBrains Mono | 500 | Licence plates, IDs, case numbers, frequencies, key caps. |

```css
@font-face { font-family: "Barlow"; src: url("fonts/barlow-latin-400-normal.woff2") format("woff2"); font-weight: 400; font-display: block; }
@font-face { font-family: "Barlow"; src: url("fonts/barlow-latin-500-normal.woff2") format("woff2"); font-weight: 500; font-display: block; }
@font-face { font-family: "Barlow"; src: url("fonts/barlow-latin-600-normal.woff2") format("woff2"); font-weight: 600; font-display: block; }
@font-face { font-family: "Barlow"; src: url("fonts/barlow-latin-700-normal.woff2") format("woff2"); font-weight: 700; font-display: block; }
@font-face { font-family: "Barlow Semi Condensed"; src: url("fonts/barlow-semi-condensed-latin-500-normal.woff2") format("woff2"); font-weight: 500; font-display: block; }
@font-face { font-family: "Barlow Semi Condensed"; src: url("fonts/barlow-semi-condensed-latin-600-normal.woff2") format("woff2"); font-weight: 600; font-display: block; }
@font-face { font-family: "Barlow Semi Condensed"; src: url("fonts/barlow-semi-condensed-latin-700-normal.woff2") format("woff2"); font-weight: 700; font-display: block; }
@font-face { font-family: "JetBrains Mono"; src: url("fonts/jetbrains-mono-latin-500-normal.woff2") format("woff2"); font-weight: 500; font-display: block; }
```

`font-display: block` because the files are local: a swap flash in the HUD reads as a glitch.

**Size scale** (1rem = 10px at 1080p, see Scaling):

| Token | rem | px @1080p | px @720p (8px floor) | px @1440p | Use |
| --- | --- | --- | --- | --- | --- |
| `--fh-text-2xs` | 1.2rem | 12 | 9.6 | 16 | Uppercase tracked labels only (0.08em, semibold): "LEBEN", "KM/H". |
| `--fh-text-xs` | 1.3rem | 13 | 10.4 | 17.3 | Meta lines, timestamps, units, key caps. |
| `--fh-text-sm` | 1.4rem | 14 | 11.2 | 18.7 | Secondary text, table cells, chat. |
| `--fh-text-md` | 1.6rem | 16 | 12.8 | 21.3 | Body, buttons, inputs, list rows. |
| `--fh-text-lg` | 1.9rem | 19 | 15.2 | 25.3 | Panel titles, cash value, notification title. |
| `--fh-text-xl` | 2.4rem | 24 | 19.2 | 32 | Screen titles, dialog titles. |
| `--fh-text-2xl` | 3.2rem | 32 | 25.6 | 42.7 | Character name, balances. |
| `--fh-text-3xl` | 4.4rem | 44 | 35.2 | 58.7 | Speed readout, death-screen title. |
| `--fh-text-4xl` | 6.4rem | 64 | 51.2 | 85.3 | Loading-screen wordmark. |

**Weights:** `--fh-weight-regular` 400 (long text), `--fh-weight-medium` 500 (body in HUD, list rows), `--fh-weight-semibold` 600 (labels, buttons, titles), `--fh-weight-bold` 700 (display numbers, wordmark).

Line height: 1.45 for body, 1.15 for titles, 1 for numbers and key caps (inline values, not tokens). Every number uses `font-variant-numeric: tabular-nums` so values do not jitter while they change. German number format throughout: `48.210 €`, `1,2 km`, `08:42`.

## Platform constraints

FiveM NUI renders in CEF; release builds run **Chromium 103**. Everything in this system is chosen to work there:

- No `backdrop-filter`: NUI cannot blur the game picture behind the page and the property flickers on the current client. The `--fh-blur-*` tokens are bound to `0px`; legibility comes from opaque fills (`--fh-material-thick`).
- No `color-mix()`, `:has()` or container queries. Tints use the tint layer (`::after`, token colour, low opacity, `z-index: -1` inside `isolation: isolate`); hover on yellow uses `filter: brightness()`; parent styling is driven by classes the script sets; responsive behaviour uses the root rem rule and viewport units.
- Safe to use: CSS custom properties, `clamp()`/`min()`/`max()`, `conic-gradient()`, flex and grid `gap`, `inset`, `aspect-ratio`, `:focus-visible`, `font-variant-numeric`.
- Fonts and icons ship inside the resource and load via `nui://`; nothing is fetched at runtime.

## Scaling and layout

One root rule for the whole series:

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }
```

1rem = 10px at 1080p, 13.3px at 1440p, 8px at 720p (floor, so 720p renders 20 % larger than strictly proportional to stay legible), 16px cap at 4K. Every size in the system is in rem; px appear only inside `max(1px, …)` for hairlines.

**Edge anchoring.** HUD elements are positioned from the viewport edges, never on a fixed 192×108rem canvas, so ultrawide screens keep the centre free. Safe margin: `--fh-space-8` (3.2rem) from every edge.

**HUD zones.** Top-left: chat. Top-right: cash, bank, job, server ID, then the notification stack below. Bottom-left: minimap frame with the vitals strip to its right and the voice chip above the map. Bottom-centre: progress bar. Bottom-right: vehicle dial, ammo chip above it. Centre: kept free except for the interaction hint (anchored next to the object) and modals.

**Full-screen menus** fit a safe canvas of **156 × 86rem** (1560×860 at 1080p, 1248×688 at 720p), centred, so nothing overflows at the 8px floor. Phones are 38 × 76rem and anchored bottom-right at 3.2rem.

**Grid.** Panels use an 0.8rem base grid; panel padding `--fh-space-6`; gaps between sibling panels `--fh-space-4`.

## Spacing, radii, borders, shadows

| Token | Value | | Token | Value |
| --- | --- | --- | --- | --- |
| `--fh-space-0_5` | 0.2rem | | `--fh-radius-xs` | 0.2rem (key caps inner, bars) |
| `--fh-space-1` | 0.4rem | | `--fh-radius-sm` | 0.4rem (inputs, badges, slots) |
| `--fh-space-2` | 0.8rem | | `--fh-radius-md` | 0.6rem (buttons, chips, notifications) |
| `--fh-space-3` | 1.2rem | | `--fh-radius-lg` | 0.8rem (panels, dialogs) |
| `--fh-space-4` | 1.6rem | | `--fh-radius-xl` | 1.2rem (tablets, cards on world) |
| `--fh-space-5` | 2.0rem | | `--fh-radius-pill` | 999rem (dials, toggles, progress) |
| `--fh-space-6` | 2.4rem | | `--fh-border-width` | `max(1px, 0.1rem)` |
| `--fh-space-8` | 3.2rem | | `--fh-border-width-strong` | 0.2rem (input baseline, selected slot frame, drop-target frame) |
| `--fh-space-10` | 4.0rem | | | |
| `--fh-space-12` | 4.8rem | | | |
| `--fh-space-16` | 6.4rem | | | |

Radii are small on purpose: precise, instrument-like corners. Dials and pills are fully round; nothing else is.

**Shadows** (navy-tinted, never black):

- `--fh-shadow-1` — `0 0.1rem 0.2rem rgba(11,34,54,0.18), 0 0 0 max(1px,0.1rem) rgba(11,34,54,0.08)` — HUD chips, hints, notifications: a hairline plus a short drop so a white chip stays defined on a white sky.
- `--fh-shadow-2` — `0 0.2rem 0.6rem rgba(11,34,54,0.16), 0 0.8rem 2.4rem rgba(11,34,54,0.16)` — panels, phone, context menu.
- `--fh-shadow-3` — `0 0.4rem 1.2rem rgba(8,28,46,0.20), 0 2.4rem 6.4rem rgba(8,28,46,0.30)` — dialogs and tablets over the scrim.
- `--fh-glow-accent` — `0 0 0 0.3rem rgba(255,194,31,0.55)` — a yellow halo ring, used only for "live" yellow states: hold-to-confirm in progress, held interaction key, hovered radial segment. The state is always also carried by colour or icon.
- `--fh-focus-ring` — `0 0 0 0.2rem var(--fh-bg-elevated), 0 0 0 0.4rem var(--fh-text-primary)` — white gap + navy ring; visible on white panels and on dark scenes alike.

## Motion

| Token | Value | Use |
| --- | --- | --- |
| `--fh-duration-fast` | 120ms | Hover, pressed, toggle, slot highlight. |
| `--fh-duration-enter` | 200ms | Panels, notifications, menus appearing. |
| `--fh-duration-exit` | 140ms | Anything leaving; exit is shorter because the player already chose. |
| `--fh-duration-slow` | 320ms | Value changes in dials and bars, full-screen menu cross-fade, death-screen fade. |
| `--fh-ease-standard` | `cubic-bezier(0.23, 1, 0.32, 1)` | Default ease-out for every transition. |
| `--fh-ease-spring` | `cubic-bezier(0.34, 1.4, 0.64, 1)` | Small confirmations only: seatbelt click, item dropping into a slot, radial segment pick. |

Rules: enter = opacity 0 → 1 plus translate 0.8rem (notifications slide in from the right edge, panels rise 0.8rem); never scale from 0, start at 0.96 at most. No `ease-in`. Dial and bar values tween with `--fh-duration-slow`, linear for progress fills. Critical states blink with 1s steps (icon opacity 1 ↔ 0.35), not with a moving glow. Conditional HUD elements stay mounted and toggle a class so exit transitions run. `prefers-reduced-motion: reduce` (and the server option "Bewegung reduzieren") removes translation and blinking; opacity fades stay at `--fh-duration-fast`.

## Iconography

- Line icons on a 24-unit grid, 1.75 stroke, round caps and joins, no fills except status dots — the Lucide set (ISC licence) is the reference; ship only the used icons as an inline SVG sprite inside the resource.
- Sizes: 1.6rem in rows and buttons, 2rem in HUD chips and dials, 2.4rem in the radial menu, 3.2rem in empty states.
- Icons take `currentColor`: `text-primary` by default, the semantic colour inside notifications, the HUD colour inside dials.
- Maritime motifs appear only as functional pictograms where they are the clearest sign: ferry for the ferry spawn point, crane for the harbour job, lighthouse for the "Leuchtturm" spawn. Never as decoration.
- Key caps are not icons: `--fh-font-mono` semibold on a navy rounded square (`--fh-radius-sm`), white glyph, min 2.4rem square; the interaction key in world hints is a yellow cap with navy glyph.

## CSS custom properties

The complete `--fh-*` block. It is the only set of names a component may read; variant B and C bind the same names.

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }

:root {
  /* colour */
  --fh-bg-base: #E7F1F5;
  --fh-bg-surface: #F7FAFB;
  --fh-bg-elevated: #FFFFFF;
  --fh-bg-overlay: rgba(8, 28, 46, 0.66);
  --fh-border: #B9C8D3;
  --fh-text-primary: #0B2236;
  --fh-text-secondary: #3A5469;
  --fh-text-muted: #5A6F81;
  --fh-text-on-accent: #0B2236;
  --fh-accent-primary: #FFC21F;
  --fh-accent-secondary: #0A7896;
  --fh-success: #16815A;
  --fh-warning: #A95F00;
  --fh-danger: #C42F3D;
  --fh-info: #1F64C4;
  --fh-job-police: #1E4B9B;
  --fh-job-ems: #C83A24;
  --fh-job-mechanic: #6553B0;
  --fh-job-civil: #5A6E80;
  --fh-hud-health: #D3334A;
  --fh-hud-armor: #2A68D4;
  --fh-hud-hunger: #C27812;
  --fh-hud-thirst: #138BBE;
  --fh-hud-stamina: #4F8E1A;
  --fh-hud-stress: #8655C9;
  --fh-hud-voice: #0F9775;
  --fh-hud-radio: #C43C86;
  --fh-hud-fuel: #C9600E;

  /* type */
  --fh-font-sans: "Barlow", system-ui, sans-serif;
  --fh-font-display: "Barlow Semi Condensed", "Barlow", system-ui, sans-serif;
  --fh-font-mono: "JetBrains Mono", ui-monospace, Menlo, Consolas, monospace;
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
  --fh-radius-xs: 0.2rem;
  --fh-radius-sm: 0.4rem;
  --fh-radius-md: 0.6rem;
  --fh-radius-lg: 0.8rem;
  --fh-radius-xl: 1.2rem;
  --fh-radius-pill: 999rem;
  --fh-border-width: max(1px, 0.1rem);
  --fh-border-width-strong: 0.2rem;

  /* depth */
  --fh-shadow-1: 0 0.1rem 0.2rem rgba(11, 34, 54, 0.18), 0 0 0 max(1px, 0.1rem) rgba(11, 34, 54, 0.08);
  --fh-shadow-2: 0 0.2rem 0.6rem rgba(11, 34, 54, 0.16), 0 0.8rem 2.4rem rgba(11, 34, 54, 0.16);
  --fh-shadow-3: 0 0.4rem 1.2rem rgba(8, 28, 46, 0.20), 0 2.4rem 6.4rem rgba(8, 28, 46, 0.30);
  --fh-glow-accent: 0 0 0 0.3rem rgba(255, 194, 31, 0.55);
  --fh-focus-ring: 0 0 0 0.2rem var(--fh-bg-elevated), 0 0 0 0.4rem var(--fh-text-primary);
  --fh-blur-thin: 0px;
  --fh-blur-regular: 0px;
  --fh-blur-thick: 0px;
  --fh-material-thin: rgba(247, 250, 251, 0.86);
  --fh-material-regular: rgba(247, 250, 251, 0.94);
  --fh-material-thick: #F7FAFB;

  /* motion */
  --fh-duration-fast: 120ms;
  --fh-duration-enter: 200ms;
  --fh-duration-exit: 140ms;
  --fh-duration-slow: 320ms;
  --fh-ease-standard: cubic-bezier(0.23, 1, 0.32, 1);
  --fh-ease-spring: cubic-bezier(0.34, 1.4, 0.64, 1);
}
```

`tokens.css` in this package binds the repository's shared design-system schema (`--bg`, `--fg`, `--accent`, …) to the same values for Open Design artefacts; it maps `--bg` → `bg-base`, `--surface` → `bg-surface`, `--surface-warm` → `bg-elevated`, `--fg`/`--fg-2`/`--muted` → `text-primary`/`-secondary`/`-muted`, `--accent` → `accent-primary`.

## Shared component rules

Every screen is assembled from these primitives. Interaction notation: **element → what it does → what it produces** (the NUI callback posted to the client script, named `<module>:<action>`, and the visible result).

**Panel.** `bg-surface` (`--fh-material-thick` over the world), `--fh-radius-lg`, `--fh-shadow-2`, padding `--fh-space-6`. Header row: title `--fh-text-xl` semibold display, optional meta right-aligned, close button (×, 3.2rem square) top-right. A full-screen menu is a panel on the safe canvas over `--fh-bg-overlay`.

**Buttons.** Height 4rem (3.2rem compact), padding 0 `--fh-space-4`, `--fh-radius-md`, `--fh-text-md` semibold sans.
- Primary: `accent-primary` fill, `text-on-accent`. One per view. Hover `filter: brightness(0.94)`, pressed `0.88`.
- Secondary: `bg-elevated` fill, `border` frame, `text-primary`.
- Quiet: no fill, `text-primary`, hover `bg-base`.
- Destructive: `danger` fill, white text; always confirmed by a confirm dialog or a hold.
- Disabled: 45 % opacity, `not-allowed` cursor, and the reason as a tooltip or a line under the button ("Nicht genug Bargeld").
- Hold-to-confirm: a button whose fill sweeps left → right over 1.2s while the key or mouse is held; releases early = nothing happens; `--fh-glow-accent` while held.
- Every button: `:focus-visible` → `--fh-focus-ring`; Enter/Space activate; the key shortcut, when there is one, is shown as a key cap inside the button.

**Key cap and interaction hint.** See HUD § Interaction hint.

**Inputs.** Height 4rem, `bg-base` fill, `border` frame, a `--fh-border-width-strong` baseline in `text-muted` (identifies the field at 4.97:1), `--fh-radius-sm` top corners. Label above in `--fh-text-2xs` uppercase. Focus: baseline `text-primary` + focus ring. Error: baseline `danger`, message under it in `danger` `--fh-text-xs` with an alert icon. Number inputs use tabular display font and a unit suffix in `text-muted`.

**Select, segmented control, stepper, slider, toggle, swatch.**
- Segmented: a `bg-base` track, selected segment `bg-elevated` with `--fh-shadow-1` and `text-primary`; others `text-secondary`.
- Stepper: "‹ 12 / 48 ›" — arrows 3.2rem quiet buttons; ← → keys step; value in tabular display.
- Slider: 0.4rem track `border`, filled part `text-primary`, 1.8rem white thumb with `--fh-shadow-1`; value right-aligned; ← → step 1, Shift+← → step 10.
- Toggle: 4.4 × 2.4rem pill, off = `border` track, on = `accent-secondary` track, white knob; label to the left.
- Swatch: 3.2rem square, `--fh-radius-sm`; selected = focus-ring style double ring.

**Tabs.** Text tabs `--fh-text-md` semibold, `text-secondary`; active `text-primary` with a 0.3rem `accent-secondary` underline. Q / E or ← → switch tabs where the screen is keyboard-driven.

**List row and table.** Row height 4.4rem (3.6rem dense), divider `border` hairline. Hover `bg-base`. Selected: `accent-secondary` leading bar 0.3rem + 12 % tint. Numbers right-aligned tabular. Table header `--fh-text-2xs` uppercase `text-secondary`.

**Badge.** `--fh-text-2xs` semibold uppercase display, 0.2rem × 0.8rem padding, `--fh-radius-sm`. Job badges: job colour fill, white text, preceded by a 0.6rem white square (the signal flag). Status badges: semantic colour as text on 12 % tint of itself.

**Notification (toast).** See HUD § Notifications.

**Progress.** Linear 0.6rem track `border` 50 % / fill `text-primary`; label above-left, percentage above-right in tabular display.

**State patterns.** Every data-bearing screen draws these four states with the same primitives:
- **Filled** — the data.
- **Loading** — skeleton blocks in `bg-base` with a 1.2s opacity pulse (0.6 ↔ 1) in place of rows, plus the panel title; never a full-screen spinner. Inline actions are disabled.
- **Empty** — 3.2rem line icon in `text-muted`, one title line `--fh-text-lg` `text-primary`, one sentence `text-secondary`, at most one action (secondary button, or primary if it is the only way forward).
- **Error** — inline banner at the top of the panel body: 0.6rem `danger` flag, alert icon, title + one sentence, "Erneut versuchen" quiet button. Data already shown stays visible below it. Field-level errors use the input error state.

**Dialog.** `bg-elevated`, `--fh-radius-lg`, `--fh-shadow-3`, width 48rem (input) / 44rem (confirm), over `--fh-bg-overlay`; title `--fh-text-xl`; buttons right-aligned, primary last. Esc = cancel, Enter = confirm (unless focus is in a multi-line field). Focus starts on the first field (input dialog) or on "Abbrechen" (destructive confirm).

## Screens — session

### Loading screen

Full-bleed server artwork (harbour by day). A `bg-overlay` gradient rises from the bottom-left (0 → 0.66 alpha over the lowest 45 %). Bottom-left block, 3.2rem from the edges: harbour mark (4.8rem square), wordmark `--fh-text-4xl` bold display uppercase in white, one subtitle line `--fh-text-lg` white; below, the progress line (56rem wide, 0.4rem, white 30 % track, `accent-primary` fill) with phase text left ("Ressourcen laden · 214 / 386") and percentage right. Bottom-right: tip card (36rem, `--fh-material-thick`, `--fh-radius-lg`): label "TIPP 3 / 12", one tip sentence. Top-right: server chips (players online, queue position when queued).

- **Loading** (default): progress advances; phase text follows the client's load phases (Verbinden → Ressourcen laden → Karte laden → Sitzung starten). Tips rotate every 8s with a 320ms cross-fade.
- **Queued**: progress line replaced by "Warteschlange · Platz 7 von 23" and an indeterminate 0.4rem bar; estimated wait right-aligned in white.
- **Slow**: after 90s in one phase a line appears under the progress: "Das dauert länger als üblich. Große Downloads beim ersten Start sind normal."
- **Error**: not drawn by the loading screen — FiveM ends the session with its own disconnect message. **Empty**: not applicable (the screen always has a phase).
- Interaction: none. The loading screen takes no input; music volume is controlled from the pause menu.

### Multi-character selection

The game camera frames the selected character on the quay; UI is a left column and a right detail block on `--fh-material-thick` panels.

Left column (44rem wide, top 3.2rem to bottom 3.2rem): header with harbour mark + "Charakter wählen"; up to 5 slot cards (8.8rem tall): name `--fh-text-lg` semibold, job badge, "Bargeld 1.250 € · Bank 48.210 €", "Zuletzt gespielt: gestern, 22:14". Selected card: `accent-secondary` leading bar and tint. Free slot: dashed `border` frame, plus icon, "Freier Platz". Locked slot: lock icon, "Platz gesperrt · Unterstützer-Slot".

Right block (52rem, bottom-right): name `--fh-text-2xl`, born / nationality / phone number lines, job and grade, then actions: primary "Spielen" with [Enter] cap, secondary "Löschen" (destructive → confirm dialog with typed name).

- **Filled**: 1–5 characters.
- **Loading**: three skeleton cards; the ped is hidden; "Spielen" disabled.
- **Empty**: no characters → left column shows only the empty state "Noch kein Charakter" / "Erstelle deinen ersten Charakter, um in die Stadt zu kommen." with primary "Charakter erstellen".
- **Error**: banner "Charaktere konnten nicht geladen werden" / "Der Server antwortet nicht. Versuche es gleich noch einmal." + "Erneut versuchen".
- Interactions: slot card click / ↑ ↓ → selects → `multichar:preview {citizenId}`, camera swaps ped. Free slot → opens Character creator → `multichar:create {slot}`. "Spielen" / Enter → `multichar:play {citizenId}` → fades to the Spawn selector. "Löschen" → confirm dialog (type the character's first name to enable "Endgültig löschen") → `multichar:delete {citizenId}` → card leaves, success notification.

### Character creator

Ped centred; left panel (48rem, full safe height) with a step tab row: Herkunft · Gesicht · Haare · Merkmale · Kleidung · Fertig (step numbers 1–6; done steps show a check). Bottom of the panel: "Zurück" (quiet) and "Weiter" (primary); on the last step "Charakter erstellen". Bottom-centre camera hint chip: [A][D] Drehen · [W][S] Zoom · [Q][E] Kamera.

Step content uses the primitives: Herkunft = Vorname, Nachname, Geburtsdatum (TT.MM.JJJJ), Geschlecht segmented (Weiblich / Männlich), Größe slider (150–210 cm), Mutter/Vater stepper, Ähnlichkeit and Hautton sliders. Gesicht = sliders grouped "Nase", "Augen", "Kiefer". Haare = style stepper, colour swatches (16), highlight swatches. Merkmale = overlays with opacity sliders. Kleidung = starter outfits (3 cards). Fertig = summary list + rules checkbox "Ich habe die Regeln gelesen".

- **Filled**: every field set.
- **Empty**: a new creator opens with defaults and empty name fields; "Weiter" on step 1 is disabled until both names are valid.
- **Loading**: while the ped model streams: panel controls disabled, a skeleton over the step body, chip "Modell lädt …".
- **Error**: field errors ("Nur Buchstaben, 2–16 Zeichen", "Du musst mindestens 18 sein"); server rejection on create shows the error banner "Name bereits vergeben" and jumps back to step 1 with the name field in error.
- Interactions: every control → live preview → `creator:update {key, value}` (debounced 80ms). Tabs click / Q E → change step (allowed backwards always, forwards only when the current step is valid). "Charakter erstellen" → `creator:submit {…}` → button loading state (spinner replaces label, disabled) → Spawn selector on success.

### Spawn selector

Left: a stylised harbour chart (100 × 86rem panel, `bg-base` water, `bg-elevated` land, `border` grid lines, district labels in `text-muted`) with pins: 2.4rem circles, `text-primary` fill + white icon; selected pin `accent-primary` fill + navy icon + a label flag. Right: list panel (48rem): "Wo möchtest du aufwachen?" and rows with icon, name, district, distance hint: Letzter Standort · Hauptbahnhof · Fischmarkt · Fähranleger · Leuchtturm · Wohnung Speicherstraße 4 · Polizeiwache Hafen (job-locked: badge "Polizei", hidden for others). Bottom: primary "Hier aufwachen".

- **Filled**: as above.
- **Loading**: list skeleton; chart visible without pins.
- **Empty**: only "Letzter Standort" exists (new or restricted characters) → one row, chart shows one pin, sentence "Weitere Orte schaltest du durch Wohnung und Job frei."
- **Error**: chosen spawn blocked → error banner "Ort gerade nicht verfügbar" / "Dort ist kein Platz frei. Wähle einen anderen Ort."; row gets a `danger` badge "Belegt".
- Interactions: row or pin click / ↑ ↓ → select → `spawn:preview {spawnId}` → camera flies to the place (320ms UI cross-fade; camera time owned by the script). "Hier aufwachen" / Enter → `spawn:confirm {spawnId}` → screen fades out.

## Screens — HUD

All HUD chips: `--fh-material-thick` (opaque), `--fh-radius-md`, `--fh-shadow-1`. HUD is hidden when the pause menu is open, while a full-screen menu is open, and when the player toggles "HUD aus".

### Vitals (health, armor, hunger, thirst, stamina, stress)

To the right of the minimap frame, bottom-aligned with it: one chip (height 6.4rem) holding six instrument dials (4.8rem each, `--fh-space-2` apart). Dial = `bg-elevated` face, a 0.4rem ring track in `border` 60 %, value arc in the vital's HUD colour drawn clockwise from 12 o'clock, 2rem icon in the centre in the same colour. Under each dial `--fh-text-2xs` label (LEBEN, PANZER, HUNGER, DURST, AUSDAUER, STRESS).

- Health also shows as a 0.6rem bar along the bottom edge inside the minimap frame (with armour above it) so it is legible in the corner of the eye.
- Value 100–26 %: normal. ≤ 25 % (≥ 75 % for stress): icon blinks 1s, arc switches to `danger` for health, label turns `danger`. 0 %: dial face becomes `danger` 12 % tint.
- Armour at 0 % and stress at 0 % hide their dial (collapse 200ms); stamina hides while full and not running.
- Interactions: none (display only). Driven by `hud:update {health, armor, hunger, thirst, stamina, stress}`.

### Voice and radio indicator

Above the minimap frame, left-aligned: chip with microphone icon, range label and three range pips (Flüstern · Normal · Rufen), and — when tuned in — a radio segment "Funk 101,5".

- **Idle**: icon `text-secondary`, pips filled up to the active range in `text-primary`.
- **Speaking**: icon and pips `hud-voice`, the chip gets a 0.2rem `hud-voice` ring; the label stays navy.
- **Transmitting on radio**: radio segment fills `hud-radio` with white text "Funk 101,5 · Sendet"; the microphone icon turns `hud-radio`.
- **Radio muted / out of range**: radio segment struck through icon, `text-muted` "Funk 101,5 · kein Empfang".
- **Voice disconnected**: chip turns `danger` 12 % tint with "Sprachchat getrennt".
- Interactions: range key (default F11 in pma-voice style; server-configurable) → cycles range → `voice:range {1|2|3}`; pips animate with `--fh-ease-spring`.

### Cash, bank, job

Top-right stack, right-aligned, 3.2rem from the edges: cash chip ("Bargeld" label + `--fh-text-lg` bold tabular "1.250 €"), bank chip ("Bank" + "48.210 €"), job chip (job badge + "Hafenarbeiter · Kranführer"), a small server ID chip "ID 42". Changes show a delta line under the chip for 3s: "+ 850 €" in `success`, "− 45 €" in `danger`, sliding in 0.8rem.

- Duty state: job chip shows a 0.8rem dot — `success` "Im Dienst" / `text-muted` "Außer Dienst".
- Interactions: none. Driven by `hud:money {cash, bank}` and `hud:job {name, grade, duty}`.

### Ammo

Bottom-right, above the vehicle dial (or in its place on foot): chip with weapon name `--fh-text-sm` and "24 / 120" — magazine `--fh-text-2xl` bold tabular, reserve `--fh-text-md` `text-secondary`. Magazine ≤ 20 %: magazine number turns `warning`; 0: `danger` and "Nachladen [R]". Hidden when unarmed and for melee weapons.

### Minimap frame

The native minimap is shown inside a rounded-rect frame: 0.4rem `--fh-material-thin` ring, `--fh-radius-lg`, `--fh-shadow-1`; health (bottom) and armour (above it) bars inside the bottom edge. Above the frame: a compass strip chip (N · NO · O · SO · S · SW · W · NW, German letters; current heading centred in `text-primary` with "12°"), and the street chip "Kaistraße" + district "Fischmarkt" in `text-secondary`. When the big map opens the frame hides.

### Vehicle HUD

Bottom-right, 3.2rem from the edges, shown only in a vehicle (fade 200ms in / 140ms out): a 22rem instrument dial — `bg-elevated` face on a `--fh-material-thin` bezel, tick scale 0–240 km/h (major ticks every 20, labels every 40 in `text-secondary`), the speed as a `text-primary` arc from 7 o'clock on a `bg-base` track, a short pointer on the scale (yellow `accent-primary` bar outlined in navy, from the arc inwards to the tick ring — no centre hub, so the readout stays clear), centre readout `--fh-text-3xl` bold tabular + "km/h". Gear "3" chip at the bottom of the face. The outer bezel holds the fuel arc in the bottom gap (`hud-fuel` on a `border` track, 0–100 % from 5 to 7 o'clock, pump icon at its start). Below the dial a status row of four chips: indicator left · seatbelt · engine · indicator right. Boats use the same dial with "kn" and no seatbelt; aircraft are out of this system.

- **Indicators**: arrows `text-muted` when off; `success` and blinking at 1 Hz when on; hazard = both.
- **Seatbelt**: buckled = belt icon `text-primary`; unbuckled above 20 km/h = `danger` chip blinking + "Gurt!"; unbuckled while standing = `text-muted`. Toggle key (default B) → `vehicle:belt {on}`, spring click animation.
- **Engine**: on = engine icon `text-primary`; off = `text-muted` + "Motor aus"; damaged (health < 40 %) = `warning`; failing (< 15 %) = `danger` blinking. Engine key (default G) → `vehicle:engine {on}`.
- **Fuel**: ≤ 15 % arc and icon `warning`, ≤ 5 % `danger` + warning notification once.
- **Loading / empty / error**: not applicable — the vehicle HUD only exists while the client has a vehicle; electric vehicles show "Akku" with the same arc.

### Notifications

Stack at the top-right under the job chip, max 4 visible (older ones collapse into "+2 weitere"), width 40rem. Each: `--fh-material-thick`, `--fh-radius-md`, `--fh-shadow-1`; 0.6rem signal-flag bar on the left in the type colour; icon (2rem, type colour); title `--fh-text-md` semibold; text `--fh-text-sm` `text-secondary` (max 2 lines); optional timestamp `--fh-text-xs` muted. Types: **Info** (`info`, i-circle), **Erfolg** (`success`, check-circle), **Warnung** (`warning`, triangle), **Fehler** (`danger`, octagon-x). Errors stay 8s, others 5s; a thin 0.2rem bar in the type colour along the bottom shows remaining time. Enter: slide 0.8rem from the right + fade 200ms; exit: fade 140ms, stack closes up 200ms.

- Interactions: none by default (the cursor is not focused in the HUD). An actionable notification (rare: "Rechnung erhalten") shows a key cap "[Y] Öffnen" and posts `notify:action {id}`.
- Produces: driven by `notify:push {type, title, text, duration}`.

### Progress bar

Bottom-centre, 8rem above the bottom edge: chip 48rem wide: label left ("Netze flicken …"), percentage right, 0.6rem track with `text-primary` fill (linear motion), and a cancel hint "[X] Abbrechen" right of the chip. Finished: fill turns `success` 200ms and the chip fades. Cancelled: fill turns `danger`, label "Abgebrochen", fade after 800ms.

- Interaction: X → cancels → `progress:cancel {id}`.

### Interaction hint

Anchored next to the world object (projected by the script) or, without projection, at 58 % screen height centred. Chip: yellow key cap (`accent-primary`, navy glyph, `--fh-font-mono`) + action text `--fh-text-md` medium ("Kiste öffnen"). Multiple actions stack vertically, the active one has the yellow cap, the others a navy cap. Hold actions show a ring filling around the cap (`--fh-glow-accent` while held). Unavailable: cap `border` fill, text `text-muted` + reason ("Abgeschlossen").

- Interaction: E (or the shown key) → performs → `interact:use {targetId, action}`; ↑ ↓ / mouse wheel cycles stacked actions.

### Death and unconscious screen

Full-screen `--fh-bg-overlay` over the world (the desaturation of the scene is the client's timecycle effect, not CSS). Centred block, top at 30 %:

- **Bewusstlos** (can be revived): status chips and actions are `bg-elevated` chips with navy text on the scrim; title "Bewusstlos" `--fh-text-3xl` bold white; line "Rettungsdienst kann dich noch versorgen."; timer chip "Ausbluten in 04:12"; actions: "[G] Notruf senden" (secondary, light) → `death:callEms` → becomes "Notruf gesendet · Rettung unterwegs" (disabled, `success` dot); "[E] halten · Aufgeben" appears only after 60s → hold 3s → `death:giveUp` → switches to Tot.
- **Tot** (respawn): title "Du bist gestorben"; line "Du wachst im Krankenhaus auf. Erinnerungen an die letzten Minuten sind verloren."; respawn timer "Aufwachen möglich in 02:00"; then "[E] halten · Im Krankenhaus aufwachen" (hold 3s, yellow ring) → `death:respawn` → fade to white 320ms.
- **Rettung kommt**: when an EMS unit accepted the call: chip "Rettung unterwegs · 350 m" in `job-ems` badge style.
- Empty / loading / error: not applicable; if the EMS call cannot be placed ("Kein Rettungsdienst im Dienst") the G action is replaced by that line in white and the give-up action is offered immediately.

## Screens — interaction surfaces

### Radial menu

Hold the radial key (default F1) → centred ring, outer radius 22rem, inner hub 7.2rem. Ring = `--fh-material-thick` 8 segments (max 10) separated by 0.2rem gaps; each segment shows a 2.4rem icon and a `--fh-text-xs` semibold label. Hovered segment: `accent-primary` fill, navy icon and label, `--fh-glow-accent`; the hub shows the hovered item's name `--fh-text-md` semibold and a one-line hint. Segments with children show a small chevron; choosing one replaces the ring with its children (200ms) and the hub shows "‹ Zurück". Disabled segment: 40 % opacity, hub explains why.

- Items (default): Fahrzeug · Ausweis zeigen · Rechnung · Animationen · Job · Begleiten · Kleidung · Funk.
- Interactions: mouse direction or stick → hover → `radial:hover` (sound only). Release key or click → `radial:select {id}`; release in the hub → closes without action. Esc / right-click → back one level or close.
- States: **Empty** (no actions available, e.g. while cuffed): hub "Keine Aktionen verfügbar", no ring. **Loading/error**: not applicable (items are local).

### Context menu

Opened by targeting an object (third-eye) or by script: panel 36rem at the right third of the screen, vertically centred. Header: title "Kiste · Lager 7" + subtitle; rows 5.2rem: icon, label, description line `text-secondary`, chevron for submenus or a key cap for direct actions. Hover/selected row: tint + leading bar. Disabled row: muted, description gives the reason ("Brecheisen benötigt"). Submenus slide in from the right; header gets "‹".

- Interactions: click / ↑ ↓ + Enter → `context:select {menuId, itemId}` → menu closes unless the item keeps it open. Esc → back or close (`context:close`).
- States: **Loading** (server-provided menu): 3 skeleton rows. **Empty**: "Hier gibt es nichts zu tun." **Error**: banner "Aktion fehlgeschlagen" with the server message.

### Input dialog

Modal 48rem, `bg-elevated`, over scrim. Title, optional description, 1–6 fields (text, number with unit, select, multi-line, date, checkbox), buttons "Abbrechen" (secondary) and the action verb (primary, e.g. "Überweisen").

- Validation is inline on blur and on submit; the primary is enabled when required fields are filled (it does not wait for validity — submit reveals errors).
- **Loading**: after submit, primary shows a spinner + "Wird gesendet …", fields read-only. **Error**: server error banner at the top of the dialog, fields stay editable. **Empty**: required fields empty → primary disabled.
- Interactions: Enter → submit → `input:submit {id, values}`; Esc / Abbrechen → `input:cancel {id}`; Tab moves through fields.

### Confirm dialog

Modal 44rem. Icon (neutral: info; destructive: alert in `danger`), title as a question ("Fahrzeug verkaufen?"), one sentence of consequence ("Du erhältst 12.400 €. Das kann nicht rückgängig gemacht werden."), buttons "Abbrechen" + action verb. Destructive: action button `danger`, initial focus on "Abbrechen"; for irreversible deletes the action is hold-to-confirm (1.2s) or requires typing a word.

- Interactions: confirm → `confirm:accept {id}`; Abbrechen / Esc → `confirm:decline {id}`. Loading: action button spinner. Error: banner inside the dialog.

### Chat

Top-left, 3.2rem from the edges, 56rem wide, 12 visible lines. Lines on `--fh-material-regular` panel (idle the panel fades to 0 after 8s and the lines with it; new message re-shows for 8s). Each line: channel tag (badge style: OOC `job-civil`, ME / DO `accent-secondary`, Funk `hud-radio`, Polizei `job-police`, Rettung `job-ems`, System `info`, Admin `danger`), author `--fh-text-sm` semibold, text `--fh-text-sm` `text-primary`, time `--fh-text-xs` `text-secondary`. When open (T): panel goes `--fh-material-thick`, an input row appears under it with a channel prefix chip; typing "/" shows a suggestion list (command, parameters in mono, description).

- **Empty**: open with no history: "Noch keine Nachrichten. Mit /ooc schreibst du außerhalb der Rolle."
- **Error**: rejected message (spam, muted) shows a System line in `danger`: "Du bist für 5 Minuten stummgeschaltet."
- Interactions: T → opens; Enter → `chat:send {channel, text}` → line appears; Esc → closes, draft kept; ↑ ↓ → input history; Tab → completes the highlighted suggestion; PgUp/PgDn → scroll.

### Scoreboard

Hold Pos1 (Home) → centred panel 88 × 72rem. Header: server name, "128 / 200 Spieler", uptime. Summary strip: job counts with badges (Polizei 6 · Rettung 3 · Werkstatt 2 · Taxi 1). Table: ID (mono), name, job badge (only for public jobs), ping (tabular; > 150 ms `warning`, > 300 ms `danger`). Own row pinned at the top with tint. Sorted by ID.

- **Loading**: skeleton rows. **Empty**: alone on the server: "Du bist gerade allein in der Stadt." **Error**: banner "Spielerliste nicht verfügbar".
- Interactions: release key → closes. Mouse wheel scrolls (cursor appears only while held + right mouse). No actions on rows (admin actions live in the Admin panel).

## Screens — economy and items

### Inventory

Full-screen menu on the safe canvas. Left panel "Taschen" (player): weight bar ("18,4 / 30 kg", fill `text-primary`, ≥ 90 % `warning`), grid 5 columns × 6 rows of 9.6rem slots; slots 1–5 are the hotbar (small number top-left). Right panel: secondary container ("Boden", "Kofferraum · HH-AB 1234", "Handschuhfach", "Kiste · Lager 7", "Spieler"), same grid. Between them: a utility column with amount input and actions "Benutzen", "Geben", "Teilen".

Slot: `bg-elevated`, `border` frame, `--fh-radius-sm`; item image centred (4.8rem), count bottom-right tabular, durability as a 0.3rem bar on the bottom edge (`success` > 50 %, `warning` > 20 %, `danger`). Empty slot: `bg-base` fill with dashed `border`. Hover: tooltip card (name, description, weight, metadata like serial number in mono). Selected: `accent-secondary` 0.2rem frame. Dragging: slot lifts with `--fh-shadow-2`, target slot shows a 0.2rem `accent-secondary` dashed frame; invalid target (too heavy, wrong container) shows `danger` frame and the cursor reason "Zu schwer".

- **Filled**, **Empty** (secondary "Kofferraum ist leer" in the grid area; pockets never fully empty-stated, empty slots suffice), **Loading** (secondary container opening: grid skeleton, "Kofferraum wird geöffnet …"), **Error** (move rejected by server → item snaps back with `--fh-ease-spring`, error notification "Zu schwer für den Kofferraum").
- Interactions: drag slot → slot → `inventory:move {from, to, slot, amount}`; Shift+drag → splits half; amount field + drag → moves that amount; double-click / "Benutzen" → `inventory:use {slot}`; "Geben" → picks nearest player (list if several) → `inventory:give {slot, target, amount}`; 1–5 keys → `inventory:useHotbar {n}`; Tab / Esc → close.

### Phone

Device 38 × 76rem anchored bottom-right (slides up 0.8rem, 200ms), `--fh-radius-xl`, 0.8rem navy bezel (`text-primary`), screen `bg-surface`. Status bar: time, network bars, battery. Home: wallpaper (calm water photo slot, overlaid with `--fh-material-regular` under the app grid); 4-column app grid, icons 6.4rem squares in `--fh-radius-lg` with a single-colour pictogram on a tinted tile (each app one token colour: Telefon `success`, Nachrichten `info`, Kontakte `job-civil`, Bank `accent-secondary`, Garage `job-mechanic`, Karte `hud-thirst`, Kamera `text-primary`, Dienste `accent-primary` with navy icon, Einstellungen `job-civil`), labels `--fh-text-xs`. Dock: 4 apps. Notifications on the lock screen as compact toasts.

Apps follow the panel primitives at phone scale (list rows 5.6rem, title bar with "‹ Zurück"). Messages app: thread list → conversation (own bubbles `accent-secondary` with white text, others `bg-elevated` with `text-primary`), input bar with send.

- **Loading** (app opening / data): app title bar + skeleton rows. **Empty**: "Keine Nachrichten" + "Neue Nachricht". **Error**: "Kein Netz" banner in the status area when the player is out of coverage (tunnel, sea); sending fails with a per-bubble "Nicht zugestellt · Erneut senden".
- Interactions: M → open/close → `phone:open`/`phone:close`; app tile → opens app; send → `phone:sendMessage {number, text}`; call button → `phone:call {number}` → call screen (accept `success` round button, decline `danger`).

### Bank and ATM

**Bank** (counter): panel 120 × 76rem. Left column: accounts list (Girokonto, Sparkonto, Firmenkonto [job-colour flag], Gemeinschaftskonto) with balance; selected account header: name, IBAN-style number in mono, balance `--fh-text-2xl` bold. Actions row: "Einzahlen", "Abheben", "Überweisen" (primary only on "Überweisen" when that tab is active). Below: transaction table (Datum, Text, Betrag right-aligned; incoming `success` "+", outgoing `text-primary` "−").

**ATM**: compact panel 52 × 64rem: card inserted header, PIN pad (3×4 keys 7.2rem, `bg-elevated` keys, mono digits), PIN dots, then quick amounts (50 / 100 / 200 / 500 €) + "Anderer Betrag" and "Kontostand".

- **Loading**: balance and table skeleton. **Empty**: "Noch keine Buchungen auf diesem Konto." **Error**: ATM "PIN falsch · noch 2 Versuche" (dots shake 2× 120ms, field `danger`); "Automat außer Betrieb" full-panel error; transfer "Empfänger nicht gefunden" field error; insufficient funds disables the amount with reason.
- Interactions: account row → `bank:selectAccount {id}`; Einzahlen/Abheben → input dialog (amount) → `bank:deposit|withdraw {account, amount}`; Überweisen → dialog (Empfänger-Kontonummer, Betrag, Verwendungszweck) → `bank:transfer {…}`; ATM keys / number keys → PIN entry → `atm:pin {pin}`; quick amount → `atm:withdraw {amount}`.

### Shop

Panel 132 × 80rem: header (shop name "Hafenkiosk Elbblick", category tabs: Alles · Essen · Getränke · Werkzeug · Elektronik), product grid (4 columns, cards 26 × 24rem: image, name, price `--fh-text-lg` bold tabular, stock line), cart column (40rem): line items with steppers, subtotal, payment segmented "Bar / Karte" with the available balance under each, primary "Bezahlen · 37,50 €".

- Product states: in stock; low stock "Nur noch 3"; sold out (image 40 %, badge "Ausverkauft", add disabled); license-locked ("Waffenschein nötig").
- **Empty** cart: "Dein Warenkorb ist leer." **Loading**: grid skeleton. **Error**: "Nicht genug Bargeld" under the payment control, primary disabled; server reject → banner.
- Interactions: card click / "+" → `shop:addToCart {itemId}`; stepper → `shop:setQty`; Bezahlen → `shop:checkout {cart, method}` → success notification + cart clears.

### Garage

Panel 120 × 76rem titled with the garage ("Garage Speicherstadt", or "Abschlepphof" for impound). Vehicle list rows (8.8rem): model name, German plate chip (white, navy mono "HH-AB 1234", 0.4rem `info` strip on the left, `border` frame), status badge — Eingeparkt (`success`), Unterwegs (`info`), Abgeschleppt (`warning`), Beschlagnahmt (`danger`) — and three condition bars Tank / Motor / Karosserie (0.4rem, colour by threshold). Selected row opens a detail column: larger plate, mileage, last parked location, and actions: primary "Ausparken", secondary "Umbenennen"; for impounded "Auslösen · 450 €".

- **Loading**: row skeletons. **Empty**: "Hier steht kein Fahrzeug von dir." + "Fahrzeuge parkst du an jeder Garage mit [E] ein." **Error**: "Ausparken nicht möglich — Stellplatz blockiert" banner; "Fahrzeug ist bereits unterwegs" disables Ausparken with the reason.
- Interactions: row → `garage:select {plate}`; Ausparken / Enter → `garage:takeOut {plate}` → menu closes, vehicle spawns; Auslösen → confirm dialog (fee) → `garage:payImpound {plate}`; Umbenennen → input dialog → `garage:rename {plate, label}`.

### Clothing store

The camera frames the ped; a left panel (44rem): category list (Oberteile, Unterteile, Schuhe, Jacken, Hüte, Brillen, Accessoires, Taschen) with icons; selected category shows two steppers "Modell 12 / 48" and "Variante 3 / 8", a price line, and a "Gespeicherte Outfits" section. Bottom: cart total, primary "Bezahlen · 214 €", secondary "Outfit speichern". Camera chip at bottom-centre: [A][D] Drehen · [W][S] Zoom · [H] Hände hoch.

- **Loading**: stepper values "…" while the drawable streams; the ped keeps the previous item. **Empty**: no saved outfits → "Noch keine Outfits gespeichert." **Error**: "Dieses Teil passt nicht zu deinem Modell" (stepper skips; notification); payment failure banner.
- Interactions: stepper / ← → → `clothing:preview {category, drawable, texture}`; Bezahlen → `clothing:buy {changes}`; Outfit speichern → input dialog (name) → `clothing:saveOutfit {name}`; Esc → confirm "Änderungen verwerfen?" if unpaid changes exist.

### Crafting

Panel 132 × 80rem at a workbench ("Werkbank · Werft 2"). Left: recipe list with category filter chips (Werkzeug, Fischerei, Elektronik, Medizin) and search; rows show result icon, name, craft time; locked recipes muted with "Stufe 3 nötig". Right: recipe detail: result card, required materials as rows "Stahlplatte 2 / 3" — have/need tabular; missing rows `danger` text with "fehlt 1"; quantity stepper; total time; primary "Herstellen". Bottom: queue strip with progress chips per running craft.

- **Loading**: list skeleton. **Empty**: no recipes known → "Du kennst noch keine Rezepte. Bauanleitungen findest du bei Händlern im Hafen." Queue empty → strip hidden. **Error**: missing materials → "Herstellen" disabled + reason; server reject → banner.
- Interactions: recipe row → `crafting:select {recipeId}`; stepper → quantity; Herstellen → `crafting:start {recipeId, amount}` → queue chip appears, progress bar runs; queue chip × → `crafting:cancel {jobId}` (materials returned, notification).

### Invoice

Received invoice modal 52rem (`bg-elevated`, paper-clean): header with issuer (company name + job-colour flag badge, e.g. "Rettungsdienst"), invoice number mono "RE-2026-00412", date, due date; recipient; line items table (Leistung, Menge, Betrag); total `--fh-text-2xl` bold tabular; status badge Offen (`warning`) / Bezahlt (`success`) / Überfällig (`danger`). Buttons: "Ablehnen" (quiet, only if the issuer allows) and primary "Bezahlen · 1.250 €" with source select (Bank / Bar).

Issuing is the input dialog "Rechnung stellen" (Empfänger, Leistung, Betrag, Notiz).

- **Loading**: on pay, button spinner. **Empty**: invoices list (phone Bank app) → "Keine offenen Rechnungen." **Error**: "Nicht genug Guthaben auf dem Girokonto" under the source select.
- Interactions: Bezahlen → `invoice:pay {id, source}` → status badge turns Bezahlt, dialog closes after 800ms; Ablehnen → confirm → `invoice:decline {id}`.

### ID card

Shown when a player shows their card: card 54 × 34rem (ID-1 ratio) at the left-centre of the receiver's screen, `bg-elevated`, `--fh-radius-xl`, `--fh-shadow-2`, a 1.2rem `accent-secondary` header band with "PERSONALAUSWEIS" `--fh-text-2xs` white tracked and the town's coat of arms placeholder mark. Body: photo (mugshot render) 14 × 18rem, fields in two columns: Name, Vorname, Geburtsdatum, Geburtsort, Staatsangehörigkeit, Größe; ID number bottom in mono "L01X00T47"; signature line. Variants: Führerschein (header `info`, classes as small badges B · BE · C1 · A), Dienstausweis (header in the job colour, with grade), Waffenschein.

- Auto-hide after 8s or on Esc / moving away; holder sees "Du zeigst deinen Ausweis" notification.
- **Loading**: photo placeholder silhouette while the mugshot renders. **Error**: expired card shows a `danger` badge "Abgelaufen" beside the header title (no stamp graphics). **Empty**: not applicable.
- Interactions: none on the card; showing is `idcard:show {type, target}` from radial "Ausweis zeigen".

## Screens — staff tools

All tablets: device 156 × 86rem (the full safe canvas), `--fh-radius-xl`, 1.2rem `text-primary` bezel, screen `bg-base`, over `--fh-bg-overlay`. Left nav rail 24rem `bg-surface`; header bar 6.4rem in the job colour (white title and officer/user name). Esc closes; the tablet prop animation plays in-world.

### Police MDT

Header `job-police`: "Einsatzleitrechner · Polizei Hafen", officer "POK Brandt · 21/12", status chip FMS status (1 Frei auf Funk · 2 Frei auf Wache · 3 Einsatz übernommen · 4 Am Einsatzort · 6 Nicht einsatzbereit) with a status selector. Nav: Übersicht, Personen, Fahrzeuge, Vorgänge, Haftbefehle, Strafkatalog, Leitstelle. Personen view: search field (name or ID) → result list → person record: mugshot, personal data, licences, flags (badges: "Gesucht" `danger`, "Bewaffnet" `warning`), vehicles (plate chips), records table (Datum, Vorgang, Delikte, Strafe, Beamter). Leitstelle view: units list with status chips and open calls with priority.

- **Loading**: search shows row skeletons; record shows skeleton blocks. **Empty**: "Keine Treffer für „Petersen“." with hint "Suche nach Vorname, Nachname oder Bürger-ID."; new person with no records: "Keine Einträge." **Error**: "Verbindung zur Datenbank unterbrochen" banner; save of a report failed → banner + the form keeps the draft.
- Interactions: search Enter → `mdt:searchPerson {query}`; result row → `mdt:getPerson {citizenId}`; "Haftbefehl ausstellen" (danger secondary) → input dialog (Delikte, Begründung) → confirm → `mdt:createWarrant {…}`; "Vorgang anlegen" → form → `mdt:saveReport {…}`; status selector → `mdt:setStatus {code}`; call row "Übernehmen" → `mdt:acceptCall {id}` (sets status 3, waypoint).

### EMS tablet

Header `job-ems`: "Rettungsdienst · Leitstelle Hafen", medic name and status. Nav: Patienten, Einsätze, Behandlungen, Medikamente. Patienten view: list with triage chip (SK1 rot = `danger`, SK2 gelb = `accent-primary` with navy text, SK3 grün = `success`), name, location, time since call. Patient chart: vitals row (Puls, Blutdruck, SpO₂, Bewusstsein) as tabular values, injury map (front/back body outline in `border`, injured zones filled `danger` 40 % with labels "Schusswunde links Oberarm"), treatment log (time, measure, medic), action buttons "Behandlung eintragen" (primary), "In Klinik einliefern".

- **Loading**: chart skeleton. **Empty**: "Keine offenen Patienten. Ruhige Schicht." **Error**: "Patientendaten nicht verfügbar" banner.
- Interactions: patient row → `ems:getPatient {id}`; Behandlung eintragen → input dialog (Maßnahme select, Medikament, Notiz) → `ems:addTreatment {…}`; "Einsatz annehmen" → `ems:acceptCall {id}`; triage chip click → select SK → `ems:setTriage {id, level}`.

### Boss menu

Panel 132 × 80rem titled with company and job badge ("Hafenbetrieb Nord · Hafenarbeiter"). Top row: company account card (balance `--fh-text-2xl`, "Einzahlen" / "Abheben"), staff count, on-duty count. Main table: employees (Name, Rang select, Gehalt/h tabular, Im Dienst dot, Seit), row actions "Befördern" / "Degradieren" / "Entlassen" (danger, confirm). Side: "Einstellen" — nearby players list with "Einladen".

- **Loading**: table skeleton. **Empty**: "Noch keine Mitarbeitenden. Lade Spieler in deiner Nähe ein." **Error**: "Keine Berechtigung" when grade too low (full-panel error, no data); "Firmenkonto reicht nicht" on payout.
- Interactions: rank select → confirm → `boss:setGrade {citizenId, grade}`; Entlassen → destructive confirm → `boss:fire {citizenId}`; Einladen → `boss:hire {serverId}` → notification "Einladung gesendet"; Einzahlen/Abheben → input dialog → `boss:deposit|withdraw {amount}`; salary edit → `boss:setSalary {grade, amount}`.

### Admin panel

Tablet layout with header in `text-primary` navy (staff is not a job colour) and a `danger` 0.4rem flag line under it. Nav: Spieler, Meldungen, Server, Protokoll. Spieler view: table (ID mono, Name, Steam/Discord short ids mono, Ping, Spielzeit, flags), selected player detail with actions grouped: Navigation (Hinteleportieren, Herholen, Zuschauen), Hilfe (Wiederbeleben, Heilen, Einfrieren), Sanktion (Verwarnen, Kicken, Bannen — `danger`). Meldungen view: report queue (Offen / In Bearbeitung / Erledigt badges) with "Übernehmen". Server view: player count, resource status list (running `success` / stopped `text-muted` / error `danger`).

- **Loading**: skeleton. **Empty**: "Keine offenen Meldungen." **Error**: action failure banner "Spieler nicht mehr online"; permission-limited actions disabled with reason "Nur ab Rang Moderator".
- Interactions: Bannen → input dialog (Dauer select, Grund) → hold-to-confirm 1.2s → `admin:ban {serverId, duration, reason}`; Kicken → input dialog (Grund) → confirm → `admin:kick {…}`; Teleport actions → `admin:goto|bring|spectate {serverId}` (panel closes for goto/spectate); report "Übernehmen" → `admin:claimReport {id}`; every action writes the Protokoll.

## Accessibility and input

- Contrast targets as in the palette table; nothing relies on `text-muted` below thick material.
- Every interactive element has a visible `:focus-visible` (`--fh-focus-ring`) and is reachable by keyboard; key shortcuts are always shown as key caps, never only documented.
- Colour is never the only carrier: vitals have icons and labels, statuses have words, triage has SK numbers, job badges have names.
- Minimum hit area 3.2rem at 1080p (25.6px at the 720p floor).
- Blinking stays ≤ 1 Hz and stops under reduced motion; no flashing above 3 Hz anywhere.
- Text is German, set in sentence case; uppercase only for `--fh-text-2xs` labels and badges.
- Key bindings named here are defaults; the UI reads the bound key from the client and renders that cap.

## Copy

Voice: short, factual, friendly, "du"-form, no exclamation marks except the seatbelt warning, no RP slang in system copy.

**Loading tips** (rotate):
1. „Mit [F1] öffnest du das Radialmenü — Ausweis zeigen, Rechnungen und mehr.“
2. „Die Fähre zum Leuchtturm fährt alle 15 Minuten von Anleger 3.“
3. „Bargeld kann man verlieren. Was auf der Bank liegt, bleibt dir.“
4. „Fahrzeuge parkst du an jeder Garage mit [E] ein. Abgeschleppte holst du am Abschlepphof ab.“
5. „Schnall dich an: Ab 20 km/h ohne Gurt fliegt man bei einem Unfall durch die Scheibe.“
6. „Notruf: Im Handy unter Dienste — Polizei, Rettungsdienst oder Werkstatt.“
7. „Im Hafen wird nachts nicht gefischt. Der Fischmarkt öffnet um 6 Uhr.“
8. „Regelfragen? Schreib /report — das Team meldet sich.“

**Death screen**: Bewusstlos — „Rettungsdienst kann dich noch versorgen.“ · „Notruf gesendet · Rettung unterwegs“ · „Kein Rettungsdienst im Dienst.“ Tot — „Du bist gestorben“ · „Du wachst im Krankenhaus auf. Erinnerungen an die letzten Minuten sind verloren.“ · „Aufwachen möglich in 02:00“ · „[E] halten · Im Krankenhaus aufwachen“.

**Generic states**: Loading — no text, skeletons only (a label "Lädt …" for screen readers). Error title „Das hat nicht geklappt“ + specific sentence + „Erneut versuchen“. Connection — „Keine Verbindung zum Server. Wir versuchen es weiter.“

**Notification samples**: Info „Fähre legt ab“ / „Abfahrt Anleger 3 in 2 Minuten.“ · Erfolg „Gehalt erhalten“ / „+ 850 € auf dein Girokonto.“ · Warnung „Tank fast leer“ / „Noch 8 % — nächste Tankstelle in 1,2 km.“ · Fehler „Zahlung abgelehnt“ / „Nicht genug Guthaben.“

Placeholders: the server name "Nordhafen" and its subtitle are stand-ins until the real wordmark exists.

## Anti-patterns

- Rope, anchor, wheel, life-ring, wood, brick or rivet decoration; nautical clip-art; pirate typefaces.
- Text directly on the world, or `text-muted` on thin or regular material.
- Yellow as text, as a thin line or as a focus ring on light surfaces (1.5:1).
- More than one primary (yellow) action per view; yellow warning toasts (warning is amber `#A95F00`).
- Dark mode by inverting tokens: Maritim is a light system; night readability comes from the opaque chips, which the night frame proves.
- Full-screen spinners, modal loading for data that can show skeletons.
- Hard-coded hex values in components; every colour reads an `--fh-*` token, tints use the tint layer.
- `backdrop-filter`, `color-mix()`, `:has()`, container queries — see Platform constraints.
- px sizes for layout or type; everything is rem against the root rule.
- New `--fh-*` names: the set above is closed so variants B and C stay swappable.
