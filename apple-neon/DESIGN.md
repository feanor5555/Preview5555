# FiveM Street Neon

> Category: Themed & Unique
> FiveM roleplay UI, variant E. Apple-style glass and restraint over a near-black base, Los Santos nightlife in two neon hues used only for state and focus.

Street Neon is the interface layer of a FiveM roleplay server. Players are in the middle of a scene and glance at the HUD, notifications and hints for a fraction of a second. Menus, phone, inventory and job tablets take over the screen for a few seconds to a few minutes. The system is built for both: quiet glass chrome that never competes with the game, and dense panels that stay calm while a police officer runs a plate or a mechanic writes an invoice.

The design language follows current Apple practice: layered translucent material, continuous rounded shapes, generous spacing, a single tint for interaction and SF-style typography. It is carried into a Los Santos night of wet asphalt, a magenta sign over a bar and a cyan light on a dashboard. It uses no Apple trademarks, logos, product names or SF fonts. The type is Inter Variable, which is self-hosted.

Preview of every element below: `work/fivem-harbour-designsystem/apple-neon-preview.html` (repository root relative).

## 1. Visual Theme & Atmosphere

- **Who it is for.** The people this system serves are German-speaking roleplay players on a mid-size community server, plus the staff who run it: police, EMS, mechanics, business owners and admins. All UI copy is German, and the system prose is English.
- **The mood.** Late night in the city. The base is near-black with a faint violet cast (`#07070B`) rather than pure black, so glass panels can sit on it and the scene still feels like night air. Magenta (`#FF4FA3`) is the *you* colour: focus, selection, the primary action, and your own radio transmission. Cyan (`#5CE1FF`) is the *live* colour: someone is talking, a process is running, information is arriving. No third neon exists.
- **Restraint is the brand.** On any screen at most two elements glow, and the glow always means *focused* or *live*. A screen with nothing focused and nothing live has no glow at all. Everything else is neutral glass, white text and grey secondary text.
- **Glass without fake blur.** FiveM renders NUI off-screen in Chromium 103 and composites it over the game. `backdrop-filter` can neither see nor blur the game world, and over a transparent page it can flicker or paint black. Glass is therefore built from a dense tint (about 80 % opaque on the HUD), a 1px specular top edge, a hairline rim and a soft shadow. Full-screen menus get their frosted world from the game itself: the client calls the native `TriggerScreenblurFadeIn` behind the translucent scrim. CSS `backdrop-filter` is off by default, even over NUI-owned pixels. It flickers on the current client, and in testing for this system a 4rem blur made the whole element disappear in Chromium. The `--fh-blur-*` tokens stay defined so the variants remain swappable, and are used only as an opt-in that a resource has verified on the target client.
- **Readable over anything.** Every surface that carries text over the game uses `material-regular` or denser. This was measured against a pure white sky, the worst case for a dark-glass system (§2, §17).

**Key characteristics**
- Near-black base, three opaque tiers, three glass materials, one scrim
- Two neon hues: magenta for focus, selection and primary, cyan for live and info
- Inter Variable with optical sizing. Tabular numerals everywhere a number changes.
- Continuous-feel rounded rectangles with concentric radii, and capsules for actions and HUD chips
- Monoline SF-style icons, 2px stroke on a 24 grid, filled only when active
- Ring gauges for body stats, capsules for money and speed, and no bars stacked six high
- Progressive disclosure: hunger, thirst, stress and stamina appear only when they say something

## 2. Color Palette & Roles

