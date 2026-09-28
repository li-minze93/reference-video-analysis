# Motion system

Read this reference before producing `motion-cards.json`. Analyze behavior as a state sequence, not as a list of CSS properties.

## Motion grammar

For each repeated or potentially reusable behavior, describe:

1. initial state: position, scale, opacity, crop, emphasis, and visible layers;
2. entry: direction, distance, duration, easing character, and stagger rule;
3. settled state: what is readable and what remains active;
4. change: trigger, affected element, and whether surrounding elements yield;
5. exit or loop: removal, replacement, fade, cut, or continuous cycle;
6. hierarchy: the one primary focus and the layers that support it.

Prefer descriptive names such as `stagger-step-row`, `center-bright-conveyor`, or `white-fade-transition`. Do not use the source creator, product, or video title in a reusable card ID. One card represents one behavior family; a different item count or text payload is normally a parameter, not a new card.

## Parameter extraction

Record measured or approximate values only when they help implementation:

- `enterDurationSec`;
- `staggerSec`;
- `fromY` or other displacement;
- loop speed or direction;
- focus scale or brightness;
- transition duration;
- canvas-relative positions and safe areas.

If the source is too compressed or the frame rate is unknown, use a range or qualitative value. Do not manufacture sub-frame precision.

## Card boundary test

Propose a candidate card when the behavior has at least two of these properties:

- it repeats or is clearly parameterizable;
- it has a coherent visual purpose;
- its source-specific text and media can be replaced;
- its timing can be driven by a semantic event or an explicit clock;
- it can be previewed independently.

Keep a one-off composition in the analysis as a shot-level pattern rather than forcing it into the library.

## Handoff to video-refcraft

The candidate card should tell `video-refcraft` what to inspect and implement, not claim implementation already exists. Include the likely component name, inputs, motion contract, adaptation notes, and evidence range. Let `video-refcraft` apply its own naming rules, card schema, preview requirement, audio rules, and library registration rules.
