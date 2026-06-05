# Website Sync — The Demon Core

> **Canonical rules live in the Standard:** `MyWebssite/docs/standard/` (formatting, figure directives, cross-ref conventions, heading hierarchy). This file records only the **project-specific content contract** the website's importer relies on. Where this file and the Standard disagree, the Standard wins.

## The website is the sole renderer

The site `other.fubsypoly.com` renders this project's content via the shared `packages/ui` design system (repo `tjscientist/fubsypoly`, previously `jeff-web`). It reads a read-only snapshot of the source files below — it never consumes the local `_build/build_single_html.py` HTML output. **The `_build/build_single_html.py` builder is deprecated legacy** — retained for provenance, not maintained. Author clean Markdown; the website renders it.

This project's repo is `tjscientist-labs/otherstuff-demon-core` (private, transferred from the earlier `tjscientist/` namespace).

## What syncs

The `apps/other/sync-other.ts` importer pulls a read-only snapshot of:

- `02-inputs/deep_dive/*.md` — published as the page body (one page per `vol*.md`, or merged into a single page; the site decides)
- `02-inputs/deep_dive/figs/**` — images referenced from the Markdown
- `03-outputs/figs/**` — publishable build photos, schematics, rendered exports

The following are **NOT** synced:

- Anything outside `02-inputs/deep_dive/` and `03-outputs/figs/`
- Raw CAD files (`03-outputs/manufacturing/`) — too large; only renders/photos publish
- `01-about-me/`, `04-templates/`, `05-resources/`
- Anything matched by `.gitignore`

## Hard dependencies (don't refactor without coordinating)

- **`<!-- FIGURE: filename :: caption :: credit -->`** directive — the importer parses this exactly. Format must match the OtherStuff / Electronics convention.
- **`vol_NN_*.md` / `volN.md` filename convention** — the importer uses the leading digit to order pages.
- **Figure paths must be relative** to the `.md` file (e.g. `figs/agnew_with_box.jpg`).

Everything else — heading style, prose cross-refs ("Vol 1 §3.2"), table style, link style — can be refactored freely.

## Publishability notes

- **History content (vol1)** is original analysis built from public sources — all citations point to Wikipedia, the Atomic Heritage Foundation, *Nuclear Secrecy* (Alex Wellerstein), and the *Twilight Time* memoir. Publishable.
- **Replica build content (vol2)** is original how-to text. Embedded 3D-print files (Printables IDs **451707** by FuzzyRaptor and **1390266** by blackrat) are linked, not redistributed — the site links to Printables for downloads. Publishable.
- **Historical photographs** require care: most Manhattan-Project-era images are in the U.S. public domain (federal employee, pre-1989 publication) but each must be verified individually before site publication. Photo Helper's Wikimedia Commons path will return CC/PD-licensed images with attribution captured in `creditLine`. Use those preferentially.

## Third-party design note

The original plutonium box design is Philip Morrison's, machined by Ralph Sparks. The reproduction technique documented in vol2 is informed by Adam Savage's 2024 *Tested* "Builds a Demon Core" video and the FuzzyRaptor + blackrat Printables models. Jeff's narration, build log, photographs, and modifications are publishable; upstream STL files and Tested-original footage are not — link to them at the source.