The colour tokens are named the same in all six FiveM variants, and the values below belong to Street Neon. In each row, the contrast figure is foreground against the background named in brackets. **Worst-world** means the colour sits on `material-regular` composited over a pure white game frame (#39393E). This is the darkest-UI-on-brightest-world case, and every HUD element must survive it.

### Surfaces

| Token | Hex | Usage | Contrast |
|---|---|---|---|
| `bg-base` | `#07070B` | Full-screen opaque canvas: loading screen, character select backdrop, scoreboard sheet when the world must vanish | text-primary on it 18.5:1 |
| `bg-surface` | `#111118` | Opaque panels inside tablets (MDT, EMS, admin), table bodies, inventory slot wells | text-primary on it 17.3:1 |
| `bg-elevated` | `#1B1B24` | Raised opaque element on a surface: selected row, popover, dropdown, slot hover | text-primary on it 15.7:1 |
| `bg-overlay` | `rgba(4,4,8,0.60)` / `#04040899` | Full-screen scrim behind modal UIs (inventory, dialogs, tablets, death screen) that dims the world | text-primary on it over a white frame 5.1:1, over a sky frame 6.7:1 |
| `border` | `rgba(255,255,255,0.12)` / `#FFFFFF1F` | Hairline rim of glass and cards, dividers. Decorative, never the only signal of a state. | 1.4:1 against bg-surface (decorative, exempt under WCAG 1.4.11) |

### Text

| Token | Hex | Usage | Contrast |
|---|---|---|---|
| `text-primary` | `#F5F5F7` | Titles, values, body, button labels on neutral fills | 17.3:1 (bg-surface) · 10.5:1 worst-world |
| `text-secondary` | `#B8B8C4` | Subtitles, labels, metadata, inactive tab labels | 9.6:1 (bg-surface) · 5.8:1 worst-world |
| `text-muted` | `#9A9AA8` | Placeholders, timestamps, helper text, disabled-adjacent captions. Allowed on opaque and `material-thick` surfaces only. | 6.8:1 (bg-surface) · 5.7:1 on thick over white |
| `text-on-accent` | `#0A0A0F` | Label on magenta, cyan and semantic fills. Dark text is used on neon because white fails on it. | 6.5:1 (accent-primary) · 12.9:1 (accent-secondary) · 6.4:1 (danger) |

### Accent (the two neon hues)

| Token | Hex | Usage | Contrast |
|---|---|---|---|
| `accent-primary` | `#FF4FA3` | Focus ring, selected item, primary button fill, active tab indicator, your own radio TX. At most two visible uses per screen. | 6.2:1 (bg-surface) · 3.8:1 worst-world (graphics and large text only there) |
| `accent-secondary` | `#5CE1FF` | Live state: voice activity, running progress, GPS route, "im Dienst", live data badges | 12.2:1 (bg-surface) · 7.5:1 worst-world |

### Semantic

| Token | Hex | Usage | Contrast |
|---|---|---|---|
| `success` | `#30D158` | Completed action, stored vehicle, paid invoice, online | 9.3:1 (bg-surface) · 5.7:1 worst-world |
| `warning` | `#FFB340` | Needs attention soon: low fuel (<25 %), seatbelt off, invoice due, vehicle out | 10.5:1 (bg-surface) · 6.4:1 worst-world |
| `danger` | `#FF5A52` | Failure, destructive action, impounded, wanted, critical health | 6.1:1 (bg-surface) · 3.7:1 worst-world (icon plus text-primary label there) |
| `info` | `#5CE1FF` | Neutral information toast and hint badges. It shares the cyan hue on purpose so the screen never shows a third cool neon. | 12.2:1 (bg-surface) · 7.5:1 worst-world |

### Jobs

| Token | Hex | Usage | Contrast |
|---|---|---|---|
| `job-police` | `#6492FF` | Police job chip, MDT brand stripe, police blips in lists, police chat tag | 6.3:1 (bg-surface) · 3.9:1 worst-world |
| `job-ems` | `#FF6B6B` | EMS job chip, EMS tablet stripe, medical chat tag | 6.8:1 (bg-surface) · 4.1:1 worst-world |
| `job-mechanic` | `#FF9F45` | Mechanic job chip, workshop invoices, mechanic chat tag | 9.2:1 (bg-surface) · 5.6:1 worst-world |
| `job-civil` | `#A1A1AA` | Civilian or unemployed. It is grey on purpose, because no job means no colour. | 7.3:1 (bg-surface) · 4.5:1 worst-world |

### HUD

| Token | Hex | Usage | Contrast |
|---|---|---|---|
| `hud-health` | `#3DDC84` | Health ring. It follows the green GTA convention, and below 25 % the ring turns `danger`. | 10.5:1 (bg-surface) · 6.4:1 worst-world |
| `hud-armor` | `#7C8CFF` | Armour ring, hidden at 0 | 6.3:1 (bg-surface) · 3.9:1 worst-world |
| `hud-hunger` | `#FF9F45` | Hunger ring, shown below 50 % | 9.2:1 (bg-surface) · 5.6:1 worst-world |
| `hud-thirst` | `#4FB0FF` | Thirst ring, shown below 50 % | 8.0:1 (bg-surface) · 4.9:1 worst-world |
| `hud-stamina` | `#F5D64E` | Stamina ring, shown while sprinting or swimming and below 100 % | 13.1:1 (bg-surface) · 8.0:1 worst-world |
| `hud-stress` | `#B48CFF` | Stress ring, shown above 10 % | 7.3:1 (bg-surface) · 4.4:1 worst-world |
| `hud-voice` | `#5CE1FF` | Proximity voice: talking indicator and range dots | 12.2:1 (bg-surface) · 7.5:1 worst-world |
| `hud-radio` | `#FF4FA3` | Radio: own transmission glows magenta, and the channel number shows | 6.2:1 (bg-surface) · 3.8:1 worst-world |
| `hud-fuel` | `#FFC857` | Fuel capsule bar. Below 25 % it shows `warning` and below 10 % `danger`. | 12.2:1 (bg-surface) · 7.5:1 worst-world |

**Rules of colour**
- Colour marks a *state* and never decorates. Panel headers, borders, icons at rest and numbers at rest are neutral.
- Every coloured signal is paired with an icon or a word. Colour is never the only carrier, and the job, status and HUD colours all come with their icon.
- Tinted fills (badges, icon tiles, toast dots) put the colour at 16 % behind the coloured glyph. Build them with a `::before` layer filled with `currentColor` at `opacity: .16`. Chromium 103 has no `color-mix()`.
- Shared values are deliberate: `info` = `accent-secondary` = `hud-voice` (cyan), `hud-radio` = `accent-primary` (magenta) and `hud-hunger` = `job-mechanic` (orange). They never appear in the same component.

## 3. Typography Rules

### Families (self-hosted, no CDN)

FiveM NUI loads from the resource. Ship the woff2 files in the resource, list them under `files {}` in `fxmanifest.lua`, and reference them by relative URL. No `fonts.googleapis.com` and no `@import` from the web.

| Token | Stack | File(s) in this package |
|---|---|---|
| `--fh-font-sans` | `"Inter Variable", "Inter", system-ui, "Segoe UI", sans-serif` | `fonts/InterVariable.woff2` (wght 100–900, opsz 14–32), OFL in `fonts/OFL-inter.txt` |
| `--fh-font-display` | same family. Display sizes get the optical size axis through `font-optical-sizing: auto`, which gives the tight "display" cut at 32px and above. | same file |
| `--fh-font-mono` | `"IBM Plex Mono", ui-monospace, Consolas, "Courier New", monospace` | `fonts/IBMPlexMono-Regular-latin.woff2` (400), `fonts/IBMPlexMono-Medium-latin.woff2` (500), OFL in `fonts/OFL-ibmplexmono.txt` |

```css
@font-face { font-family: "Inter Variable"; src: url("fonts/InterVariable.woff2") format("woff2");
  font-weight: 100 900; font-style: normal; font-display: block; }
@font-face { font-family: "IBM Plex Mono"; src: url("fonts/IBMPlexMono-Regular-latin.woff2") format("woff2");
  font-weight: 400; font-display: block; }
@font-face { font-family: "IBM Plex Mono"; src: url("fonts/IBMPlexMono-Medium-latin.woff2") format("woff2");
  font-weight: 500; font-display: block; }
```

Use `font-display: block`, because NUI loads from local disk in well under 100 ms and a fallback-font flash on the HUD looks like a glitch.

**Mono is for codes and nothing else.** Use it for licence plates, ID numbers, case numbers, server IDs, log lines in the admin console, IBANs and coordinates. Names, prices and speed use Inter with tabular numerals.

### Features

- The global setting is `font-feature-settings: "tnum" 1, "cv11" 1;`: tabular numerals so changing values do not jitter, and `cv11` for a single-storey `a`, which reads calmer at small sizes.
- Display sizes (≥ `2xl`) take `letter-spacing: -0.02em` and `font-weight: 650`, the variable axis between semibold and bold that gives the machined headline feel.
- Small caps labels (section headers, HUD micro labels) are `2xs`, uppercase, `letter-spacing: 0.08em`, weight 600. Use them at most once per group.

### Scale (rem; 1rem = 10px at 1080p)

| Token | rem | px @1080p | Weight | Line height | Use |
|---|---|---|---|---|---|
| `--fh-text-2xs` | 1.1 | 11 | 600 | 1.2 | Uppercase micro labels, key-cap legends, HUD unit labels |
| `--fh-text-xs` | 1.2 | 12 | 500 | 1.35 | Captions, timestamps, table meta, badge text |
| `--fh-text-sm` | 1.4 | 14 | 400/500 | 1.4 | Secondary body, list subtitles, helper text, chat lines |
| `--fh-text-md` | 1.6 | 16 | 400/600 | 1.45 | Body, buttons, list titles, input values |
| `--fh-text-lg` | 2.0 | 20 | 600 | 1.25 | Panel section titles, notification titles in large mode, money values |
| `--fh-text-xl` | 2.4 | 24 | 650 | 1.2 | Panel titles, dialog titles |
| `--fh-text-2xl` | 3.2 | 32 | 650 | 1.1 | Screen titles (character select, bank balance) |
| `--fh-text-3xl` | 4.4 | 44 | 650 | 1.05 | Big numbers: account balance, death timer |
| `--fh-text-4xl` | 6.4 | 64 | 650 | 1.0 | Speedometer value, loading-screen wordmark |

### Weights

| Token | Value | Use |
|---|---|---|
| `--fh-weight-regular` | 400 | Body, descriptions, chat |
| `--fh-weight-medium` | 500 | Values in lists, secondary buttons, table cells that matter |
| `--fh-weight-semibold` | 600 | Buttons, list titles, labels, HUD values |
| `--fh-weight-bold` | 700 | Display numbers only (speed, balance, timers). Headlines use the 650 axis value directly. |

## 4. Spacing, Layout & Scaling

### Root scaling (shared rule for all six variants)

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }
```

`1rem` is 10px at 1080p and 13.3px at 1440p, and it clamps to 8px at 720p and 16px at 1728p and above. Every size in the system is in `rem`, and px is used only for the 1px hairline floor. The consequences are:

- **The layout budget is 160 × 90 rem.** At 1280×720 the viewport is 160 × 90 rem, because the 8px floor keeps text readable instead of shrinking with the screen. At 1080p and 1440p it is 192 × 108 rem. Every full-screen composition must fit 160 × 90 rem and anchor to edges or centre, never to a fixed 192 × 108 canvas.
- **Safe margin.** HUD and panels keep `--fh-space-10` (4rem) from every edge. That leaves an inner area of at least 152 × 82 rem.
- **Largest panels.** A centred tablet (MDT, EMS, admin, boss) is at most 148 × 80 rem. A two-column panel (inventory, garage, bank, shop) is at most 136 × 76 rem.
- **Above 16:9.** Ultrawide screens get more horizontal rem, so keep anchors at the edges and the centre content centred. Do not stretch panels.

### Spacing scale

| Token | rem | px @1080p | Use |
|---|---|---|---|
| `--fh-space-0_5` | 0.2 | 2 | Ring-to-icon gap, hairline offsets |
| `--fh-space-1` | 0.4 | 4 | Icon–label gap in badges, segmented-control inset |
| `--fh-space-2` | 0.8 | 8 | Inside chips, gap between HUD rings, key cap to label |
| `--fh-space-3` | 1.2 | 12 | Row inner gap, toast padding (vertical) |
| `--fh-space-4` | 1.6 | 16 | Default control padding, toast padding (horizontal), list gap |
| `--fh-space-5` | 2.0 | 20 | Button horizontal padding, card padding (compact) |
| `--fh-space-6` | 2.4 | 24 | Card padding, gap between panel sections |
| `--fh-space-8` | 3.2 | 32 | Panel padding, dialog padding |
| `--fh-space-10` | 4.0 | 40 | Screen safe margin, gap between panel columns |
| `--fh-space-12` | 4.8 | 48 | Large section separation on full-screen flows |
| `--fh-space-16` | 6.4 | 64 | Hero spacing on loading screen and character select |

### Control sizes (component constants, rem)

| Element | Height | Notes |
|---|---|---|
| Button (default) | 4.4 | Capsule, padding 0 2rem |
| Button (small) | 3.2 | Capsule, padding 0 1.4rem, `text-sm` |
| Button (large, flow CTA) | 5.6 | Capsule, `text-lg` |
| Text field / select | 4.4 | Radius `sm` |
| List row | 5.6 (two-line 6.4) | Radius `md` when standalone, flush inside grouped lists |
| Key cap | 2.4 × min 2.4 | Radius `xs` |
| HUD ring | 4.8 outer, 0.4 stroke | Inside a capsule of 6.4 height |
| Inventory slot | 8.8 × 8.8 | Radius `md` |

### HUD anchor map (1080p reference, all offsets 4rem safe margin)

| Zone | Content |
|---|---|
| Top-left | Chat (52rem wide, 7 lines at rest, fades out after 10 s idle) |
| Top-centre | Notification stack (44rem wide, max 3) |
| Top-right | Money capsules (cash, bank) and job capsule |
| Centre | Radial menu and context menu at the cursor or target. Interaction hint 8rem below the screen centre. |
| Bottom-centre | Progress capsule (14rem above the bottom edge) |
| Bottom-left | Minimap frame, street label above it, status ring capsule to its right, voice and radio capsule above the rings |
| Bottom-right | Vehicle HUD (in vehicle), ammo capsule above it, or alone in the corner on foot |

## 5. Shape, Depth & Materials

### Radii, continuous and concentric

| Token | rem | px @1080p | Use |
|---|---|---|---|
| `--fh-radius-xs` | 0.6 | 6 | Key caps, tiny tags, checkbox |
| `--fh-radius-sm` | 1.0 | 10 | Inputs, selects, small tiles, icon tiles in rows |
| `--fh-radius-md` | 1.4 | 14 | List rows, inventory slots, cards inside panels, popover items |
| `--fh-radius-lg` | 2.0 | 20 | Notifications, context menu, cards, minimap frame |
| `--fh-radius-xl` | 2.8 | 28 | Panels, dialogs, tablets, phone screen |
| `--fh-radius-pill` | 99.9 | — | Buttons, HUD capsules, badges, segmented control, progress bar |

- **Concentricity.** An inner element's radius is the outer radius minus the padding between them, never larger. Examples: a panel at `xl` (2.8) with 1.6 padding holds a card at 1.2, so use `sm` or `md`. A capsule holds capsules.
- **Continuous corners.** CSS radii are circular arcs. Apple's continuous (squircle) feel is approximated by using generous radii and never placing a small radius on a large surface. Chromium 103 does not support `corner-shape`, so do not use it.
- Never mix a sharp corner with a round one on the same element. Tables inside tablets sit in a rounded `bg-surface` well, and rows have no corners of their own.

### Borders

| Token | Value | Use |
|---|---|---|
| `--fh-border-width` | `max(1px, 0.1rem)` | Hairline rim of every glass surface, dividers, field outline at rest |
| `--fh-border-width-strong` | `0.2rem` | Selected card or slot (in `accent-primary`), drag-target outline, error field outline (in `danger`) |

Glass gets its edge from light, not lines. Every glass surface gets `border: var(--fh-border-width) solid var(--fh-border)` **plus** a specular top edge `inset 0 0.1rem 0 rgba(255,255,255,0.08)`. Do not use other outlines.

### Shadows and glow

| Token | Value | Use |
|---|---|---|
| `--fh-shadow-1` | `0 0.2rem 0.8rem rgba(0,0,0,0.35)` | HUD capsules, key caps, chips over the world (separation from bright frames) |
| `--fh-shadow-2` | `0 0.8rem 2.4rem rgba(0,0,0,0.45), 0 0.2rem 0.6rem rgba(0,0,0,0.30)` | Notifications, menus, cards that float |
| `--fh-shadow-3` | `0 2.4rem 6.4rem rgba(0,0,0,0.55), 0 0.6rem 1.6rem rgba(0,0,0,0.35)` | Panels, dialogs, tablets, phone |
| `--fh-glow-accent` | `0 0 0 0.1rem rgba(255,79,163,0.55), 0 0 2.4rem rgba(255,79,163,0.40)` | The *one* hero glow: primary CTA in a flow, selected character, active radial segment, own radio TX |
| `--fh-focus-ring` | `0 0 0 0.2rem var(--fh-bg-base), 0 0 0 0.4rem var(--fh-accent-primary), 0 0 1.6rem rgba(255,79,163,0.45)` | Keyboard and controller focus on every interactive element |

A cyan "live" glow is not a token. Where a live element glows (talking indicator, running progress), it uses `0 0 1.6rem rgba(92,225,255,0.45)` inline. It appears only while the state is live and stops the moment it ends.

### Materials and blur

| Token | Value | Use | Text allowed |
|---|---|---|---|
| `--fh-material-thin` | `rgba(18,18,25,0.70)` | Chrome without small text: key-cap plates, the radial ring track, the minimap frame, the vehicle indicator pod | text-primary ≥ `lg` only (6.4:1 worst-world) |
| `--fh-material-regular` | `rgba(14,14,20,0.82)` | HUD capsules, notifications, hint, progress, context menu, chat input | text-primary and text-secondary (≥ 5.8:1 worst-world) |
| `--fh-material-thick` | `rgba(10,10,15,0.90)` | Panels and dialogs with dense text: inventory, bank, shop, garage, scoreboard, chat log, tablets | all text tokens (muted ≥ 5.7:1 worst-world) |

| Token | Value | Use |
|---|---|---|
| `--fh-blur-thin` | `1.2rem` | Opt-in only: sheet over NUI content (phone dock over wallpaper, dropdown over a panel) |
| `--fh-blur-regular` | `2.4rem` | Opt-in only: dialog over an NUI panel (confirm over inventory) |
| `--fh-blur-thick` | `4rem` | Opt-in only: loading-screen glass over its own NUI art |

**Blur rule (Chromium 103 / NUI off-screen rendering).** CSS blur is off by default. Every surface must meet §2 with its tint alone. A resource may add `backdrop-filter: blur(var(--fh-blur-*)) saturate(160%)` only to a surface whose backdrop is NUI content, and only after it has checked on the target client that the surface neither flickers nor disappears. Never apply it over the transparent world: it cannot blur the game and may flicker or paint black. To blur the world itself, use the native screen blur described next.

**Full-screen menus: native blur and scrim.** A modal UI (inventory, shop, garage, bank, dialogs, tablets, death screen) blurs the world with the game's own screen blur. On open the client calls `TriggerScreenblurFadeIn(200)`, matching `--fh-duration-enter`, and on close `TriggerScreenblurFadeOut(140)`, matching `--fh-duration-exit`. The NUI then dims the blurred frame with `--fh-bg-overlay` on a full-screen layer, plus a radial vignette `radial-gradient(120% 90% at 50% 50%, transparent 40%, rgba(0,0,0,0.35))`. Legibility is specified without the native blur, so the scrim plus `material-thick` alone meet §2, and the blur is atmosphere. The HUD, notifications, hints and progress never trigger the screen blur. The HUD has no scrim. Instead, the HUD corners get a legibility gradient only when a bright frame is detected (optional client hook `hud.setLegibility(true)`): a 40rem corner `radial-gradient` from `rgba(0,0,0,0.35)` to transparent.

## 6. Motion

| Token | Value | Use |
|---|---|---|
| `--fh-duration-fast` | `120ms` | Hover, press, toggle thumb, focus ring in, colour changes |
| `--fh-duration-enter` | `200ms` | Panels, toasts, menus, hints entering |
| `--fh-duration-exit` | `140ms` | Everything leaving. Exit is shorter because the player already decided. |
| `--fh-duration-slow` | `420ms` | Screen-level transitions (loading → character select, spawn camera fade), ring value changes |
| `--fh-ease-standard` | `cubic-bezier(0.23, 1, 0.32, 1)` | Default for every UI transition (strong ease-out) |
| `--fh-ease-spring` | `cubic-bezier(0.34, 1.4, 0.64, 1)` | Small overshoot for *one* gesture per component: radial menu open, toggle thumb, notification drop-in, slot drop. Never on panels. |

**Patterns**
- **Enter:** `opacity 0 → 1` + `transform: translateY(0.8rem) scale(0.98) → none`, `enter` with `ease-standard`. Notifications drop from `translateY(-1.2rem)` with `ease-spring`.
- **Exit:** `opacity → 0` + `scale(0.98)`, `exit`. Never animate from `scale(0)`. Use the individual `transform` property, because the `scale`/`translate` properties are Chromium 104+ and not in NUI.
- **Keep mounted, toggle a class.** HUD elements that come and go (hunger ring, ammo, vehicle HUD) stay in the DOM and toggle `.is-visible` so the exit transition plays.
- **HUD values** animate ring `stroke-dasharray` over `slow`. Health loss flashes the ring once (opacity 1 → 0.4 → 1, 2 × 120ms) and never shakes.
- **Live pulses** (talking, indicators, seatbelt warning) are the only loops. The talking glow breathes at 1.2 s, the indicators blink at 0.75 s on / 0.75 s off like a real car, and the seatbelt warning pulses at 1 s while the speed is over 30 km/h.
- **Progress** fills linearly, the only linear curve in the system.
- **Reduced motion.** `@media (prefers-reduced-motion: reduce)` and the server setting `ui.reduceMotion` drop all translate and scale, keep opacity fades at `fast`, and turn pulses into steady states. NUI ignores the OS media query, so the client must set `html.reduce-motion`.

## 7. Iconography

- **Style.** Monoline, SF-Symbols-like but drawn for this system. 24 × 24 grid, 2px stroke (`0.2rem` at display size 2.4rem), `stroke-linecap: round`, `stroke-linejoin: round`, 2px corner rounding, optical centre on the grid, no detail under 2px.
- **Filled variant = active.** The outline is at rest and the filled glyph is active, for example the microphone while talking, the seatbelt when buckled, or the selected tab. This is the only place fill appears.
- **Sizes.** 1.6rem inline with `sm` text, 2rem in rows and buttons, 2.4rem in the HUD and toasts, and 3.2rem in empty states. Icons take `currentColor`, which defaults to `text-primary` and becomes the state colour only when the state is non-neutral.
- **Icon tiles.** In lists and toasts an icon sits in a 3.6rem tile (radius `sm`) or circle tinted at 16 % of its state colour. Neutral tiles use `rgba(255,255,255,0.08)`.
- **Delivery.** Ship one inline SVG sprite (`<symbol id="i-…">`) per resource and reference it with `<use href="#i-…">`. Do not use icon fonts or remote sprites.
- **Core set (names fixed across variants):** heart, shield, food, drop, run, brain, mic, radio, wallet, bank, briefcase, bullet, seatbelt, engine, fuel, arrow-left, arrow-right, gauge, map-pin, home, car, phone, bag, cart, wrench, hammer, file, id, police, cross, crown, terminal, user, users, search, filter, check, x, alert, info, chevron, plus, minus, lock, clock, gear, logout, eye, trash, send.

## 8. Token Reference

Every NUI resource pastes this block (plus §3 `@font-face` and the §4 root rule) into its stylesheet. The names are shared by all six FiveM variants, so swapping a variant means swapping this block.

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }

:root {
  /* Colour: surfaces */
  --fh-bg-base: #07070B;
  --fh-bg-surface: #111118;
  --fh-bg-elevated: #1B1B24;
  --fh-bg-overlay: rgba(4, 4, 8, 0.60);
  --fh-border: rgba(255, 255, 255, 0.12);

  /* Colour: text */
  --fh-text-primary: #F5F5F7;
  --fh-text-secondary: #B8B8C4;
  --fh-text-muted: #9A9AA8;
  --fh-text-on-accent: #0A0A0F;

  /* Colour: accent and semantic */
  --fh-accent-primary: #FF4FA3;
  --fh-accent-secondary: #5CE1FF;
  --fh-success: #30D158;
  --fh-warning: #FFB340;
  --fh-danger: #FF5A52;
  --fh-info: #5CE1FF;

  /* Colour: jobs */
  --fh-job-police: #6492FF;
  --fh-job-ems: #FF6B6B;
  --fh-job-mechanic: #FF9F45;
  --fh-job-civil: #A1A1AA;

  /* Colour: HUD */
  --fh-hud-health: #3DDC84;
  --fh-hud-armor: #7C8CFF;
  --fh-hud-hunger: #FF9F45;
  --fh-hud-thirst: #4FB0FF;
  --fh-hud-stamina: #F5D64E;
  --fh-hud-stress: #B48CFF;
  --fh-hud-voice: #5CE1FF;
  --fh-hud-radio: #FF4FA3;
  --fh-hud-fuel: #FFC857;

  /* Typography */
  --fh-font-sans: "Inter Variable", "Inter", system-ui, "Segoe UI", sans-serif;
  --fh-font-display: "Inter Variable", "Inter", system-ui, "Segoe UI", sans-serif;
  --fh-font-mono: "IBM Plex Mono", ui-monospace, Consolas, "Courier New", monospace;
  --fh-text-2xs: 1.1rem;
  --fh-text-xs: 1.2rem;
  --fh-text-sm: 1.4rem;
  --fh-text-md: 1.6rem;
  --fh-text-lg: 2rem;
  --fh-text-xl: 2.4rem;
  --fh-text-2xl: 3.2rem;
  --fh-text-3xl: 4.4rem;
  --fh-text-4xl: 6.4rem;
  --fh-weight-regular: 400;
  --fh-weight-medium: 500;
  --fh-weight-semibold: 600;
  --fh-weight-bold: 700;

  /* Spacing */
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

  /* Shape */
  --fh-radius-xs: 0.6rem;
  --fh-radius-sm: 1rem;
  --fh-radius-md: 1.4rem;
  --fh-radius-lg: 2rem;
  --fh-radius-xl: 2.8rem;
  --fh-radius-pill: 99.9rem;
  --fh-border-width: max(1px, 0.1rem);
  --fh-border-width-strong: 0.2rem;

  /* Depth */
  --fh-shadow-1: 0 0.2rem 0.8rem rgba(0, 0, 0, 0.35);
  --fh-shadow-2: 0 0.8rem 2.4rem rgba(0, 0, 0, 0.45), 0 0.2rem 0.6rem rgba(0, 0, 0, 0.30);
  --fh-shadow-3: 0 2.4rem 6.4rem rgba(0, 0, 0, 0.55), 0 0.6rem 1.6rem rgba(0, 0, 0, 0.35);
  --fh-glow-accent: 0 0 0 0.1rem rgba(255, 79, 163, 0.55), 0 0 2.4rem rgba(255, 79, 163, 0.40);
  --fh-focus-ring: 0 0 0 0.2rem var(--fh-bg-base), 0 0 0 0.4rem var(--fh-accent-primary), 0 0 1.6rem rgba(255, 79, 163, 0.45);

  /* Materials */
  --fh-blur-thin: 1.2rem;
  --fh-blur-regular: 2.4rem;
  --fh-blur-thick: 4rem;
  --fh-material-thin: rgba(18, 18, 25, 0.70);
  --fh-material-regular: rgba(14, 14, 20, 0.82);
  --fh-material-thick: rgba(10, 10, 15, 0.90);

  /* Motion */
  --fh-duration-fast: 120ms;
  --fh-duration-enter: 200ms;
  --fh-duration-exit: 140ms;
  --fh-duration-slow: 420ms;
  --fh-ease-standard: cubic-bezier(0.23, 1, 0.32, 1);
  --fh-ease-spring: cubic-bezier(0.34, 1.4, 0.64, 1);
}
```

