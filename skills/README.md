# Skills

On-demand production. A skill generates an asset (a sales deck, a one-pager, a LinkedIn
carousel) from approved context when a human asks for one. Skills are the read side of the
system: [jobs](../builder/jobs/) run on a cadence and write into
[context](../context/); skills run when you need them and read out of it.

> **Status: not battle-tested.** These skills are new and have not been proven across
> repeated real use. Treat every output as a first draft, expect rough edges, and review
> closely before anything ships. Refine the skills as you go.

## The rule

**Skills read context; they never write it.** A skill never edits the canon, the content
index, the visual identity, or an entity. If a skill run reveals a gap (a component with no
canon entry, a missing color value), it surfaces the gap for a human and the
[builder](../builder/) to fix. Generating an asset and updating the source of
truth are different jobs, and keeping them separate is what makes the context trustworthy.

## Anatomy of a skill

Each skill is a folder named `artifact-{asset}` (matching the naming used across client
repos), holding:

- **SKILL.md**: the workflow. It declares which canon components it reads (by ID), reads
  [visual-identity](../context/visual-identity.md) for design facts, and asks the human only
  for the job-specific variables context cannot hold (the deck's purpose, the campaign's
  offer, the post's topic). A skill never asks for positioning, audience, proof, voice, or
  brand colors; context already holds those.
- **A reference file**: the distilled craft the skill applies. Platform specs and dimensions,
  copy density limits, layout patterns, anti-patterns. Facts and frameworks, not examples to
  imitate.

## What the output is

A skill produces a draft asset built entirely from approved messaging and observed visual
identity. It is still a draft: a human reviews it before it ships. Skills remove the
blank-page and the off-brand failure modes, not the human judgment.

## Skills in this folder

| Skill | Generates |
|---|---|
| [artifact-sales-deck](artifact-sales-deck/) | slide-by-slide deck outline, speaker notes, and a design-generation prompt |
| [artifact-one-pager](artifact-one-pager/) | print-ready one-pager spec (product, solution, integration, or vertical format) |
| [artifact-landing-page](artifact-landing-page/) | 7-section campaign page wireframe with copy, plus mockup prompt or deploy-ready HTML |
| [artifact-homepage-wireframe](artifact-homepage-wireframe/) | black-and-white homepage wireframe (plus linked page skeletons) showing information architecture and copy, deployed to S3 as a shareable link |
| [artifact-paid-ad-creative](artifact-paid-ad-creative/) | multi-variant ad set for LinkedIn and Meta, each variant a distinct angle |
| [artifact-linkedin-carousel](artifact-linkedin-carousel/) | carousel copy, PDF generation prompt, and the accompanying post |
| [artifact-blog-featured-image](artifact-blog-featured-image/) | blog hero and social share card concepts, consistent per content category |
| [artifact-youtube-thumbnail](artifact-youtube-thumbnail/) | 3 thumbnail concepts with distinct click-through hypotheses |
| [artifact-animated-ui-mockup](artifact-animated-ui-mockup/) | standalone HTML animation of the product UI for heroes and social |

The reference files distill frameworks and platform specs adapted from Jenna Potter's
[Claude Design Kit for B2B Marketers](https://www.linkedin.com/in/jennapotter), restructured
to read from context instead of running intake.
