# 04 — Design System

Tokens extracted from the Stitch **Readome Design System** (formerly "Readova"). These are the canonical values for the Compose/Material 3 theme. Light is the base; dark + reader themes derive from it.

## 1. Brand & aesthetic

- **Editorial minimalism** — chrome recedes; covers and typography lead.
- **Physical paper metaphor** — warm parchment surfaces, hairline borders, sculpted pill controls.
- **Material precision** — Material You ergonomics, 48dp touch targets, soft container transitions (no harsh shadows).

## 2. Color tokens (light / base)

| Role | Token | Hex |
|------|-------|-----|
| Primary | `primary` | `#012d1d` |
| Primary container | `primary-container` | `#1b4332` |
| On-primary | `on-primary` | `#ffffff` |
| On-primary-container | `on-primary-container` | `#86af99` |
| Secondary | `secondary` | `#356855` |
| Secondary container | `secondary-container` | `#b5ebd3` |
| Tertiary (amber ink) | `tertiary` | `#352200` |
| Tertiary container | `tertiary-container` | `#523600` |
| Amber accent | `amber-deep` / `tertiary-fixed-dim` | `#C5832B` / `#fdba45` |
| Sage | `sage-soft` | `#9BB9A0` |
| Error | `error` | `#ba1a1a` |
| Base canvas | `surface` / `surface-ivory` | `#fff9ee` / `#FBF9F5` |
| Card surface | `surface-cream` | `#F4F0E8` |
| Container (low→high) | `surface-container-*` | `#f9f3e9` → `#e8e2d8` |
| On-surface | `on-surface` | `#1d1b15` |
| On-surface-variant | `on-surface-variant` | `#414844` |
| Hairline border | `border-hairline` / `outline-variant` | `#E5DFD5` / `#c1c8c2` |
| Outline | `outline` | `#717973` |

**Dark base:** `night-bg #121413`, `night-surface #1C1E1D`, `night-text #E3E3DC`, `inverse-primary #a5d0b9`.

## 3. Typography

| Role | Font | Notes |
|------|------|-------|
| Headline | **Plus Jakarta Sans** | UI headings, titles |
| Label / UI | **Plus Jakarta Sans** | buttons, chips, nav |
| Body (UI editorial) | **Newsreader** | elegant serif for reading-adjacent copy |
| **Reader fonts** | Literata (serif) · Roboto (sans) · Lora · **OpenDyslexic** | user-selectable in S7 |

## 4. Spacing, radius, elevation

- **Spacing:** 8dp base rhythm + 4dp micro-step. Screen margins ~20dp (mobile), gutters 16dp.
- **Radius:** `ROUND_FULL` — pill/sculpted surfaces; cards use generous rounded corners.
- **Touch targets:** minimum 48×48dp hit area, even for small icons.
- **Elevation:** no harsh shadows. Cards = `surface-cream` + 1px `border-hairline` + diffused warm shadow `rgba(27,67,50,0.04)` blur 12 offset 2. Sheets/floating = `surface-ivory` + `rgba(26,28,26,0.06)` blur 20 offset 4.
- **Chrome concealment:** reader bars fade out over ~150ms in Zen/active reading.

## 5. App themes (UI)

| Theme | Use |
|-------|-----|
| **Light** | Default (ivory base). |
| **Dark** | System dark (night surfaces). |
| **System** | Follow OS setting (set in S10). |

## 6. Reader themes (canonical — unified set)

> One set, used identically by S5 (PDF quick-toggle), S6 (EPUB quick-toggle), and S7 (full settings). This replaces the three conflicting naming sets found in the designs (see R-02).

| Theme | Label in S7 | Background | Text |
|-------|-------------|-----------|------|
| **Day** | Day Ivory | `#FBF9F5` ivory | `#1d1b15` |
| **Sepia** | Sepia Archival | `#F4ECD8` | `#5F4B32` |
| **Night** | Night Charcoal | `#1C1E1D` | `#E3E3DC` |
| **OLED** | OLED Pitch Mint | `#000000` pitch | mint on black |

Old names to retire: *Console* (brief), *Parchment / Nocturne* (EPUB). Map: Ivory→Day, Parchment→Sepia, Nocturne→Night, Console/Pitch→OLED.

## 7. Iconography

Material Symbols (outlined), consistent weight. Icon-only controls must carry content descriptions (accessibility). Key icons in use: `local_library`, `folder_copy`/`bookmarks`, `edit_note`, `settings` (bottom nav); `search`, `tune`, `filter_list`, `add`, `more_vert`, `format_size`, `bookmark`, `grid_view`/`view_list`, `headphones`/`volume_up` (TTS).

## 8. Component inventory

See [Information Architecture §4](02-information-architecture.md). All components share these tokens — spacing, radius, typography, icon style, and color — with no per-screen deviations.

## 9. Accessibility

- Contrast meets WCAG AA for text; never rely on color alone for status (pair with icon/label).
- Scalable text; reading comfortable across the S7 size range.
- 48dp targets; accessible labels for all icon-only actions.
- Respect system font scale and dark-mode preference.