**The repository schema in `tokens.css`** carries the same decisions in px for Open Design artefacts: `--bg` = bg-base, `--surface` = bg-surface, `--surface-warm` = bg-elevated, `--fg` / `--fg-2` / `--muted` = text-primary / text-secondary / text-muted, `--border` = border, `--accent` = accent-primary, `--accent-on` = text-on-accent, `--success` / `--warn` / `--danger` = success / warning / danger, and the type scale is the px column of §3.

**Chromium 103 compatibility.** The values contain no `color-mix()`, `oklch()`, relative colour syntax, `:has()`, container queries, `dvh`, `text-wrap` or individual `scale`/`translate` properties. `clamp()`, `max()`, `inset`, `aspect-ratio`, flex `gap`, `conic-gradient`, `:focus-visible`, `accent-color`, `@layer`, variable fonts and `font-optical-sizing` are all safe.

## 9. Interaction Model & Shared States

### Input and focus

- **NUI focus.** A screen that takes input calls `SetNuiFocus(true, true)` when it opens and `SetNuiFocus(false, false)` when it closes. HUD, notifications, hints and progress never take focus. A panel opens with focus on its first meaningful control: the search field in lists, the primary field in dialogs, the selected card in flows.
- **Keyboard everywhere.** `Esc` closes the top layer, or steps back one level in nested flows. `Tab`/`Shift+Tab` and the arrow keys move focus, `Enter` activates, and `Space` toggles. Every control shows `--fh-focus-ring` on `:focus-visible`. Inside grids (inventory, app grid, radial) the arrow keys move between cells.
- **Close affordance.** Every panel has a 3.2rem round close button at its top-right showing the `x` icon, plus an `Esc` key-cap hint in the footer.
- **Pointer.** Hover lightens neutral fills from `rgba(255,255,255,0.08)` to `0.14`. Press darkens back to `0.06` and scales to 0.98. The cursor is the game's NUI cursor, so no custom cursors.

