# Homepage Wireframe Patterns

Reference for the artifact-homepage-wireframe skill. The craft this skill applies: how the
wireframe is structured, the section pattern, the copy discipline, the build scaffold, and the
deploy step. Rules and frameworks, not examples to copy.

## What this makes, and what it deliberately is not

A black-and-white, structural wireframe of a company's homepage, built to show information
architecture and messaging, not visual design. The output is a set of linked single-file HTML
pages the user opens in a browser. Internal links work.

This is the one artifact skill that does not apply the visual identity. No brand colors, no
fonts, no imagery. Boxes, labels, hatched image placeholders, system sans-serif, black on
white. Design happens after the IA and copy are approved. If you reach for brand-visual-identity.md,
stop. (Contrast with artifact-landing-page, which is a campaign page rendered in brand colors.
This is the main-site homepage, wireframe-first.)

Every page carries, as the first element in the body, a red banner reading: "The primary
purpose of this exercise is to show information architecture. No copy is final." A small fixed
WIREFRAME tag sits in the top-right.

## The human owns the information architecture

Do not invent the nav. The IA (top-nav items, dropdown children, footer columns) comes from the
human; they will often sketch it. Ask for it, or reflect the live site's IA back as a starting
point and let them restructure. Build the nav and footer from their structure exactly.

Wire every nav and footer target to a real future filename (pricing.html, ai-review.html), even
before that page exists, so links light up as pages get built. Build the homepage first and in
depth; other pages can start as thin skeletons. One file per target keeps the set navigable.

## The hero

- One headline true across all products, framed by audience rather than product ("Legal
  software built for operators", not "The AI contracting platform"). A badge or stamp next to
  the headline is welcome when it earns a credibility beat (for example a "Lawyer Approved"
  seal).
- Reader-voice, customer-centered. Open on the reader's own situation or uncomfortable truth
  ("You didn't sign up to be the lawyer."), not on the company ("We offer..."). The brand
  appears once, as the thing that helps them.
- One positioning subhead beneath, true across all products. If it names a value trio, make the
  trio map onto the product sections that follow.
- One primary CTA. No secondary in the hero.

## The section pattern, one per product or pillar, locked

Each section, in this exact shape:

1. **Eyebrow** the product or pillar name. No "Product 1 of 3" counter.
2. **Headline** a short benefit-outcome line.
3. **One subhead** a single sentence carrying all three of: who it is for, what it does, why it
   is better. Not three separate labeled columns. One subhead.
4. **Three benefits** three bordered cards, each a bold benefit plus one line. No "Benefits"
   label above them. No numbering.
5. **CTA row** one primary button ("Try it free") plus, when useful, a text-only secondary link
   ("Learn more ->"). Some sections drop the secondary.
6. Optional one-line footnote (integrations, license, format).

### Two rules that carry the weight

- **Each section's "why it's better" is that product's own differentiator.** Never reuse one
  differentiator across sections. If product A wins on a lawyer-vetted, market-standard starting
  point and product B wins on speed plus multi-team routing, say each where it belongs. Reusing
  a differentiator is the most common way these sections go wrong.
- **The subhead does the who/what/why work in one sentence.** An earlier draft of this pattern
  used three labeled columns (What it does / Who it's for / Why it's better). The human
  collapsed them to one subhead. Keep them collapsed.

### Body treatment can vary by section type

Three benefit cards is the default. A catalog or library section (a set of templates,
agreements, integrations) reads better as a directory list of the top five or so items (name,
one-line description, View ->) than as benefit cards. Match the body to what the section is.

## Copy discipline: build lean, expect cuts

The human consistently cuts chrome. Default to less. Before showing a section, remove:

- Section counters ("Product 1 of 3").
- Redundant labels over obvious content ("Benefits", "Most-used agreements", "How it works").
- Numbering on lists that do not need order.
- The second sentence of a subhead when the first carries the point.
- A secondary CTA when the primary is enough.

Ground every line in approved messaging. Read the canon; pull verbatim where you can. When the
human points you to a live product page, align that section's headline, subhead, and pillars to
it. Never invent claims, proof, or numbers; an absent claim is a gap to flag, not fill.

### Voice (from the brand-writing-identity lexicon)

- No em dashes anywhere. Commas, colons, periods, parentheses.
- No tricolons for cadence, no mirrored negation, no vague intensifiers.
- No generic SaaS filler (frictionless, seamless, best-in-class, and the rest of the canon's
  banned list).
- Specific over general. Numbers beat adjectives. Named roles over "teams".
- Reader-voice ("you"), present tense, active.

## The build scaffold

One self-contained .html per page. Inline `<style>`. No external dependencies. The wireframe
look:

- System sans-serif, black text on white.
- `1px solid #000` borders on structural blocks; an uppercase 11px label on each.
- Image placeholders: a hatched box (45deg repeating-linear-gradient) labeled IMAGE,
  SCREENSHOT, or HEADSHOT.
- Buttons: bordered; primary is solid black with white text. Text-link CTAs are bold with a ->.
- Top nav: logo box, the human's nav items, dropdowns on hover (pure CSS), Sign in and Sign up
  on the right.
- The red IA-disclaimer banner is the first element in the body; the fixed WIREFRAME tag sits
  top-right.
- Footer mirrors the IA columns.

Keep the shared nav, footer, disclaimer, and `<style>` identical across pages so the set feels
like one site. When you add a page, copy the chrome and change the main content only.

## Working cadence

Build one piece, render it, open it, show it, wait for the reaction. One decision at a time;
present multi-part proposals in small pieces, not a wall. Re-open the file in the browser after
every change (`open <file>` on macOS) so the human is always looking at the current state. Name
judgment calls explicitly and offer the reorder or cut; do not bury them.

## Deploy to S3, the finish

The deliverable ends in a shareable link. Use the user's pretty-page uploader, not its markdown
renderer. The renderer applies a themed template and would destroy the wireframe styling. Upload
the HTML exactly as-is:

Hat-tip to Alex Hillman, whose pretty-page skill powers this deploy step. For guidelines on
setting up the S3 or R2 bucket and deploying to a public URL, see
[alexknowshtml/claude-skills/pretty-page](https://github.com/alexknowshtml/claude-skills/tree/main/pretty-page).

```bash
source ~/.zshrc 2>/dev/null   # loads S3 creds from the shell profile into the env
python3 ~/.claude/skills/pretty-page/upload.py <path-to.html> <project-prefix>/<page>.html
```

- Give the set a stable project key prefix (for example `acme-wireframe/`) and upload each page
  under it, so internal links resolve once the matching files are up.
- The returned URL is public to anyone with the link. Say so in the handoff.
- The HTML on disk is the source of truth; re-uploading the same key overwrites the live page.
