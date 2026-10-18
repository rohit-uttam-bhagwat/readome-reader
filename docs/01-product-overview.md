# 00 — Product Overview

## 1. Vision

Readome Reader is a **premium, local-first reading app** for Android. It turns the books, PDFs, and documents already on a person's device into a calm, elegant, organized personal library — without accounts, tracking, or cloud dependence. It should feel like a combination of a curated digital library and a distraction-free reading room.

**Design north stars**
- **Editorial calm** — chrome recedes; covers and text lead.
- **Local & private** — the app reads only what the user explicitly imports or points it to. No implied access to all device files.
- **Tactile & warm** — paper metaphor: ivory surfaces, hairline borders, soft shadows, pill controls.
- **Native Android ergonomics** — bottom navigation, 48dp touch targets, light/dark, system insets.

## 2. Target platform

- Android phones, viewport ~**393 × 852 dp** (compact and larger phones supported).
- Implementation: **Kotlin + Jetpack Compose**, Material 3 (Material You) foundations.
- Offline-first; no backend required for v1.

## 3. Primary users & top jobs-to-be-done

| User | Job |
|------|-----|
| The technical reader | "Keep my PDFs, EPUBs, and papers in one tidy place and pick up exactly where I left off." |
| The leisure reader | "Read novels comfortably with my preferred fonts and a sepia/night theme." |
| The organizer | "Group my books into shelves and find anything instantly." |
| The annotator | "Highlight, bookmark, and take notes, then find them all later." |

## 4. Scope — v1 (locked)

v1 is defined by the **9 generated screens**, plus two surfaces required to eliminate dead-end entry points.

### In scope
1. **Library Home** — continue reading, recently added, full library, filter/sort, grid/list, import.
2. **Search & Filters** — live search by title/author/filename, format chips, sort, scope extension to notes.
3. **Import Files** — browse files, add storage folder, discovered-files list, permission explanation, format support.
4. **Book Details** — cover, metadata, progress, Read Now, add-to-shelf, notes, TTS, share, metadata edit, remove.
5. **PDF Reader** — paginated document canvas, page indicator, zoom/fit, search-in-doc, bookmark, thumbnails, quick theme, Zen mode.
6. **EPUB Reader** — reflowable text, chapter nav, TOC, progress, text-selection actions (highlight/note/copy/define/speak), quick theme, Zen mode.
7. **Reader Appearance Settings** — theme, font family, size, weight, line spacing, margins, alignment/hyphenation, page-turn style, brightness; live preview.
8. **Bookmarks & Notes (Notes)** — unified annotations hub: All / Highlights / Notes / Bookmarks, filter by book, export, resume reading.
9. **Shelves** — standard & smart shelves, create/rename/delete, add/remove books, favorites, recently updated.
10. **Settings** *(new, minimal)* — resolves the Settings nav tab: appearance, default reader settings, library/permissions, storage, about/privacy, version. Drive sync shown as optional & unauthorized.
11. **TTS mini-player** *(surface, not a full screen)* — appears above bottom nav when read-aloud is active: title/chapter, play/pause, prev/next, speed; tap to expand controls. Resolves the Speak/TTS entry points.

### Out of scope for v1 (roadmap)
- **Audiobook media files** (mp3/m4b playback) — v1 "listening" = TTS read-aloud only.
- **Full-screen TTS player** with voice picker & sleep timer — v1 ships the mini-player; full player later.
- **Library Organization browse-by views** (Authors / Series / Folders / Duplicates as dedicated screens) — covered partially by Search and Smart Shelves in v1.
- **Extra file formats** beyond PDF/EPUB/TXT (DOCX, MOBI, CBZ, DjVu) — detection/UI deferred.
- **Cloud sync / backup** beyond showing Drive as an unauthorized option.

## 5. Non-goals / principles

- No sign-in or account required to use the app.
- Never imply unrestricted file-system access; every folder/file access is user-granted and explained.
- Destructive actions (remove book, delete shelf, delete annotation) always confirm.
- Don't rely on color alone to convey status; icon-only controls carry accessible labels.

## 6. Success criteria for this phase

- Every interactive element in every screen maps to a defined destination or result — **zero dead ends** (see [Functional Flows](04-functional-flows.md)).
- Terminology, themes, and branding are consistent across all screens (see [Inconsistencies & Resolutions](06-inconsistencies-and-resolutions.md)).
- Every screen traces to at least one user story with acceptance criteria.
