---
name: repo-design-system
description: "Extract and refine a repository-backed visual system without inventing tokens, replacing components, or adding a second UI framework."
source: self
risk: safe
---

# Repository-Backed Design System

## When to Use This Skill

Use when improving the design consistency of an existing website or product (such as EventGraph or the Ferro site), documenting its visual rules, or proposing a small token change for responsive screens.

Do not use for video editing, a complete rebrand without authorization, or automatic framework migration. For a single small styling fix, change the existing component directly instead of creating a separate design-system document.

## Workflow

1. **Inventory before proposing.** Search the actual repository for CSS variables, theme settings, Tailwind configuration, existing tokens, typography, colors, component libraries, icons, spacing, radius, motion, and responsive breakpoints. Prefer code over screenshots. Record file paths and the existing names; do not silently rename or fork them.
2. **Identify the product's intent.** Describe the users and primary screens. EventGraph favors legible relations, evidence provenance, timeline orientation, and responsive graph exploration. Ferro favors readable research, article scanning, and high-density data without false visual precision. Preserve the project's existing brand and information hierarchy unless asked otherwise.
3. **Capture only justified tokens.** Make a table: category, current value, source file, semantic role, candidate adjustment, and reason. Add a new token only if a repeated need cannot be met with an existing one; values missing from the repo are **unknown**, not permission to invent a brand standard.
4. **Map states, not just components.** Inspect states that already exist: loading, empty, selected, hover, focus, graph expansion, time-filtering, source withdrawal, light/dark, narrow mobile, and Chinese/English long labels. Record what the component does in each state; do not invent product behavior.
5. **Propose minimal deltas.** Reuse existing components. Specify exactly which token or component would change, why it helps comprehension, and what screens are affected. Preserve relevant established layouts and accessibility semantics. Avoid ornamental animations and universal gradients.
6. **Check on real layouts when tools allow.** Compare desktop and small-screen screenshots, long copy, color contrast, keyboard focus, reduced motion, and text scale. Never claim a visual check unless an actual rendered frame or browser inspection occurred.
7. **Deliver a compact contract.** The output is a mapping from existing sources to design decisions, a proposed patch or small guide, and explicitly noted gaps. Do not add a separate CSS framework, theme provider, design app format, or assets pipeline.

## Example

User: “Unify the EventGraph timeline and evidence panel styles without changing their interactions.”

```yaml
inventory:
  - token: "--existing-foreground-token"
    source_file: "<verified CSS path>"
    value: "<read from that file>"
    role: "evidence body text"
proposal:
  - screen: "event story + focused graph"
    change: "reuse the existing foreground token for the evidence panel"
    reason: "reduce inconsistent text emphasis without modifying graph behavior"
checks:
  desktop: "not yet visually checked"
  mobile: "not yet visually checked"
  bilingual_overflow: "not yet visually checked"
```

The names and paths above are placeholders. Replace them by reading the repo; never paste them as working configuration.

## Limitations

This is a repository inspection and design-decision skill, not BaoCut's proprietary design-system file format or editor. It cannot infer exact values from descriptions alone, generate a font license, or verify appearance without rendered inspection. It does not authorize production deployment.

## Method Provenance

Independently written for existing-web-app maintenance. Method-level inspiration: [BaoCut design-system](https://github.com/JimLiu/baocut/tree/main/skills/baocut/built-in-skills/design-system) (BaoCut Community License). No BaoCut code, templates, or file schema are copied.
