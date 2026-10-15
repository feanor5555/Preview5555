# FiveM Apple Tactical

> Category: Themed & Unique
> Variant F of the FiveM harbour roleplay UI. Graphite liquid glass, sand and olive accents, tabular numerals, thin precise rules. Calm, data-dense and readable over the game world.

Variant F is the "Tactical" design system for the in-game UI (NUI) of a north-German harbour-town roleplay server on FiveM (GTA V). It serves the players, who read it at a glance while driving, fighting or role-playing, and the staff and faction members (police, EMS, company bosses, admins) who work in its dense tablet screens for minutes at a time. It is one of six interchangeable variants. All six share the same `--fh-*` token names, so any later screen built against those names can switch variant by swapping the token block.

Product copy is German. This document is English.

Companion artefacts:

- `tokens.css` holds the repository's shared token schema (`--bg`, `--fg`, `--accent`, …) mapped onto this variant's values. Open Design composes it into prompts.
- `components.html` is the compact component fixture. Its `:root` is identical to `tokens.css`.
- `fonts/` holds the self-hosted woff2 files and their OFL licences.
- The full preview of every element is at `work/fivem-harbour-designsystem/apple-tactical-preview.html`.

## 1. Visual Theme & Atmosphere

The model is the precision of an outdoor instrument face at night, like a dive or expedition watch in wayfinder mode, carried into Apple's current material language. In concrete terms:

- **Graphite, not black.** The canvases are graphite with a faint olive cast (`#0C0D0B` → `#20231E`), never pure `#000`. Text is a warm off-white (`#ECEDE6`), never pure `#FFF`.
- **One quiet accent.** Sand (`#D3C29A`) marks focus, the primary action and the selected state. Olive (`#A4AC7C`) is the secondary accent for passive emphasis such as tabs, filters and the "own" marker. Saturated colour is reserved for status (health, danger, radio) so that it means something.
- **Liquid glass, used honestly.** Surfaces are translucent graphite with a 1px hairline edge, a 1px inner specular line at the top, and continuous rounded corners that nest concentrically (inner radius = outer radius − padding). Section 5 sets out what glass can and cannot do inside FiveM.
- **Data-dense but calm.** Many values share a screen, but each one has a fixed slot, a label in small caps and a tabular numeral. Nothing jumps when a number changes. Rules are 1px, alignment is strict, and colour is used sparingly.
- **Functional realism.** Units are always shown (`km/h`, `L`, `kg`, `$`). The vocabulary is that of instruments and dispatch: callsign, grid, ETA, priority. There is no camouflage, stencil type, chevrons, scanlines, glitch or HUD-brackets kitsch.

Key characteristics:

- Graphite translucent materials at three densities; hairline borders `#3B3F37`.
- Sand accent for action and focus; olive for passive emphasis.
- Inter for words; JetBrains Mono, or Inter with `tnum`, for every number.
- Small-caps labels: 11–12px, uppercase, tracking +0.08em, `text-secondary`.
- Rings and thin bars as gauges, after watch complications. Values appear as numerals next to the gauge, not inside dense graphics.
- Status is shown by colour **and** shape or text, never colour alone.

## 2. Color Palette & Roles

All values are final. Contrast is the WCAG 2.x ratio against the background named for each token.

- **Surfaces.** For a surface token the ratio is that of `text-primary` on it.
- **Text, accent, status and job colours.** These are measured against `bg-surface` (`#161814`).
- **HUD colours.** These sit on `bg-overlay` above the game world. They are measured against `bg-overlay` composited over **pure white**, the worst case (snow, sun glare, white walls), with the over-black value in brackets.

Normal text needs 4.5:1, large text (≥ 18.7px bold / 24px) and UI graphics need 3:1.

### Surfaces and lines

| Token | Hex | Usage | Background | Contrast |
|---|---|---|---|---|
| `bg-base` | `#0C0D0B` | Opaque full-screen canvas the NUI owns: loading screen, character select, creator. | `text-primary` on it | 16.53:1 |
| `bg-surface` | `#161814` | Opaque panel body, tablet and phone screen; the default reading surface. | `text-primary` on it | 15.17:1 |
| `bg-elevated` | `#20231E` | Raised element inside a panel: input field, card, selected list row, key cap shell. | `text-primary` on it | 13.50:1 |
| `bg-overlay` | `#10110FCC` (rgba(16,17,15,0.80)) | Translucent glass over the game world: every HUD chip, hint, notification, dialog over gameplay. | `text-primary` on it over white / over black | 8.71:1 / 16.42:1 |
| `border` | `#3B3F37` | 1px hairline: panel edges, dividers, table rules. Decorative only, never the sole boundary of a control. | `bg-surface` | 1.66:1 (decorative) |

### Text

| Token | Hex | Usage | Background | Contrast |
|---|---|---|---|---|
| `text-primary` | `#ECEDE6` | Values, titles, body copy, all HUD numerals. | `bg-surface` | 15.17:1 (over game 8.71:1) |
| `text-secondary` | `#B5B9AD` | Labels, small-caps headers, metadata. The minimum for information shown over the game world. | `bg-surface` | 8.94:1 (over game 5.14:1) |
| `text-muted` | `#8D9285` | Placeholders, disabled text, units, timestamps on opaque surfaces. Never used for information over the game world. Also the 1px outline of input fields. | `bg-surface` | 5.60:1 (over game 3.22:1, large text only) |
| `text-on-accent` | `#15160F` | Text and icons on a filled accent, status or key-cap fill. | `accent-primary` | 10.36:1 |

### Accent and status

| Token | Hex | Usage | Background | Contrast |
|---|---|---|---|---|
| `accent-primary` | `#D3C29A` | Sand. Primary button fill, focus ring, selected item, active slider, own position marker. | `bg-surface` | 10.17:1 |
| `accent-secondary` | `#A4AC7C` | Olive. Active tab underline, filter chip on, secondary emphasis, own-faction markers. | `bg-surface` | 7.47:1 |
| `success` | `#73C08B` | Completed, paid, online, on duty, engine OK. | `bg-surface` | 8.21:1 |
| `warning` | `#E8B04E` | Low values (fuel < 20 %, hunger < 25 %), pending, overdue soon, damaged engine. | `bg-surface` | 9.15:1 |
| `danger` | `#F46A58` | Destructive actions, errors, wanted, critical health, seatbelt off at speed. | `bg-surface` | 6.00:1 (over game 3.45:1, large or bold only) |
| `info` | `#8DBBCB` | Neutral system information, hints, dispatch info entries. | `bg-surface` | 8.60:1 |

### Jobs

Job colours mark affiliation as a 6px dot, a 3px rail or an icon tint. The job name itself is always set in `text-primary`.

| Token | Hex | Usage | Background | Contrast |
|---|---|---|---|---|
| `job-police` | `#7499DB` | Police (LSPD / Wasserschutz): job pill dot, MDT header rail, scoreboard group. | `bg-surface` | 6.23:1 |
| `job-ems` | `#E8907F` | EMS / Rettungsdienst: job pill dot, EMS tablet header rail. | `bg-surface` | 7.43:1 |
| `job-mechanic` | `#D08E5A` | Mechanics / Hafenwerkstatt. | `bg-surface` | 6.55:1 |
| `job-civil` | `#AEB3A7` | Civilians and unemployed; neutral default affiliation. | `bg-surface` | 8.35:1 |

### HUD

HUD colours fill gauges and tint icons. The numeral beside a gauge is always `text-primary`.

| Token | Hex | Usage | Background | Contrast |
|---|---|---|---|---|
| `hud-health` | `#EE7B6C` | Health ring and bar. Switches to `danger` below 25 % and to a 1 Hz pulse below 10 %. | `bg-overlay` over white (over black) | 3.76:1 (7.08:1) |
| `hud-armor` | `#93B2DE` | Armor bar. Hidden at 0. | `bg-overlay` | 4.72:1 (8.90:1) |
| `hud-hunger` | `#D8AB78` | Hunger ring. | `bg-overlay` | 4.90:1 (9.23:1) |
| `hud-thirst` | `#70C0D6` | Thirst ring. | `bg-overlay` | 4.99:1 (9.40:1) |
| `hud-stamina` | `#B2CB7E` | Stamina ring. Shown only while < 100 %. | `bg-overlay` | 5.74:1 (10.81:1) |
| `hud-stress` | `#B79AD8` | Stress ring. Shown only while > 0. | `bg-overlay` | 4.22:1 (7.95:1) |
| `hud-voice` | `#A2DBB2` | Proximity voice: mic glyph and range ticks while the player is talking. | `bg-overlay` | 6.51:1 (12.27:1) |
| `hud-radio` | `#EE9759` | Radio: transmitting state, active channel, radio speaker list. | `bg-overlay` | 4.50:1 (8.48:1) |
| `hud-fuel` | `#DDC95F` | Fuel bar and value. Switches to `warning` < 20 % and `danger` < 8 %. | `bg-overlay` | 6.16:1 (11.61:1) |

**Over-game rule.** Every HUD colour clears 3:1, the graphics threshold, in the white worst case. Text over the game world is set only in `text-primary` or `text-secondary`. `danger` text over the game world is bold and at least `--fh-text-md`.

## 3. Typography

### Families and files

FiveM NUI runs offline inside CEF. Every font is shipped with the resource and loaded with `@font-face` from a relative path, with no CDN. SF Pro is not redistributable, and its stand-ins here are:

| Role | Family | Files (in `fonts/`) | Licence |
|---|---|---|---|
| Sans (`--fh-font-sans`, `--fh-font-display`) | Inter (variable, wght 100–900) | `inter-latin-wght-normal.woff2`, `inter-latin-ext-wght-normal.woff2` | SIL OFL 1.1 (`OFL-inter.txt`) |
| Mono (`--fh-font-mono`) | JetBrains Mono (variable, wght 100–800) | `jetbrains-mono-latin-wght-normal.woff2`, `jetbrains-mono-latin-ext-wght-normal.woff2` | SIL OFL 1.1 (`OFL-jetbrains-mono.txt`) |

