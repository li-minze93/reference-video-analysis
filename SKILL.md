---
name: reference-video-analysis
description: Analyze a local reference video into an evidence-linked package covering structure, semantic timing, visual language, motion behavior, captions, audio relationships, and candidate motion cards. Use when a reference video should be understood for adaptation or handoff to video-refcraft; do not use it to produce the final video or implement Remotion cards.
---

# Reference Video Analysis

Turn one reference video into a local, reviewable analysis package for the user's own production workflow. Preserve the reference's useful production logic while separating it from source-specific content, branding, identity, and unverified assumptions.

This skill is an analysis stage only. It must not:

- modify the user's main Remotion project, `DESIGN.md`, `SHOTBOOK.md`, or central QA records;
- register anything in `video-refcraft/library/`;
- create a final video, generate replacement media, clone a person's voice, or copy source assets without explicit authorization;
- present an inferred sound cue, exact frame boundary, or hidden implementation as observed fact.

## Inputs and output location

Accept a local video path. A supported URL must be downloaded to a project-local working directory before analysis. Also accept an optional analysis brief describing what the user wants to preserve, change, or avoid. Resolve the output directory in this order:

1. an explicit `--out` or user-provided directory;
2. `<video-parent>/reference-analysis/`;
3. a project-local `reference-analysis/` directory.

Do not use the global `video-refcraft` library as the analysis output location. It is reserved for confirmed, implemented cards.

## Required workflow

1. Inspect the media with `ffprobe` or an equivalent local tool. Prefer the system `ffprobe`; if it is unavailable, use a project-local binary such as `bin/ffprobe`, `mediainfo`, or an available media-inspection library. Record duration, dimensions, frame rate, audio streams, and any limitations.
2. Prepare or locate evidence: complete audio listening, transcript, word timestamps when available, representative frames/contact sheet, and shot or scene boundaries. Reuse existing evidence when its source and version are clear.
3. Read [reference-understanding.md](references/reference-understanding.md) before making whole-video claims.
4. Read [semantic-timing.md](references/semantic-timing.md) for spoken or text-led videos. For silent or purely visual videos, use event timing and state changes instead.
5. Read [motion-system.md](references/motion-system.md) before proposing cards.
6. Read [audio-system.md](references/audio-system.md) whenever music, effects, ambience, dialogue, or mixed audio is present.
7. Write the output files described in [output-contract.md](references/output-contract.md). Keep observed evidence, measurement, interpretation, and uncertainty distinguishable.
8. Before handoff, check every candidate card against the existing `video-refcraft` naming rules if that Skill is available. Do not force the candidate package into the registered-card schema: the candidate intentionally contains analysis evidence and may not have an implementation path yet.

## Evidence discipline

Use these labels in notes and JSON:

- `observed`: directly visible or audible in the supplied media;
- `measured`: derived from a timestamp, frame, waveform, or tool output;
- `interpreted`: a reasoned explanation of purpose or relationship;
- `unknown`: not established by the available evidence;
- `unverified`: plausible but awaiting a cleaner source, isolated stem, or human review.

Every important claim should include an evidence reference such as `00:12.40-00:15.10`, frame numbers, a transcript phrase, or a file path. Use ranges and approximate wording when precision is not supported. Do not infer independent SFX from peaks in a mixed track. Do not infer hidden layers from a visual result alone.

## Handoff rule

The next Skill receives:

```text
reference-analysis.json
reference-overview.md
semantic-timeline.json
visual-system.md
motion-system.md
audio-system.md
motion-cards.json
adaptation-plan.md
unknowns.md
```

`motion-cards.json` contains candidate abstractions. `video-refcraft` decides whether a candidate is a reusable card, creates the Remotion implementation, renders its preview, and only then updates its own library. Keep source-specific facts in the analysis package; keep reusable behavior in the candidate card.

## Completion standard

The analysis is complete when another Agent can explain the reference's structure, identify the reason for its major visual changes, locate those changes against speech or events, distinguish reusable mechanisms from source-specific content, and know what remains unknown. A polished prose summary without evidence is not sufficient.
