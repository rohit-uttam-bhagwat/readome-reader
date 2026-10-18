# 05 — Inconsistencies & Resolutions

Audit of the 9 generated Stitch screens (+ the seed `DESIGN.md`). Each finding has a resolution that is already reflected in the other docs. Status: **Resolved** (decided) or **Open** (needs a design change pushed to Stitch / confirmation).

---

### R-01 — Branding split: Readome vs Readova
**Finding:** In-app headers say **"Readome"** (Home, Shelves, "Remove from Readome"); the Stitch project, every screen title, and the design system say **"Readova"**; the repo/request says "Readome Reader".
**Resolution (Resolved):** Canonical name = **Readome**. Rename Stitch project, all screen titles, and the design system from Readova → Readome. All docs use "Readome".
**Design change needed in Stitch:** Yes — retitle project + screens; update any "Readova" text in screen HTML.

---

### R-02 — Reader theme names differ on every screen *(highest impact)*
**Finding:** Three different naming sets for the same feature:
- Seed brief: Day / Night / Sepia / **Console**
- Appearance Settings (S7): Day Ivory / Sepia Archival / Night Charcoal / **OLED Pitch Mint** (4)
- EPUB quick-palette (S6): **Ivory / Sepia / Parchment / Nocturne** (4, different names)
- PDF quick-palette (S5): Day / Sepia / Night (3, **no OLED**)
**Resolution (Resolved):** One canonical set **Day · Sepia · Night · OLED**, used identically in S5, S6, S7. Mapping: Ivory→Day, Parchment→Sepia, Nocturne→Night, Console/Pitch→OLED. Add OLED to the PDF quick-toggle.
**Design change needed in Stitch:** Yes — rename EPUB palette chips; add OLED to PDF toggle.

---

### R-03 — TTS entry points with no player
**Finding:** "TTS Voice" (S4), "Speak"/headphones (S6), mic (S8) imply text-to-speech, but no TTS player/mini-player screen was generated. The seed brief required a full player + mini-player.
**Resolution (Resolved):** v1 = **TTS read-aloud only** via a **mini-player surface (M6)** above the bottom nav (play/pause, prev/next, speed, expand, close). Full-screen player + voice picker + sleep timer = **roadmap (US-K.3)**. No inert "coming soon" controls ship.
**Design change needed in Stitch:** Yes — add a TTS mini-player surface; ensure Speak/TTS actions reference it.

---

### R-04 — File-format coverage mismatch
**Finding:** Import (S3) lists EPUB/PDF/TXT/DOCX/MOBI/CBZ/DjVu (7), but Library (S1) and Search (S2) only filter **PDF/EPUB/TXT** (3).
**Resolution (Resolved):** v1 **supported & filterable formats = PDF, EPUB, TXT**. Remove DOCX/MOBI/CBZ/DjVu from the import "supported" list for v1 (roadmap). Keeps import, library, and search consistent.
**Design change needed in Stitch:** Yes — trim S3 supported-format list to PDF/EPUB/TXT (or clearly mark others "coming soon", but preferred = remove for v1).

---

### R-05 — "Audiobooks" shelf with no audio-file support
**Finding:** Shelves (S9) includes an **Audiobooks** example shelf, but the app has no audiobook/media-file concept (and v1 audio = TTS only).
**Resolution (Resolved):** **Remove** the Audiobooks example shelf from v1. Replace with a reading-oriented starter shelf (e.g., "To Read"). Revisit if audiobook files enter scope (roadmap).
**Design change needed in Stitch:** Yes — replace the Audiobooks shelf card in S9.

---

### R-06 — Header `document_scanner` action has no destination
**Finding:** Library Home (S1) header has a `document_scanner` button; scan-to-import (camera) is not part of any flow and not in v1 scope.
**Resolution (Resolved):** For v1, **route it to Import (S3)** or **remove it**. Recommended: **remove** (no camera-scan in v1); re-add when document scanning is built.
**Design change needed in Stitch:** Yes — remove/retarget the header button in S1.

---

### R-07 — Avatar / `person` icon implies an account
**Finding:** A `person` avatar appears top-right on S1, S4, S8, S9. The app is **local, account-less** — there is no profile/account to open.
**Resolution (Resolved):** Repurpose the avatar as the **Settings (S10)** entry, **or remove it** (Settings is already in the bottom nav). Recommended: **remove** to avoid implying an account; keep Settings reachable via bottom nav.
**Design change needed in Stitch:** Yes — remove the avatar or relabel it as a Settings shortcut across screens.

---

### R-08 — `mic` voice-search icons may be inert
**Finding:** `mic` appears in Search (S2) and Notes (S8). Voice search is P2.
**Resolution (Resolved):** If voice search ships in v1, wire `mic` to platform speech input. If deferred, **remove the mic icon** (no inert control).
**Design change needed in Stitch:** Conditional — remove mic if voice search is deferred.

