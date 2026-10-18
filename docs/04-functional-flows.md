# 03 — Functional Flows

This document maps **every actionable element** on every screen to a destination or result. The goal is **zero dead ends**. Anything in the Stitch designs that pointed nowhere is called out here and resolved (cross-referenced to [Inconsistencies & Resolutions](06-inconsistencies-and-resolutions.md), codes `R-xx`).

Legend: **→** navigates/pushes · **⤵** opens modal/sheet · **⟳** in-place state change · **⇲** system/OS surface · **ⓘ** informational (no action).

---

## Global navigation graph

```
                         ┌──────────────────────────────────────────────┐
                         │               BOTTOM NAV (4)                  │
                         │  Library · Shelves · Notes · Settings         │
                         └──────────────────────────────────────────────┘
                              │         │         │          │
                              ▼         ▼         ▼          ▼
                            S1        S9        S8         S10
   ┌──────────────────────── S1 Library Home ───────────────────────────┐
   │ search → S2        import → S3        book tap → S4                   │
   │ book ⋮ ⤵ M2        sort ⤵ M1          continue → S5/S6                │
   └─────────────────────────────────────────────────────────────────────┘
          │                      │                        │
          ▼                      ▼                        ▼
   S2 Search ──extend notes──▶ S8     S3 Import ──done──▶ S1(toast)   S4 Book Details
                                                               │ Read Now → S5/S6
                                                               │ Add to Shelf ⤵ (shelf picker)
                                                               │ Notes(N) → S8 (this book)
                                                               │ Speak → M6
                                                               │ View all → S8 (this book)
                                                               │ Remove → M5 → S1
   S5 PDF Reader / S6 EPUB Reader
          │ back → S4 (or S1 if from Continue)
          │ format_size → S7      search → in-doc/in-book overlay
          │ bookmark → ⟳          TOC(S6) ⤵      thumbnails(S5) ⤵
          │ select text(S6) ⤵ M7 → Highlight/Note/Copy/Define/Speak(M6)
          │ Zen → ⟳ hide chrome   quick theme ⟳ (Day/Sepia/Night/OLED)
   S7 Appearance → back to reader (live preview)
   M6 TTS mini-player ──tap──▶ (expanded controls)   persists over S1/S8/S9/S10
```

---

## S1 — Library Home

| Element | Action |
|---------|--------|
| Header: search | → S2 Search |
| Header: `document_scanner` | → S3 Import *(scan-to-import not in v1 — route to Import or remove; see R-06)* |
| Header: `filter_list` | ⤵ Filter/Sort sheet (M1) |
| Header: avatar (`person`) | → S10 Settings *(no accounts in v1 — avatar = Settings entry, or remove; see R-07)* |
| Search bar ("Search books, authors, files") | → S2 Search |
| "Quick Library Import" banner → **Import** | → S3 Import |
| "Offline Library Ready" / `offline_pin` | ⓘ status |
| Continue Reading card | → S5/S6 at saved position |
| "See all (N)" (Continue) | → full Continue-Reading list (library filtered: In progress) |
| Format chips: All / PDF / EPUB / TXT | ⟳ filter library |
| Chips: Recent / Unread | ⟳ filter library |
| "Sort: Recently Opened ▾" | ⤵ Sort sheet (M1) |
| Grid / List toggle | ⟳ change presentation (persists) |
| Book cover card (tap) | → S4 Book Details |
| Book card `more_vert` | ⤵ M2: Book Details & Metadata → S4 · Add to Shelf ⤵ · Share or Export File ⇲ · Delete from Device → M5 · Cancel |
| Bottom nav | Library(self) · Shelves→S9 · Notes→S8 · Settings→S10 |

**States:** empty (illustration + Import CTA → S3) · loading (skeleton cards) · populated.

---

## S2 — Search & Filters

| Element | Action |
|---------|--------|
| Back `arrow_back` | → S1 |
| Search field (type) | ⟳ live results (title/author/filename) |
| Clear `close` | ⟳ clear query |
| `mic` voice | ⇲ speech input *(P2; if deferred, remove icon — R-08)* |
| Recent chips (Kafka, …) | ⟳ rerun search |
| Recent "Clear" | ⟳ clear recents |
| Format chips: All / PDF / EPUB / TXT | ⟳ filter results |
| Attribute chips: Has Notes / Favorites | ⟳ filter results |
| Sort "Relevance ▾" | ⤵ sort menu (Relevance, Recently Read, Title A-Z, Author, File Size) |
| Result row (tap) | → S4 Book Details |
| Result `more_vert` | ⤵ M2 overflow |
| "Extend search to Bookmarks & Notes (N) → View" | → S8 pre-filtered to query |
| Header `more_vert` | ⤵ clear filters / search settings |