```css
@font-face { font-family: "Inter"; src: url("fonts/inter-latin-wght-normal.woff2") format("woff2"); font-weight: 100 900; font-display: block; }
@font-face { font-family: "Inter"; src: url("fonts/inter-latin-ext-wght-normal.woff2") format("woff2"); font-weight: 100 900; font-display: block;
  unicode-range: U+0100-024F, U+1E00-1EFF, U+20A0-20AB, U+20AD-20C0; }
@font-face { font-family: "JetBrains Mono"; src: url("fonts/jetbrains-mono-latin-wght-normal.woff2") format("woff2"); font-weight: 100 800; font-display: block; }
@font-face { font-family: "JetBrains Mono"; src: url("fonts/jetbrains-mono-latin-ext-wght-normal.woff2") format("woff2"); font-weight: 100 800; font-display: block;
  unicode-range: U+0100-024F, U+1E00-1EFF; }
```

German umlauts and ß are in the latin subset. `font-display: block` avoids a fallback flash on HUD numerals; the files are local, so the block period is a single frame. List all four files in the resource's `fxmanifest.lua` `files {}`.

### Numerals

- **Every changing number is tabular.** On Inter, set `font-feature-settings: "tnum" 1, "cv11" 1` on the HUD root and on every tablet. `cv11` is Inter's single-storey a; it reads calmer at small sizes.
- **Identifiers are JetBrains Mono.** This covers plates, IDs, case numbers, account numbers, frequencies, coordinates, ammo and serials.
- **Large instrument numerals are Inter.** The speedometer and money use Inter at weight 600 with `tnum`, tracking −0.02em. Inter is crisper than mono at display size.
- **Numbers are formatted in German.** Use the thousands dot and decimal comma (`12.480 $`, `112,40 MHz`, `0,5 kg`), via `Intl.NumberFormat('de-DE')`.

### Scale

Rem-based at the shared root rule (Section 4: 1rem = 10px at 1080p).

| Token | rem | px @1080p | px @720p | px @1440p | Use |
|---|---|---|---|---|---|
| `--fh-text-2xs` | 1.1rem | 11 | 8.8 | 14.7 | Small-caps labels, units. Uppercase only, tracking +0.08em, weight 600. |
| `--fh-text-xs` | 1.2rem | 12 | 9.6 | 16 | Metadata, timestamps, table headers. |
| `--fh-text-sm` | 1.3rem | 13 | 10.4 | 17.3 | Dense tablet body, list rows, chat. |
| `--fh-text-md` | 1.5rem | 15 | 12 | 20 | Default body, buttons, notifications title. |
| `--fh-text-lg` | 1.7rem | 17 | 13.6 | 22.7 | Panel titles, HUD money. |
| `--fh-text-xl` | 2.0rem | 20 | 16 | 26.7 | Dialog titles, ammo count. |
| `--fh-text-2xl` | 2.4rem | 24 | 19.2 | 32 | Screen titles (tablet header, shop name). |
| `--fh-text-3xl` | 3.2rem | 32 | 25.6 | 42.7 | Large values (bank balance, ATM amount). |
| `--fh-text-4xl` | 4.8rem | 48 | 38.4 | 64 | Hero titles (loading, character name, death countdown). The speedometer uses `calc(var(--fh-text-4xl) * 1.5)`. |

Weights: `--fh-weight-regular` 400 (body), `--fh-weight-medium` 500 (values in lists, buttons secondary), `--fh-weight-semibold` 600 (titles, primary values, labels), `--fh-weight-bold` 700 (key caps, critical numerals only).

Leading: 1.45 for body, 1.2 for titles, 1.0 for single-line numerals. Tracking: −0.02em at ≥ `--fh-text-2xl`, 0 for body, +0.08em for uppercase labels.

## 4. Layout, Scaling & Spacing

### Root scaling rule (shared by all six variants)

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }
```

- The rule gives 1rem = 10px at 1080p (reference), 8px at 720p (clamped, scale 0.8) and 13.33px at 1440p (scale 1.333). At 2160p it is capped at 16px.
- **Every size is in rem.** That covers type, spacing, radii, blur and component dimensions. The two exceptions are 1px hairlines, which stay `1px` so they stay crisp, and positions, which are percentages of the viewport.
- At 720p the 0.8 clamp keeps `--fh-text-2xs` at 8.8px rather than 7.3px. Layouts are designed so that the scale-0.8 version still fits 1280px: full-screen panels are at most 156rem wide.
- Ultrawide (21:9) keeps the 16:9 HUD zones anchored to the edges, and full-screen panels stay centred at max 156rem.

### HUD zones (reference 1920×1080, safe inset 3.2rem sides / 3.2rem top / 4.0rem bottom)

| Zone | Anchor | Contents |
|---|---|---|
| Top-left | 3.2rem / 3.2rem | Chat (collapsed: last 4 lines, fades after 8 s). |
| Top-right | 3.2rem / 3.2rem | Status card (time, server ID, job pill, cash, bank), then notification stack below it (gap 1.2rem). |
| Bottom-left | 3.2rem / 4.0rem | Minimap frame, with health/armor bars along its top edge and the needs rings plus voice capsule to its right. |
| Bottom-centre | centred / 4.0rem | Vehicle HUD (in vehicle only). The progress bar sits above it at 22rem from the bottom. |
| Bottom-right | 3.2rem / 4.0rem | Weapon and ammo (armed only). |
| Centre | centred / 31.2rem from the bottom | Interaction hint, above the progress-bar zone; options stack upward, so they stay below the screen centre at 1080p and clear the progress bar at 720p. |

Full-screen menus (inventory, tablets, shops) are centred, max 156 × 88rem, over native screen blur (Section 5).

### Spacing

The base is 4px at 1080p (Tailwind-like keys; 1 = 0.4rem).

| Token | rem | px @1080p | Typical use |
|---|---|---|---|
| `--fh-space-0_5` | 0.2rem | 2 | Gap between a gauge and its tick, icon nudge. |
| `--fh-space-1` | 0.4rem | 4 | Label to value, inside pills. |
| `--fh-space-2` | 0.8rem | 8 | Icon to text, chip padding, list row inner gap. |
| `--fh-space-3` | 1.2rem | 12 | Card padding (dense), HUD chip padding, stack gap. |
| `--fh-space-4` | 1.6rem | 16 | Panel padding (dense), form gap. |
| `--fh-space-5` | 2.0rem | 20 | Panel padding (default). |
| `--fh-space-6` | 2.4rem | 24 | Column gap in tablets. |
| `--fh-space-8` | 3.2rem | 32 | Screen safe inset, section gap. |
| `--fh-space-10` | 4.0rem | 40 | Bottom safe inset, large section gap. |
| `--fh-space-12` | 4.8rem | 48 | Full-screen header height spacing. |
| `--fh-space-16` | 6.4rem | 64 | Loading-screen margins, hero spacing. |

Grids:

- Tablets (MDT, EMS, boss, admin) use a 12-column grid inside 156rem, with gutter `--fh-space-6`. The left rail is 22rem.
- List rows are 4.4rem high, compact rows 3.6rem.
- Click targets are at least 3.2rem (32px at 1080p) on mouse screens.

## 5. Shape, Borders, Depth & Materials

### Radii (continuous corners)

CSS has no true squircle. Every radius is applied with `border-radius` and, where supported (Chromium ≥ 139), `corner-shape: squircle` as progressive enhancement. On Chromium 103 the plain radius is the fallback. Radii nest concentrically: an inner element's radius = outer radius − the padding between them, and never below `--fh-radius-xs`.

| Token | rem | px | Use |
|---|---|---|---|
| `--fh-radius-xs` | 0.4rem | 4 | Bars, ticks, tags, table cells. |
| `--fh-radius-sm` | 0.8rem | 8 | Inputs, key caps, list rows, inventory slots. |
| `--fh-radius-md` | 1.2rem | 12 | Cards, HUD chips, notifications, menus. |
| `--fh-radius-lg` | 1.8rem | 18 | Panels, dialogs, tablets. |
| `--fh-radius-xl` | 2.8rem | 28 | Phone body inner screen, character cards, loading hero card. |
| `--fh-radius-pill` | 999px | – | Buttons, voice capsule, interaction hint, status pills. |

### Borders

- `--fh-border-width` is `1px`, in `border` colour. Every glass surface has it, and dividers use it.
- `--fh-border-width-strong` is `2px`. It marks the selected item (accent colour), the active drop target, and the critical state outline (danger).
- Inputs carry a 1px `text-muted` outline, so the field boundary reaches 5.6:1. On focus the outline is replaced by `--fh-focus-ring`.

### Shadows and glow

- `--fh-shadow-1` is `0 0.2rem 0.6rem rgba(0,0,0,0.28)`. It goes on HUD chips, key caps and small cards.
- `--fh-shadow-2` is `inset 0 1px 0 rgba(236,237,230,0.06), 0 0.8rem 2.4rem rgba(0,0,0,0.36)`. It goes on panels, menus and notifications. The inset line is the glass specular edge.
- `--fh-shadow-3` is `inset 0 1px 0 rgba(236,237,230,0.08), 0 2.4rem 6.4rem rgba(0,0,0,0.50)`. It goes on dialogs, the phone and tablets.
- `--fh-glow-accent` is `0 0 0 1px rgba(211,194,154,0.35), 0 0 1.6rem rgba(211,194,154,0.18)`. It appears on the selected radial segment, the selected character card and the active spawn pin, and nowhere else. Tactical means no neon.
- `--fh-focus-ring` is `0 0 0 2px #0C0D0B, 0 0 0 4px #D3C29A`. The dark inner ring keeps the sand ring visible over any background.

### Materials and blur

