# website-01-personal-portfolio — File-by-File Learning Guide

> **Project:** Mira Halvorsen — Wayfinding & Sign Systems, Rotterdam
> **Stack:** HTML5 + CSS3. No JavaScript, no CSS framework, no build step.
> **Core practice files:** 2 (1 HTML, 1 CSS, 0 JavaScript)

This guide is a study order, not a file inventory. It covers **every** eligible HTML, CSS and JavaScript file in the project, numbered from the first file to open to the last file to finish. Media, artwork and documentation are deliberately excluded.

---

## 1. Project Overview

A single-page portfolio for a fictional environmental graphic designer. The design direction is a **"specimen sheet"**: a sign schedule drawn for a sign designer. Warm newsprint paper, charcoal enamel plates, one signal vermilion, hairline rules, a monospaced annotation layer, numbered tab plates and an asymmetric hero built around a dark destination plate.

| Field | Detail |
|---|---|
| Subject | Portfolio of Mira Halvorsen, wayfinding and sign systems designer |
| Audience | Architects, transit authorities, hospitals, cultural institutions commissioning signage |
| Structure | One page: masthead → hero → 01 Work → 02 Approach → 03 Practice → 04 Contact → colophon |
| Styling model | One hand-authored stylesheet organised into 14 numbered sections |
| Interactivity | None at runtime. The only state is the URL hash (`#work`, `#approach`, `#practice`, `#contact`) |
| External dependency | Google Fonts (Archivo, Space Mono), with system fallbacks |
| Total lines | `index.html` 419 lines · `style.css` 1,355 lines |

**What this project teaches well**

- Semantic single-page document structure: landmarks, one `h1`, a clean `h2`/`h3` hierarchy, `figure`/`figcaption`, `dl`/`dt`/`dd`, `time`, `address`.
- Design tokens as custom properties, and a two-layer palette (paper/ink plus a dark plate layer).
- Flexbox layout without Grid, `clamp()` fluid type and spacing, logical properties (`margin-inline`, `inset-block`).
- Pseudo-elements used as real design objects: tab plates, nav underlines, the destination-plate arrow, the survey rule ticks.
- Responsive design in additive `min-width` bands, with the navigation wrapping instead of hiding behind a menu.
- Accessibility practice: skip link, 44 px targets, visible focus rings with a dark-band override, reduced-motion support, decorative elements hidden from assistive technology.
- Print styles as a first-class part of the stylesheet.

**Why the sequence has only two entries**

The project genuinely contains two eligible source files. Every HTML, CSS and JS file is listed below exactly once — nothing is skipped, nothing is padded with images, `README.md` or SVG artwork.

---

## 2. Actual Project Folder Structure

```text
website-01-personal-portfolio/
├── index.html                                  ← core practice file 01
├── style.css                                   ← core practice file 02
├── website-01-personal-portfolio-LEARNING-GUIDE.md
├── README.md                                   excluded (documentation)
├── share/
│   └── Personal-Portfolio_Cover.png            excluded (generated cover image)
└── assets/
    ├── favicon.svg                             excluded (media)
    └── fig-01-line-d.svg                       excluded (media, referenced by figure)
```

**Eligible inventory:** 1 HTML + 1 CSS + 0 JS = **2 core practice files**.

---

## 3. Website Execution Flow