### Component states (every interactive element)

| State | Treatment |
|---|---|
| Default | Neutral fill `rgba(255,255,255,0.08)` (buttons, rows), or `accent-primary` fill (primary button) |
| Hover | Neutral fill at 0.14, primary at `#FF6BB3` |
| Focus-visible | `--fh-focus-ring`, independent of hover |
| Pressed | Fill at 0.06 (primary `#E8408F`), `transform: scale(0.98)`, `fast` |
| Selected | `--fh-border-width-strong` ring in `accent-primary` plus a filled icon. A selected card also gets `--fh-glow-accent` when it is the screen's single hero. |
| Disabled | Opacity 0.38 and no hover. A tooltip or helper line says *why* ("Nur im Dienst verfügbar"). |
| Busy | Label replaced by a 1.6rem spinner (cyan arc) with the label kept for width. The control stays focusable and repeat clicks do nothing. |

### The four data states (every screen that shows data)

| State | Pattern |
|---|---|
| **Loading** | Skeleton rows and blocks in `rgba(255,255,255,0.06)` with a shimmer sweep (1.4 s, linear) and the layout already at its final size. After 8 s the skeleton gets the line "Dauert länger als üblich …" and a ghost `Erneut versuchen` button. |
| **Empty** | A centred 3.2rem neutral icon, a one-line title in `text-primary`, one line of `text-secondary` saying what fills this place, and at most one action. The empty state is never coloured. |
| **Error** | A centred `alert` icon in `danger` tint, the title "Konnte nicht geladen werden", the cause in plain German ("Keine Verbindung zum Server"), and `Erneut versuchen` (secondary). An error from an action shows as a `danger` toast, and the panel stays usable. |
| **Filled** | The real content. Lists over 8 rows scroll inside the panel with a 2.4rem fade mask at the top and bottom. Their headers stay pinned. |

### NUI messages

Each interactive element below names its effect as `→ nui:<resource>.<action> {payload}` (a `fetch('https://<resource>/<action>')` from the page) and the result it produces. The Lua side answers `{ ok: true, data }` or `{ ok: false, error }`. `ok: false` always ends in the screen's error pattern or a `danger` toast with the server's message.

## 10. Component Rules — Shared Primitives

| Component | Anatomy | Rules |
|---|---|---|
| **Button** | Capsule, icon 2rem optional, label `md` 600 | Variants: `primary` (accent fill, on-accent label, one per view), `secondary` (white 8 %), `ghost` (transparent, `text-secondary`), `danger` (danger 16 % tint and danger label, solid danger fill only inside a confirm dialog). Sizes: small 3.2, default 4.4, large 5.6. Labels are verbs in German infinitive ("Ausparken", "Bezahlen"). |
| **Icon button** | 3.2 or 4.4 round | Neutral fill. Always has `aria-label` and a tooltip after 500 ms hover. |
| **Text field** | Label `sm` `text-secondary` above, 4.4 field radius `sm`, helper `xs` below | Fill `rgba(255,255,255,0.06)` with a hairline border. Focus shows the focus ring. Error shows a strong `danger` border and a `danger` helper line starting with the `alert` icon. Number fields right-align with tabular figures and a unit suffix (€, km/h, kg). |
| **Select / dropdown** | Field with a `chevron`. The list is a `bg-elevated` popover, radius `md`, `shadow-2`, max 8 rows. | Arrow keys move, type-ahead works, and the selected row shows a magenta `check`. |
| **Segmented control** | Capsule track `rgba(255,255,255,0.08)` with a sliding thumb `rgba(255,255,255,0.18)`, labels `sm` 600 | Use 2–5 options. The thumb slides over `enter` with `ease-standard`. It does not use accent: the selection is the thumb, not colour. |
| **Tabs (panel)** | Text tabs `md` 600 with a 0.3rem × 2.4rem accent bar under the active one | Inactive tabs use `text-secondary`. A count badge can follow the label. |
| **Slider** | 0.6rem track, 2.4rem white thumb with `shadow-1` | Fill up to the thumb in `accent-primary` only while dragging or focused, `text-secondary` otherwise. Shows the value in tabular `sm`. |
| **Stepper** | `−` value `+` in one capsule | Holding repeats after 400 ms. The bounds disable the matching button. |
| **Toggle** | 5.2 × 3.2 capsule | On is `success` fill with a white thumb, like the platform convention, and the thumb moves with `ease-spring`. |
| **List row** | Icon tile 3.6, title `md` 600, subtitle `sm` `text-secondary`, trailing value or chevron | Height 5.6 (or 6.4 for two lines). Hover is white 6 %, selected is `bg-elevated` with an accent strong ring. |
| **Badge** | Capsule 2.4 high, `xs` 600 | Tinted with `::before currentColor 16 %`. Status words always accompany the colour. |
| **Key cap** | 2.4 high, min 2.4 wide, radius `xs`, white 14 % fill, hairline, `2xs`/`sm` 700 | Shows the bound key from the client keymap, never a hardcoded letter. |
| **Card** | `bg-surface` or white 6 % on glass, radius `lg`, padding `space-6` | Selectable cards follow the list-row selected rule. |
| **Panel** | `material-thick`, radius `xl`, padding `space-8`, `shadow-3`, specular edge | The header has an `xl` title, an optional `sm` subtitle and the close button. The footer holds key hints at left and actions at right. |
| **Dialog** | Panel at 48rem (input) or 40rem (confirm), centred on the scrim | It traps focus. `Enter` triggers the default and `Esc` cancels. |
| **Toast** | See §13.1 | — |
| **Ring gauge** | SVG circle r = 2.2 with stroke 0.4, track white 12 %, value in the state colour, icon 2rem centred | Starts at 12 o'clock and fills clockwise (`pathLength="100"` + `stroke-dasharray`). |
| **Bar** | Capsule 0.8 high (HUD) or 0.6 (in panels) | Track white 12 %, fill in the state colour, rounded ends. |
| **Skeleton / spinner / empty / error** | See §9 | — |
| **Tooltip** | `bg-elevated`, radius `sm`, `xs` text, `shadow-2`, 8 px offset | It appears after 500 ms and has no arrow. |

## 11. Screens — Session Flow

### 11.1 Loading screen

**For:** every player while the client downloads and starts resources (30–180 s). It is the server's first impression and the player's only reading time.

**Layout.** It is full-screen and NUI-owned (`bg-base` plus server key art). The top-left has a wordmark "HARBOUR" (`4xl`, 650, `-0.02em`) and a sub-line "Los Santos · Roleplay" in `text-secondary`. Bottom-centre has a 64rem progress block: the stage label left, the percent right, a 0.8rem bar in cyan, and four stage dots below (Verbinden · Ressourcen · Spielwelt · Charaktere). Bottom-left holds a tip card (40rem, `material-regular`). Bottom-right holds a music capsule (track title and artist, play/pause, a volume slider, the key hint `[Leertaste]`). Top-right has server facts (players online, Discord handle text) in `text-secondary`.

**Interactions**
| Element | Does | Produces |
|---|---|---|
| Music play/pause | Toggles background music (with `loadscreen_cursor 'yes'`) | Audio pauses or resumes, and the icon switches pause ↔ play |
| `Leertaste` | Same as play/pause, for players without a cursor | Same |
| Volume slider | Sets music volume 0–100 % | Volume persists in `localStorage` for the next connect |
| Tip card | Rotates every 8 s with a fade, and the `‹ ›` buttons cycle manually | Next or previous tip |

**States**
- **Connecting** (before the first progress event): the bar is indeterminate (a cyan 30 % sweep) and labelled "Verbinde mit Server …".
- **Loading:** determinate, and the label follows the stage ("Lade Ressourcen · 214 / 386").
- **Slow:** after 60 s on one stage the label adds "Dauert länger als üblich" in `text-secondary`, and nothing turns red.
- **Empty tips:** the tip card is hidden.
- **Error:** connection failures are shown by the FiveM client, not the loading screen. When the server sends `loadscreen:error`, the bar turns `danger` and the label shows the reason.
- **Filled / done:** 100 % shows the label "Bereit", and the page fades out over `slow` into character select.

### 11.2 Multi-character selection

**For:** returning players choosing which of up to 4 characters to play. New players land in the empty state.

**Layout.** The world is visible: the ped stands centre-right in a lit scene. The left column (4rem margin, 40rem wide, vertically centred) has the title "Charakter wählen" (`2xl`), the sub-line "2 von 4 Plätzen belegt", and a stack of slot cards (40 × 10rem, radius `lg`, `material-thick`). Each card shows initials in a tile, the name (`lg`), the job badge in its job colour, and cash plus last played in `text-secondary`. The bottom-right holds actions: `Spielen` (large primary with `glow-accent`) and `Löschen` (danger ghost). The selected character's details sit right of the ped in a glass card: date of birth, job and grade, bank balance, phone number and play time.

**Interactions**
| Element | Does | Produces |
|---|---|---|
| Slot card (filled) | Selects the character → `nui:multichar.preview {cid}` | The ped and details swap (ped crossfade `slow`), and the card gets a strong accent ring and glow |
| Slot card double-click / `Enter` | Plays → `nui:multichar.play {cid}` | Screen fades, then the spawn selector opens |
| Empty slot "+ Neuer Charakter" | Starts the creator → `nui:multichar.create {slot}` | The character creator opens |
| Locked slot (lock icon) | Disabled, and its tooltip explains "Weitere Plätze für Unterstützer" | Nothing |
| `Löschen` | Opens a confirm dialog that asks for the name to be typed | On confirm → `nui:multichar.delete {cid}`, the card leaves (`exit`) and a toast confirms |
| `↑`/`↓` | Moves the selection | Same as clicking the card |