| Token | Value | Use |
|---|---|---|
| `--fh-material-thin` | `rgba(22,24,20,0.56)` | Only over NUI-painted content or native screen blur: segmented controls on a tablet, the loading-screen card over its own artwork. |
| `--fh-material-regular` | `rgba(16,17,15,0.80)` (= `bg-overlay`) | Default glass. Every HUD element and everything over the raw game world. |
| `--fh-material-thick` | `rgba(12,13,11,0.90)` | Dialogs, context menus, phone shell, critical overlays; anything holding body text over an unknown background. |
| `--fh-blur-thin` | 1.2rem | Backdrop blur for thin material. |
| `--fh-blur-regular` | 2.4rem | Backdrop blur for regular material. |
| `--fh-blur-thick` | 4.0rem | Backdrop blur for thick material. |

**How glass works in FiveM.**

1. **`backdrop-filter` cannot blur the game.** The game frame is not part of the NUI page, so `backdrop-filter` only blurs NUI content painted beneath it. Over the raw game world it does nothing, and on the CEF Chromium 103 client it also causes repaint flicker.
2. **HUD elements therefore never set `backdrop-filter`.** Their legibility comes from the material opacity alone. The contrast figures in Section 2 are computed that way, without blur.
3. **Full-screen menus blur the game natively.** When a full-screen menu opens (inventory, phone, tablets, shops, garage, clothing, crafting, bank, scoreboard, boss, admin, death), the Lua side calls `TriggerScreenblurFadeIn(200.0)`, and on close `TriggerScreenblurFadeOut(140.0)`. The panels then use `--fh-material-regular` over the natively blurred frame.
4. **`backdrop-filter` with the blur tokens is allowed only for NUI-over-NUI layering.** That means a dialog over a tablet, a menu over the phone, or a card over the loading screen's own background. Always pair it with an opaque-enough material, so the surface still works when the filter is dropped.
5. **Browser support.** The live client is on Chromium 103; Canary has moved to 144. Production CSS must not need container queries, `cq` units, `:has()` or `color-mix()`. Every colour in this system is therefore a literal hex or rgba.

## 6. Motion

| Token | Value | Use |
|---|---|---|
| `--fh-duration-fast` | 120ms | Hover, press, toggle, value tick. |
| `--fh-duration-enter` | 200ms | Element appears: panel, notification, menu, hint. |
| `--fh-duration-exit` | 140ms | Element leaves. Exits are decisive. |
| `--fh-duration-slow` | 320ms | Screen-level transitions: character switch, spawn camera handoff, death overlay fade. |
| `--fh-ease-standard` | `cubic-bezier(0.23, 1, 0.32, 1)` | Default for everything. |
| `--fh-ease-spring` | `cubic-bezier(0.34, 1.36, 0.64, 1)` | Slight overshoot, only for radial-menu segment selection, toggle knobs and the selected character card lift. |

Rules:

- **Enter and exit.** Entries combine opacity 0 → 1 with `translateY(0.8rem)` → 0, or `scale(0.96)` → 1 for dialogs and menus. Never scale from 0, never use `ease-in`.
- **Notifications** slide in from the right by 2.4rem over 200ms. The stack reflows with `transform` over 200ms.
- **Gauges** ease value changes over 320ms linear (data motion may be linear). Numerals switch instantly; there is no counting animation on the HUD. Money changes show a `+1.250 $` / `−80 $` delta line beside the value for 2.4 s.
- **Pulses** run at 1 Hz with an opacity of 1 → 0.45, never a scale pulse. They mark only three things: critical health (< 10 %), seatbelt off above 20 km/h, and transmitting on the radio (the radio uses a steady glow, not a pulse).
- **Turn indicators** blink at 1.5 Hz (on 330ms / off 330ms), matching the vehicle.
- **Loops.** Loading spinners are thin 1.6rem arcs rotating at 900ms linear. Skeleton rows shimmer at 1.4 s linear with an `rgba(236,237,230,0.06)` band.
- **Reduced motion.** `prefers-reduced-motion` and a settings toggle (`data-motion="reduced"` on `html`) turn translate and scale into pure opacity fades at `--fh-duration-fast` and stop the shimmer. The pulses become a static `--fh-border-width-strong` outline.

## 7. Iconography

- **Style.** Outline icons on a 24-unit grid, 1.5-unit stroke, round caps and joins, no fills except status dots and the filled state of toggles. The look is that of SF Symbols "regular", drawn independently. Use an OFL/ISC set (Lucide, ISC licence) bundled locally as inline SVG sprites, or draw custom glyphs on the same grid.
- **Sizes.** 1.6rem in dense lists, 2.0rem for HUD and buttons, 2.4rem for tablet navigation, 3.2rem for empty states.
- **Colour.** Icons take `currentColor`. HUD icons are tinted with their `hud-*` token; navigation icons use `text-secondary`, or `text-primary` when active.
- **No logos or trademarks.** Do not use the Apple logo, SF Symbols glyphs, real police crests, real brand marks, or GTA logos. Faction marks are abstract monograms in a rounded square, for example "P" on a `job-police` tint.
- **Key caps.** A key glyph (`E`, `G`, `F1`, `⇧`) is set in JetBrains Mono 700 on a `text-primary` fill with `text-on-accent` text, radius `--fh-radius-sm`, min 2.8rem square.

## 8. CSS Custom Properties

The shared `--fh-*` block for all six variants. This variant's values follow. NUI resources paste it once into their root stylesheet.

```css
html { font-size: clamp(8px, calc(100vh / 108), 16px); }

:root {
  /* palette */
  --fh-bg-base: #0C0D0B;
  --fh-bg-surface: #161814;
  --fh-bg-elevated: #20231E;
  --fh-bg-overlay: rgba(16, 17, 15, 0.80);
  --fh-border: #3B3F37;
  --fh-text-primary: #ECEDE6;
  --fh-text-secondary: #B5B9AD;
  --fh-text-muted: #8D9285;
  --fh-text-on-accent: #15160F;
  --fh-accent-primary: #D3C29A;
  --fh-accent-secondary: #A4AC7C;
  --fh-success: #73C08B;
  --fh-warning: #E8B04E;
  --fh-danger: #F46A58;
  --fh-info: #8DBBCB;
  --fh-job-police: #7499DB;
  --fh-job-ems: #E8907F;
  --fh-job-mechanic: #D08E5A;
  --fh-job-civil: #AEB3A7;
  --fh-hud-health: #EE7B6C;
  --fh-hud-armor: #93B2DE;
  --fh-hud-hunger: #D8AB78;
  --fh-hud-thirst: #70C0D6;
  --fh-hud-stamina: #B2CB7E;
  --fh-hud-stress: #B79AD8;
  --fh-hud-voice: #A2DBB2;
  --fh-hud-radio: #EE9759;
  --fh-hud-fuel: #DDC95F;

  /* typography */
  --fh-font-sans: "Inter", "Segoe UI", system-ui, sans-serif;
  --fh-font-display: "Inter", "Segoe UI", system-ui, sans-serif;
  --fh-font-mono: "JetBrains Mono", ui-monospace, Consolas, monospace;
  --fh-text-2xs: 1.1rem;
  --fh-text-xs: 1.2rem;
  --fh-text-sm: 1.3rem;
  --fh-text-md: 1.5rem;
  --fh-text-lg: 1.7rem;
  --fh-text-xl: 2rem;
  --fh-text-2xl: 2.4rem;
  --fh-text-3xl: 3.2rem;
  --fh-text-4xl: 4.8rem;
  --fh-weight-regular: 400;
  --fh-weight-medium: 500;
  --fh-weight-semibold: 600;
  --fh-weight-bold: 700;

  /* spacing (1 = 4px at 1080p) */
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
  --fh-radius-xs: 0.4rem;
  --fh-radius-sm: 0.8rem;
  --fh-radius-md: 1.2rem;
  --fh-radius-lg: 1.8rem;
  --fh-radius-xl: 2.8rem;
  --fh-radius-pill: 999px;
  --fh-border-width: 1px;
  --fh-border-width-strong: 2px;

  /* depth */
  --fh-shadow-1: 0 0.2rem 0.6rem rgba(0, 0, 0, 0.28);
  --fh-shadow-2: inset 0 1px 0 rgba(236, 237, 230, 0.06), 0 0.8rem 2.4rem rgba(0, 0, 0, 0.36);
  --fh-shadow-3: inset 0 1px 0 rgba(236, 237, 230, 0.08), 0 2.4rem 6.4rem rgba(0, 0, 0, 0.5);
  --fh-glow-accent: 0 0 0 1px rgba(211, 194, 154, 0.35), 0 0 1.6rem rgba(211, 194, 154, 0.18);
  --fh-focus-ring: 0 0 0 2px #0C0D0B, 0 0 0 4px #D3C29A;

  /* materials */
  --fh-blur-thin: 1.2rem;
  --fh-blur-regular: 2.4rem;
  --fh-blur-thick: 4rem;
  --fh-material-thin: rgba(22, 24, 20, 0.56);
  --fh-material-regular: rgba(16, 17, 15, 0.80);
  --fh-material-thick: rgba(12, 13, 11, 0.90);

  /* motion */
  --fh-duration-fast: 120ms;
  --fh-duration-enter: 200ms;
  --fh-duration-exit: 140ms;
  --fh-duration-slow: 320ms;
  --fh-ease-standard: cubic-bezier(0.23, 1, 0.32, 1);
  --fh-ease-spring: cubic-bezier(0.34, 1.36, 0.64, 1);
}
```

No other `--fh-*` names exist. A screen that needs a derived value computes it locally with `calc()` from these tokens, e.g. `calc(var(--fh-text-4xl) * 1.5)` for the speedometer.

## 9. Shared Component Primitives

Every screen in Section 10 is assembled from these primitives. Their states hold wherever they appear.

**Glass panel.**

- **Fill and edge.** `--fh-material-regular` with a `--fh-border-width` `border` edge, `--fh-shadow-2` and `--fh-radius-lg`.
- **Header.** 5.6rem tall: title in `--fh-text-lg`/600, optional small-caps context label above it, close button on the right.
- **Body.** Padding `--fh-space-5`.

**Buttons.** All buttons are pill-shaped and 3.6rem high (4.4rem for primary dialog actions), with padding `0 --fh-space-4` and label `--fh-text-md`/600.