1. **Request** — the browser loads `index.html`; there is no router, no bundler and no server-side step.
2. **Head parsing** — the document title and description load, then the SVG favicon, then two `preconnect` hints and the Google Fonts stylesheet, then the local `style.css`. Because `style.css` is last, its rules win over the font stylesheet without `!important`.
3. **Document build** — skip link → survey rule → sticky masthead (wordmark + four numbered in-page links) → `main` with five sections (hero, work, approach, practice, contact) → colophon footer.
4. **Style application** — the single stylesheet cascades in its own order: tokens, reset, typography, layout primitives, then one block per page region, then motion, then responsive bands, then reduced-motion and print.
5. **No script execution** — no event listeners, no menu toggle, no scroll spy, no form. Navigation is plain fragment linking; `:target` highlights the section that the hash points at, and only above 768 px.
6. **Responsive resolution** — styles widen progressively at 480, 640, 768, 1024, 1280 and 1536 px, with one `max-width: 639px` correction for the specimen image and the plate switching from a wide band to a portrait panel at 640 px.
7. **Motion** — a single `rise` animation with a `--i` stagger plays on hero elements on load; `breathe` and `marker` loop on the status lamp and plate marker. Smooth scrolling is opt-in via `prefers-reduced-motion: no-preference`, and everything is disabled under `reduce`.
8. **Output** — static HTML and CSS. The page is complete with fonts blocked, and prints as a clean document.

---

## 4. Complete Numbered Learning Sequence

| No. | Learning Phase | Exact File Path | Type | What to Study |
|---|---|---|---|---|
| 01 | Project Entry | `index.html` | HTML | Read the document top to bottom in visitor order: head metadata and its dependencies, then skip link, masthead, hero, the four numbered sections and the colophon. Learn how landmarks, a single `h1`, `h2`/`h3` sections and in-page anchors hold a one-page portfolio together without JavaScript. |
| 02 | Styling and Presentation | `style.css` | CSS | Work through the 14 numbered sections in file order, from tokens to print, tracing every selector back to the class it styles in `index.html`. Learn how one stylesheet carries the whole specimen-sheet identity, including the component states, the responsive bands and the motion preferences. |

**File 01 is where you start. File 02 is the final core source file to study.**

### Why this order

1. **`index.html` first** — it is the only entry point and the only place where the project's content model exists. Every class name in `style.css` is meaningless until you have seen the element it decorates, and the document order (work → approach → practice → contact) is the order the CSS sections follow.
2. **`style.css` second** — the stylesheet is written as a top-down system: tokens define the vocabulary, the reset and typography establish defaults, layout primitives set the page grid, and each later section styles one region of the HTML you just read. Reading it in file order means every rule arrives with its dependencies already explained.

There is no JavaScript phase, because the project contains no `.js` files.

### Study focus for 01 — `index.html`

Read in these groups, in this order:

- **Head (lines 1–41).** Character set and viewport; title and description written as a real pitch; author and `theme-color`; canonical placeholder; SVG favicon; font `preconnect` + Archivo/Space Mono stylesheet; then the local `style.css`. Note that Open Graph and Twitter/X cards reuse the same title, description and a `share/` image URL, and that every decorative requirement is declared here rather than in script.
- **Skip link and survey rule (43–47).** The first focusable element points at `#main`; the coordinate strip is `aria-hidden` decoration that only appears at large sizes.
- **Masthead (46–82).** `header` + wordmark link to `#top` + `nav aria-label="Sections of this page"`. Each of the four links carries a visible two-digit number and a label, which is the navigation concept the CSS later turns into tab plates.
- **Hero (87–140).** An `h1` split into two spans for the two-line setting; eyebrow, statement, bio and availability line; a `mailto:` plate button with an arrow span; a text link; and the destination plate — a link styled as an enamel sign, with top marker, CSS-drawn arrow, label and meta line, plus a `figcaption`-style caption underneath.
- **01 Work (143–241).** `section` + `aria-labelledby`, a `data-ghost="01"` attribute consumed by CSS, an `ol.schedule` of four `li.project` rows using `time datetime`, and a `figure`/`figcaption` specimen whose `img` carries real `width`/`height`, `loading="lazy"` and `decoding="async"`.
- **02 Approach (244–296).** An ordered list of three principles; study how number, heading, paragraph and deliverable line are separated into semantic blocks rather than one blob of text.
- **03 Practice (299–370).** The two-column practice layout: biography, a `ul.capabilities` of six numbered capabilities, and a `dl.facts` built from `div` rows wrapping each `dt`/`dd` pair.
- **04 Contact (373–407).** The dark band: `mailto:` email link, `tel:` phone link, machine-readable `address`, and studio hours.
- **Colophon (411–418).** Coordinates, typeface credit and the line that states the constraint plainly: "HTML5 and CSS3, no JavaScript".