**States:** *Loading* has three skeleton cards and a disabled `Spielen`. *Empty* has one large card, "Erstelle deinen ersten Charakter", with a primary `Charakter erstellen`. *Error* reads "Charaktere konnten nicht geladen werden" with `Erneut versuchen`. *Filled* is as described, with the last-played character preselected. *Busy* is `Spielen` with a spinner while the spawn data loads.

### 11.3 Character creator

**For:** a new player building their character, which takes 3–15 minutes. The creator must feel like a calm studio, not a spreadsheet.

**Layout.** The ped is centre-right. A step capsule at top-centre holds six steps as a segmented control: Herkunft · Gesicht · Haare · Merkmale · Kleidung · Daten. The left panel (44 × 76rem, `material-thick`) holds the current step's controls in grouped cards. Camera controls sit in a right-edge vertical capsule: Kopf · Oberkörper · Ganzkörper, plus `‹ ›` rotate. The bottom bar has the footer key hints at left (`A`/`D` drehen, Maus zoomen), and `Zurück` (secondary) and `Weiter` (primary) at right. On the last step the primary reads `Charakter erstellen`.

**Controls per step**
- **Herkunft:** mother and father as portrait carousels (`‹ name ›`), then sliders for Ähnlichkeit and Hautton (0–100 %).
- **Gesicht:** 20 feature sliders grouped as Nase, Augenbrauen, Wangen, Kiefer, Kinn, Lippen and Augen, with a `Zufällig` ghost button per group.
- **Haare:** style carousel, colour swatches (2.8rem round, selected with an accent ring), highlight swatches, eyebrows and beard.
- **Merkmale:** overlays with style, opacity and colour (Narben, Sommersprossen, Make-up).
- **Kleidung:** starter outfit cards (2 × 3 grid).
- **Daten:** fields Vorname, Nachname, Geburtsdatum (TT.MM.JJJJ), Geschlecht (segmented), Größe (stepper in cm) and Herkunft (select).

**Interactions**
| Element | Does | Produces |
|---|---|---|
| Step capsule | Jumps to any visited step. Unvisited steps are reachable in order only. | The panel crossfades and the camera preset changes |
| Slider / carousel / swatch | → `nui:creator.set {key, value}` (debounced 60 ms) | Live ped update |
| Camera preset / rotate | → `nui:creator.camera {preset|rotate}` | The camera moves (`slow`) |
| `Zufällig` | Randomises that group | The ped updates and the values animate to new positions |
| `Weiter` on Daten | Validates locally, then → `nui:creator.finish {data}` | Busy → character select with the new card selected, or field errors |
| `Esc` | Opens a confirm: "Erstellung abbrechen? Änderungen gehen verloren." | Back to character select |

**States:** *Loading* (step change while assets stream) puts a spinner in the ped area's bottom capsule ("Lade Modell …"), and controls stay usable. *Error* shows field-level messages ("Name bereits vergeben", "Geburtsdatum ungültig – TT.MM.JJJJ") or a danger toast for a server failure. *Empty* does not occur, because every control has a default. *Filled* is the normal case.

### 11.4 Spawn selector

**For:** the player choosing where to wake up after selecting a character, and after respawn.

**Layout.** A map on the full screen: the stylised city map at NUI `bg-base` with pins, or the native map with NUI pins over it. The left list (40rem, `material-thick`, radius `xl`) has the title "Wo möchtest du aufwachen?" and rows with an icon tile, the place name, the district, and a trailing badge. The rows are: Letzter Standort (always first), Wohnung, Motel, Krankenhaus, and Revier (job-only, police colour). The bottom of the list holds the primary `Hier aufwachen`. Map pins are 4rem round glass pins with an icon, and the selected pin is magenta with `glow-accent` and a label capsule.

**Interactions**
| Element | Does | Produces |
|---|---|---|
| Row or pin | Selects → `nui:spawn.preview {id}` | The camera flies to the location (`slow`), and the row and pin highlight together |
| Row hover | Highlights the pin | The pin lifts (`scale(1.08)`) |
| `Hier aufwachen` / `Enter` | → `nui:spawn.confirm {id}` | Screen fade, then the player spawns and the HUD fades in |
| Job-only row when off duty | Disabled, with the helper line "Nur im Dienst" | Nothing |

**States:** *Loading* has skeleton rows and greyed pins. *Empty* is only "Letzter Standort", which is always available, so the list never empties. *Error* ("Spawnpunkt nicht verfügbar") is a danger toast that returns the selection to "Letzter Standort". *Filled* is as described.

## 12. Screens — HUD & Vehicle HUD

The HUD is glanceable chrome. Every element sits on `material-regular` with `shadow-1`. Numbers are tabular and colour appears only on the ring or bar that carries the state. The HUD never takes focus and has no hover states.

### 12.1 Status rings (health, armor, hunger, thirst, stamina, stress)

**Layout.** One capsule right of the minimap frame, bottom-aligned with it, 6.4rem high. It holds ring gauges at 4.8rem with an icon inside. Order: health · armor · hunger · thirst · stamina · stress.

| Ring | Visible when | Icon | Low state |
|---|---|---|---|
| Health | Always | heart | < 25 %: the ring turns `danger` and the heart icon fills and pulses at 1 s |
| Armor | > 0 | shield | Hidden at 0 (the capsule shortens with an `exit` transition) |
| Hunger | < 50 % | food | < 15 %: the ring turns `danger` |
| Thirst | < 50 % | drop | < 15 %: the ring turns `danger` |
| Stamina | Sprinting or swimming and < 100 % | run | It drains visibly and hides 2 s after it is full |
| Stress | > 10 % | brain | > 75 %: the icon pulses, and the screen effects are the client's job |

**States:** *Filled* is normal. *Empty* (all optional rings hidden) shrinks the capsule to health alone or health plus armor. There is no loading state: until the first `hud:update` the HUD stays hidden. *Error* does not apply.

### 12.2 Voice and radio indicator

**Layout.** A capsule above the rings (3.6rem high) with the mic icon, three range dots (Flüstern · Normal · Rufen, the active range in cyan), and, when the player is on the radio, a separator, the radio icon and the channel "Funk 3 · 104.3".

| State | Visual |
|---|---|
| Idle | Mic outline in `text-secondary`, range dots in white 30 %, active dot in white |
| Talking (proximity) | Mic filled cyan, cyan live glow breathing at 1.2 s, active range dot in cyan |
| Radio TX (own transmission) | Radio icon filled magenta with `glow-accent` and the channel label in `text-primary` |
| Radio RX (someone else) | Radio icon cyan and the speaker's callsign capsule ("2-ADAM-12") for the duration |
| Muted / disconnected | Mic with a slash in `danger`, the text "Voice getrennt" and the capsule border in `danger` |

**Interactions:** none in the HUD. The range cycles with the client keybind, and the capsule animates the dot.

### 12.3 Cash, bank and job

**Layout.** Top-right, three right-aligned capsules stacked with a 0.8rem gap, 4rem high. **Cash** has the wallet icon and "2.450 €" (`lg` 600, tabular). **Bank** has the bank icon and "48.920 €". **Job** has a job icon tinted with its job colour, then "LSPD · Officer II" and, when on duty, a cyan dot with "Im Dienst".

**States:** a change makes the capsule show a delta chip for 3 s ("+ 250 €" in `success`, "− 1.250 €" in `danger`) while the value counts to the new number over `slow`. *Hidden mode* (cinematic toggle) hides cash and bank, and they peek for 4 s on change. *Off duty* shows "Außer Dienst" in `text-secondary` with no dot.

### 12.4 Ammo

**Layout.** Bottom-right above the vehicle HUD (or alone at bottom-right on foot). The capsule has the weapon name in `sm` `text-secondary` (e.g. "Pistole .50"), the magazine count `2xl` 700, a "/" and the reserve `lg` `text-secondary`.

**States:** shown only while a firearm is equipped. Below 25 % of the magazine the count turns `warning`, and at 0 it turns `danger` with the key cap hint `R` and "Nachladen". Melee and throwables show the weapon name only.

### 12.5 Minimap frame and street label

**Layout.** The frame aligns to the native minimap rectangle. Lua reads the minimap anchor at resolution change and posts `{x, y, w, h}`. The frame is a `material-thin` ring 0.6rem thick with radius `lg`, `shadow-1` and a specular edge. Above it sits a capsule with a compass heading in a key cap ("NO") followed by the street name "Vinewood Blvd" in 600 and the zone "Alta" in `text-secondary`.

**States:** the frame is hidden when the minimap is hidden (on foot, if the server hides it). In a vehicle it gains a waypoint distance chip ("1,2 km"). On a GPS route the chip has a cyan route dot.

### 12.6 Vehicle HUD

**For:** the driver, and passengers in a reduced version (speed only).

**Layout.** Bottom-right, a capsule about 36 × 13.6rem. On the left is a speed ring (11.2rem, a 270° cyan arc for RPM with a white tick at the redline) enclosing the speed (`4xl` 700 tabular) with "km/h" (`2xs` uppercase) below. On the right sit a stacked fuel bar (fuel icon, 12rem bar in `hud-fuel`, percent) and a status row of icons: seatbelt · engine · lights · lock. Indicator arrows sit in a `material-thin` pod 2rem above the capsule, left and right, plus the gear "D3" in mono. A one-line `xs` caption under the icons names the worst current state ("Gurt offen · Motor 38 %").

| Element | States |
|---|---|
| Speed | Value; the ring shows RPM; the redline tick turns `danger` when hit |
| Fuel | `hud-fuel` > 25 %, `warning` 10–25 %, `danger` < 10 % with the icon pulsing; "E" when empty |
| Seatbelt | Buckled: filled icon in `text-primary`. Unbuckled: outline `warning`, and pulsing `danger` above 30 km/h. |
| Engine | Running: filled. Off: outline `text-muted`. Damaged (< 40 %): `warning`. Failing (< 15 %): `danger` pulse. |
| Indicators | Left / right / hazard: arrows blink `success` at 0.75 s |
| Lights | Off is outline, low beam is filled, and high beam is filled with a cyan dot |
| Lock | Locked uses the filled lock, unlocked the outline |

**Interactions:** none. All state comes from `hud:vehicle` messages at 10 Hz (speed) and on change (everything else).

## 13. Screens — Feedback Overlays

### 13.1 Notifications (four types)

**Layout.** Top-centre stack, 44rem wide, max 3 visible, 0.8rem apart, newest on top. Each toast is a `material-regular` card with radius `lg` and `shadow-2`. Inside are an icon dot (3.6rem circle tinted 16 % with the state glyph), a title (`md` 600) and a body (`sm` `text-secondary`, max 2 lines), plus an optional source label and time ("Bank · jetzt") at the top-right in `xs` `text-muted`.