**States:** results · no-match empty state (adjust filters / import).

---

## S3 — Import Files

| Element | Action |
|---------|--------|
| Back `arrow_back` | → S1 (or caller) |
| "Local-First & Private" `shield_person` | ⓘ / ⤵ permission explanation (M4) |
| **Browse Files** `note_add`/`folder_open` | ⇲ Android document picker (SAF) → adds to selected list |
| **Add Storage Folder** `create_new_folder` | ⇲ SAF folder grant → scan for supported files |
| Supported-format indicators (EPUB/PDF/TXT…) | ⓘ *(v1 filterable set = PDF/EPUB/TXT; others roadmap — R-04)* |
| "Discovered in Downloads" list items | ⟳ toggle selection; status badge (New/Added/Unreadable) |
| Unreadable/unsupported item | ⓘ error state, not selectable |
| Select All | ⟳ select all discovered |
| Auto-generate cover thumbnails | ⟳ toggle |
| Scan sub-directories recursively | ⟳ toggle |
| **Import N Selected Books** `cloud_download` | ⟳ import → toast (M8) → S1 (Recently Added) |
| Cancel | → S1 |

---

## S4 — Book Details

| Element | Action |
|---------|--------|
| Back `arrow_back` | → caller (S1/S2/S9) |
| Header `more_vert` | ⤵ overflow (file operations) |
| Avatar (`person`) | → S10 Settings *(R-07)* |
| **Read Now (Continue Ch. N)** | → S5/S6 at saved position |
| **Add to Shelf** `create_new_folder` | ⤵ shelf picker (add/remove this book) |
| **Notes (N)** `sticky_note_2` | → S8 filtered to this book |
| **Speak (TTS)** `headphones` | → M6 TTS mini-player (starts read-aloud) |
| **Share** | ⇲ Android share sheet |
| Recent Annotations card (tap) | → reader at that position |
| "View all (N)" | → S8 filtered to this book |
| Edit Book Metadata `edit_note` | ⤵ metadata editor (title/author/cover) |
| Re-scan File `sync` | ⟳ re-read file metadata |
| **Remove from Readome** `delete_outline` | ⤵ M5 confirm → removes → S1 |

---

## S5 — PDF Reader

| Element | Action |
|---------|--------|
| Back `arrow_back` | → S4 (or S1 if from Continue) |
| Title | ⓘ |
| `format_size` | ⤵ S7 Appearance Settings |
| `search` | ⤵ in-document search (match nav) |
| `bookmark` | ⟳ toggle bookmark on current page |
| `more_vert` | ⤵ reader overflow (share, go-to, details) |
| Page indicator "X of Y" | ⤵ page-jump input |
| Zoom `remove` / `add`, `fit_screen` | ⟳ zoom / fit (pinch supported) |
| Thumbnails `grid_view` | ⤵ page-thumbnail drawer |
| Annotate `edit`/`brush`/`sticky_note_2` | ⟳ PDF annotation tools |
| Quick theme: Day / Sepia / Night / **OLED** | ⟳ apply reader theme *(add OLED to match set — R-02)* |
| **Zen** `visibility_off` | ⟳ hide all chrome (tap to restore) |
| Tap page center | ⟳ toggle chrome |

---

## S6 — EPUB Reader

| Element | Action |
|---------|--------|
| Back `arrow_back` | → S4 (or S1 if from Continue) |
| `format_size` / `text_fields` | ⤵ S7 Appearance Settings |
| `more_vert` | ⤵ reader overflow |
| TOC `format_list_bulleted` | ⤵ table of contents → jump to chapter |
| `bookmark` | ⟳ toggle bookmark at location |
| `search` | ⤵ in-book search |
| Chapter nav: Ch. I ⟵ / ⟶ Ch. III (`skip_previous`/`skip_next`) | ⟳ prev/next chapter |
| A- / A+ | ⟳ decrease/increase font size |
| Quick theme: Ivory/Sepia/Parchment/Nocturne → **Day/Sepia/Night/OLED** | ⟳ apply theme *(rename to canonical set — R-02)* |
| **Long-press text** → M7 | ⤵ Highlight · Note · Copy · Define · **Speak**→M6 |
| Tap center | ⟳ toggle chrome / Zen |
| Progress indicator | ⓘ |

---

## S7 — Reader Appearance Settings

