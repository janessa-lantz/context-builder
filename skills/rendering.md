# Rendering

Shared reference for every skill in this folder. A skill's job ends in a file the user can
open, not a prompt to paste elsewhere. This file is the how: it maps the visual identity to a
build tool, names the output format per asset, and defines the QA pass.

## The principle

Each skill reads the [canon](../context/messaging-canon.md) and
[visual-identity](../context/visual-identity.md), asks its job-specific questions, drafts the
content, then **renders that content to a file** in the brand's colors and type. The render
is the deliverable. No external design product is in the loop.

## Visual identity to design tokens

Before building, read [visual-identity.md](../context/visual-identity.md) and pull:

- **colors**: each named hex with its role (primary, dark, light/background, accent, neutrals)
- **typography**: display/heading face, body face, the weights in use
- **style**: the motifs to repeat (a texture bar, an edge treatment, flat color blocks) and the things to avoid
- **usage-notes**: accent restraint, contrast minimums, logo handling

Carry the company's own color names into the build as constants so the code reads in the
brand's language, not invented names.

## Pipelines by format

### Slides and multi-page documents (decks, carousels) → `.pptx`

Build with `pptxgenjs`. It is installed globally; resolve it with `NODE_PATH`:

```bash
NODE_PATH=$(npm root -g) node build-<asset>.js
```

- Decks: `LAYOUT_16x9`.
- Carousels: define a custom layout for the target ratio, e.g. 1080x1350 is `pres.defineLayout({ name:'CAR', width:9, height:11.25 })` then `pres.layout='CAR'` (inches, any scale that holds the ratio).
- Map each brand color to a hex constant at the top of the script.
- One slide per outline row; set `margin:0` on text boxes you align to shapes.
- Repeat the brand motif on every slide (e.g. Common Paper's grain fleck bar along the base of dark slides).
- Put speaker notes in the notes pane with `slide.addNotes(...)` so the deck is one file.

### Single-page print (one-pager) → `.pptx` sized to the page

Use `pptxgenjs` with a page-sized custom layout: US Letter is `defineLayout({name:'LET',width:8.5,height:11})`, A4 is `width:8.27,height:11.69`. One slide, built to the format's section allocation. Export to PDF when LibreOffice is available (below); otherwise the `.pptx` is the print-ready deliverable.

### Web (landing page, animated UI mockup) → `.html`

Write a single self-contained `.html` file: inline `<style>`, brand colors as CSS custom
properties, the brand's fonts via a Google Fonts link or system fallback, no external
dependencies beyond fonts. This renders natively in any browser, so no raster step is needed.
For the animated mockup, respect `prefers-reduced-motion` and keep the file within the size
budget in its reference file.

### Static images (ads, thumbnails, blog heroes) → `.html` at exact pixel dimensions, then `.png`

Write one `.html` file per variant (or a set in one file), with each artboard a `<div>` sized
to the exact pixel dimensions the platform requires (e.g. `width:1080px;height:1080px`). This
gives a pixel-accurate, brand-controlled layout the user can open and see immediately. To
produce the actual `.png`:

- If a headless browser is available (Playwright via the webapp-testing skill, or `chrome --headless --screenshot`), capture each artboard to PNG at its native size.
- If not, the sized `.html` is the reviewable artifact and the user screenshots it; say so in the handoff rather than implying a PNG exists.

## QA (required, every render)

Assume the first render is wrong. Two passes:

**Content.** For `.pptx`, extract text and check order, completeness, and that no banned term
or em/en dash from the canon's lexicon survived:

```bash
python3 -m markitdown <file>.pptx        # or python-pptx to walk shapes
```

For `.html`, grep the file for the same.

**Visual.** Render to images and inspect with fresh eyes (a subagent is best, since you will
see what you expect):

```bash
# pptx → images, when LibreOffice + poppler are present
soffice --headless --convert-to pdf <file>.pptx && pdftoppm -jpeg -r 150 <file>.pdf slide
```

Look for overlaps, text overflow, low contrast (especially light text on fiber/cream), uneven
gaps, and elements under 0.5in from the edge. Fix, then re-verify the affected artboards;
one fix often creates the next problem.

**When no renderer is available** (no LibreOffice, no headless browser), keep layouts
conservative, run the content pass, and state plainly in the handoff that the visual pass was
not run and the draft needs human eyes. That honesty is the point: the artifact is a draft for
review, never a finished asset shipped blind.

## Output location and naming

Write to the deployment's drafts area, named `YYYY-MM-DD-<asset>-<subject>.<ext>`. Hand back
the full path. If the skill also produced a companion (speaker notes, a canon-gap log that
cannot live inside the file), write it beside the artifact with the same slug.
