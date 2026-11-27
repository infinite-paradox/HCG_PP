# Website 01 — Personal Portfolio

**Level:**
Beginner

**Technology:**
HTML5 + CSS3. No CSS framework, no JavaScript, no build step.

**Pages:**
1 page — `index.html`

**Design Style:**
"Specimen sheet": a sign schedule for a sign designer. Warm newsprint paper, charcoal plates, one signal vermilion, hairline rules, a monospaced annotation layer, numbered tab plates, an asymmetric hero with a dark destination plate, and a fixed survey rule on wide screens. Influences: Swiss/transit signage, enamel plates, survey drawings.

**Main Practice Areas:**

- **HTML** — semantic document structure; one `h1` with an `h2`/`h3` hierarchy; `header`, `nav`, `main`, `section`, `article`, `figure`/`figcaption`, `dl`/`dt`/`dd`, `ol`/`ul`, `time`, `address`, `footer`; in-page anchor navigation; skip link; `mailto:` / `tel:` links.
- **CSS** — custom properties as design tokens; box model and logical properties; basic Flexbox layout (no Grid); `clamp()` fluid type and spacing; pseudo-elements for the tab markers, nav underline and plate arrow; `:hover`, `:focus-visible`, `:target`; one load sequence of keyframes; `prefers-reduced-motion`.
- **Responsive** — mobile-first, with breakpoints at 480 px, 640 px, 768 px, 1024 px, 1280 px and 1536 px. Navigation wraps rather than hiding behind a menu; the hero plate goes from wide band to tall portrait panel; project rows go from stacked to a four-column schedule line; the survey rule and ghost numerals appear only where there is room.
- **Accessibility** — skip link, landmarks, visible 2 px focus rings (paper-coloured on dark bands), 44 px minimum targets, contrast-checked palette, decorative elements hidden from assistive technology, meaningful `alt` text, reduced-motion support.
- **SEO / metadata** — contextual title and description, canonical placeholder, Open Graph and Twitter/X cards, `theme-color`, SVG favicon.

**Folder Structure:**

```text
website-01-personal-portfolio/
├── index.html
├── style.css
├── README.md
└── assets/
    ├── fig-01-line-d.svg
    └── favicon.svg
```

**Asset Source:**
The shared `../src/` directory is not present in this workspace, so the project carries its own two small SVG graphics (`assets/fig-01-line-d.svg`, `assets/favicon.svg`). If `../src/` is added later, its images, favicon and fonts can replace them through relative paths. Typefaces (Archivo, Space Mono) load from Google Fonts with system fallbacks, so the page still works offline.

**How to Open:**
Open `index.html` in a modern browser.

**Important Static Limitations:**

- No JavaScript anywhere: no menu toggle, no filtering, no form, no scroll-spy navigation.
- Mobile navigation is the same four in-page links wrapped onto two rows — deliberately not a drawer.
- The only interface state is the URL hash (`#work`, `#approach`, `#practice`, `#contact`), styled with `:target`.
- Project rows are descriptive articles; they do not link to case-study pages, because this project is one page by specification.
- The practitioner, projects, address, phone number and email are fictional practice content. `mailto:` and `tel:` simply open the visitor's own mail client or phone app.
- Open Graph and Twitter image URLs are placeholder `mirahalvorsen.example` addresses; nothing is deployed.
