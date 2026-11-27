# Noor Haverkamp Portfolio — File-by-File Learning Guide

**Project:** `website-01-personal-portfolio`
**Scope:** 13 core practice files — 1 HTML, 5 CSS, 7 JavaScript
**Excluded from this sequence:** `share/portfolio-cover.png` (social card image), `README.md` (documentation), and the repository-level shared `src/` folder (favicon and Roboto Mono font referenced from outside this website).

This guide is a study roadmap, not an inventory. Every HTML, CSS and JavaScript file in the project appears exactly once, in a continuous order that follows the real dependency graph: document → styling layers → data → independent behaviour modules → feature modules → the entry orchestrator.

---

## 1. Project Overview

A single-page portfolio for a fictional front-end engineer in Rotterdam. It is built with one HTML document, five hand-written CSS layers and seven native ES modules. There is no framework, bundler, package manager, build step, backend or tracker.

**What the page actually does**

- Presents a hero, a status band, and four anchored sections: About, Practice, Work and Contact.
- Applies a light/dark theme before first paint, persists the choice, and follows the system preference until the visitor overrides it.
- Turns the header navigation into a mobile sheet below 64 rem, returns focus on close, and highlights the section currently being read.
- Renders four project records as expandable articles with a category filter, live result count and empty state.
- Validates a demo contact form locally with inline errors, an error summary, a live character counter and a success panel.
- Shows the current Rotterdam time and year in three places.

**Architectural character**

| Concern | Approach |
| --- | --- |
| Rendering | One static document; project cards built in JS from a data module |
| Theming | `data-theme` on `<html>`, set by an inline head script, then kept in sync by `theme.js` |
| State | `localStorage` for the theme only (`portfolio.noor.v1.theme`); everything else is per-visit |
| Styling | Fixed cascade: variables → base → layout → components → responsive |
| Modules | Each behaviour file exports a single `init*()` function; `main.js` calls them in order |
| Accessibility | Skip link, `aria-expanded`/`aria-current`/`aria-invalid`, real error elements, focus moves |

**External dependencies (not practice files):** `index.html` loads Bricolage Grotesque from Google Fonts and a favicon from `../src/favicon/`; `css/variables.css` declares `@font-face` for Roboto Mono from `../../src/fonts/`. All of these sit outside this website folder and are intentionally excluded from the sequence.

---

## 2. Actual Project Folder Structure

```
website-01-personal-portfolio/
├── index.html                        ← 01
├── css/
│   ├── variables.css                 ← 02
│   ├── base.css                      ← 03
│   ├── layout.css                    ← 04
│   ├── components.css                ← 05
│   └── responsive.css                ← 06
├── scripts/
│   ├── data/
│   │   └── projects.js               ← 07
│   ├── clock.js                      ← 08
│   ├── theme.js                      ← 09
│   ├── navigation.js                 ← 10
│   ├── projects.js                   ← 11
│   ├── contact-form.js               ← 12
│   └── main.js                       ← 13
├── share/portfolio-cover.png          (media — excluded)
└── README.md                          (documentation — excluded)
```

**Counts verified by recursive scan:** 1 HTML + 5 CSS + 7 JS = **13 eligible files**.

---

## 3. Website Execution Flow

### Before first paint

1. The `<head>` runs a small **inline** script that reads `localStorage["portfolio.noor.v1.theme"]`, falls back to `prefers-color-scheme`, sets `data-theme` on `<html>` and updates the `theme-color` meta tag. It is deliberately inline and in `<head>` so the correct theme is painted immediately; any storage error falls back to light.
2. Five stylesheets load in a fixed order — `variables.css → base.css → layout.css → components.css → responsive.css`. Each layer only refines the previous one; nothing is imported inside CSS except the `@font-face` source.
3. The document is a single page: header, hero (`#top`), status band, `#about`, `#practice`, `#work`, `#contact`, footer.

### Module boot

