# 02 — User Stories

Format: **US-<epic>.<n>** — *As a … I want … so that …* followed by acceptance criteria (AC). Stories are grouped by epic; each epic maps to a screen/area. Priority: **P0** (v1 must-have), **P1** (v1 should-have), **P2** (roadmap).

---

## Epic A — Library Home (S1)

**US-A.1 (P0)** — As a reader, I want to see my whole library on one home screen so that I can get to any book quickly.
- AC: Shows app name/header, a search action, and sections: **Continue Reading** (horizontal cards), **Recently Added**, and the **full library**.
- AC: Each book card shows cover, title, author, file-type badge, and reading progress where applicable.
- AC: Layout stays elegant and scannable at 100+ books (no oversized covers / excessive whitespace).

**US-A.2 (P0)** — As a reader, I want to continue exactly where I left off so that I don't lose my place.
- AC: Continue Reading shows the most recent in-progress book with % and page/chapter.
- AC: Tapping it opens the correct reader (PDF→S5, EPUB→S6) at the saved position.

**US-A.3 (P0)** — As a reader, I want to filter and sort my library so that I can narrow it down.
- AC: Format filter chips — **All / PDF / EPUB / TXT** — with live counts; counts reconcile to the "All" total.
- AC: Quick chips for **Recent** and **Unread**.
- AC: Sort bottom sheet (M1): Recently Opened, Recently Added, Title, Author, File Size.

**US-A.4 (P0)** — As a reader, I want a grid/list toggle so that I can choose cover-first or compact browsing.
- AC: `grid_view` / `view_list` toggle switches presentation; choice persists.

**US-A.5 (P0)** — As a reader, I want a prominent Import action so that I can add books.
- AC: Import action is reachable from the top area / prominent control; opens S3.

**US-A.6 (P0)** — As a reader, I want per-book quick actions so that I can manage a book without opening it.
- AC: `more_vert` opens overflow (M2): Book Details & Metadata, Add to Shelf, Share/Export File, Delete from Device (confirmed via M5).

**US-A.7 (P1)** — As a reader, I want clear empty/loading states so that a fresh install isn't confusing.
- AC: Empty library shows an illustration + "Import books" CTA → S3.
- AC: Loading shows skeleton cards, not a blank screen.
- AC: An "Offline Library Ready" status reassures that content is on-device.

---

## Epic B — Search & Filters (S2)

**US-B.1 (P0)** — As a reader, I want results to update as I type so that search feels instant.
- AC: Matches by **title, author, and filename**; results refresh on each keystroke (debounced).

**US-B.2 (P0)** — As a reader, I want recent searches so that I can rerun them.
- AC: Shows recent query chips (e.g., Kafka, Distributed Systems) with a Clear action.

**US-B.3 (P0)** — As a reader, I want to filter and sort results so that I can focus.
- AC: Format chips All / PDF / EPUB / TXT (counts), plus attribute chips **Has Notes**, **Favorites**.
- AC: Sort: Relevance, Recently Read, Title (A–Z), Author, File Size. Clear-filters action available.

**US-B.4 (P1)** — As a reader, I want search to extend into my annotations so that I can find a remembered passage.
- AC: When matches exist in notes/highlights, show "Extend search to Bookmarks & Notes (N)" → opens S8 pre-filtered.

**US-B.5 (P0)** — As a reader, I want a helpful empty state so that a no-match search isn't a dead end.
- AC: No results → message + suggestion to adjust filters or import.

**US-B.6 (P2)** — As a reader, I want voice search so that I can search hands-free.
- AC: `mic` affordance present; wired to platform speech input (P2 — if deferred, the mic icon is removed, not left inert).

---

## Epic C — Import (S3)

**US-C.1 (P0)** — As a reader, I want to browse and pick individual files so that I can import specific books.
- AC: "Browse Files" opens the Android document picker (SAF); selected files appear in a selected-file list.

**US-C.2 (P0)** — As a reader, I want to add a storage folder so that the app can discover books there.
- AC: "Add Storage Folder" grants a scoped folder (SAF tree); app scans it for supported files.

**US-C.3 (P0)** — As a reader, I want to understand what access I'm granting so that I trust the app.
- AC: A **Local-First & Private** explanation states the app reads only user-selected files/folders (M4); no implied full-device access.

**US-C.4 (P0)** — As a reader, I want to see and confirm what will be imported so that I stay in control.
- AC: "Discovered in Downloads" lists found files with name, format badge, size, and status (New / Added / Unreadable).
- AC: Select All / per-item selection; primary action "Import N Selected Books" reflects the count.

**US-C.5 (P0)** — As a reader, I want clear handling of supported formats so that I know what works.
- AC: Supported formats surfaced (v1 filterable: **PDF, EPUB, TXT**). Unsupported/unreadable files show an error state and are not importable.