---

### R-09 — Settings tab dead-ends (no Settings screen)
**Finding:** Every primary screen's bottom nav has a **Settings** tab, but no Settings screen was generated. (The "Reader Appearance Settings" screen is reader styling, not app settings.)
**Resolution (Resolved):** Add a **minimal app Settings screen (S10)** as the tab destination: appearance/theme, default reader settings, library/folder permissions, default sort/layout, storage usage, find duplicates, optional Drive sync (unauthorized), about/privacy/version.
**Design change needed in Stitch:** Yes — generate a Settings screen.

---

### R-10 — Terminology: Collections vs Shelves
**Finding:** S9 mixes "Collection", "Shelf", "Smart Shelf"/"Smart Shelves", and the bottom-nav label is "Collections".
**Resolution (Resolved):** Canonical term = **Shelves**. Rename the bottom-nav tab and screen title "Collections" → "Shelves"; "All Collections" → "All Shelves". Keep "Smart Shelves".
**Design change needed in Stitch:** Yes — rename tab + screen title + segment label.

---

### R-11 — Library/Search count mismatch
**Finding:** Format chips total "All 42" but PDF 18 + EPUB 16 + TXT 5 = **39** (3 books unaccounted — likely a 4th format with no chip).
**Resolution (Resolved):** Counts must reconcile: `All = sum(format chips)`. Since v1 formats = PDF/EPUB/TXT, sample data should total **39** (or add the missing 3 to one of the three formats). Enforce "All = Σ chips" as a data rule.
**Design change needed in Stitch:** Yes — fix sample counts so All = 39.

---

### R-12 — Missing seed-brief screens (Library Organization)
**Finding:** The seed brief listed Library Organization (Authors/Series/Folders/Formats/Duplicates) as a screen; not generated.
**Resolution (Resolved):** **Out of v1 by decision** (scope = generated screens). Partially covered by Search (S2) and Smart Shelves (S9); duplicate detection lives in Settings (S10). Dedicated browse-by views = roadmap. No dead ends result because no v1 element links to it.
**Design change needed in Stitch:** None for v1.

---

## Summary table

| Code | Issue | Resolution | Stitch change |
|------|-------|-----------|---------------|
| R-01 | Readome vs Readova | Use **Readome** | Rename project/screens |
| R-02 | Reader theme names differ | **Day/Sepia/Night/OLED** everywhere | Rename chips, add OLED to PDF |
| R-03 | TTS has no player | Mini-player (M6); full player roadmap | Add mini-player |
| R-04 | Format coverage mismatch | v1 = PDF/EPUB/TXT | Trim import list |
| R-05 | Audiobooks shelf | Remove for v1 | Replace shelf card |
| R-06 | `document_scanner` dead button | Remove (or → Import) | Remove/retarget |
| R-07 | Account avatar in local app | Remove (or → Settings) | Remove/relabel |
| R-08 | `mic` possibly inert | Wire or remove | Conditional |
| R-09 | Settings tab dead-ends | Add minimal Settings (S10) | Generate screen |
| R-10 | Collections vs Shelves | Use **Shelves** | Rename tab/title |
| R-11 | Count mismatch 42≠39 | All = Σ chips | Fix sample counts |
| R-12 | Library Org screen missing | Out of v1 scope | None |

## Status of the Stitch designs

**Decision: the Stitch project is left as-is; these docs are the single source of truth.** The R-01…R-12 resolutions above are authoritative and will be applied directly when the Compose UI is built — not back-ported into Stitch.

Why: an attempt to apply the fixes via the Stitch MCP (`edit_screens`) showed that in this `TEXT_TO_UI_PRO` project the tool acts as an **agentic generator**, not an in-place editor — it left the 10 originals unchanged and generated ~17 additional screens (project grew to 27). There is **no `delete_screen` API** (only `delete_project`), so stray screens can only be pruned in the Stitch UI. We chose not to.

**Implications for implementation:**
- The 10 original Stitch screens still contain the pre-resolution wording (old theme names, Audiobooks shelf, dead `document_scanner`/avatar buttons, `Collections` label, DOCX/MOBI/CBZ in import). **Ignore those**; follow this document.
- The extra auto-generated Stitch screens (Onboarding, Sign In/Sign Up, Analytics, Insights, etc.) are **not part of the v1 spec** and should be disregarded. A few (Settings & Storage, Audio/TTS, Empty Library State, TOC, In-Book Search, Storage Permission) happen to align with features here and may serve as loose visual reference only.
- Treat all Stitch output as **visual reference**, never as the behavioral/scope contract. This document is the contract.
