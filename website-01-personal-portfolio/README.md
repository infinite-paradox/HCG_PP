# Noor Haverkamp — Personal Portfolio

## Project Overview

A single-page portfolio for a fictional front-end engineer based in Rotterdam. The site is built as an annotated working drawing: warm paper, hairline rules, monospaced annotations, a drafting-oxide accent, and a sticky section index. It presents an introduction, working principles, an honest skills inventory, four expandable project sheets, and a contact form that validates locally.

This is **website 01** of the 40-website JavaScript practice curriculum. No other project has been started.

## Difficulty

Beginner

## Technology

HTML5 + raw CSS3 + Vanilla JavaScript (native ES modules). No frameworks, libraries, build tools, or CDN CSS.

## Pages and Views

| Page | Purpose |
| --- | --- |
| `index.html` | The complete portfolio: header, hero and identity plate, current-status band, About, Practice, selected Work, Contact form, footer revision block. |

The page uses in-page anchors (`#top`, `#about`, `#practice`, `#work`, `#contact`) rather than separate documents, which matches the beginner one-page requirement.

## Features

- Sticky header with inline navigation on laptop and a disclosure navigation sheet below 64rem.
- Active-section highlighting from a passive scroll check with `aria-current="location"`.
- Light / dark theme with persistence, system-preference fallback, and theme-color metadata updates.
- Project list rendered from a data module, filtered by category (All / Product / Tooling / Experiment) with live result counts and an empty state.
- Single-open project detail accordion with `aria-expanded` / `aria-controls` and safe DOM construction.
- Client-side contact form validation: field-level messages, an error summary that receives focus, live re-validation, a message counter, and a success panel.
- Local time in Rotterdam and a live copyright year.
- CSS-only entrance motion and a breathing availability dot, both disabled by `prefers-reduced-motion`.
- Theme-aware duotone treatment applied to shared-library imagery.
- Purpose-built 1200 × 630 Open Graph / Twitter share card with descriptive alt text.

## JavaScript Practice Areas

- `querySelector` / `querySelectorAll`, `createElement`, `DocumentFragment`, `replaceChildren`
- `dataset`, `classList`, attributes, `textContent`
- Event listeners, event delegation, keyboard events (`Escape`), outside-click handling
- `matchMedia` for breakpoint behavior and system theme preference
- `localStorage` reads/writes inside `try`/`catch` with value validation
- Passive scroll tracking for active-section state
- `Intl.DateTimeFormat` with an explicit time zone
- Data-driven rendering from an exported array of objects
- Form state (attempted, invalid, success), conditional rendering, focus management
- Array methods: `map`, `filter`, `find`, `forEach`; optional chaining and nullish coalescing
- Regular-expression email check, string trimming and length validation

Modules: `scripts/main.js` (entry), `theme.js`, `navigation.js`, `projects.js`, `contact-form.js`, `clock.js`, `data/projects.js`.

## HTML and CSS Practice Areas

- Semantic landmarks (`header`, `nav`, `main`, `section`, `article`, `aside`, `figure`, `footer`), ordered headings, `dl` metadata blocks, `time`
- Accessible nav disclosure, skip link, visible `:focus-visible` rings, `aria-live` result count, `role="alert"` error summary, `role="status"` success panel
- Box model, custom properties, Flexbox header/actions, CSS Grid for the 12-column hero and section shells
- `clamp()` fluid type and spacing, `minmax()`, `aspect-ratio`, `object-fit`, dotted/hairline rules, pseudo-elements, `:is()`-free explicit selectors, `mix-blend-mode` duotone
- Theme tokens via `[data-theme]`, `color-mix()`, `@supports` backdrop-filter fallback
- Responsive restructuring: navigation mode, grid spans, thumbnail proportions, form columns, footer layout, 4K container caps
- CSS keyframes plus reduced-motion support; hover/active feedback on transform and opacity only
- Print stylesheet that removes navigation and interaction chrome

## Data and Persistence

- Project content lives in `scripts/data/projects.js` (titles, categories, years, summaries, briefs, constraints, outcomes, stacks, shared image paths and alt text).
- Theme preference is the only persisted value: `localStorage` key `portfolio.noor.v1.theme`, limited to `"light"` or `"dark"`. Malformed, blocked, or unavailable storage falls back to the system preference for the visit.
- Filter and accordion state are intentionally temporary.
- The contact form stores nothing. It does not send data anywhere.

## Folder Structure

```text
website-01-personal-portfolio/
├── index.html
├── css/
│   ├── variables.css
│   ├── base.css
│   ├── layout.css
│   ├── components.css
│   └── responsive.css
├── scripts/
│   ├── main.js
│   ├── theme.js
│   ├── navigation.js
│   ├── projects.js
│   ├── contact-form.js
│   ├── clock.js
│   └── data/
│       └── projects.js
├── share/
│   └── portfolio-cover.png
└── README.md
```

Shared assets are referenced from the repository-level `src/` folder using relative paths; nothing was copied or modified there.

## How to Run

The page uses native ES modules, so open it through a local static server rather than `file://`.

- VS Code: install **Live Server**, right-click `index.html` → *Open with Live Server*.
- Or from the repository root: `python -m http.server 8000`, then visit `http://localhost:8000/website-01-personal-portfolio/`.

## Limitations

- Fictional person, projects, studio, email domain (`haverkamp.example`), and canonical URL. The OG/Twitter card is a real 1200 × 630 image in `share/`, but its absolute URL points at the fictional domain until the site is hosted there.
- The contact form validates in the browser only. It does not submit, send email, store data, or claim a backend.
- Theme preference is stored in this browser only; it is not synchronized anywhere.
- Project outcome figures are sample portfolio content, not audited client results.
- Filter and accordion state are deliberately view-only: they are not written to the URL, so a filtered list cannot be deep-linked.
- The hero uses a drawn identity plate rather than a portrait because the shared asset library contains abstract renders, not people.
- The display typeface is loaded from Google Fonts; offline use falls back to the system sans-serif stack. The monospace face is the shared variable Roboto Mono TTF (no WOFF2 conversion was added).
- Current status: the repository root is **not** a Git repository in this environment, so no commits were created.

## Git Practice Checkpoints

Suggested meaningful commits for this project (initialise or use an existing repository first; do not create a nested repository):

```text
chore: scaffold website-01 project structure
feat: build portfolio layout and semantic markup
feat: implement navigation, theme, and section state
feat: add responsive styles and accessibility states
feat: implement project filtering and form validation
fix: validate form and storage edge cases
docs: document website-01 implementation
```

A possible branch name: `feat/website-01-personal-portfolio`.