**US-C.6 (P1)** — As a reader, I want import conveniences so that my library looks good.
- AC: Options: Auto-generate cover thumbnails; Scan sub-directories recursively.
- AC: On completion, a toast confirms "N books imported" and returns to S1 with new books in Recently Added.

---

## Epic D — Book Details (S4)

**US-D.1 (P0)** — As a reader, I want a details screen so that I can see a book's info and decide what to do.
- AC: Large cover; title, author; format badge; file size; reading progress + last-opened date; file location.

**US-D.2 (P0)** — As a reader, I want one clear primary action so that reading is one tap away.
- AC: Prominent **Read Now (Continue Ch. N)** opens the correct reader at the saved position.

**US-D.3 (P0)** — As a reader, I want secondary actions that aren't all equally loud so that the hierarchy is clear.
- AC: Secondary row: **Add to Shelf**, **Notes (N)**, **Speak (TTS)**, **Share**. Metadata edit, Re-scan file, and Remove are lower-priority (grouped/below or in overflow).

**US-D.4 (P0)** — As a reader, I want to see this book's annotations so that I can jump back to them.
- AC: "Recent Annotations" shows cards (quote, page/chapter, timestamp) with "View all (N)" → S8 filtered to this book.

**US-D.5 (P0)** — As a reader, I want to remove a book safely so that I don't delete by accident.
- AC: **Remove from Readome** confirms via M5 and clarifies device-vs-library implications.

**US-D.6 (P1)** — As a reader, I want to edit metadata so that titles/authors are correct.
- AC: "Edit Book Metadata" opens editable title/author/cover; saves locally.

---

## Epic E — Reading: PDF (S5)

**US-E.1 (P0)** — As a reader, I want a distraction-free PDF canvas so that I can focus on the page.
- AC: Realistic page proportions with real sample text/headings; top bar (back, title, search, bookmark, overflow) that can hide.

**US-E.2 (P0)** — As a reader, I want to know and change my place so that I can navigate a long PDF.
- AC: Page indicator "Page X of Y"; page-jump control; next/prev page.

**US-E.3 (P0)** — As a reader, I want zoom and fit so that I can read dense pages.
- AC: Zoom in/out (`remove`/`add`) and **fit-screen**; pinch-zoom supported.

**US-E.4 (P0)** — As a reader, I want to search within the document so that I can find a term.
- AC: `search` opens in-document search with match navigation.

**US-E.5 (P0)** — As a reader, I want thumbnail navigation and bookmarks so that I can move around.
- AC: `grid_view` opens page-thumbnail drawer/sheet; `bookmark` toggles a bookmark on the current page.

**US-E.6 (P1)** — As a reader, I want quick theme + Zen mode so that I can tune the view fast.
- AC: Quick theme toggle offers **Day / Sepia / Night / OLED** (same set as S7); **Zen** hides all chrome until tapped.
- AC: `format_size` opens full appearance settings (S7).

---

## Epic F — Reading: EPUB (S6)

**US-F.1 (P0)** — As a reader, I want reflowable, elegant book text so that long-form reading is comfortable.
- AC: Serif body text, comfortable margins/line length; book title + current chapter shown; reading-progress indicator.

**US-F.2 (P0)** — As a reader, I want minimal chrome that appears on tap so that text is the focus.
- AC: Tapping toggles reader controls; full-screen/Zen reading mode available.

**US-F.3 (P0)** — As a reader, I want a table of contents and chapter navigation so that I can jump around.
- AC: `format_list_bulleted` opens TOC; prev/next chapter controls (Ch. I ↔ Ch. III).

**US-F.4 (P0)** — As a reader, I want text-selection actions so that I can annotate.
- AC: Long-press selection shows M7: **Highlight**, **Note**, **Copy**, **Define**, **Speak**.
- AC: Highlight uses the restrained highlight palette; notes attach to the selection and appear in S8.

**US-F.5 (P0)** — As a reader, I want search-in-book and bookmarks so that I can find and mark passages.
- AC: `search` searches the book; `bookmark` marks the current location.

**US-F.6 (P1)** — As a reader, I want quick appearance control so that I can tune typography.
- AC: `format_size`/`text_fields` opens S7; quick theme + A-/A+ size controls available inline; themes match the unified set.

---

## Epic G — Reader Appearance Settings (S7)

**US-G.1 (P0)** — As a reader, I want to pick a reading theme so that reading suits my environment.
- AC: Theme selector: **Day · Sepia · Night · OLED** (single canonical set used by S5, S6, S7).

**US-G.2 (P0)** — As a reader, I want typography control so that text is comfortable.
- AC: Font family (Literata/Serif, Roboto/Sans, Lora, OpenDyslexic), size slider, weight (Regular/Medium/Bold), line spacing (Compact/Normal/Generous), margins (Narrow/Standard/Wide), alignment (justify/left) & hyphenation.

**US-G.3 (P0)** — As a reader, I want a live preview so that I see changes immediately.
- AC: Sample book text updates in real time as controls change.