| Type | Colour | Icon | Example |
|---|---|---|---|
| Success | `success` | check | "Fahrzeug eingeparkt" / "Sultan RS · HH-SN 2047" |
| Info | `info` | info | "Neue Nachricht" / "Mara: Bin in 5 Minuten da." |
| Warning | `warning` | alert | "Tank fast leer" / "Noch 8 % – nächste Tankstelle 1,4 km" |
| Error | `danger` | x | "Zahlung fehlgeschlagen" / "Nicht genug Guthaben auf dem Girokonto." |

**Behaviour:** they enter with a drop and spring (`enter`) and leave with fade and lift (`exit`). Default life is 5 s, warning 7 s, and error stays until the next input or 10 s. Hovering with an NUI cursor pauses the timer. A 4th toast collapses the oldest into a "+2 weitere" capsule. Duplicates within 3 s merge, and the count shows as "×3". **Interaction:** an actionable toast carries one small button ("Antworten", "Anzeigen") → `nui:notify.action {id}`, which only works while NUI focus is held (phone open). Otherwise its key hint is shown.

### 13.2 Progress bar

**Layout.** Bottom-centre, 14rem above the bottom edge, a capsule 40rem wide. It holds an icon tile, a label (`md` 600, "Fahrzeug wird repariert …"), the percent at right (tabular), a 0.8rem bar below in cyan with the cyan live glow, and the hint "`X` Abbrechen" in `text-secondary` when it can be cancelled.

**States:** *running* fills linearly. *Cancelled* turns the bar `danger`, the label reads "Abgebrochen" and it exits after 600 ms. *Done* turns the bar `success` with the check icon and exits after 400 ms. *Blocked* (the action is not allowed) shows no bar, only a warning toast.

### 13.3 Interaction hint

**Layout.** Centred horizontally, 8rem below the screen centre. A `material-regular` capsule holds the key cap (2.8rem, `text-md` 700) and the action label (`md` 600). With several options they stack vertically with a 0.6rem gap, and the primary option (the first) gets its key cap in `accent-primary` fill with the `text-on-accent` label.

**States:** *available* is as described. *Hold* replaces the key cap with a ring that fills around it over the hold time ("`E` halten – Tresor knacken"). *Unavailable* shows the label in `text-secondary`, the key cap struck through, and a reason ("Werkzeug fehlt"). Hints enter with a fade and `translateY(0.4rem)` over `enter` and exit over `exit`.

### 13.4 Death / unconscious screen

**For:** a player who is down: unconscious and waiting for EMS, or bleeding out.

**Layout.** Full-screen `bg-overlay` plus a dark-red vignette `radial-gradient(… rgba(60,0,10,0.55))`. The vignette is not `danger`: it is a mood and carries no signal. Centre: the title "Bewusstlos" (`3xl`) and "Du wurdest schwer verletzt." in `text-secondary`, then the timer capsule "Respawn möglich in 04:59" (`2xl` tabular). Two actions sit below: `G` Rettungsdienst rufen (secondary) and `E` halten – Im Krankenhaus aufwachen (disabled until the timer ends).

**Interactions**
| Element | Does | Produces |
|---|---|---|
| `G` Rettungsdienst rufen | → `nui:death.callEms` | The button turns busy, then into a chip with cyan "Rettungsdienst informiert · 2 Einheiten verfügbar". It can be used once per 60 s, and a countdown shows on the chip. |
| `E` halten (3 s) | Hold ring fills → `nui:death.respawn` | Fade to black and the spawn selector opens (hospital preselected). A fee notice follows as a toast. |

**States:** *Waiting* (the respawn timer runs). *EMS on the way* shows the chip "Rettungsdienst unterwegs · ETA 01:20" in cyan. *Being treated* replaces the actions with a progress capsule "Wirst behandelt … 64 %". *Respawn available* enables the `E` action, whose key cap turns magenta. *No EMS on duty* shows the chip "Kein Rettungsdienst im Dienst" in `warning`, and the respawn timer is halved by server rule.

## 14. Screens — Menus & Dialogs

### 14.1 Radial menu

**For:** quick actions without a panel (`F1` or held key): animations, vehicle, walk style, documents, phone, and job actions.

**Layout.** It is centred, with a 44rem diameter. A `material-thin` ring track holds 8 segments, each with an icon (2.8rem) and a label (`sm` 600) on the ring. The centre disc (16rem, `material-regular`) shows the hovered segment's title (`lg`) and a hint line ("Klicken zum Öffnen"). The hovered segment fills with `accent-primary` at 22 % and its icon turns magenta, and the selection wedge points at it with `glow-accent`. A submenu replaces the ring and the centre shows a back arrow.

**Interactions:** the mouse angle selects a segment, and the arrow keys or `1–8` choose it. Click or `Enter` opens the submenu or runs the action → `nui:radial.select {id}`, and the menu closes after an action (`exit`). Right-click or `Backspace` goes back a level. `Esc` or releasing the hold key closes it. Disabled segments (no vehicle nearby) use 38 % opacity with the reason in the centre on hover. **States:** *filled* (8 or fewer segments; more than 8 overflow into "Mehr …"). *Empty* (no context actions) shows only the global segments.

### 14.2 Context menu (target / third-eye)

**Layout.** It appears beside the target's screen position, offset 2.4rem right and clamped inside the safe area. The card is 28rem wide, `material-regular`, radius `lg`, `shadow-2`. The header has the target name (`md` 600) and type (`xs` `text-secondary`, e.g. "Fahrzeug · HH-SN 2047"). Rows are 4.4rem with an icon, label and trailing chevron (submenu) or key cap, and a divider separates groups. A destructive row ("Fahrzeug aufbrechen") uses a `danger` label.

**Interactions:** hovering or the arrow keys focus a row, click or `Enter` → `nui:target.select {id}`, a submenu opens to the right, and `Esc` closes it. Disabled rows say why ("Kein Dietrich"). **States:** *Loading* (server checks permissions) shows two skeleton rows for at most 400 ms. *Empty* is never shown, because no menu opens without options.

### 14.3 Input dialog

**Layout.** A centred 48rem dialog over the scrim. It holds a title (`xl`), an optional description (`sm` `text-secondary`), 1–4 fields (text, number with unit, select, textarea up to 6 lines), and a footer with `Abbrechen` (secondary) and the primary verb ("Überweisen", "Bestätigen").

**Interactions:** the first field takes focus. `Enter` submits and `Esc` cancels. Submit validates locally (required, min/max, pattern), then → `nui:input.submit {values}`. **States:** *invalid* (field errors, primary disabled until fixed), *submitting* (primary busy and fields read-only), *error* (a server message in a `danger` inline banner at the dialog top, with the fields kept).

### 14.4 Confirm dialog

**Layout.** A centred 40rem dialog. It holds an icon (4.8rem tile, the state tint), a title (`xl`), a body (`md` `text-secondary`), and a footer with `Abbrechen` and the confirm action. For destructive actions the confirm button is a solid `danger` fill with a `text-on-accent` label, and focus starts on `Abbrechen`.

**Interactions:** confirm → `nui:confirm.resolve {id, true}`, cancel or `Esc` → `{id, false}`. High-risk confirms (character delete, firing an employee) require typing the name, and the confirm stays disabled until it matches.

### 14.5 Chat

**Layout.** Top-left, 52rem wide. At rest the last 7 lines float on a `material-regular` card that fades out after 10 s idle. Open (`T`), it becomes `material-thick` with 12 lines, a scrollbar and an input capsule below. Each line is a channel tag badge (OOC grey, `/me` and `/do` violet-neutral as white 8 %, Polizei `job-police`, EMS `job-ems`, Admin `accent-primary`), then the name in 600 and the message in regular `sm`, with a timestamp on hover.

**Interactions:** `T` opens with focus in the input. `Enter` sends → `nui:chat.send {text}` and `Esc` closes. `↑` recalls the history. Typing `/` opens command suggestions above the input (`bg-elevated` popover listing the command and its parameter hint, `Tab` completes). **States:** *empty* ("Noch keine Nachrichten"), *sending* (the line shows at 60 % opacity until acknowledged), *error* (the line gets a `danger` "!" and "Nicht gesendet – erneut senden"), *rate-limited* (the input helper reads "Langsamer – 3 s").

### 14.6 Scoreboard

**Layout.** It is held on `Tab` (or `Home`) and centred at 72 × 72rem in `material-thick`. The header has the server name (`xl`), "128 / 200 Spieler" and the uptime. Below sit job tiles (police · EMS · mechanic · civil counts with job icons in their colours), and below them a player table: ID (mono), name, job badge (only for public jobs), and ping (green < 80, `warning` < 150, `danger` ≥ 150, with the number always shown).

**Interactions:** holding it shows the board and releasing hides it. A click-lock with `Tab` + click or `L` keeps it open for scrolling, and the search field filters by name or ID. **States:** *loading* (skeleton table), *filled*, *empty search* ("Kein Spieler gefunden"), *error* ("Liste nicht verfügbar").

## 15. Screens — Commerce & Personal

### 15.1 Inventory

**For:** every player, many times per session: using, moving, giving and dropping items.

**Layout.** Over the scrim, centred, 2 × 64rem columns with a 4rem gap.
- **Left: Rucksack** (`material-thick` panel). The header has the title, the weight "18,4 / 30 kg" and a weight bar (`accent-secondary` normally, `warning` > 80 %, `danger` > 95 %). Below, a hotbar row of slots 1–5 (numbered key caps in the corners), then a 6-column grid of 8.8rem slots.
- **Right: Boden / Kofferraum / Handschuhfach / Spieler** (same panel), titled after the open container.
- **Slot:** `bg-surface` well, radius `md`. It shows the item art (64 % of the slot), the count top-right (`xs` 600), and the weight bottom-left (`2xs` `text-muted`). Durability or quality shows as a 0.4rem bar at the bottom edge (`success` → `warning` → `danger`).
- **Item detail:** a floating `bg-elevated` card (32rem) on hover or focus, with the name, description, weight, count and metadata (serial in mono), plus the actions `Benutzen` (primary), `Geben`, `Teilen` and `Wegwerfen` (danger ghost).

**Interactions**
| Element | Does | Produces |
|---|---|---|
| Drag slot → slot | Moves, swaps or merges → `nui:inventory.move {from, to, count}` | The target slot gets a strong accent ring while dragging. The drop lands with `ease-spring`. A failure snaps back with a danger toast. |
| `Shift`+drag | Splits: an amount stepper popover opens | A partial move |
| Double-click / `Enter` | Uses the item → `nui:inventory.use {slot}` | Inventory closes if the item has an animation and progress shows |
| Right-click | Opens the context menu (Benutzen, Geben, Teilen, Wegwerfen) | As named |
| `Geben` | Opens a player picker of nearby players (IDs and names) | → `nui:inventory.give {slot, target, count}` |
| Keys `1–5` on slot focus | Assigns to the hotbar | The hotbar number appears on the slot |
| `Esc` / `Tab` | Closes | The panel exits |

