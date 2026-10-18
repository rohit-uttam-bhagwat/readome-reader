# 01 — Information Architecture

## 1. Navigation model

Readome uses a **bottom navigation bar** on the four primary destinations, with secondary screens pushed on top and modal surfaces (bottom sheets / dialogs) for contextual actions.

### Bottom navigation (4 destinations — consistent on every primary screen)

| Tab | Icon | Destination screen |
|-----|------|--------------------|
| **Library** | `local_library` | S1 Library Home |
| **Shelves** | `folder_copy` / `bookmarks` | S9 Shelves |
| **Notes** | `edit_note` | S8 Bookmarks & Notes |
| **Settings** | `settings` | S10 Settings |

> Reader screens (PDF/EPUB) and modal surfaces **hide** the bottom nav — reading is full-bleed.

## 2. Screen inventory

| ID | Screen | Type | Entered from | Bottom nav? |
|----|--------|------|--------------|-------------|
| **S1** | Library Home | Primary | Bottom nav · app launch (default) | Yes |
| **S2** | Search & Filters | Secondary (push) | S1 search; Notes search | No (back) |
| **S3** | Import Files | Secondary / bottom sheet | S1 Import action; S10 Settings | No (back/close) |
| **S4** | Book Details | Secondary (push) | Tap a book from S1/S2/S9 | No (back) |
| **S5** | PDF Reader | Reader (full-screen) | "Read Now" on a PDF (S4/S1 continue) | Hidden |
| **S6** | EPUB Reader | Reader (full-screen) | "Read Now" on an EPUB (S4/S1 continue) | Hidden |
| **S7** | Reader Appearance Settings | Modal panel / bottom sheet | Reader toolbar (`format_size`) in S5/S6 | Hidden |
| **S8** | Bookmarks & Notes | Primary | Bottom nav (Notes) | Yes |
| **S9** | Shelves | Primary | Bottom nav | Yes |
| **S10** | Settings | Primary | Bottom nav | Yes |

### Modal surfaces (not full screens)

| ID | Surface | Trigger |
|----|---------|---------|
| M1 | **Sort bottom sheet** | `tune`/`swap_vert` on S1, S8, S9 |
| M2 | **Book overflow menu** | `more_vert` on a book card (S1/S2) → Details, Add to Shelf, Share/Export, Delete |
| M3 | **Create Shelf sheet** | "New" on S9 → Standard shelf / Smart Rule |
| M4 | **Permission explanation dialog** | First folder/file access in S3 |
| M5 | **Confirmation dialog** | Destructive ops: remove book, delete shelf, delete annotation |
| M6 | **TTS mini-player** | Speak/TTS action in S4/S6; persists above bottom nav |
| M7 | **Text-selection action bar** | Long-press text in S6 → Highlight / Note / Copy / Define / Speak |
| M8 | **Toast / status message** | Import complete, export done, offline-ready, errors |

## 3. Top-level flow (happy path)

```
Launch ──▶ S1 Library Home
             │
   ┌─────────┼───────────────┬──────────────┬────────────────┐
   ▼         ▼               ▼              ▼                ▼
 Search    Import          Tap book       Bottom nav       Continue Reading
 (S2)      (S3)            (S4)           (S9/S8/S10)      (S5 or S6)
                            │
                      "Read Now"
                            │
                    ┌───────┴────────┐
                    ▼                ▼
               PDF (S5)         EPUB (S6)
                    │                │
         ┌──────────┼──────┐   ┌─────┼─────────┬──────────┐
         ▼          ▼      ▼   ▼     ▼         ▼          ▼
     Appearance  Search  Zen  TOC  Select-text Appearance TTS mini-
       (S7)     in-doc  mode       actions(M7)   (S7)    player (M6)
```

## 4. Reusable component library

These components appear across screens and must share spacing, radii, typography, icon style, and color tokens (see [Design System](05-design-system.md)).

| Component | Used in |
|-----------|---------|
| Book cover card (grid) | S1, S2, S4, S9 |
| Compact book list row | S1 (list view), S2, S3 (discovered files) |
| Reading progress bar / ring | S1, S4, readers |
| Search field | S1, S2, S8, S9 |
| Filter chip (format / attribute) | S1, S2, S8 |
| Sort bottom sheet (M1) | S1, S8, S9 |
| Primary / secondary / ghost button | all |
| Bottom navigation bar | S1, S8, S9, S10 |
| Reader toolbar (top + contextual) | S5, S6 |
| Floating / prominent Import action | S1 |
| Annotation card | S8, S4 (related notes) |
| Shelf card (cover mosaic + count) | S9 |
| Empty-state illustration + CTA | S1, S2, S8, S9 |
| Permission dialog (M4) | S3, S10 |
| Confirmation dialog (M5) | M2, S4, S8, S9 |
| Toast / status message (M8) | global |
| TTS mini-player (M6) | global (above bottom nav) |

## 5. Global rules

- **Back behaviour:** secondary screens pop to their entry screen; readers pop to the originating list (S4 or S1). System back respected everywhere.
- **State coverage:** every list screen defines **empty**, **loading**, and **populated** states (see stories).
- **Insets:** respect status bar, gesture nav, and system insets; bottom nav sits above the gesture area.
- **Persistence:** reading position, last theme, sort/view preferences, and shelf membership persist locally across sessions.