| Kind | Look | Hover | Press | Disabled | Busy |
|---|---|---|---|---|---|
| Primary | `accent-primary` fill, `text-on-accent` | `#DED0AE` | `#BFAE86` + `scale(0.98)` | opacity 0.4, no pointer | label replaced by 1.6rem spinner + "Bitte warten …", width kept |
| Secondary | `bg-elevated` fill, `border` edge, `text-primary` | `#2A2E27` | `scale(0.98)` | opacity 0.4 | same as primary |
| Destructive | `danger` fill, `text-on-accent` | 8 % lighter | `scale(0.98)` | opacity 0.4 | same as primary |
| Ghost | transparent, `text-secondary` | `bg-elevated` | `scale(0.98)` | opacity 0.4 | – |

- **Focus.** `--fh-focus-ring` on all kinds.
- **Keyboard.** Enter activates the focused button; Esc triggers the screen's cancel or close.

**Input field.**

- **Look.** 4.0rem high, `bg-elevated` fill, 1px `text-muted` outline, `--fh-radius-sm`. Label above it in `--fh-text-xs`/500 `text-secondary`; helper text below in `--fh-text-xs` `text-muted`.
- **States.**
  - Empty: placeholder in `text-muted`.
  - Filled.
  - Focus: `--fh-focus-ring` and a caret in `accent-primary`.
  - Error: outline `danger` at `--fh-border-width-strong`, helper text in `danger` starting with "⚠" and saying what to do.
  - Disabled: opacity 0.4.
  - Read-only: no outline, `bg-surface`.
- **Number fields** are right-aligned mono with the unit as a suffix in `text-muted`.

**List row.**

- **Look.** 4.4rem high, padding `0 --fh-space-3`, primary text `--fh-text-sm`/500, secondary line `--fh-text-xs` `text-muted`, trailing value in mono.
- **States.**
  - Hover: `bg-elevated`.
  - Selected: `bg-elevated` with a 2px `accent-primary` left rail.
  - Disabled: opacity 0.4.
- **Interaction.** Click selects; double-click or Enter runs the row's primary action. Rows are separated by 1px `border` dividers.

**Tabs and segmented control.**

- **Tabs** are text items `--fh-text-sm`/600 `text-secondary`. The active tab is `text-primary` with a 2px `accent-secondary` underline. Keyboard: Q/E, or ←/→ when the tab list is focused.
- **Segmented control.** A `bg-elevated` track with a `--fh-material-thin` thumb that slides over 200ms `--fh-ease-standard`.

**Status pill.** 2.2rem high, `bg-elevated`, a 6px dot in the status or job colour, and the label in `text-primary` `--fh-text-xs`/600.

**Key cap.** See Section 7. Paired with its action text in `text-primary`.

**Gauge (bar).**

- **Look.** Track `rgba(236,237,230,0.12)`, 0.4rem high (0.6rem for health), radius `--fh-radius-xs`, fill in the `hud-*` colour.
- **Values.** The numeral sits beside the bar in mono, `text-primary`.
- **States.**
  - Normal.
  - Low: fill switches to `warning`.
  - Critical: fill switches to `danger` and pulses.
  - Hidden: when the value carries no information (armor 0, stamina 100, stress 0).

**Gauge (ring).**

- **Look.** A 4.4rem circle with a 0.4rem stroke and a centred 1.8rem glyph, as a watch complication. The arc starts at 12 o'clock and runs clockwise. The track is `rgba(236,237,230,0.12)` and the arc is the `hud-*` colour.
- **Values.** Below 50 % the numeral appears under the ring in mono `--fh-text-2xs`.

**Generic screen states.** Every list, table or data screen has these four states.

1. **Loading.**
   - Skeleton rows matching the final row height: 3 to 8 rows of `rgba(236,237,230,0.06)` bars with shimmer.
   - A loading line in the header: a 1.6rem spinner plus the text "Lade …".
   - Actions are disabled.
   - After 8 s the text changes to "Dauert länger als üblich …", still in the loading state.
2. **Empty.**
   - A centred 3.2rem outline icon in `text-muted`.
   - A one-line title in `text-primary` `--fh-text-md`/600 and one line of guidance in `text-secondary`.
   - At most one secondary action button.
   - The copy is specific to the screen (given per screen below).
3. **Error.**
   - The icon is a "⚠" circle in `danger`.
   - The title is specific to the screen.
   - The detail line is in `text-secondary` and includes the reference code in mono (e.g. `ERR 503 · bank:balance`).
   - The actions are a primary "Erneut versuchen" button, which re-fires the same NUI callback, and a ghost "Schließen" button.
   - Data already loaded stays visible, dimmed to 0.5, behind an inline error banner. The full-panel error appears only when nothing loaded.
4. **Filled.** The normal content.

**Validation and feedback.**

- A failed NUI callback becomes a `danger` notification and leaves the screen open.
- A successful mutation becomes a `success` notification. On a full-screen menu, the changed item also shows a 1 s `accent-primary` outline flash, replaced by the static outline under reduced motion.

## 10. Screen and Component Rules

The structure of each entry:

- **Layout** at 1920×1080.
- **States** beyond the generic four of Section 9.
- **Interactions**: input → result.
- **Copy** in German.

"NUI → Lua" names the callback a control fires.

### 10.1 Loading screen

**Layout.**

- Full-screen `bg-base` with a server key visual: harbour at dusk in a graphite grade, darkened to 60 % with a bottom vignette. The visual is NUI-painted.
- **Top-left.** Wordmark "HAFENSTADT" (`--fh-text-2xl`/600, tracking +0.2em). It is the server name, set in plain type with no logo.
- **Bottom-left.** A `--fh-material-thin` card with `backdrop-filter: blur(var(--fh-blur-regular))`, 56rem wide, `--fh-radius-xl`. The card holds:
  - the progress label "Lade Spielwelt",
  - the stage text in `text-secondary` (e.g. "Ressourcen 142 / 310"),
  - a 0.4rem `accent-primary` progress bar with the percentage in mono `--fh-text-3xl`,
  - a rotating tip: "Tipp: Mit [F1] öffnest du das Handy." It rotates every 8 s with a 320ms crossfade.
- **Bottom-right.** Server news list (3 items: date in mono plus headline). Music control: a pill with play/pause, track name and a volume slider.
- **Top-right.** Keyboard reference chips (`F1` Handy, `TAB` Inventar, `M` Menü, `Z` Sprechweite).

**States.**

- Initialising: indeterminate bar, the text "Verbinde mit Server …".
- Loading: determinate progress with the stage text.
- Stalled: no progress for 30 s. The stage text becomes "Hängt bei: <resource>" in `warning`, and a hint appears: "Spiel nicht schließen – manche Ressourcen brauchen länger."
- Error: the connection was dropped. FiveM shows its own dialog, so the NUI only shows "Verbindung verloren" until it is unloaded.
- Complete: 100 %, the text "Fertig", then a 320ms fade to black handing over to character selection.

**Interactions.**

| Input | Result |
|---|---|
| Space | Toggles music. |
| Scroll on the volume slider | Changes volume in 5 % steps. |
| Click on a news item | Expands it inline. |

There is no other input; the loading screen cannot be dismissed.

### 10.2 Multi-character selection

**Layout.**

- The game camera shows the selected character, the natively blurred background behind it.
- **Left: character rail.** A 40rem rail of character cards.
  - Each card is 8.8rem high, `--fh-radius-xl`, glass regular.
  - Card content: first and last name `--fh-text-lg`/600, job pill, cash and bank in mono, last played ("Zuletzt: 14.10. · 22:41"), playtime ("212 h").
  - Slots: 4, plus one locked slot for supporters.
- **Right: detail column.** 36rem wide: birth date, nationality, phone number in mono, address, licences (Führerschein, Waffenschein as pills).
- **Bottom-centre: actions.** Primary "Spielen" (4.4rem), plus "Löschen" as a destructive ghost.

**States.**

- Loading: 4 skeleton cards.
- Empty (no characters): a centred card with the title "Noch kein Charakter" and the text "Erstelle deinen ersten Bürger der Hafenstadt." The primary button is "Charakter erstellen".
- Filled: the first or last-played character is selected and lifted with `--fh-glow-accent` and a `--fh-border-width-strong` accent edge.
- Free slot: a dashed 1px `border` card with "+ Neuer Charakter".
- Locked slot: a lock icon and "Slot gesperrt · Supporter".
- Error: the generic error state, with the title "Charaktere konnten nicht geladen werden".

**Interactions.**

| Input | Result |
|---|---|
| Click a card, or ↑/↓ | Selects it. NUI → Lua `chars:select {cid}`; the camera swaps the ped. |
| Enter or "Spielen" | `chars:play {cid}` → spawn selector. |
| "Löschen" | Confirm dialog (10.15) with typed confirmation: the character's first name must be entered. Then `chars:delete`. |
| Free slot | Opens the character creator. |

### 10.3 Character creator

**Layout.**

- The ped stands centred in the game camera.
- **Left panel (44rem).**
  - Top: a 5-step stepper with numbered segments: 1 Identität, 2 Herkunft, 3 Gesicht, 4 Haare & Merkmale, 5 Kleidung. Done steps carry a check, the current step is `accent-primary`.
  - Below it, the step form.
- **Right: camera controls.** A vertical segmented control (Ganzkörper / Oberkörper / Gesicht), a rotate slider (−180° to 180°), and a hint chip "[A]/[D] drehen".
- **Bottom: navigation.** "Zurück" (secondary) and "Weiter" (primary). On step 5 the primary button is "Fertigstellen".

**Controls per step.**

1. **Identität.** Text fields Vorname and Nachname, a date field Geburtsdatum (TT.MM.JJJJ), a segmented control Geschlecht, a select Nationalität.
2. **Herkunft.** Two parent pickers (a horizontal strip of 1:1 thumbnails), plus sliders Ähnlichkeit and Hautton (0–100).
3. **Gesicht.** About 20 sliders, grouped under small-caps headers (Nase, Augen, Kiefer …) and shown in an accordion. Each slider is a 0.4rem track with an accent thumb of 1.6rem and the value in mono to the right.
4. **Haare & Merkmale.** A swatch grid for hair colour (2.8rem chips, selected chip with a 2px accent ring), plus selects and sliders for beard, brows and age.
5. **Kleidung.** Preset outfits as cards.