**States:** *Loading* has skeleton slot wells. *Empty* (nothing carried) shows the backpack outline icon and "Dein Rucksack ist leer", with no action. *Error* reads "Inventar nicht verfügbar" with `Erneut versuchen`. *Filled* is as described. *Over weight* turns the bar `danger` and blocks the drop with the toast "Zu schwer – 2,1 kg zu viel". A *locked* container (trunk in use) shows a lock overlay and "Wird von jemand anderem benutzt".

### 15.2 Phone

**For:** every player: messages, calls, contacts, bank, garage, services and social.

**Layout.** Bottom-right, 34 × 70rem at a 4rem margin. The device frame is a 1rem bezel, radius 5.2rem, `bg-base` with a hairline, and the screen radius is 4.2rem (concentric). A status bar holds the time, signal and battery, and a pill-shaped cut-out sits top-centre. The phone is a generic device with no likeness to a real product. The home screen is a wallpaper (NUI-owned), a 4-column app grid of 6.4rem tiles (radius 1.6rem, an icon on a neutral `rgba(255,255,255,0.14)` tile, and a label `xs`), and a 4-app dock on `material-thin`. Apps: Nachrichten, Telefon, Kontakte, Bank, Garage, Karten, Kamera, Dienste, Chirp (social), Notizen, Einstellungen. App screens use `bg-base` with a large title (`2xl`) that collapses on scroll, grouped lists, and a bottom tab bar.

**Interactions:** opened with the phone key → `nui:phone.open` (focus held). App tile → opens the app (the tile scales up into the app over `slow` with `ease-standard`). Swiping up or `Esc` goes home, and a second `Esc` closes. Messages: the input capsule and `Senden` → `nui:phone.sendMessage {to, text}`, and the bubble appears right-aligned in magenta (own) or white 10 % (other). Calls: the accept (`success` round) and decline (`danger` round) buttons.

**States:** *no signal* (tunnel or underground) puts "Kein Netz" in the status bar, and send buttons are disabled with an explanation. *Low battery* is cosmetic. *Empty* app lists ("Keine Nachrichten") have a compose action. *Loading* uses skeleton list rows. *Error* uses the inline retry pattern. *Incoming call* (phone closed) shows a call capsule top-centre in the notification zone: the caller, then `Annehmen` and `Ablehnen` with key hints.

### 15.3 Bank and ATM

**For:** players managing personal and business money. The ATM is a reduced version used at street machines.

**Bank layout.** A 120 × 72rem panel. The left rail (28rem) lists accounts as cards (Girokonto, Sparkonto, Firmenkonto with a job tint), each with the name, IBAN (mono) and balance. The main area holds the balance of the selected account (`3xl` 700 tabular), the actions row (`Einzahlen`, `Abheben`, `Überweisen` as large capsules), and a transactions list: date, counterparty, purpose, and the amount right-aligned in `success` for incoming and `text-primary` for outgoing (no red for normal spending), with a filter segmented control (Alle · Eingang · Ausgang).

**ATM layout.** A 44 × 60rem panel. A PIN pad (3 × 4 keys of 8rem, radius `lg`) with four dots, then after entry: quick amounts (50 · 100 · 500 · 1.000 €), `Anderer Betrag`, and the balance display.

**Interactions**
| Element | Does | Produces |
|---|---|---|
| Account card | Selects the account | Main area switches with a crossfade |
| `Einzahlen` / `Abheben` | Opens the input dialog (amount, max = cash or balance) | → `nui:bank.deposit|withdraw {account, amount}`, then a balance count animation and a success toast |
| `Überweisen` | Input dialog: Empfänger (IBAN or phone), Betrag, Verwendungszweck | → `nui:bank.transfer {…}`. Over 10.000 € a confirm follows. |
| PIN key | Enters a digit | A dot fills. A wrong PIN shakes nothing: the dots turn `danger` and clear, with "PIN falsch – noch 2 Versuche". |
| Quick amount | → `nui:atm.withdraw {amount}` | Busy, then success and close |

**States:** *Loading* has skeleton cards and list. *Empty transactions* reads "Noch keine Buchungen". *Error* reads "Bank nicht erreichbar" with retry. *Insufficient funds* is a field error, not a toast. *Card locked* (3 wrong PINs) shows "Karte gesperrt – Filiale besuchen".

### 15.4 Shop

**For:** buying from 24/7 stores, hardware stores and gun stores.

**Layout.** A 128 × 72rem panel. The header holds the store name ("24/7 · Clinton Ave") and a search field. A category segmented control sits below it (Alles · Essen · Getränke · Werkzeug · Elektronik). The products are a grid of cards (20 × 24rem): item art on a `bg-surface` well, the name, the price (`lg` 600), and a stock hint ("Noch 3") in `warning` when low. On the right is a cart column (36rem) with item rows and steppers, the subtotal, a payment segmented control (Bar · Karte) and the primary `Bezahlen · 37,50 €`.

**Interactions:** a card click or `+` adds one (a "+1" chip flies to the cart over `enter`), the stepper changes quantity, and setting it to 0 removes the item. `Bezahlen` → `nui:shop.buy {items, method}` → busy → success toast, and the inventory updates. **States:** *loading* (skeleton cards), *empty category* ("Gerade nichts im Regal"), *empty cart* ("Warenkorb ist leer" and `Bezahlen` disabled), *out of stock* (card at 38 % with "Ausverkauft"), *licence required* (a gun-store card shows a lock and "Waffenschein nötig"), *error* (payment failed toast, cart kept), *over weight* (warning before purchase: "Passt nicht in deinen Rucksack").

### 15.5 Garage

**For:** players storing and retrieving vehicles at a garage or impound, and job vehicles.

**Layout.** A 128 × 72rem panel. Tabs: Eigene Fahrzeuge · Job-Fahrzeuge · Abschlepphof · Boote. The left list (56rem) has search, a status filter segmented control (Alle · Eingeparkt · Draußen · Abgeschleppt) and rows: car icon tile, name, plate (mono in a plate chip: white 10 % fill with the plate text), and status badge. The right detail has the vehicle art well, name (`2xl`), plate, location, three condition bars (Tank `hud-fuel`, Motor and Karosserie as white bars turning `warning` < 50 % and `danger` < 25 %), and actions.

**Interactions**
| Element | Does | Produces |
|---|---|---|
| Row | Selects | Detail updates and the row gets the selected state |
| `Ausparken` (primary, stored only) | → `nui:garage.takeOut {plate}` | Busy → panel closes, the vehicle spawns, and a success toast "Sultan RS ausgeparkt" |
| `Einparken` (only when the vehicle is nearby) | → `nui:garage.store {plate}` | Success toast and the status badge turns "Eingeparkt" |
| `Abschleppgebühr zahlen · 450 €` (impounded only) | Confirm dialog → `nui:garage.payImpound {plate}` | Status turns to stored, or a funds error |
| `Orten` (out only) | → `nui:garage.locate {plate}` | A GPS waypoint and an info toast |

**States:** *Loading* has skeleton rows. *Empty* (no vehicles) reads "Keine Fahrzeuge in dieser Garage", plus "Fahrzeuge kaufst du beim Händler" in `text-secondary`. *Empty filter* reads "Keine Fahrzeuge mit diesem Status". *Error* reads "Garage nicht verfügbar" with retry. *Spawn blocked* is the warning toast "Ausfahrt blockiert – Platz freimachen".

### 15.6 Clothing store

**For:** players changing outfits. The ped is the product, so the UI stays at the edges.

**Layout.** The ped is centre. The left rail (36rem, `material-thick`) holds categories as rows with icons (Oberteile, Unterteile, Schuhe, Jacken, Hüte, Brillen, Accessoires, Taschen), and a "Gespeicherte Outfits" group below. The right card (40rem) holds the current category's controls: model `‹ 12 / 148 ›`, texture `‹ 2 / 6 ›`, each with a slider for fast scrubbing, and the price per changed item. The bottom-centre capsule holds camera presets and rotate. The bottom-right holds the summary: "3 Änderungen · 420 €", `Zurücksetzen` (ghost) and `Kaufen` (primary).

**Interactions:** model or texture changes → `nui:clothing.preview {component, drawable, texture}` (live). `Kaufen` → `nui:clothing.buy` → busy → success, with the prompt "Outfit speichern?" (input dialog for the name) → `nui:clothing.saveOutfit {name}`. `Esc` with changes opens the confirm "Änderungen verwerfen?". **States:** *loading* (category streaming) puts a spinner on the counter, and *unavailable* drawables (job-locked) are skipped, with the counter showing "gesperrt" when jumped to directly. *Empty outfits* reads "Noch keine Outfits gespeichert". *Error* (purchase failed) is a toast, and the preview is kept.

### 15.7 Crafting

**For:** players at a workbench building items from materials.

**Layout.** A 120 × 68rem panel. The left recipe list (44rem) has search, categories (Werkzeug · Waffenteile · Elektronik), and rows with the item, crafting time and a lock icon for locked recipes ("Ab Stufe 3"). The right detail has the output item art and name, a quantity stepper, and ingredients as rows: icon, name, and a "have / need" count in `success` when enough or `danger` when missing (with "fehlt 2"). Below sit the crafting time ("45 s"), the skill XP gain, and the primary `Herstellen`.

**Interactions:** a row selects, and the stepper sets the amount (1–10). Beside it a hint shows what the material allows ("max. 1 mit deinem Material"). Above that amount, the missing ingredients turn `danger` with "fehlt N", the primary is disabled, and a `danger` helper line says how to resolve it. `Herstellen` → `nui:crafting.craft {recipe, amount}` → the panel closes and the progress bar shows "Herstellen … 1 / 3", then a success toast with the output. **States:** *loading* (skeleton), *empty* (no recipes known: "Lerne Rezepte durch Blaupausen"), *missing ingredients* (primary disabled with "Zutaten fehlen"), *locked* (detail shows the requirement), *error* (toast), *queue* ("In Arbeit: 2" chip on the bench capsule).

### 15.8 Invoice

**For:** the billed player (receive and pay) and the business that bills (create and send).

**Receive layout.** A centred 48rem card dialog. The header has the business name with a job-colour icon tile ("Los Santos Customs") and the invoice number in mono ("RE-2026-0412"). Below sit line items (description, quantity, amount), a divider, the total (`2xl` 700), the due date "Fällig in 3 Tagen" (`warning` when < 1 day), and a footer with `Ablehnen` (ghost danger) and `Bezahlen · 1.480 €` (primary).

**Create layout** (business side). An input dialog with the recipient (picker of nearby players), line items (repeatable rows: text, amount, `+ Position`), a total that updates live, and `Rechnung senden`.