1. One module script, `scripts/main.js`, loads at the end of `<body>`.
2. `main.js` imports the five behaviour modules and registers `start()`. If the document is still loading it waits for `DOMContentLoaded` once; otherwise it runs immediately.
3. `initTheme()` reads the theme already chosen by the inline script, syncs the toggle's `aria-label`/`title` and the `theme-color` meta, wires the toggle, and listens for system-preference changes (ignored once the visitor has stored a choice).
4. `initNavigation()` wires the mobile menu, then measures which section crosses the 40 % viewport reading line to set `aria-current="location"`.
5. `initProjects()` builds every project article from `scripts/data/projects.js`, renders filter chips with counts, and applies the default "All" filter.
6. `initContactForm()` attaches validation, the character counter, the error summary and the success/reset cycle.
7. `initClock()` writes the time and year immediately and refreshes every 30 seconds.

### Behaviour flow

- **Theme:** inline head script → `initTheme` → toggle click → `applyTheme(next, { persist: true })` → `data-theme` + meta + storage.
- **Menu:** toggle → `openMenu()`/`closeMenu()` → `hidden`, `aria-expanded`, `body.menu-open`, document-level Escape and outside-click listeners added/removed together.
- **Work:** data module → `buildProject()` → `applyFilter()` hides non-matching articles, updates `#work-count` and reveals `#projects-empty`; a click on one `Details` button closes the others before opening.
- **Contact:** submit → `validateAll()` → either error summary (focus moved) or success panel; input/blur revalidates only after an attempt or once a field is already invalid.

---

## 4. Complete Numbered Learning Sequence

| No. | Learning Phase | Exact File Path | Type | What to Study |
|---|---|---|---|---|
| 01 | Project Entry | index.html | HTML | Understand the single-page document: the inline pre-paint theme script, the five-stylesheet cascade, header controls (theme toggle, menu, clock), the five sections and their anchors, the Work/filter/empty placeholders, the form and success panel, and the single `scripts/main.js` entry point. |
| 02 | CSS Foundation | css/variables.css | CSS | Understand the "Working Drawings" token system: `@font-face` for Roboto Mono, paper and dark-theme colour pairs, the `clamp()` type scale, spacing, radii, durations, easing, z-index layers and header height. |
| 03 | CSS Foundation | css/base.css | CSS | Understand the reset, document defaults, base typography and heading rhythm, focus-visible treatment, and the utility classes (including the `.reveal` entrance pattern used with `--i`). |
| 04 | CSS Foundation | css/layout.css | CSS | Understand structural composition: the `.shell` container, sticky header geometry, hero grid, section grid with its numbered rail, status band, work and contact grids, and footer layout. |
| 05 | CSS Foundation | css/components.css | CSS | Understand reusable pieces: brand, buttons, theme and menu toggles, nav links, the plate and spec strip, principles, skill groups, project rows and expandable detail panel, filter chips, form fields/errors, success panel and footer revision block. |
| 06 | CSS Foundation | css/responsive.css | CSS | Understand breakpoint-only structural changes: the fixed mobile navigation sheet below 64 rem, the desktop inline nav, collapsible section grids and the fluid behaviour that keeps the page usable from 320 px upward. |
| 07 | Data Layer | scripts/data/projects.js | JavaScript | Understand the data contract: `projectCategories` and four project records with `id`, `category`, `year`, `role`, image path and alt text, summary, brief, constraint, outcome and stack — the source of truth the work section renders. |
| 08 | Independent Module | scripts/clock.js | JavaScript | Understand the smallest module and the project's `init*()` convention: `Intl.DateTimeFormat` pinned to `Europe/Amsterdam`, updating `#local-time`, `#footer-time` (plus `datetime`), `#footer-year`, and the 30-second refresh. |
| 09 | Independent Module | scripts/theme.js | JavaScript | Understand stateful theming: reading the versioned storage key, `applyTheme` updating `data-theme`, the toggle's accessible name and the `theme-color` meta, persistence with failure tolerance, and ignoring system changes after an explicit choice. |
| 10 | Shared Behaviour | scripts/navigation.js | JavaScript | Understand the mobile menu lifecycle (`hidden`, `aria-expanded`, `body.menu-open`, Escape, outside click, focus return), viewport synchronisation via `matchMedia` plus `ResizeObserver` and `requestAnimationFrame` throttling, and the scroll-spy that sets `aria-current`. |
| 11 | Feature Module | scripts/projects.js | JavaScript | Understand data-driven rendering: building articles, media and detail regions with `createElement`, accessible toggles with `aria-controls`, filter chips with counts and `aria-pressed`, single-open accordion logic, live result count and the empty/reset state. |
| 12 | Feature Module | scripts/contact-form.js | JavaScript | Understand form behaviour: per-field rules, `aria-invalid` plus `hidden` error elements, the error summary with focus and jump links, the message counter, conditional revalidation, and the success/reset cycle that restores focus to the first field. |
| 13 | Final Integration | scripts/main.js | JavaScript | Understand the composition root: the five imports, the ordered `start()` calls that define boot sequence, and the `DOMContentLoaded`-or-immediate guard that makes the entry point safe at any load state. |

