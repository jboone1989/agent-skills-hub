---
name: evidence-led-explainer
description: "Turn verified news, research, or event graphs into understandable explainers with synchronized facts, narration, and visuals."
source: self
risk: none
---

# Evidence-Led Explainer

## When to Use This Skill

Use when turning an EventGraph event, Ferro research item, paper, or other evidence-backed topic into a written explainer, storyboard, or video script. Use for explanations that must remain understandable to a newcomer **and** traceable to sources.

Do not use for general film editing, transcription, a promotional video without evidence, or factual investigation when no primary source has been read.

## Workflow

1. **Search before writing.** Inspect the current project's published events, relationships, source links, and existing presentation components. Reuse a factual summary and source list if they already exist. Do not invent an event schema or a second evidence store.
2. **Define the audience's question.** In one sentence, name the question a viewer would actually ask; in a second sentence, name what the viewer should be able to explain afterwards. Start from the question, not a company or project description.
3. **Build a compact claim ledger.** For every claim that could change the viewer's understanding, record: claim ID, wording, event/entity IDs if available, source link, publication/event timestamp, confidence or uncertainty, and permitted public visibility. Separate **reported fact**, **inference**, **example**, and **unknown**. If a source has been withdrawn or cannot be shared publicly, it must not appear in published content.
4. **Choose a concrete explanatory object.** Pick an existing artifact that carries the explanation: a transaction, timeline, relationship network, chart, product screen, or recorded event. Avoid decorative diagrams that add nothing. In EventGraph, a focused event neighborhood plus dated evidence can be the explanatory object; do not default to drawing the entire graph.
5. **Write a beat sheet.** For each beat, give the audience question being answered, the one visible change, the claim IDs, the narration line, and the source shown on screen. Introduce one unfamiliar concept at a time. If a sentence causes no change in understanding or visible state, rewrite or remove it.
6. **Keep one factual source of truth.** Every displayed number, label, time, and spoken claim should map back to the same ledger. Distinguish event occurrence time from the time a report or system learned about it. If the backend cannot answer historical as-of queries, label replay as a reconstruction based on currently retained evidence.
7. **Make a small first cut.** Deliver opening beats and one central explanation before expanding the full story. For a video, produce script/storyboard; invoke the project's actual renderer or editor only if one already exists and is available.
8. **Review as a newcomer.** Can viewers identify the question in the opening, follow each visual change, restate the result, and open its evidence? Check the mobile view and every apparent numerical or historical claim. Mark checks actually performed, not planned.

## Output Contract

Return a short brief containing the question and audience; a claim ledger with real source references; a beat sheet connecting narration, visual action and claim IDs; unknowns; and a clear distinction between **storyboard produced** and **video rendered**. Cite primary sources in publishable material, not just in working notes.

## Example

User: “Explain why two seemingly unrelated EventGraph stories became linked.”

```yaml
question: What evidence connects the two stories?
viewer_takeaway: Explain which shared entity links them, and how strong the link is
claims:
  - id: C1
    kind: reported_fact
    source: "<verified public article URL>"
    observed_at: "<actual source publication timestamp>"
    note: "Replace with a claim verified from the article"
beats:
  - question: What happened first?
    visual_action: "Show the first verified event on a focused timeline"
    narration: "Use the verified claim, not a guessed summary"
    claims: [C1]
  - question: Where is the connection?
    visual_action: "Highlight the existing relation; open its evidence"
    narration: "Explain whether the link is stated or inferred"
    claims: [C1]
historical_mode: "current evidence reconstruction; no backend as-of asserted"
```

Replace every placeholder with repository-backed evidence before publishing.

## Limitations

This skill supplies an editorial method, not a BaoCut integration or rendering engine. It cannot establish source accuracy without source access, infer missing timestamps, make nonpublic evidence public, or prove historical graph state where no temporal backend exists.

## Method Provenance

Independently written for evidence-driven agent projects. Method-level inspiration: [BaoCut explainer-video](https://github.com/JimLiu/baocut/tree/main/skills/baocut/built-in-skills/explainer-video) (BaoCut Community License). No BaoCut instructions, source code, templates, or runtime interfaces are bundled.