**Interactions:** `Bezahlen` → `nui:invoice.pay {id}` → success toast "Rechnung bezahlt", and the card shows a paid stamp chip in `success`. `Ablehnen` opens a confirm → `nui:invoice.decline {id}`. `Rechnung senden` → `nui:invoice.create {…}`. **States:** *open*, *paid* (read-only and success chip), *overdue* (`danger` "Überfällig seit 2 Tagen"), *declined*, *insufficient funds* (inline error, with a payment source select to switch to Firmenkonto if allowed), *list empty* (the invoices app reads "Keine offenen Rechnungen").

### 15.9 ID card

**For:** showing identity to another player, or seeing one shown.

**Layout.** A card of 54 × 34rem (ID-1 ratio 1.586), radius `lg`, `bg-elevated` with a subtle diagonal sheen. The header strip reads "STAAT SAN ANDREAS · Personalausweis" in `2xs` caps. A portrait well (12 × 16rem) sits left, with fields: Name, Vorname, Geburtsdatum, Geburtsort, Größe, Staatsangehörigkeit, and the ID number in mono "SA-4471-9920". The signature sits in an italic-free script stand-in using Inter 300. A driving-licence variant shows the classes as chips (A · B · C) with the valid ones `text-primary` and missing ones struck in `text-muted`.

**Interactions:** shown from the inventory "Zeigen" → `nui:id.show {target}`. The viewer sees it slide in at the right-centre for 8 s with the caption "Gezeigt von Lena Hartmann" and the key hint `Esc` Schließen. **States:** *shown*, *expired* (a `warning` badge "Abgelaufen"), *fake* (no visual tell by design: police verify in the MDT).

## 16. Screens — Job & Admin Tablets

All tablets share one frame. It is centred, 148 × 80rem maximum (fits the 720p budget), `material-thick` with radius `xl`, and has a 22rem sidebar on `bg-surface` (job icon and name at top, nav rows, the user and callsign at the bottom). The content area is on `bg-base` at 0.6 opacity over the panel tint. A job colour stripe (0.3rem) runs along the sidebar's top edge, the only place the job colour appears in the frame. Tables sit in `bg-surface` wells with radius `lg`, 4.8rem rows, pinned headers in `2xs` caps `text-muted`, and mono where a value is a code.

### 16.1 Police MDT

**For:** on-duty police officers: look up people and vehicles, file reports, manage warrants and see units.

**Sidebar:** Übersicht · Personen · Fahrzeuge · Vorfälle · Haftbefehle · Einheiten · Strafkatalog.

**Main (Personen, filled):** a search field ("Name, ID oder Telefonnummer"), a results list (28rem) and a record detail. The record holds a portrait, name, date of birth, phone and ID (mono), licence chips, flags (`danger` badge "Haftbefehl aktiv" and `warning` badge "Bewaffnet"), notes, a priors table (date, charge, fine, officer), and actions: `Haftbefehl ausstellen`, `Notiz hinzufügen`, `Bericht erstellen` (primary).

**Übersicht:** unit status tiles (on duty 12, available 7, busy 5), an active call feed with cyan live badges, and the BOLO list.

**Interactions:** search → `nui:mdt.search {type, query}` (debounced 300 ms). The record actions open input dialogs → `nui:mdt.<action>`. A unit status change (10-8 / 10-6 / 10-7 segmented in the sidebar footer) → `nui:mdt.setStatus`. **States:** *loading* (skeleton results), *empty search* ("Keine Treffer für "Hartmann""), *empty view* ("Suche nach einer Person, um ihre Akte zu öffnen"), *error* ("MDT offline – Verbindung zur Leitstelle verloren"), *off duty* (the tablet opens read-only with the banner "Außer Dienst – nur Lesen").

### 16.2 EMS tablet

**For:** on-duty paramedics and doctors: incoming calls, active patients, treatment records.

**Sidebar:** Einsätze · Patienten · Behandlungen · Personal · Bestand.

**Main (Patienten, filled):** a patient list with triage badges (Rot/Kritisch `danger`, Gelb `warning`, Grün `success`, each with its word). The patient detail has a body map (front silhouette with injury markers: tinted dots by severity, each labelled "Schusswunde · Bein links"), vitals tiles (Puls, Blutdruck, Bewusstsein) with tabular values, a treatment log timeline, and actions `Behandlung eintragen` (primary) and `Rechnung stellen`.

**Einsätze:** a call list with distance, a cyan live "neu" badge, `Annehmen` → `nui:ems.acceptCall {id}` → GPS route and status "Unterwegs".

**States:** *empty calls* ("Keine offenen Einsätze – gute Nacht"), *loading*, *error*, *off duty* (read-only banner).

### 16.3 Boss menu

**For:** business owners and high grades: staff, wages and the business account.

**Sidebar:** Übersicht · Mitarbeiter · Ränge & Gehälter · Firmenkonto · Einstellungen.

**Main (Mitarbeiter, filled):** a table with name, rank (select), wage, on duty (cyan dot and time), hired date, and a row menu (`Befördern`, `Degradieren`, `Entlassen` in danger). The header has `Einstellen` (primary): a player picker of nearby players → rank → confirm. **Firmenkonto** shows the balance (`3xl`) and `Einzahlen`/`Abheben` with a transactions list.

**Interactions:** a rank change → `nui:boss.setGrade {cid, grade}` → toast. `Entlassen` → typed-name confirm → `nui:boss.fire {cid}`. Wage edit is inline numeric with a stepper, and saving → `nui:boss.setWage {grade, amount}`. **States:** *empty staff* ("Noch keine Mitarbeiter" with `Einstellen`), *loading*, *error*, *no permission* (rows read-only and actions hidden, with the banner "Nur für Geschäftsführung").

### 16.4 Admin panel

**For:** server staff (moderators, admins): player management, reports and server state. It must be fast and dense without becoming loud.

**Sidebar:** Spieler · Meldungen · Server · Protokolle · Fahrzeuge · Wetter & Zeit.

**Main (Spieler, filled):** a dense table (4rem rows): ID (mono), name, licence identifier (mono, truncated), job badge, ping, playtime, and flags (`warning` "Verwarnt 2×"). The selected player opens a right drawer (36rem) with actions grouped: *Bewegen* (Teleportieren zu, Holen, Zuschauen), *Zustand* (Heilen, Wiederbeleben, Einfrieren), *Strafen* (Verwarnen, Kicken, Bannen in danger, each with a reason input dialog). **Meldungen** is a queue with priority badges, `Übernehmen` → `nui:admin.claimReport {id}`, and the claimed-by chip. **Protokolle** is a mono log stream with filter chips and search, and new lines enter at the top with a cyan dot for 2 s. **Server** shows the resource list with status and restart (confirm) and the player count.

**Interactions:** every destructive action uses the confirm pattern (ban needs a duration select and a reason). All actions → `nui:admin.<action> {target, …}` and log with the admin's name. **States:** *loading*, *empty reports* ("Keine offenen Meldungen"), *error* ("Keine Berechtigung" or "Server antwortet nicht"), *spectating* (the panel minimises to a capsule at top-centre: "Zuschaust: Lena Hartmann (ID 42)" with `Beenden`).

## 17. Accessibility

- **Contrast.** All text pairs in §2 meet 4.5:1 on their intended surface, including the worst case of a pure white game frame behind `material-regular`. `text-muted` is restricted to `material-thick` and opaque surfaces. Every HUD and job colour reaches at least 3.7:1 worst-world (lowest: danger 3.7:1, then accent-primary/hud-radio 3.8:1, hud-armor and job-police 3.9:1), above the 3:1 needed for graphics.
- **Never colour alone.** Every status carries an icon or word: triage words, status badges, the HUD icon in each ring, and ping numbers with their colour.
- **Focus.** A visible focus ring on every interactive element, a logical tab order, focus trapped in dialogs, and focus restored to the opener on close.
- **Motion.** The `reduce-motion` class, set by the client from a server setting, removes translate, scale and pulse (§6).
- **Size floor.** Nothing below `2xs` (11px at 1080p, 8.8px at 720p). Chat and HUD values are never below `sm`. Body text in tablets is `md`.
- **Hit targets.** At least 3.2rem (32px at 1080p) for pointer targets and 4.4rem for primary actions.
- **Language.** The interface copy is German, short and in the infinitive for actions. Error text says what happened and what to do, and never blames the player.

## 18. Do's and Don'ts

**Do**
- Give the screen one hero: one primary button, one glowing selection.
- Let glass come from tint, specular edge and shadow. Check every panel over a white frame.
- Hide HUD rings that have nothing to say, and let the capsule breathe.
- Use tabular numerals for every changing number, and mono for codes and plates.
- Use concentric radii (inner = outer − padding) and capsules for actions.
- Draw all four data states for every list and screen before calling it done.

**Don't**
- Don't add a third neon hue, gradient text, scanlines, glitch effects, hexagon grids or angled cyberpunk corners.
- Don't rely on `backdrop-filter`: it does not blur the game in NUI, flickers on the current client, and is opt-in only over NUI content. The world is blurred by `TriggerScreenblurFadeIn`.
- Don't use `color-mix()`, `:has()`, container queries, `dvh` or the individual `scale`/`translate` properties (Chromium 103).
- Don't glow at rest: no neon borders on idle panels and no glowing headings.
- Don't colour normal spending red, idle job chips blue or empty states in any colour.
- Don't stack six HUD bars, and don't let notifications cover the money capsules.
- Don't load fonts or icons from a CDN, and don't use SF Pro, Apple logos or Apple product names.
- Don't size anything in px except the 1px hairline floor.

## 19. Agent Prompt Guide

- **Start every NUI page** with the §8 block (root scaling and `:root`), the §3 `@font-face` rules, and `body { font-family: var(--fh-font-sans); color: var(--fh-text-primary); font-feature-settings: "tnum" 1, "cv11" 1; background: transparent; }`.
- **A panel:** `background: var(--fh-material-thick); border: var(--fh-border-width) solid var(--fh-border); border-radius: var(--fh-radius-xl); box-shadow: inset 0 0.1rem 0 rgba(255,255,255,0.08), var(--fh-shadow-3); padding: var(--fh-space-8);`
- **A HUD capsule:** `background: var(--fh-material-regular); border-radius: var(--fh-radius-pill); box-shadow: inset 0 0.1rem 0 rgba(255,255,255,0.08), var(--fh-shadow-1);`
- **A primary button:** `background: var(--fh-accent-primary); color: var(--fh-text-on-accent); border-radius: var(--fh-radius-pill); height: 4.4rem; padding: 0 var(--fh-space-5); font-weight: var(--fh-weight-semibold);` plus `:focus-visible { box-shadow: var(--fh-focus-ring); }`.
- **Prompt shape:** "Build the <screen> for FiveM Street Neon: <for whom>. Layout per §11–16, all four data states, every control's NUI callback named, German copy, rem only, Chromium 103-safe CSS, no blur over the world."