**States.**

- Field error: the name contains digits → "Nur Buchstaben, Bindestrich und Leerzeichen." The age is under 18 → "Mindestalter 18 Jahre."
- Name taken (checked on "Weiter"): "Dieser Name ist bereits vergeben."
- Saving: "Fertigstellen" shows the busy state.
- Save error: the generic error state as a banner. The form keeps its values.

**Interactions.**

| Input | Result |
|---|---|
| Any slider change | `creator:preview {key, value}`, live on the ped, throttled to 30 Hz. |
| "Weiter" | Validates the step. |
| "Fertigstellen" | `creator:save` → spawn selector. |
| Esc | Confirm dialog "Erstellung abbrechen? Deine Eingaben gehen verloren." |

### 10.4 Spawn selector

**Layout.**

- Full-screen map stand-in: a stylised graphite city map, NUI-painted with grid lines at 1px `border`.
- **Spawn pins.** Each pin is a 3.2rem circle with an icon. The selected pin is `accent-primary` with `--fh-glow-accent` and a label callout.
- **Right list (40rem).** Locations with name, district and distance or travel note, e.g.:
  - Letzte Position
  - Wohnung · Speicherstadt
  - Fähranleger
  - Fischmarkt
  - Hauptbahnhof
  - Krankenhaus (EMS only)
  - Präsidium (police only)
- **Bottom of the list.** Primary "Hier aufwachen".

**States.**

- Loading: skeleton list and pins hidden.
- Location unavailable: the pin and row are disabled with the reason, e.g. "Nur im Dienst".
- Last position missing: the row is hidden.
- Error: the generic error state.
- Spawning: the button is busy, then the camera transition runs over 320ms and the NUI fades out.

**Interactions.**

| Input | Result |
|---|---|
| Click on a pin or row, or ↑/↓ | Selects it and the camera previews it (`spawn:preview {id}`). |
| Enter | `spawn:confirm {id}`. |

### 10.5 HUD: player status

- **Health and armor bars.**
  - Position: over the top edge of the minimap frame, the full frame width, 0.6rem and 0.4rem high, gap 0.4rem.
  - Each bar has a mono value at its right end.
  - Armor hides at 0.
  - Health turns `danger` at < 25 % and pulses at < 10 %.
- **Needs rings: hunger, thirst, stamina, stress.**
  - Position: a 2×2 cluster of 4.4rem rings right of the minimap, gap `--fh-space-2`. Each ring sits on a 5.6rem `--fh-material-regular` rounded square (`--fh-radius-md`).
  - Visibility: hunger and thirst always show; stamina only < 100 %; stress only > 0. A hidden ring leaves no gap — the cluster collapses toward the minimap.
  - Thresholds: hunger and thirst become `warning` at < 25 % and `danger` at < 10 %, with a numeral below the ring.
- **Voice and radio capsules.**
  - Position: under the needs cluster, two stacked pills 3.2rem high (voice above, radio below), so the cluster stays narrower than 14rem and clears the vehicle HUD at 720p.
  - Content: mic glyph, range label (Flüstern / Normal / Rufen) and 3 range ticks; the active range is filled.
  - Idle: `text-secondary` glyph.
  - Talking: glyph and ticks in `hud-voice`, plus a 2px `hud-voice` edge.
  - Radio on: the second pill shows "FUNK" plus the channel in mono ("112,40") in `hud-radio`. Radio off: the pill is hidden.
  - Transmitting: the radio pill fills `hud-radio` with `text-on-accent` text and shows "SENDET".
  - Muted or no microphone: a crossed mic glyph in `danger` and the text "Kein Mikro".
- **Interactions.**
  - Range key (default Z): cycles the range. The capsule shows its label for 1.2 s.
  - Radio PTT (default CapsLock): the transmitting state.

### 10.6 HUD: money, job, ammo, minimap

- **Status card (top-right).** 30rem wide, `--fh-material-regular`, `--fh-radius-md`. It has four parts:
  - Row 1: time (mono, "21:47") and server ID ("ID 128"), in `text-secondary` `--fh-text-xs`.
  - Row 2: job pill with job dot, e.g. "Polizei · Kommissar" or "Rettungsdienst · Notfallsanitäter", and an "Im Dienst" / "Außer Dienst" dot (`success` / `text-muted`).
  - Rows 3 and 4: Bargeld and Bank. Small-caps label left, value right in Inter 600 `--fh-text-lg` with `tnum` ("12.480 $", "248.300 $").
  - Change delta: shown beside the value for 2.4 s in `success` or `danger`.
- **Money visibility.** The card shows money only for 6 s after a change or while Alt is held, so the screen stays calm. The job row always shows.
- **Ammo (bottom-right).** Shown only while armed. It has:
  - the weapon name in `--fh-text-xs` small caps, e.g. "PISTOLE .50",
  - the magazine count in `--fh-text-4xl` mono and the reserve as "/ 120" in `text-secondary` `--fh-text-xl`,
  - fire mode pills (EINZEL / SALVE / AUTO).
  States:
  - Empty magazine: the count turns `danger` and the label reads "Nachladen [R]".
  - Reloading: an 0.4rem progress line under the count.
  - Melee or no ammo: count hidden, only the weapon name.
- **Minimap frame (bottom-left).**
  - A frame matched to the native radar position set by the resource. Reference frame 27.2 × 17.6rem, `--fh-radius-md`, 1px `border` edge plus `--fh-shadow-1`, a mask on the native corners.
  - Under the frame: the street and district line, "Am Sandtorkai · Speicherstadt", and the compass heading in mono ("NO 042°").
  - When on foot and not in a vehicle the radar hides (server setting), and with it the frame. The health and armor bars then sit at the frame's former top line.

### 10.7 Vehicle HUD

**Layout.** Bottom-centre, 56rem wide, `--fh-material-regular` slab with `--fh-radius-lg`. It shows only in a vehicle.

**Elements.**

- **Speedometer.**
  - The speed is in `calc(var(--fh-text-4xl)*1.5)` Inter 600 `tnum`, padded with dim zeros: "087" with the "0" in `text-muted`. The unit "KM/H" is in small caps.
  - Above it: a 240° RPM arc of 0.3rem in `text-secondary`. From 85 % the arc turns `warning`, and at the limiter `danger`.
  - Gear in mono: "3", "N", "R".
- **Fuel.** A horizontal gauge with a fuel glyph and the value in mono ("38 L" or "62 %"). Colour `hud-fuel`, `warning` < 20 %, `danger` < 8 %. Electric vehicles show a battery glyph and "%". Low fuel also raises a warning notification once: "Tank fast leer · ca. 8 km Reichweite".
- **Seatbelt.**
  - Fastened: belt glyph in `success`.
  - Unfastened: glyph in `danger`, pulsing above 20 km/h, plus the hint "[B] Anschnallen".
  - Vehicles without belts (bikes): hidden.
- **Engine state.** A glyph plus a short label:
  - OK (`text-secondary` glyph, no label),
  - "Motor beschädigt" (`warning`, < 40 %),
  - "Motor kritisch" (`danger`, < 15 %),
  - "Motor aus" (`text-muted`).
- **Indicators.** Left and right arrows sit at the top corners of the speed block, outside the RPM arc, and blink in `success` at 1.5 Hz; hazards light both. The low beam, high beam (`info`) and cruise control ("TEMPOMAT 80" in mono) are indicator glyphs in a row under the speed. Off glyphs are `text-muted` at 0.5.
- **Extra row.** Odometer and plate in mono ("HK · 4127").

**Interactions.** None on the HUD itself. It reflects the game state only.

### 10.8 Notifications (4 types)

**Layout.**

- Top-right stack under the status card, 36rem wide, max 4 visible. Older ones collapse into a "+2 weitere" pill.
- Each notification: `--fh-material-regular`, `--fh-radius-md`, `--fh-shadow-2`, a 0.3rem rail in the type colour on the left, a type glyph, the title `--fh-text-md`/600, the body `--fh-text-sm` `text-secondary` (max 2 lines), and a time or source in `--fh-text-2xs`.

**Types.**

| Type | Colour | Example |
|---|---|---|
| Info | `info` | "Neue Nachricht", "Von Mara K.: Treffpunkt Fischmarkt?" |
| Erfolg | `success` | "Überweisung erhalten", "+1.250 $ von Hafenlogistik GmbH" |
| Warnung | `warning` | "Tank fast leer", "Reichweite ca. 8 km" |
| Fehler | `danger` | "Aktion fehlgeschlagen", "Du hast nicht genug Platz im Inventar." |

**Behaviour.**

- **Durations.** Info and Erfolg stay 5 s, Warnung 7 s, Fehler 9 s. A 1px progress hairline under the body shows the remaining time.
- **Entry and exit.** Enter from the right over 200ms, exit by fading over 140ms.
- **Duplicates** within 2 s merge into one with a "×3" counter.
- **No interaction.** The cursor is not active in gameplay.

### 10.9 Progress bar

**Layout.**

- Centred, 22rem above the bottom, 40rem wide.
- The label sits above the bar, left-aligned, e.g. "Reparatur läuft …". The percentage or remaining seconds sit right-aligned in mono ("62 %" / "4,2 s").
- The bar is a 0.6rem `accent-primary` fill on a `rgba(236,237,230,0.12)` track inside a `--fh-material-regular` pill container.
- Below the bar: "[X] Abbrechen" if the action is cancellable.

**States.**

- Running.
- Cancelled: the fill turns `danger`, the label reads "Abgebrochen", and it fades out after 0.8 s.
- Complete: the fill turns `success`, the label gets a check, and it fades out after 0.6 s.

**Interaction.** X cancels: `progress:cancel`.

### 10.10 Interaction hint "[E] …"

**Layout.**