**US-G.4 (P1)** — As a reader, I want page-turn style and brightness so that the experience feels right.
- AC: Page-turn: **Page Curl / Slide / Continuous**; in-reader brightness; "Restore Defaults" and "Done Styling".
- AC: Settings can scope to **EPUB & Books** vs **PDF Documents** where relevant.

---

## Epic H — Bookmarks & Notes / Notes hub (S8)

**US-H.1 (P0)** — As a reader, I want all my annotations in one hub so that nothing gets lost.
- AC: Tabs/segments: **All (N) · Highlights (N) · Notes (N) · Bookmarks (N)** with accurate counts.

**US-H.2 (P0)** — As a reader, I want to filter and search annotations so that I can find a passage.
- AC: Search by quote/note text; filter by book (`All Books`); sort (Recent, …).

**US-H.3 (P0)** — As a reader, I want rich annotation cards so that I have context.
- AC: Each card shows selected text, book title, page/chapter, timestamp, and type indicator.
- AC: Card actions: open source location (opens reader at position), edit note, copy quote, share, delete (confirmed).

**US-H.4 (P0)** — As a reader, I want to resume reading from here so that the hub is actionable.
- AC: "Resume Reading" opens the most recent reading position.

**US-H.5 (P1)** — As a reader, I want to export my annotations so that I can use them elsewhere.
- AC: "Export (N)" exports selected/all annotations (e.g., text/markdown) via the Android share sheet.

**US-H.6 (P1)** — As a reader, I want to create a standalone note so that I can jot without a selection.
- AC: "New Note" creates a note (optionally attached to a book).

**US-H.7 (P1)** — As a reader, I want an empty state so that first use guides me.
- AC: No annotations → illustration + "Create your first bookmark or note".

---

## Epic I — Shelves (S9)

**US-I.1 (P0)** — As an organizer, I want shelves with cover mosaics so that groups are recognizable.
- AC: Shelf cards show a small cover mosaic, title, book/doc count, and last-updated time.

**US-I.2 (P0)** — As an organizer, I want to create shelves so that I can group books.
- AC: "New" opens M3: **Standard** shelf or **Smart Rule** (Smart Shelves auto-populate by rule).

**US-I.3 (P0)** — As an organizer, I want to browse and manage shelves so that organizing is easy.
- AC: Segments: **All Collections** → relabeled **All Shelves**, **Favorites**, **Recently Updated**, **Smart Shelves**.
- AC: Per-shelf `more_vert`: rename, delete (confirmed), add/remove books.

**US-I.4 (P0)** — As an organizer, I want a shelf detail view so that I can read from a shelf.
- AC: Opening a shelf lists its books with sort + grid/list toggle; tapping a book → S4/reader.

**US-I.5 (P1)** — As an organizer, I want realistic starter shelves so that the feature is self-explanatory.
- AC: Example shelves: Currently Reading, Software/Technology, Fiction, Research/Papers, To Read. *(No "Audiobooks" shelf in v1 — see resolution R-05.)*

---

## Epic J — Settings (S10, new minimal screen)

**US-J.1 (P0)** — As a user, I want an app Settings screen so that the Settings tab leads somewhere.
- AC: Sections: **Appearance & theme** (Light/Dark/System), **Default reader settings** (links to S7 defaults), **Library scanning & folder permissions** (manage granted folders → S3), **Default sorting & layout**, **Storage usage**, **About / Privacy / App version**.

**US-J.2 (P1)** — As a user, I want duplicate detection so that my library stays clean.
- AC: A "Find duplicates" entry surfaces likely duplicate books for review (confirm before removing).

**US-J.3 (P1)** — As a privacy-minded user, I want cloud sync to be opt-in so that I stay local by default.
- AC: Google Drive sync shown as **optional** and **not connected**; requires explicit authorization before any data leaves the device.

---

## Epic K — Listening / TTS (M6, mini-player)

**US-K.1 (P0)** — As a reader, I want to have a book read aloud so that I can listen when I can't look.
- AC: "Speak" (S6 selection / S4 TTS action) starts system TTS from that point; a **mini-player** appears above the bottom nav.
- AC: Mini-player shows current book/chapter, play/pause, previous/next, and playback speed.

**US-K.2 (P1)** — As a listener, I want playback to continue while I browse so that listening isn't interrupted.
- AC: Mini-player persists across Library/Shelves/Notes; closing it stops playback.

**US-K.3 (P2)** — As a listener, I want a full player with voice selection and a sleep timer.
- AC: Deferred to roadmap; v1 ships mini-player only. *(No inert "coming soon" controls in v1 — see R-03.)*

---

## Traceability

| Screen | Epic |
|--------|------|
| S1 Library Home | A |
| S2 Search & Filters | B |
| S3 Import | C |
| S4 Book Details | D |
| S5 PDF Reader | E |
| S6 EPUB Reader | F |
| S7 Appearance | G |
| S8 Notes | H |
| S9 Shelves | I |
| S10 Settings | J |
| M6 TTS mini-player | K |
