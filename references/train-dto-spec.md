# TrainDTO JSON Specification

## Contents

- [Purpose](#purpose)
- [Output contract](#output-contract)
- [Non-train exclusion rule](#non-train-exclusion-rule)
- [Unknown-value defaults](#unknown-value-defaults)
- [Formatting and normalization rules](#formatting-and-normalization-rules)
- [Research and confidence rules](#research-and-confidence-rules)
- [TrainDTO schema fields](#traindto-schema-fields)
- [Allowed values](#allowed-values)
- [Valid eras](#valid-eras)
- [Core model rules](#core-model-rules)
- [Prototype rules](#prototype-rules)
- [Fictional model rules](#fictional-model-rules)
- [Decision guidance for multi-item products](#decision-guidance-for-multi-item-products)

## Purpose

Generate `TrainDTO` JSON for a train product named by the user.

This specification covers:
- single locomotives
- railcars
- passenger cars
- cabooses
- rail utility vehicles
- train sets containing multiple included rail items
- fictional train items with a real-world prototype basis

## Output Contract

- Return only raw JSON.
- Do not wrap the result in markdown fences.
- Do not include explanations.
- Output must be valid JSON.
- Use valid values only.
- If the product contains exactly one object, return a single JSON object.
- If the product contains more than one distinct included object, return a JSON array of `TrainDTO` objects, with one DTO per included object.
- Do not combine multiple included items into a single DTO.
- If a set includes duplicate or near-identical items, still return one DTO per physical included item unless the user explicitly asks for the set to be collapsed.
- Preserve shared set information where appropriate, but fill in each object's individual identity fields separately when those details are known.

## Non-Train Exclusion Rule

Do not include items that are not trains in the output.

Exclude:
- accessories
- scenery
- figures
- track
- road vehicles
- buses
- cars
- buildings
- containers
- removable loads
- packaging extras
- any included item that is not itself a locomotive, railcar, passenger car, caboose, or rail utility vehicle

If a product contains both train and non-train items, return DTOs only for the train items.

## Unknown-Value Defaults

- Unknown string fields: `""`
- Unknown numeric fields: `0`
- Unknown booleans: `false` unless clearly supported
- Unknown optional dates: `null`

## Formatting And Normalization Rules

- Use ISO 8601 format for all dates.
- Use inches for:
  - `length`
  - `minimumRadius`
- Use ounces for:
  - `weight`
- Use `railCount = 2` unless the model clearly uses a different rail system.
- Use `condition = "New"` unless otherwise specified.
- Use `purchaseDate = null` unless known.
- Use `purchaseLocation = ""` unless known.
- Use `pricePaid = 0` unless known.
- Use `msrp = 0` unless known.
- Use `createdAt = "1970-01-01T00:00:00Z"`
- Use `updatedAt = "1970-01-01T00:00:00Z"`

## Research And Confidence Rules

- Prefer official manufacturer pages, catalog entries, and published specs for model-specific fields.
- Prefer established prototype references for real-world prototype fields.
- If sources conflict:
  - prefer manufacturer information for model features, dimensions, and included equipment
  - prefer widely accepted historical references for prototype details
- Do not invent unsupported features or values.
- If the product cannot be identified with reasonable confidence, fill only confirmed fields and leave all unknown values at the required defaults.

## TrainDTO Schema Fields

- `name: String`
- `category: String`
- `locomotiveType: String`
- `roadName: String`
- `roadNumber: String`
- `modelNumber: String`
- `manufacturer: String`
- `scale: String`
- `railCount: Int`
- `era: String`
- `livery: String`
- `condition: String`
- `decoder: String`
- `dccAddress: String`
- `isDCC: Bool`
- `isSound: Bool`
- `hasLights: Bool`
- `hasSmoke: Bool`
- `isDummy: Bool`
- `hasNEM362Pocket: Bool`
- `couplerType: String`
- `trucksTuned: Bool`
- `wheelsReplaced: Bool`
- `weight: Double`
- `length: Double`
- `minimumRadius: Double`
- `purchaseDate: Date?`
- `purchaseLocation: String`
- `pricePaid: Double`
- `msrp: Double`
- `notes: String`
- `prototypeName: String`
- `prototypeRailroadOperator: String`
- `prototypeRoadNumber: String`
- `prototypeBuilderManufacturer: String`
- `prototypeBuildDate: Date?`
- `prototypeServiceEntryDate: Date?`
- `prototypeRetirementDate: Date?`
- `prototypeWheelArrangement: String`
- `prototypePowerType: String`
- `prototypeClassDesignation: String`
- `prototypeGauge: String`
- `prototypeRouteRegion: String`
- `prototypeLiveryEra: String`
- `prototypeLength: Double`
- `prototypeWeight: Double`
- `prototypeMaxSpeed: Double`
- `prototypeHorsepower: Double`
- `prototypeTractiveEffort: Double`
- `prototypeServiceRole: String`
- `prototypeHistoricalNotes: String`
- `createdAt: Date`
- `updatedAt: Date`

## Allowed Values

### category

Valid values:
- `Locomotive`
- `Rolling Stock`
- `Passenger`
- `Caboose`
- `Utility`

### locomotiveType

Valid values:
- `""`
- `Steam`
- `Diesel`
- `Electric`
- `Turbine`

### condition

Valid values:
- `New`
- `Like New`
- `Used`
- `Weathered`
- `Needs Repair`

### couplerType

Valid values:
- `Knuckle`
- `Horn Hook`
- `Fishhook`
- `Hook and Loop`

## Valid Eras

### US eras

- `Era I (pre-1870) - Steam / Pioneer`
- `Era II (1870-1920) - Steam / Expansion`
- `Era III (1920-1945) - Steam dominant / Early diesel`
- `Era IV (1945-1960) - Steam + Diesel / Transition era`
- `Era V (1960-1980) - Diesel / Classic diesel`
- `Era VI (1980-2000) - Diesel / Modern begins`
- `Era VII (2000-Present)`

### European epochs

- `Epoch I (pre-1920)`
- `Epoch II (1920-1945)`
- `Epoch III (1945-1970)`
- `Epoch IV (1970-1990)`
- `Epoch V (1990-2005)`
- `Epoch VI (2005-Present)`

## Core Model Rules

- `locomotiveType` should only be filled in when `category` is `"Locomotive"`.
- For non-locomotive entries, use `""`.
- For `Passenger`, `Caboose`, `Rolling Stock`, and `Utility` entries, set `locomotiveType` to `""`.
- `decoder` and `dccAddress` may be empty strings even when `isDCC` is `true`, if those details are unknown or not configured.
- If the item is clearly DCC-equipped, set `isDCC` to `true` even if `decoder` and `dccAddress` are empty.
- If the item is clearly sound-equipped, set `isSound` to `true`.
- If lighting is not explicitly confirmed, do not assume it; use `false` unless clearly documented.
- If smoke is not explicitly confirmed, use `false`.
- If the item is a dummy unit, set `isDummy` to `true`; otherwise `false`.
- Keep `notes` concise but informative.
- Prefer manufacturer specs for model features and dimensions.
- Do not invent unsupported features.
- Choose the most appropriate era or epoch based on the modeled livery and prototype period.
- Use inches for model `length` and `minimumRadius`.
- Use ounces for model `weight`.

## Prototype Rules

- Base prototype fields on the real prototype represented by the model.
- Keep model identity fields and prototype fields separate.
- `roadName`, `roadNumber`, `livery`, `notes`, and other model identity fields should describe the actual model being sold, including fictional branding when applicable.
- All `prototype*` fields must describe only the real-world prototype basis.
- All `prototype*` fields must not mix in fictional operators, fictional biographies, fictional route information, fictional regions, or story details.
- For non-locomotive entries, do not infer locomotive-only prototype data.
- For non-locomotive entries, leave `prototypePowerType` empty unless the real prototype itself clearly has a relevant and documented power type.
- If a prototype field is genuinely unknown, use empty string, `0`, or `null` as appropriate.
- Keep all prototype fields internally consistent with the same prototype basis.
- If instructed that all prototype fields should match a specific prototype basis, use that basis consistently for every prototype field.
- If multiple possible prototype bases exist, choose the one most widely accepted and use it consistently across all `prototype*` fields.

## Fictional Model Rules

- If the model represents a fictional item in any category, fill in prototype information using the real-world prototype the fictional item was based on.
- This applies to fictional locomotives, passenger cars, cabooses, rolling stock, and utility equipment.
- If the model represents fictional rolling stock, a fictional coach, a fictional caboose, or other fictional non-locomotive equipment, fill in prototype information using the real-world prototype the fictional item was based on.
- For fictional items, keep model identity fields separate from prototype fields in the same way as non-fictional items.
- Model fields may contain fictional branding, names, numbers, liveries, or operators.
- `prototype*` fields for fictional items must contain only real prototype-basis information.
- Do not copy fictional road names, fictional operators, fictional regions, or fictional biography details into prototype fields unless the fictional item truly has no real-world prototype basis.
- If a fictional item has a known real-world basis, use that real-world basis consistently for every `prototype*` field.
- If a fictional item has multiple possible prototype bases, choose the one most widely accepted and use it consistently across all `prototype*` fields.
- If there is no clear real-world prototype basis, leave prototype fields unknown rather than inventing details.
- If the model represents a fictional character or item based on a real-world prototype, append concise famous appearances, character associations, or well-known facts about the fictional character or item to `prototypeHistoricalNotes`, while keeping all other `prototype*` fields based strictly on the real-world prototype basis.
- Example: if the model is Thomas the Tank Engine from Thomas & Friends, fill in prototype information for the LB&SCR E2 class prototype basis rather than the fictional biography.

## Decision Guidance For Multi-Item Products

When a product contains multiple included rail items:
- Return one DTO per physical train item.
- Do not collapse separate items into a shared DTO.
- Duplicate cars should still produce separate DTOs unless the user explicitly asks to collapse duplicates.