- Centred, its bottom edge 31.2rem above the screen bottom, a `--fh-material-regular` pill 4.4rem high: key cap plus action text `--fh-text-md`/500.
- An optional second line in `text-secondary` gives context, e.g. "Garage Speicherstadt".
- Multiple options stack vertically, max 3, each with its own key (E, G, H).

**States.**

- Available.
- Unavailable: key cap dimmed and the reason shown, e.g. "Abgeschlossen".
- Holding: for hold actions the key cap is ringed by a 0.3rem `accent-primary` progress arc and the text reads "Halten: Tür aufbrechen".

**Interaction.** Pressing the key fires the bound action. The hint plays a 120ms scale(0.96) feedback.

### 10.11 Death / unconscious screen

**Layout.**

- The game is natively blurred and desaturated, with a full-screen `rgba(12,13,11,0.55)` vignette.
- **Centre.**
  - Title "Bewusstlos" in `--fh-text-4xl`/600.
  - Subline in `text-secondary`: "Du wurdest schwer verletzt. Warte auf den Rettungsdienst."
  - A respawn countdown in mono `--fh-text-3xl` ("04:32"), inside a 16rem ring that empties clockwise.
- **Below.**
  - Status line: "Notruf gesendet · Rettungsdienst informiert", with a `success` dot.
  - Or, before a call: "[G] Notruf absetzen".
  - When EMS is en route: the ETA in mono.

**States.**

- Unconscious, countdown running: the respawn action is disabled and reads "Aufwachen im Krankenhaus in 04:32".
- Call sent.
- EMS en route ("Rettungsdienst unterwegs · ETA 01:10").
- Being revived: a progress bar with "Wiederbelebung läuft …".
- Countdown done: "[E] Im Krankenhaus aufwachen (Kosten 500 $)" becomes available.
- Revived: fades out over 320ms.

**Interactions.**

| Input | Result |
|---|---|
| G | `death:callEms`, once. The key then shows "Notruf gesendet". |
| E (after the countdown) | Confirm dialog, then `death:respawn`. |

### 10.12 Radial menu

**Layout.**

- Centred, 44rem diameter.
- 6 to 8 segments in a `--fh-material-thick` ring with 1px `border` dividers. The centre disc (14rem) shows the hovered item's label and description.
- Each segment holds a 2.4rem glyph and a short label (`--fh-text-xs`). Segments with children carry a small "›" at the outer edge.
- Example root: Fahrzeug, Kleidung, Ausweis zeigen, Emotes, Rechnungen, Job, Walkie-Talkie, GPS.

**States.**

- Hover or selected segment: `bg-elevated` fill, label `text-primary`, outer arc 2px `accent-primary`, `--fh-glow-accent`. The scale lifts to 1.02 with `--fh-ease-spring`.
- Disabled segment: opacity 0.4, with the reason in the centre ("Nur im Fahrzeug").
- Submenu: the ring replaces its segments over 200ms, and the centre shows "‹ Zurück".
- Empty (no options): the centre shows "Keine Aktionen verfügbar".

**Interactions.**

| Input | Result |
|---|---|
| Hold M (default) | Opens the menu with the cursor centred. |
| Mouse direction | Highlights a segment. |
| Release, or click | Executes it: `radial:select {id}`. |
| Right-click | Back. |
| Esc | Closes without action. |

### 10.13 Context menu

**Layout.**

- Anchored at the cursor or the target item, 24rem wide, `--fh-material-thick`, `--fh-radius-md`, `--fh-shadow-2`.
- A header with the target name in small caps, e.g. "WASSERFLASCHE".
- Rows 3.6rem: glyph, label, shortcut in mono at the right. Groups are separated by 1px dividers. Destructive rows are in `danger`.

**States.**

- Row hover: `bg-elevated`.
- Disabled row: opacity 0.4, with a tooltip reason.
- Row with submenu: "›"; the submenu opens to the right, or flips left at the screen edge.
- Loading (options fetched): 3 skeleton rows.

**Interactions.**

| Input | Result |
|---|---|
| Click or Enter | Runs the row. |
| ↑/↓ | Moves through rows. |
| Esc, or a click outside | Closes. |

Example rows: Benutzen, Geben …, Teilen …, Wegwerfen.

### 10.14 Input dialog

**Layout.**

- Centred modal, 48rem wide, `--fh-material-thick` with `backdrop-filter` when over NUI, `--fh-radius-lg`, `--fh-shadow-3`.
- Title `--fh-text-xl`/600, then a description, then 1 to 4 fields (text, number with unit, select, textarea), then the actions right-aligned: "Abbrechen" (secondary) and the primary action named with a verb ("Überweisen", "Speichern").

**States.**

- Empty: primary disabled until all required fields are valid.
- Field error.
- Submitting: primary busy.
- Server error: inline banner above the actions. The values are kept.

**Interactions.**

| Input | Result |
|---|---|
| Enter | Submits. |
| Esc | Cancels. |
| Tab | Cycles the fields. |

On submit, the dialog returns `{values}` to the calling resource via its callback.

### 10.15 Confirm dialog

**Layout.**

- 44rem, the same material as 10.14.
- A glyph (warning or danger) at the left of the title, a question title (e.g. "Fahrzeug verkaufen?"), the consequence in `text-secondary` ("Der Sultan RS wird für 18.400 $ an den Händler verkauft. Das kann nicht rückgängig gemacht werden."), then the actions "Abbrechen" and "Verkaufen".

**States.**

- Normal.
- Destructive: the primary is the destructive button and focus starts on "Abbrechen".
- Typed confirmation: for deletions, a field "Gib LÖSCHEN ein"; primary disabled until it matches.
- Busy.
- Error banner.

**Interactions.** Enter confirms, unless the dialog is destructive with focus on cancel. Esc cancels.

### 10.16 Chat

**Layout.**

- Top-left, 52rem wide.
- **Collapsed.** The last 4 messages are shown without a background panel. Each line sits on its own `--fh-material-regular` row pill (`--fh-radius-sm`) so it stays readable over the game. The lines fade out after 8 s.
- **Open (T).**
  - The panel gets a `--fh-material-regular` background, 12 visible lines, a scroll area and an input at the bottom (4.0rem).
  - Channel tabs: Alle / OOC / Fraktion / Admin.
- **Message line.**
  - Timestamp in mono `text-muted`, then a channel tag pill, then the sender and ID ("Mara K. [57]") in `text-primary` 600, then the text.
- **Channel tag colours.**

  | Tag | Colour |
  |---|---|
  | `OOC` | `text-secondary` |
  | `ME` | `hud-stress` |
  | `DO` | `info` |
  | `TWT` | `info` |
  | `POLIZEI` | `job-police` |
  | `LSMD` | `job-ems` |
  | `ADMIN` | `danger` |

  Each tag also carries its text.

**States.**

- Empty (no messages): the open panel shows "Noch keine Nachrichten. Mit /help siehst du alle Befehle."
- Command suggestion: typing "/" opens a suggestion list above the input, showing the command, its parameters in mono and a description.
- Send error ("Du schreibst zu schnell. Warte 2 s."): `danger` helper text under the input.
- Muted: the input is disabled with "Du bist für 10 min stummgeschaltet."

**Interactions.**

| Input | Result |
|---|---|
| T | Opens the chat. |
| Enter | Sends (`chat:send`). |
| Esc | Closes. |
| ↑/↓ | Input history. |
| Tab | Completes a suggestion. |
| PageUp/PageDown | Scrolls. |

### 10.17 Scoreboard

**Layout.**

- Centred panel 96 × 72rem.
- **Header.**
  - The server name and "128 / 200 Spieler" in mono.
  - Job counters as pills with job dots: "Polizei 14", "Rettungsdienst 6", "Mechaniker 4". Counts only, no names in the police column (a role-play rule).
  - Uptime and restart time ("Neustart in 02:14").
- **Table.** Columns: ID (mono), Name, Job (dot plus name), Spielzeit, Ping (mono, coloured by quality: < 80 `success`, < 150 `warning`, else `danger`, plus a bar glyph). Rows 3.6rem; own row with an `accent-secondary` left rail.

**States.**

- Loading skeleton.
- Filled.
- Search with no result: "Kein Spieler mit „xyz“ gefunden."
- Error: the generic error state.

**Interactions.**

| Input | Result |
|---|---|
| Hold Home/F10 (configurable) | Shows the scoreboard; release hides it. |
| While shown, click | Activates the cursor and the search field. |
| Click a column header | Sorts by that column. |

### 10.18 Inventory

**Layout.** A full-screen centred panel 156 × 80rem over native blur, with three columns.

- **Left: the player inventory.**
  - A 5-column grid of slots, 10.4rem square, `--fh-radius-sm`, `bg-elevated` at 0.7 alpha.
  - Hotbar slots 1–5 are marked with a mono number in the slot's top-left corner.
  - Each slot holds the item image area (glyph stand-in), the count in mono at the top-right ("×4"), the name in `--fh-text-2xs` at the bottom and a durability bar if relevant.
  - A weight bar in the header: "24,6 / 40,0 kg" in mono, with the bar `warning` > 85 %.
- **Centre: equipped and quick info.** Character silhouette with slots: Waffe, Rucksack, Weste, Telefon, Funkgerät. Below it, a selected-item detail card: name, description, weight, metadata (serial number in mono, quality %) and the actions "Benutzen", "Teilen", "Geben".
- **Right: secondary inventory.** The context decides what it is: Boden (ground), Kofferraum "HK · 4127" (vehicle trunk), Handschuhfach, Lager or another player when searching. It has the same slot grid and its own weight bar.

**States.**

- Loading: skeleton slots.
- Empty: the player inventory reads "Deine Taschen sind leer." The ground shows an empty grid with "Hier liegt nichts. Ziehe Gegenstände hierher, um sie abzulegen."
- Dragging: the source slot is dimmed to 0.4, the ghost follows the cursor with `--fh-shadow-2`, a valid target gets a 2px `accent-primary` border, an invalid target a 2px `danger` border plus a reason tooltip ("Zu schwer", "Slot belegt").
- Overweight: the weight bar is `danger` and the header reads "Überladen – du bewegst dich langsamer".
- Error: a failed move snaps the item back over 200ms and raises an error notification.
- Locked (another player is searching the same container): an overlay with "Wird gerade von jemand anderem durchsucht."