**Total: 13 numbered entries — matching the 13 eligible source files exactly.**

### Why this order

- **01: the document first.** `index.html` names every section, control and placeholder; reading it first gives each later module a destination to hang on.
- **02 → 06: the styling cascade in load order.** Tokens exist before base rules, base before layout, layout before components, and breakpoints last — the same order the browser applies, so each file's selectors are already familiar when the next one arrives.
- **07: data before behaviour.** `scripts/data/projects.js` has no imports and is consumed directly by the work section; studying it here means the rendering module later has nothing unexplained in it.
- **08 → 09: the two smallest independent modules.** `clock.js` teaches the `init*()` pattern with no state; `theme.js` adds the one piece of persisted state and the pre-paint handshake with `index.html`.
- **10: shared behaviour with lifecycle.** `navigation.js` is where event listeners are added and removed, media queries are watched, and focus is managed — concepts reused later.
- **11 → 12: the two feature modules, in dependency order.** `projects.js` depends on the data file you just read; `contact-form.js` is self-contained but the densest validation and accessibility code, so it comes after the rendering patterns.
- **13: the entry point last, because it is only legible once you know what it starts.** `main.js` contains no logic of its own; it is the file that explains the boot order you have already studied module by module.

---

## 5. Learning Checkpoints

**Checkpoint A — after 01**
Can you name every section id in anchor order, the control ids the JS will look for (`theme-toggle`, `menu-toggle`, `local-time`, `project-list`, `contact-form`, …), and explain why the theme script sits inline in `<head>` rather than in `main.js`?

**Checkpoint B — after 06**
Can you assign five new style rules to the correct CSS file, and say why the desktop navigation needs no `hidden` attribute but the mobile one does? Can you find the token that drives spacing and the one that drives the display heading size?

**Checkpoint C — after 07**
Can you write a fifth project record from memory, matching every field the renderer expects? Which fields are rendered where, and which ones only appear inside the expanded detail panel?

**Checkpoint D — after 10**
Describe the three states of the menu (`hidden`, `aria-expanded`, `body.menu-open`) and explain which listener cleans up what. Explain how the scroll spy decides the "current" section, and why `aria-current` is better than a colour-only highlight.

**Checkpoint E — after 12**
Explain the two conditions that allow a field to be revalidated while typing. Explain why the error summary is `role="alert"` with `tabindex="-1"`, and trace what happens to focus on a failed submit, a successful submit and the reset button.

**Checkpoint F — after 13**
Narrate the full boot sequence in order and predict what would break if `initProjects()` ran before `initNavigation()` or before the DOM was ready.

---

## 6. Final Mastery Checklist

- [ ] I can explain the page as one document plus five stylesheets plus seven modules, in under a minute.
- [ ] I can place any style rule in the correct one of the five CSS layers and justify it.
- [ ] I can explain the pre-paint theme handshake between `index.html` and `theme.js`.
- [ ] I can describe the `init*()` module convention and how `main.js` sequences it.
- [ ] I can add a fifth project to the data file and predict exactly what appears on the page.
- [ ] I can explain every ARIA attribute the page sets (`aria-expanded`, `aria-controls`, `aria-current`, `aria-invalid`, `aria-pressed`, `aria-live`) and which file sets it.
- [ ] I can trace a menu open/close cycle including focus restoration and listener cleanup.
- [ ] I can explain the form's validation, error-summary and success states without opening the file.
- [ ] I can point to every place `localStorage` is read or written, and what happens when it throws.
- [ ] I can rebuild one module from scratch and wire it into `main.js` without touching the others.

If any item fails, return to the numbered entry whose phase it belongs to and re-read only that file — the sequence is ordered so the answer always sits in a file you have already studied.
