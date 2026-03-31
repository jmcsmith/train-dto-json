---
name: train-dto-json
description: Generate strict TrainDTO JSON for named train models, train sets, and fictional rail items. Use when Codex needs to identify a train product, apply TrainDTO schema rules and defaults, separate model fields from prototype fields, exclude non-train accessories, and return raw valid JSON only.
---

# TrainDTO JSON

Generate `TrainDTO` JSON for a user-named train product.

## Quick Start

1. Identify the product and any included train items with reasonable confidence.
2. Exclude accessories, scenery, figures, track, road vehicles, buildings, removable loads, packaging extras, and any other non-train items.
3. Return only raw valid JSON with no markdown fences or explanation.
4. Return a single JSON object for exactly one train item, or a JSON array with one DTO per physical included train item.
5. Leave unknown values at the required defaults instead of guessing.

## Workflow

1. Determine whether the product is a single train item or a multi-item set.
2. Keep model identity fields separate from `prototype*` fields.
3. For fictional items, keep fictional details in model fields, but base `prototype*` fields on the closest real-world prototype basis when known.
4. If identification confidence is low, fill only confirmed fields and leave the rest at defaults.
5. Keep enum values within the allowed set and keep all dates in ISO 8601 format.

## Output Rules

- Return one DTO per physical included train item.
- Do not combine multiple included train items into a shared DTO.
- Keep duplicate included cars as separate DTOs unless the user explicitly asks to collapse duplicates.
- Do not invent unsupported features, dimensions, dates, or prototype history.
- Use [references/train-dto-spec.md](references/train-dto-spec.md) for defaults, schema fields, enums, prototype rules, and multi-item guidance.
- Use [references/examples.md](references/examples.md) for concrete prompt patterns and expected behavior.

## References

- Read [references/train-dto-spec.md](references/train-dto-spec.md) for the complete TrainDTO ruleset.
- Read [references/examples.md](references/examples.md) when examples would help with ambiguity or edge cases.
