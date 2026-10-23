---
name: deterministic-event-motion
description: "Design seekable, evidence-grounded event and graph animations whose state is reproducible at any requested time."
source: self
risk: safe
---

# Deterministic Event Motion

## When to Use This Skill

Use when animating an EventGraph timeline, focused relationship graph, evidence callout, numerical change, or research explainer. The result should have a stable state at arbitrary playback times so replay, scrubbing, screenshots, and tests agree.

Do not use to justify a second graph renderer, a video transcoding pipeline, or historical database replay the backend cannot support. A static page does not need an animation merely because motion is available.

## Workflow

1. **Inspect before building.** Locate existing timeline selection, graph focus, relation evidence, animation primitives, and as-of APIs. Reuse the project's renderer and data pipeline. Identify how UI filters already hide withdrawn or private sources; preserve those rules.
2. **Separate clocks.** Event time (when something happened), knowledge time (when a source or database knew it), and animation time (seconds into the presentation) are distinct. Name the selected mode. Only label an as-of view if its backend query truly enforces that time dimension.
3. **Define pure visual state.** Express each frame as `frame = renderAt(animationTime, normalizedPublicEvidence, fixedLayout)`. The same inputs must give the same frame: no per-frame network requests, random placements, mutable simulation drift, or wall-clock dependencies. Cache data and anchor coordinates outside rendering.
4. **Create a beat map.** A beat has a start/end second, relevant evidence IDs, active event/entity IDs, emphasized relation, viewport target, and caption. Treat unverified numbers as examples, never as data. Make one salient change at a time.
5. **Preserve spatial continuity.** Keep selected entity positions and neighborhood layout stable across adjacent beats; interpolate camera/focus movement instead of remounting the entire graph. Show only relations supported by the selected public evidence and time mode.
6. **Handle scale and accessibility.** At mobile width, prioritize readable labels and the currently selected relationship. Provide reduced-motion and pause/scrub states; content and evidence navigation must remain usable without motion.
7. **Verify determinism and meaning.** Scrub to the same timestamp twice and compare state; inspect initial, middle, selected transition and final frames; check labels, bounds, evidence IDs, source dates, and whether the animation implies causation that evidence does not establish. Record what was actually rendered and inspected.
8. **Stop at the requested surface.** Implement motion in the existing view, or produce a storyboard if rendering is outside the task. Do not introduce new compositors, frameworks, persistent workers, or background schedules.

## Example

A small **illustrative** state reducer (not an EventGraph API contract):

```ts
type Beat = {
  atSeconds: number;
  focusId: string;
  highlightedRelationId?: string;
};
function stateAt(t: number, beats: readonly Beat[]) {
  const elapsed = Math.max(0, t);
  let current: Beat | undefined;
  for (const beat of beats) {
    if (beat.atSeconds > elapsed) break;
    current = beat;
  }
  return {
    focusId: current?.focusId ?? null,
    highlightedRelationId: current?.highlightedRelationId ?? null
  };
}
// Given identical sorted beats, stateAt(3.5, beats) is always the same.
```

Prepare `beats` from *already filtered, source-linked public evidence*; do not perform visibility, time filtering, or source retrieval inside this visual reducer. For continuous camera motion, interpolate between fixed beat endpoints using a pure easing function. Test with time seek, not only forward playback.

## Limitations

A deterministic visual animation is not a historical facts engine. It does not recover deleted evidence, infer missing valid/known times, claim past graph states, or make claims about source truth. Animation screenshots require a real renderer; descriptions alone are not visual verification.

## Method Provenance

Independently written for interactive event interfaces. Method-level inspiration: [BaoCut motion-graphics](https://github.com/JimLiu/baocut/tree/main/skills/baocut/built-in-skills/motion-graphics) (BaoCut Community License). No BaoCut scaffold, renderer, scripts, or proprietary runtime are included.