| Element | Action |
|---------|--------|
| Back `arrow_back` / **Done Styling** | → back to reader (changes already applied via live preview) |
| Restore Defaults `restart_alt` | ⟳ reset to defaults |
| Scope: **EPUB & Books** / **PDF Documents** | ⟳ switch which target the settings apply to |
| Theme: **Day Ivory · Sepia Archival · Night Charcoal · OLED Pitch Mint** | ⟳ select theme (canonical set) |
| Typeface: Literata / Roboto / Lora / OpenDyslexic | ⟳ select font |
| Size slider | ⟳ font size |
| Weight: Regular / Medium / Bold | ⟳ font weight |
| Line spacing: Compact / Normal / Generous | ⟳ |
| Margins: Narrow / Standard / Wide | ⟳ |
| Alignment: justify / left · Hyphenation | ⟳ |
| Page-turn: Page Curl / Slide / Continuous | ⟳ |
| Brightness (`brightness_low`↔`brightness_high`) | ⟳ in-reader brightness |
| Live preview | ⓘ reflects all changes |

---

## S8 — Bookmarks & Notes (Notes hub)

| Element | Action |
|---------|--------|
| Header search | ⟳ search annotations |
| `tune` filter | ⤵ filter options |
| `more_vert` | ⤵ hub overflow (export all, select) |
| Avatar (`person`) | → S10 Settings *(R-07)* |
| Tabs: All (N) / Highlights (N) / Notes (N) / Bookmarks (N) | ⟳ switch segment |
| "Select" `select_all` | ⟳ multi-select mode |
| `mic` | ⇲ voice search *(P2; else remove — R-08)* |
| "Recent ▾" `swap_vert` | ⤵ sort |
| "All Books ▾" `auto_stories` | ⤵ filter by book |
| Annotation card (tap) | → reader at source position |
| Card: "Jump to page" `menu_book` | → reader at position |
| Card: copy `content_copy` | ⟳ copy quote |
| Card: share | ⇲ share sheet |
| Card: bookmark_add / delete | ⟳ / ⤵ M5 confirm |
| **Resume Reading** `play_arrow` | → most recent reading position |
| **Export (N)** `arrow_forward` | ⇲ export selected/all (text/markdown) |
| **New Note** `draw` | ⤵ create note (optionally attached to a book) |
| Bottom nav | Notes(self) + others |

**States:** populated · per-tab empty states ("Create your first bookmark/note").

---

## S9 — Shelves

| Element | Action |
|---------|--------|
| Header title "Shelves" | ⓘ *(was "Collections" — renamed, R-01)* |
| Header search | → S2 (scoped to shelves) |
| Avatar (`person`) | → S10 Settings *(R-07)* |
| **+ New** `add` | ⤵ M3: **Standard** shelf / **Smart Rule** |
| M3 → Standard `folder` / Smart Rule `bolt` | ⟳ choose type |
| M3 → Create Shelf | ⟳ create → appears in list |
| M3 → Cancel | ⟳ dismiss |
| Segments: All Shelves `folder_special` / Favorites `star` / Recently Updated `history` / Smart Shelves `auto_awesome` | ⟳ filter |
| Shelf card (tap) | → Shelf detail (book list + sort + grid/list) |
| Shelf card `more_vert` | ⤵ rename · delete (M5) · add/remove books · favorite |
| Shelf detail → book (tap) | → S4/reader |
| Bottom nav | Shelves(self) + others |

> Note: the "Audiobooks" example shelf from the mockup is **removed** in v1 (R-05). "Create Shelf"/"Smart Shelves" wording is retained since v1 term is Shelves.

---

## S10 — Settings (new minimal screen)

| Element | Action |
|---------|--------|
| Appearance & theme | ⟳ Light / Dark / System |
| Default reader settings | → S7 (defaults mode) |
| Library scanning & folder permissions | → manage granted folders / S3 |
| Default sorting & layout | ⤵ choose defaults |
| Storage usage | ⓘ usage breakdown |
| Find duplicates | → duplicate review (confirm before remove) |
| Google Drive sync | ⤵ **optional, not connected** — requires authorization (R-09) |
| About / Privacy / Version | → info pages |
| Bottom nav | Settings(self) + others |

---

## M6 — TTS mini-player (surface)

| Element | Action |
|---------|--------|
| Appears above bottom nav when read-aloud active | ⓘ |
| Play / Pause | ⟳ |
| Previous / Next (chapter/section) | ⟳ |
| Playback speed | ⤵ speed options |
| Tap mini-player body | ⤵ expanded controls |
| Close | ⟳ stop playback, dismiss |

> Full-screen TTS player (voice selection, sleep timer) is **roadmap** (R-03). v1 ships only the mini-player — no inert controls.

---

## Dead-end audit result

After the resolutions in [06](06-inconsistencies-and-resolutions.md): **every** element above resolves to a navigation target, a modal, an in-place change, a system surface, or is explicitly informational. No element is left pointing at an undefined destination.
