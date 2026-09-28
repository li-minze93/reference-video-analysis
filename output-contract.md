# Output contract

Write the following files under the selected output directory. Use UTF-8 JSON and Markdown. Keep paths relative to the analysis package when possible.

```text
reference-analysis.json      package metadata and status
reference-overview.md        whole-piece structure and causal reading
semantic-timeline.json       timed events and semantic triggers
visual-system.md             palette, typography, composition, hierarchy, and media roles
motion-system.md             reusable motion grammar and shot-level behavior
audio-system.md              speech, music, SFX, ambience, and confidence
motion-cards.json            candidate cards for video-refcraft; not registered cards
adaptation-plan.md           what to preserve, replace, transform, or avoid
unknowns.md                  unresolved observations and their impact
```

Validate `reference-analysis.json` and `semantic-timeline.json` against their schemas. Store `motion-cards.json` as an object with `schemaVersion`, `source`, `cards`, and optional `transitions`; validate each candidate entry in `cards` or `transitions` against `motion-card.schema.json`:

- `../schemas/reference-analysis.schema.json`;
- `../schemas/semantic-timeline.schema.json`;
- `../schemas/motion-card.schema.json`.

## Candidate card requirements

Each candidate needs:

- a source-independent proposed ID and human name;
- kind: `page`, `overlay`, `transition`, `caption`, `sound`, or `scene`;
- one or more evidence ranges;
- trigger and source timing when available;
- initial, entry, hold, change, and exit behavior;
- replaceable inputs;
- adaptation notes;
- confidence and unresolved questions.

The candidate may include `audio.cue`, but use `null` and `unverified` unless the sound is independently established. A candidate card is not an implementation and must not contain a false `component` path. `componentSuggestion` is acceptable as a suggestion.

## Handoff checklist

Before handing off:

- the package identifies the exact source file and its media metadata;
- every major claim has an evidence range or is marked unknown;
- absolute times and semantic triggers are not conflated;
- repeated behavior is separated from source-specific content;
- audio claims distinguish mixed-track evidence from isolated cues;
- candidate IDs obey `video-refcraft` naming guidance;
- no candidate is marked adopted, implemented, rendered, or registered;
- the adaptation plan states the required identity, content, voice, music, and asset changes.
