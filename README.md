# Ahan Dhingra — portfolio

Static site. No build step, no dependencies, no framework. Every page is one
self-contained HTML file with its CSS and JS inline.

## Structure

```
site/
├── index.html                    home — sidebar, project grid, about, skills, contact
├── images/                       all photos go here
│   └── robot_summer.JPG          ← add this file
├── projects/
│   ├── project-01.html               Mars Habitat Robot (written)
│   ├── project-short-template.html    ← use this for most projects
│   └── project-template.html          long form, for another flagship
└── README.md
```

## First thing to do

Drop `robot_summer.JPG` into `images/`. Both the home page card and the
project hero point at it. Until it's there you'll see a broken image.

## Design tokens

Every colour lives in the `:root` block at the top of each file's `<style>`.
Change these six and the whole page re-skins:

| Token        | Value     | Used for                        |
|--------------|-----------|---------------------------------|
| `--paper`    | `#e8eae4` | page background                 |
| `--paper-2`  | `#f1f2ec` | empty photo slots, diagram fill |
| `--ink`      | `#14161a` | text + structural black rules   |
| `--ink-soft` | `#5f6560` | secondary text, captions        |
| `--rule`     | `#cbcec6` | hairlines                       |
| `--accent`   | `#a8352a` | section numbers, sheet labels   |

Dark mode values sit in the `[data-theme="dark"]` block right underneath.

Type is **Space Grotesk** (content) + **Space Mono** (labels, nav, numbers),
loaded from Google Fonts. The rule: anything *you* say is Space Grotesk,
anything the *page* says about itself is Space Mono.

## Two page shapes

**Short form** (`project-short-template.html`) — default. Title block, hero,
150–250 words of prose, 2–4 captioned figures, one outcome line. The captions
do the technical explaining. Use this unless a project genuinely has separable
subsystems.

**Long form** (`project-template.html`) — only for flagship builds like the
Mars robot: numbered sections, alternating subsystem blocks, architecture
diagram, stats grid. If you can't fill three subsystems and four real numbers,
use the short form instead — a half-empty long page looks worse than a
complete short one.

Third option: some projects don't need a page at all. Point the card's `href`
straight at the GitHub repo and add `target="_blank"`.

## Adding a project

1. `cp projects/project-short-template.html projects/project-02.html`
2. Fill in everything in `[brackets]` — title, title block, sections.
3. On `index.html`, update the Sheet 02 card: `href`, `<h3>`, `<p>`, and swap
   `[project photo]` for `<img src="images/your-photo.jpg" alt="…">`.
4. Add `lead` to a card's class (`class="card lead rise"`) to make it span two
   columns. Only one card should have it.

Paths inside `projects/` are one level down, so images are `../images/…` and
the home page is `../index.html`.

## Editing the home page

- **Name and bio** — top of the sidebar.
- **Nav** — `<nav class="nav">`; each link's `href` must match a section `id`.
- **Skills** — four `<div>` groups; add or remove freely, the grid reflows.
- **Local time** — `const TZ` at the bottom of the file.
- **Contact** — email in the `mailto:` and the link text, plus the social row.

## The architecture diagram

`projects/project-01.html` has a hand-drawn SVG in the Architecture section.
It uses the CSS variables, so it inverts with dark mode and stays sharp at any
zoom. Boxes are `<rect>`, connections are `<line>` with an arrowhead marker.
Coordinates are on a 900×360 grid — move a box by editing its `x`/`y`, then
move the matching line endpoints.

## Deploying

**Netlify (easiest):** drag the `site` folder onto https://app.netlify.com/drop

**GitHub Pages:** push the contents of `site/` to a repo named
`yourusername.github.io`. Live at `https://yourusername.github.io` in a minute.

**Custom domain:** buy from Namecheap or Cloudflare, then point it at Netlify
or Pages in their dashboard. `ahandhingra.com` or `.xyz` for a few dollars.

## Known placeholders

- `alt="[Project Name] photo"` on the robot images — write real alt text
- Results numbers on project-01 — placement, team count, task count
- Timeline and Role cells in the project-01 title block
- Subsystem photos (Figs. 02–05) and the competition photo (Fig. 07)
- About and Skills copy on `index.html`

## Notes

The theme toggle resets on reload. To persist it, add
`localStorage.setItem('theme', root.dataset.theme)` inside the click handler
and read it back on load — about four lines at the bottom of each file.
