# Readome Reader — Product & Design Documentation

> **Written for:** the engineers and designers who will build Readome Reader (Android, Kotlin + Jetpack Compose).
> **Status:** Pre-code alignment. This set defines the agreed scope, stories, and flows. No code is written until these are signed off.

Readome Reader is a **local-first, privacy-focused Android e-book & document reader** — import, organize, read, annotate, and manage books and documents stored on the device. Editorial aesthetic (warm ivory surfaces, deep forest-green accent), distraction-free reading, familiar Android navigation.

## How this documentation is organized

| # | Document | Purpose |
|---|----------|---------|
| 00 | [Product Overview](01-product-overview.md) | Vision, scope, canonical decisions, what's in/out of v1 |
| 01 | [Information Architecture](02-information-architecture.md) | Screen inventory, navigation model, global components |
| 02 | [User Stories](03-user-stories.md) | Epics → stories → acceptance criteria |
| 03 | [Functional Flows](04-functional-flows.md) | Per-screen behaviour + the full navigation graph (every actionable element has a destination) |
| 04 | [Design System](05-design-system.md) | Colors, typography, spacing, themes, reusable components |
| 05 | [Inconsistencies & Resolutions](06-inconsistencies-and-resolutions.md) | Audit of the Stitch designs + every correction applied here |

## Source of truth

The **9 generated Stitch screens** are the design source of truth (not the original seed brief). This documentation reconciles them into one coherent, buildable specification.

Stitch project: `Readova Design System` (`projects/4049167456778891781`) — to be renamed to **Readome**. Screens: Library Home, Search & Filters, Import Files, Book Details, PDF Reader, EPUB Reader, Reader Appearance Settings, Bookmarks & Notes, Shelves (Collections).

## Canonical decisions (locked)

| Decision | Resolution |
|----------|------------|
| App name | **Readome** (one name everywhere; "Readova" retired) |
| Grouping concept | **Shelves** (tab = "Shelves"; "Smart Shelves" for rule-based) |
| Audio / listening | **TTS read-aloud only** in v1 (system TTS); mini-player surface; audiobook files deferred |
| v1 screen scope | The 9 generated screens + 1 minimal **Settings** screen + a **TTS mini-player** surface (both required to remove dead-end entry points) |
| Reader themes | **Day · Sepia · Night · OLED** (unified set, same everywhere) |
| v1 file formats | **PDF · EPUB · TXT** (filterable). Other formats = roadmap |

See [Inconsistencies & Resolutions](06-inconsistencies-and-resolutions.md) for the reasoning behind each.
