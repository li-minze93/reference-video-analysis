# Semantic timing

Read this reference for spoken, caption-led, or text-led videos. The central question is not only "at what second?" but also "in response to which word, phrase, visual event, or pause?"

## Timing sources

Prefer evidence in this order:

1. confirmed word-level timestamps from the actual audio;
2. confirmed caption or transcript boundaries aligned to the media;
3. measured frame changes from a contact sheet or frame inspection;
4. approximate manual observation, explicitly marked as approximate.

Never invent word timing from a script when the supplied performance differs. If no final voice exists, describe semantic intent without pretending it is final timing.

## Event record

Every important event should answer:

```text
event id
time range or point
trigger: word, phrase, cue break, pause, action, or clock
visual state before
visual state after
purpose
confidence
evidence
```

For speech, use a semantic anchor where possible:

```json
{
  "trigger": {
    "type": "phrase",
    "text": "按词对齐",
    "rangeSec": [12.4, 12.95],
    "status": "measured"
  }
}
```

Keep absolute time as evidence and semantic trigger as the reusable instruction. A future adaptation can remap the trigger to a new performance while preserving the intended relationship.

## What to record

- entrance: what causes it to appear and how long the entrance takes;
- hold: what remains visible and for which semantic range;
- transformation: what changes in response to the next word or event;
- exit: what causes removal or replacement;
- overlap: which layers coexist and which one has highest visual priority;
- audio relation: whether the motion follows speech, music, SFX, or is unconfirmed.

Use `point` for a discrete event and `range` for a visual that remains present. A page may have an absolute `sourceRange` while its reusable trigger is semantic. These are complementary, not competing, fields.

## Transcription limitations

If the video has multiple speakers, preserve speaker labels when they are known. If captions differ from spoken words, record display text and spoken text separately. If transcription is uncertain, keep the uncertainty local to the affected event instead of lowering confidence for the entire video.

For silent or music-led videos, replace phrase anchors with actions, cuts, musical sections, or clock-based events. Do not force semantic timing onto content that has no spoken semantic anchor.