Keep a scratch list of every class you meet, grouped by region. That list is your map for file 02.

### Study focus for 02 — `style.css`

Read the file's own 14 sections in order; do not jump to the responsive block first.

- **`01 Tokens` (lines 24–69).** Three colour groups (paper/ink, plate, accent), two type stacks, a 4 px spacing scale, layout limits (`--container`, `--reading`, `--rail`, `--hairline`), motion durations and easing, and `--focus`. Every later value should be traceable to one of these.
- **`02 Reset and base` (70–185).** `box-sizing`, body type defaults, list and image normalisation, link underline offsets, `::selection`, `:focus-visible` with a plate-coloured override for dark bands, the off-screen skip link that slides in on focus, and `scroll-margin-block` so anchored headings clear the sticky masthead.
- **`03 Typography` (186–247).** Fluid `clamp()` sizes, tight display leading and negative tracking, the container-query (`cqi`) refinement on the name, `text-wrap: balance`/`pretty`, tabular numerals for the annotation layer, and the shared `.subhead` mono style.
- **`04 Layout primitives` (248–282).** `.shell` (`min(100% - gutters, container)`), `.section` padding, hairline top borders and scroll margin, and the `.tab` plate.
- **`05 Masthead and index navigation` (283–410).** Sticky positioning, wrapping flex header, wordmark square drawn with `::before`, the nav underline built from a scaled `::after`, 44 px minimum targets and hover/focus colour changes.
- **`06 Hero and destination plate` (411–678).** The faint 4 rem grid drawn with two gradients and faded by `mask-image`; the pulsing status lamp; the plate button's sliding fill and 1 px active nudge; the destination plate with `clip-path` arrow, hover translation and a divider built from a semi-transparent border.
- **`07 Work schedule and specimen` (679–775).** Schedule rows as flex columns that become a four-part line at 768 px, meta items separated by `::before` bullets, the specimen frame, and the wide-bleed treatment on small screens.
- **`08 Approach` (776–826).** The tinted band, principles as stacked rows, the large vermilion numeral, and the mono deliverable line.
- **`09 Practice` (827–912).** Bio/aside flex split, the capabilities list with hover numerals, and the definition list as label/value rows with hairline separators.
- **`10 Contact` (913–984).** Complete dark-band inversion: background, text, tab, ghost numeral and focus rings all switch layers.
- **`11 Colophon` (985–1014).** The compact three-part footer row.
- **`12 Motion` (1015–1071).** `rise`, `breathe` and `marker` keyframes, the `--i` index assignments, the staggered load sequence, and smooth scrolling gated behind `no-preference`.
- **`13 Responsive` (1072–1304).** Six additive `min-width` bands plus one `max-width` correction: navigation unwraps, the plate becomes a 4:7 portrait, the ghost numeral and `:target` highlight appear, project and principle rows turn horizontal, the survey rail and body offset arrive, and column widths settle.
- **`14 Reduced motion and print` (1305–1355).** The global animation/transition kill switch, arrow transforms removed, the lamp ring hidden, and a print sheet that drops chrome and dark backgrounds.

After each section, return to `index.html` and find the exact elements it targets. That round trip is the actual exercise.

---

## 5. Learning Checkpoints

### Checkpoint 1 — After file 01 (`index.html`)

You should be able to answer without opening the CSS:

