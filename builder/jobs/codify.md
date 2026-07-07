# Codify

A job you run to turn corrections into context. When a human takes a generated artifact and
changes it before it ships (rewrites the hero, cuts a claim, renames a term), that correction
is the strongest signal the system receives, and today's runs are the cheapest place to
capture it. This job captures the learning so the same correction never has to be made twice.
Skills stay read-only; codify is how their learnings travel: a skill files what it hit as an
[issue](../issues/), a human corrects the output, and the builder writes the approved
learning into context.

Three principles:

- **Propose, never impose.** Codify drafts updates; a human approves each one before it is
  written. Approved canon and identity entries are marked `source: human`, because their
  authority is the human's correction, not a live surface.
- **One correction, one destination.** Every learning lands in exactly the file the next run
  will read. If no file would have prevented the correction, say so; a one-off preference is
  not a rule.
- **Evidence, not opinion.** Each proposal cites the correction that produced it: the diff,
  the run, or the instruction.

## Inputs

Either or both of:

- **A correction in hand**: a generated artifact plus what actually shipped (a file pair, a
  diff, or the human's verbal corrections).
- **The backlog**: open `correction` and `process` themes in [issues](../issues/), plus
  `missing` themes whose evidence is a skill run.

## Where learnings land

Classify each correction by what would have prevented it, and propose the update there:

| The correction was about | It lands in |
|---|---|
| tone, phrasing, a banned or preferred term | [brand-writing-identity](../../context/brand-writing-identity.md): Voice, Guardrails, or Lexicon |
| the message itself (a claim, a frame, an emphasis) | the [canon](../../context/messaging-canon.md) component, as a `source: human` entry; or an issue, if the correction contradicts currently published copy |
| the craft of one artifact type (layout, structure, section order, emphasis) | that skill's patterns or reference file, or its checklist, in [skills](../../skills%20-%20Work%20in%20Progress/) |
| how the system itself behaved (a rule broken, a spec misread, a parse missed) | one new rule in [AGENTS.md](../../AGENTS.md), or a clarification in the job or spec that was misread |

## The run

1. Gather the inputs: the corrections in front of you, and the open `correction` and
   `process` themes in [issues](../issues/).
2. For each distinct correction, classify it per the table and draft the smallest update
   that would have prevented it. A correction that repeats across artifacts outranks a
   one-off; when unsure whether a correction is a rule or a preference, file it as a
   `correction` theme at `low` confidence and wait for recurrence instead of writing a rule.
3. Present the proposals to the human, one destination at a time: the exact entry, where it
   goes, and the evidence behind it.
4. Write only what is approved. Mark canon and identity entries `source: human` with the
   date. Never overwrite an existing human-authored entry; append, or ask.
5. Mark the consumed themes `actioned` and stamp their `last_run`.

Run it after an artifact ships with human changes, or on a cadence against the backlog, the
way the [analyzer](analyzer.md) runs against new summaries.

## Output

Approved entries in the canon and brand identities, sharpened skill and job specs, and at
most one new AGENTS.md rule per real incident, each traceable to the correction that
produced it.
