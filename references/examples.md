# TrainDTO JSON Skill Examples

## Single item

Input:
Create JSON for Marklin Mini-Club 8892

Expected behavior:
- Return one TrainDTO JSON object
- Use only allowed enum values
- Keep unknown values at defaults
- Return raw JSON only

## Multi-item set

Input:
Create JSON for Walthers 920-42539

Expected behavior:
- Return a JSON array
- One TrainDTO per included train item
- Exclude non-train accessories and extras
- Do not collapse duplicates unless explicitly requested

## Fictional item

Input:
Create JSON for Thomas the Tank Engine

Expected behavior:
- Model identity fields may reflect Thomas
- Prototype fields should reflect the real-world prototype basis
- Add concise famous character/context notes only to `prototypeHistoricalNotes`
- Leave unknown prototype values blank or zero rather than inventing them

## Low-confidence identification

Input:
Create JSON for an unclear or partially identified train product

Expected behavior:
- Fill only confirmed fields
- Keep all unknown values at defaults
- Still return valid raw JSON