- What is the single `h1`, and how do the four sections share one `h2` level with `h3` items inside?
- Which landmarks exist, and what does the skip link skip to?
- Why are the navigation numbers inside the links rather than generated by CSS?
- What does `data-ghost="01"` do, and where is it consumed?
- Why are `width` and `height` set on the specimen image, and what do `loading`/`decoding` change?
- Which elements are `aria-hidden`, and what is the accessibility reason in each case?
- What happens when a visitor clicks "Work" with JavaScript disabled?

### Checkpoint 2 — After file 02, sections 01–04

- Point to the token that controls each of: paper background, accent, container width, reading measure, focus ring.
- Explain how `.shell` centres content and why it uses `min()` rather than a fixed width.
- Explain why `scroll-margin-block` exists on sections and links.
- Describe the difference between the paper focus ring and the contact-band focus ring, and where the override lives.

### Checkpoint 3 — After file 02, sections 05–11

- Rebuild the nav underline and the wordmark square from memory; name every pseudo-element involved.
- Explain how the destination-plate arrow is drawn without an image.
- Explain how the plate button's background slides in, and why `isolation` and `overflow` matter.
- Identify the two places where a hover state also needs a keyboard equivalent, and confirm both exist.
- Explain how `.project__meta` gets its `·` separators without extra markup.

### Checkpoint 4 — After file 02, sections 12–14

- List the animation stagger order in the hero and the custom property that produces it.
- Name every breakpoint and the one thing each band changes first.
- Explain why smooth scrolling is inside `no-preference` rather than being disabled inside `reduce`.
- Explain what the print sheet removes and why the contact section needs its own print override.
- Confirm the page still reads correctly with fonts blocked, motion reduced, and stylesheet printed.

### Checkpoint 5 — Cross-file trace

Pick three components and trace them end to end, markup → tokens → layout → component rules → responsive band → motion → print:

1. `.dest-plate` (hero plate)
2. `.project` (work schedule row)
3. `.contact__email` (dark-band email link)

If you can reproduce each trace without searching the file, the project is learned.

---

## 6. Final Mastery Checklist

**Document structure**

- [ ] I can explain the landmark layout and heading outline of `index.html` from memory.
- [ ] I can list every semantic element used (`header`, `nav`, `main`, `section`, `figure`, `figcaption`, `ol`, `ul`, `dl`, `time`, `address`, `footer`) and justify each one.
- [ ] I understand the metadata block: title, description, canonical, `theme-color`, Open Graph and Twitter cards.
- [ ] I know why this page needs no JavaScript, and what would break if a drawer menu were added.

**Styling system**

- [ ] I can name the token groups and give an example value from each.
- [ ] I understand the two palette layers: paper/ink and plate/plate-ink, and how the contact band inverts them.
- [ ] I can explain the reset choices and why `:focus-visible` is used instead of `:focus`.
- [ ] I can explain the `.shell` width formula and the spacing scale.
- [ ] I can describe how typography stays fluid with `clamp()` and how the name responds to its container with `cqi`.

**Components and state**

- [ ] I can rebuild the tab plate, nav underline, wordmark square and plate arrow using pseudo-elements and `clip-path`.
- [ ] I can explain the plate button's sliding fill, arrow nudge and active state.
- [ ] I know how `:target` highlights the active section and at which width it activates.
- [ ] I can explain every hover state and its keyboard/focus counterpart.
- [ ] I understand the `--i` stagger and the three keyframe animations.

**Responsive and resilience**

- [ ] I can list the breakpoints in order and the main change at each.
- [ ] I can explain why the mobile navigation wraps instead of hiding.
- [ ] I understand the 44 px target rule and where it is enforced.
- [ ] I can explain reduced-motion handling and the print stylesheet.
- [ ] I have opened the page at 360 px, 768 px, 1280 px and in print preview and can predict each layout before looking.

**Completion**

- [ ] I have read both core files end to end, in the numbered order above.
- [ ] I have traced all three cross-file components.
- [ ] I can rebuild the page's structure and visual system from a blank file without copying.