**Interactions.**

| Input | Result |
|---|---|
| Drag and drop | Moves the item (`inv:move {from, to, slot, count}`). |
| Shift + drag | Splits the stack: an input dialog asks for the amount. |
| Right-click | Context menu (10.13). |
| Double-click | Uses the item. |
| 1–5 while closed | Uses the hotbar slot. |
| TAB or Esc | Closes and fires `TriggerScreenblurFadeOut`. |

### 10.19 Phone

**Layout.**

- Bottom-right, 36 × 74rem.
- The shell is `--fh-material-thick` with a 1px `border` and `--fh-radius-xl`. The screen inside is `bg-base` with radius `--fh-radius-xl` − 0.8rem (concentric).
- **Status bar.** Time in mono, carrier "Hafen Mobil", signal and battery glyphs.
- **Home.** A grid of 4 × 5 app tiles (6.4rem rounded squares in `bg-elevated` with an outline glyph in the app's hue; labels `--fh-text-2xs`) and a dock with Telefon, Nachrichten, Kontakte and Kamera.
- **Apps drawn in the preview.** Home, Nachrichten thread and incoming call.
- **App list.** Telefon, Nachrichten, Kontakte, Kamera, Galerie, Bank, Hafenmarkt (classifieds), Dienste (Taxi/Mechaniker/Polizei), Karte, Einstellungen, Notizen, Musik.

**Screens.**

- **Messages.**
  - The thread list shows avatar initials, name, a 1-line preview and the time in mono.
  - In the conversation, own bubbles are `accent-primary` with `text-on-accent` and the other side's bubbles are `bg-elevated`.
  - Input bar with a send button.
- **Incoming call.** Full-screen within the phone: the caller name `--fh-text-2xl`, the number in mono, and the buttons "Ablehnen" (danger circle 6.4rem) and "Annehmen" (success circle).
- **Notification banner on the phone.** Slides down within the screen.

**States.**

- No signal (in a tunnel, or in the water): the status bar reads "Kein Netz" and sending is disabled with "Kein Netz – Nachricht wird gesendet, sobald du Empfang hast."
- Battery empty: a black screen with "Akku leer".
- Empty thread list: "Keine Nachrichten".
- Loading: a spinner in the app header.
- Error: the generic error state within the app.

**Interactions.**

| Input | Result |
|---|---|
| F1 | Opens; the phone slides up from 4rem below over 200ms. |
| Esc | Closes. |
| Click a tile | Opens the app. |
| Swipe gesture (drag up from the bottom bar) | Goes home. |

### 10.20 Bank / ATM

**Layout.**

- **Bank (counter).** Panel 120 × 72rem.
  - Left rail: the accounts list (Girokonto, Sparkonto, Firmenkonto with role) with balances in mono.
  - Main area:
    - balance hero `--fh-text-3xl`,
    - account number in mono ("HK-DE 0482 1173"),
    - quick actions Einzahlen / Abheben / Überweisen as 3 cards,
    - the transaction list: date mono, counterparty, purpose, amount right-aligned mono with `success` for + and `text-primary` for −.
  - Statement filters: 7 / 30 / 90 Tage.
- **ATM.** A compact 56 × 64rem variant.
  - A card-insert step, then a PIN entry with 4 dots and a numeric keypad in a 3×4 grid of 6.4rem keys.
  - Then the menu: Kontostand, Abheben with presets (50 / 100 / 200 / 500 / Anderer Betrag) and Einzahlen.
  - A daily limit line: "Tageslimit 5.000 $ · verbleibend 3.200 $".

**States.**

- Loading: skeleton balance.
- Empty transactions: "Noch keine Umsätze in diesem Zeitraum."
- Insufficient funds (field error): "Nicht genug Guthaben. Verfügbar: 1.240 $".
- Wrong PIN: the dots shake once and turn `danger`, with "PIN falsch · 2 Versuche übrig". After 3 tries: "Karte gesperrt. Wende dich an die Bank."
- Processing: the busy button.
- Success: a check, the amount and "Neuer Kontostand 247.050 $".
- Error: "Bank nicht erreichbar".

**Interactions.**

| Input | Result |
|---|---|
| Keypad (keyboard digits work too) | Enters the PIN. |
| Enter | Confirms the PIN. |
| Backspace | Deletes a digit. |
| Amount preset click | Fills the amount. |
| "Überweisen" | Input dialog (Empfänger-Konto, Betrag, Verwendungszweck) → confirm → `bank:transfer`. |

### 10.21 Shop

**Layout.**

- Panel 140 × 80rem.
- **Header.** The shop name ("Kiosk Sandtorkai · 24/7"), category tabs (Alle, Getränke, Essen, Werkzeug, Elektronik) and a search field.
- **Product grid.** 4 columns of cards (`bg-elevated`, `--fh-radius-md`): glyph area, name, price in mono, stock ("12 auf Lager", `warning` ≤ 3, "Ausverkauft" `danger`), and a "+" add button.
- **Right: cart (40rem).** Each line has a quantity stepper (− 2 +), the line total in mono and a remove "×". The footer has the subtotal and total in mono `--fh-text-xl`, a payment segmented control (Bar / Karte), and the primary "Bezahlen · 55 $".

**States.**

- Empty cart: "Dein Warenkorb ist leer. Wähle links Artikel aus."
- Out of stock: the card is dimmed and the button disabled.
- Not enough money: the primary is disabled with "Nicht genug Bargeld (fehlen 12 $)".
- Inventory full: the error banner "Nicht genug Platz im Inventar".
- Paying: busy.
- Success: a notification, the cart clears and the panel stays open.
- Loading.
- Error.

**Interactions.**

| Input | Result |
|---|---|
| "+" | Adds one. |
| Stepper | Changes the quantity. |
| Search | Filters live. |
| "Bezahlen" | `shop:checkout {items, method}`. |

### 10.22 Garage

**Layout.**

- Panel 130 × 76rem.
- **Left: filter tabs.** Alle / Hier geparkt / Abgeschleppt / Unterwegs.
- **Vehicle list.** Rows show the model name, the plate in mono on a plate chip ("HK · 4127", `bg-elevated` with a 1px `text-muted` edge), the location, and fuel, engine and body condition as three mini bars with mono % values. The status pill reads "Geparkt" (`success`), "Abgeschleppt" (`warning`) or "Unterwegs" (`info`).
- **Right: detail.** A stand-in silhouette, stats, and actions "Ausparken" (primary), "Umbenennen" and "Schlüssel teilen". For an impounded vehicle: "Auslösen · 750 $".

**States.**

- Empty: "Keine Fahrzeuge in dieser Garage. Parke ein Fahrzeug, indem du in die Einfahrt fährst und [E] drückst."
- Spawn point blocked: an error banner "Ausfahrt blockiert – warte, bis der Platz frei ist."
- Unterwegs: "Ausparken" is disabled with "Fahrzeug ist bereits unterwegs".
- Loading, error and spawning (busy) states.

**Interactions.**

| Input | Result |
|---|---|
| Row click | Selects the vehicle. |
| Enter or "Ausparken" | `garage:takeOut {plate}`, then the panel closes. |

### 10.23 Clothing store

**Layout.**

- The ped sits centred-right in the camera.
- **Left panel (48rem).**
  - Category tabs as glyphs with tooltips: Oberteil, Unterteil, Schuhe, Hut, Brille, Accessoires, Masken.
  - For each component: a slider row "Modell 14 / 212" with ‹ › step buttons and a mono value, plus "Textur 2 / 6".
  - Below: a saved-outfits list with "Outfit speichern".
- **Bottom.** The price summary ("Änderungen: 3 Teile · 240 $") with "Verwerfen" and "Kaufen · 240 $".
- **Camera control.** As in 10.3.

**States.**

- Unchanged: "Kaufen" disabled with "Keine Änderungen".
- Changed: the changed component tabs carry a 6px `accent-primary` dot.
- Item restricted (job clothes): disabled with "Nur für Polizei".
- Not enough money.
- Busy.
- Error.

**Interactions.**

| Input | Result |
|---|---|
| ←/→ | Steps the model. |
| ↑/↓ | Changes the category. |
| Any change | Live preview `clothing:preview`. |
| Esc with changes | Confirm "Änderungen verwerfen?". |

### 10.24 Crafting

**Layout.**

- Panel 130 × 76rem.
- **Left: recipe list.** Grouped by category, each row with a glyph, name, craft time in mono and an availability dot (`success` craftable, `text-muted` missing ingredients).
- **Centre: recipe detail.**
  - The output item with its quantity.
  - An ingredients list where each line reads "Metallschrott 4 / 6" in mono: `success` if enough, `danger` if not, plus the missing count.
  - The required tool and workbench level.
  - A quantity stepper and the primary "Herstellen · 45 s".
- **Right: queue.** Up to 3 jobs, each with a progress bar, remaining time in mono and a cancel "×".

**States.**

- No recipes unlocked: "Noch keine Baupläne. Baupläne findest du bei Händlern am Hafen."
- Missing ingredients: the primary is disabled with "Es fehlen 2 Zutaten".
- Queue full: "Warteschlange voll (3/3)".
- Crafting: progress shown.
- Done: the item gets "Abholen" and a `success` notification.
- Loading and error states.

**Interactions.**

| Input | Result |
|---|---|
| Select a recipe | Shows its detail. |
| "Herstellen" | `craft:start {recipe, qty}`. |
| Queue "×" | Confirm, then `craft:cancel` (ingredients returned). |

### 10.25 Invoice

**Layout.**

- **Two modes.**
  - Create (business side): an input dialog variant 52rem with Empfänger (the nearest players as a select with ID), Betrag, Grund and Firma (from the job).
  - Receive: a centred 48rem document card in `bg-surface` (opaque, paper-like but graphite).
- **Receive card content.**
  - Header: firm name and a mono invoice number ("RE-2026-00417").
  - Date and due date.
  - Line items, total in `--fh-text-3xl` mono.
  - Status pill: Offen (`warning`), Bezahlt (`success`), Überfällig (`danger`).
  - Actions: "Bezahlen" (primary) and "Später" (secondary).
- **List view** (opened via the radial menu → Rechnungen): tabs Offen / Bezahlt, with rows.

**States.**

- Empty list: "Keine offenen Rechnungen."
- Overdue: the danger pill reads "seit 3 Tagen überfällig · +10 % Mahngebühr".
- Pay error: "Nicht genug Guthaben auf dem Girokonto".
- Paying: busy.
- Paid: the stamp "BEZAHLT" in `success` outline, rotated 0°. Tactical means no skew.

**Interactions.**

| Input | Result |
|---|---|
| "Bezahlen" | `invoice:pay {id}` → notification. |
| Esc | Closes and keeps the invoice open. |

### 10.26 ID card

**Layout.**

- Shown to the target player at the bottom-left above the minimap, or to oneself centred. It is 48 × 30rem, `--fh-radius-lg`, an opaque `bg-surface` card.
- A 0.4rem top band in `accent-secondary`, and the issuing authority in small caps: "HAFENSTADT · PERSONALAUSWEIS".
- The photo area (a silhouette stand-in) at the left.
- Fields: Name, Geburtsdatum, Staatsangehörigkeit, Größe, Ausweisnummer in mono ("HK 7Q4 18C 2"), Ausgestellt and Gültig bis.
- A machine-readable zone line in mono `text-muted` at the bottom.
- **Variants.** Führerschein (licence classes as pills A, B, C) and Dienstausweis (job-coloured band).

**States.**

- Shown: auto-hides after 8 s, or with Esc.
- Expired: a `danger` pill "Abgelaufen" beside Gültig bis.
- Fake ID: visually identical. Detection is an RP mechanic, not a UI cue.

**Interaction.** Showing the card: radial → "Ausweis zeigen" → the nearest player sees it (`id:show {target}`).

### 10.27 Police MDT

**Layout.**

- A tablet frame 156 × 88rem in `--fh-material-thick` with `--fh-radius-xl`. The screen inside is `bg-surface` with a 0.3rem `job-police` rail at the top.
- **Header.** Officer name and callsign in mono ("A-12"), status pills (Verfügbar / Im Einsatz / Pause) and the time.
- **Left nav (22rem).** Übersicht, Einsätze, Personen, Fahrzeuge, Akten, Haftbefehle, Bußgeldkatalog, Beamte. Each item has a glyph, an active-item `accent-secondary` rail and count badges in mono.
- **Overview.**
  - Active dispatch calls list: priority pill P1 `danger` / P2 `warning` / P3 `info`, code ("10-31"), location, time since in mono, assigned units.
  - A units table: callsign, name, status and vehicle.
  - Recent BOLOs.
- **Person search.** A search field, then results, then a profile.
  - The profile: photo, name, DOB, licences and flags ("Gesucht" danger pill, "Bewaffnet" warning pill).
  - Vorstrafen: a table of date, charge and sentence in mono.
  - Notizen.
- **Case file editor.** Title, involved persons as chips, charges picked from the Bußgeldkatalog with a fine and jail-time sum in mono, a report textarea and "Akte speichern".

**States.**

- Search empty (no query): "Name, Telefonnummer oder Kennzeichen eingeben."
- No result: "Keine Treffer für „Krüger“."
- Loading: a skeleton for the result list.
- Error: "MDT-Server nicht erreichbar", with a retry.
- Off duty: the whole MDT is locked with "Nur im Dienst verfügbar".
- Unsaved changes: a dot on the tab and a confirm on leave.

**Interactions.**

| Input | Result |
|---|---|
| Click a call | Detail drawer from the right (40rem): "Übernehmen" (attach the unit) and "Wegpunkt setzen". |
| Status pills | `mdt:setStatus`. |
| Esc | Closes the tablet. |

### 10.28 EMS tablet

**Layout.** The same frame as the MDT, with a `job-ems` rail. The nav: Übersicht, Einsätze, Patienten, Behandlungen, Medikamente, Dienstplan.

- **Overview.**
  - Incoming emergency calls with distance and ETA in mono and the patient state "Bewusstlos".
  - A beds-occupancy grid: Krankenhaus Mitte, 12 beds, each a cell that is free, occupied or blocked.
- **Patient sheet.**
  - Vitals as large mono numerals with units: Puls 112 bpm, RR 90/60, SpO₂ 92 %, Temp 36,4 °C, GCS 9. Each vital is coloured against its normal range, with the range in `text-muted`.
  - An injury body map: front and back silhouettes with marked zones; a selected zone is `danger` outline.
  - A treatment log: time in mono, measure, medic.
  - Actions: "Behandlung eintragen" and "Rechnung stellen".

**States.**

- No active calls: "Keine offenen Notrufe. Gute Schicht."
- Patient not found.
- Loading.
- Error.
- Off duty: locked.

**Interactions.**

| Input | Result |
|---|---|
| Accept a call | Sets a waypoint (`ems:accept`). |
| Body zone click | Opens an injury detail popover. |

### 10.29 Boss menu

**Layout.**

- Panel 140 × 80rem with a header rail in the job colour.
- Firm name, the society account balance in `--fh-text-3xl` mono, and the actions Einzahlen and Abheben.
- **Tabs.**
  - Mitarbeiter: a table of name, rank select, status (online dot), hired-date mono and a row menu (Befördern, Degradieren, Entlassen).
  - Ränge & Gehälter: an editable table with salaries in mono and an "Ändern" inline edit.
  - Einstellen: the nearest players list with "Einstellen".
  - Finanzen: a transaction list and a weekly bar chart of income versus spending, with thin bars, `success` and `text-muted`, and mono axis labels.

**States.**

- No employees: "Noch keine Mitarbeiter. Stelle Personen in der Nähe ein."
- Insufficient rank for an action: disabled with "Nur ab Rang Chef".
- Firing: a typed-confirm dialog.
- Loading.
- Error.

**Interactions.**

| Input | Result |
|---|---|
| Rank select | `boss:setGrade`. |
| Withdraw | Input dialog. |

### 10.30 Admin panel

**Layout.** A tablet frame with a `danger` rail. The header warns: "ADMIN-MODUS" pill `danger`, with the admin name.

- **Nav.** Spieler, Fahrzeuge, Reports, Bans, Server, Logs.
- **Players.**
  - A table with ID, name, identifier (mono, truncated), ping, job and flags.
  - A selected-player side panel with actions as grouped buttons:
    - Teleport: Zu Spieler / Spieler holen.
    - Moderation: Freeze, Spectate, Kick, Ban. Kick and Ban are destructive.
    - Utility: Heilen / Wiederbeleben / Inventar ansehen.
- **Reports.** A queue with an age in mono, the reporter and the reason. Statuses: Offen `warning`, In Bearbeitung `info`, Erledigt `success`. Actions: "Übernehmen" and "Schließen".
- **Server.** Uptime, resource count, tick time in mono, and a "Ankündigung senden" input dialog.

**States.**

- Ban dialog: a typed reason (required), a duration segmented control (1 h / 24 h / 7 d / permanent) and a typed-confirm for permanent.
- No reports: "Keine offenen Reports."
- Permission denied: "Keine Berechtigung (benötigt: superadmin)".
- Loading.
- Error.

**Interactions.**

| Input | Result |
|---|---|
| Every action | Logs and returns a toast (`admin:<action>`). |
| F6 (default) | Toggles the panel. |

## 11. Accessibility & Readability over the Game World

- **Contrast.** Every pairing in Section 2 is verified. Text over the game world uses `text-primary` or `text-secondary` on at least `--fh-material-regular`. Text over unknown backgrounds of any length uses `--fh-material-thick`.
- **Colour is never alone.**
  - Status always pairs colour with a glyph or word: the "Gesucht" pill has text, ping has bars.
  - Hunger and thirst rings have distinct glyphs.
  - Health bar and armor bar differ by position and thickness.
- **Minimum sizes.**
  - The smallest text is `--fh-text-2xs` (11px at 1080p, 8.8px at 720p), and it is uppercase labels only.
  - Values are never smaller than `--fh-text-xs`.
  - Pointer targets are at least 3.2rem.
- **Keyboard.**
  - Every screen is operable with the keyboard: Tab order, Enter and Esc as specified.
  - `:focus-visible` uses `--fh-focus-ring`. The cursor appears only when a full-screen menu or dialog has NUI focus (`SetNuiFocus(true, true)`).
- **Settings.** HUD scale override (0.8–1.2 multiplier on the root rule), reduced motion and colour-blind safe mode. In the colour-blind safe mode, `hud-health` becomes `#F2A65A` and `success` becomes `#8DBBCB`; it is a theme override, not new tokens.
- **Safe zone.** All HUD anchors respect GTA's safe-zone setting; the resource multiplies insets by `GetSafeZoneSize()`.

## 12. Do's and Don'ts

**Do**

- Use tabular numerals for every changing value, and mono for identifiers.
- Keep one accent per view; sand marks the one thing to act on.
- Hide HUD elements that carry no information (full stamina, zero stress, zero armor, ammo while unarmed).
- Give every list its loading, empty and error drawing before shipping it.
- Pair full-screen menus with `TriggerScreenblurFadeIn`.

**Don't**

- Rely on `backdrop-filter` for legibility over the game world, or put it on HUD elements at all.
- Use military kitsch: camo, stencil fonts, chevrons, corner brackets, scanlines, glitch, neon glow, red "tactical" tint everywhere.
- Use pure black or pure white surfaces or text.
- Use Apple logos, SF fonts, SF Symbols or any real-world agency crest.
- Use `color-mix()`, `:has()`, container queries or `cq` units in production NUI CSS; the live CEF is Chromium 103.
- Animate with `ease-in`, scale from 0, or count numbers up on the HUD.
- Show a spinner without text for longer than 1 s, or an error without a next step.
