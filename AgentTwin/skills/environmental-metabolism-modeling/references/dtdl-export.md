# DTDL export instructions

## Model

Read [model.json](model.json) before exporting. Use these bundled definitions unless the user supplies another agreed model. The source is [model_map_test.json](https://chatgpt.com/library?file_id=libfile_c81e1ba9121081918039c6335c510b6f&account_id=personal), adopted on 2026-10-31.

- Interfaces: `dtmi:environmental:Twin;3`, `InputTwin;3`, `ProcessTwin;3`, and `OutputTwin;3`, all in the `dtmi:environmental:` namespace. The three roles extend Twin.
- DTDL language context: `dtmi:dtdl:context;2`. Model version `;3` does not mean DTDL v3.
- Twin properties: `name` string, `system` string, and `stock` Map.
- Relationships: `contains` targets Twin with no custom properties; `flowsTo` targets Twin with `name` string, `system` string, and `flow` Map.
- Both maps have string keys and Object values containing `value` double and `unit` string.

Use stable IDs and quantity keys. Each twin must represent a physical asset, existing or proposed, with an input, process, or output role. Use map entries for quantities and flows between physical source and receiving assets; do not create standalone twins for abstract resources, energy, heat, services, or system labels. Containment is decomposition, not an energy or material transfer. Existing scalar-model instances are not automatically migrated.

## Quantities

Record timing, capacities, assumptions, evidence, boundary status, and unknown quantities in `ledger.json`, identified by twin/stock key or source twin/relationship/flow key. Omit unquantified map entries rather than substituting zero or text. Keep ledger values consistent with graph values.

Units are plain strings: validate dimensions and conversions in calculations. Keep different resources separate and document mappings such as electricity to stored energy. Do not add undeclared properties to twins, relationships, or quantity objects.

## Explorer files

Deliver `model.json` and `graph.json`, plus the ledger and calculations. Separate twin and relationship files are optional. Include only assets and relationships belonging to the requested design; do not copy unrelated test or example twins. The bundled model defines interfaces, not instance assets.

Each twin uses `$dtId`, `$metadata: { "$model": "<exact model ID>" }`, and declared properties. Each relationship uses `$relationshipId`, `$sourceId`, `$targetId`, `$relationshipName`, and its declared properties.

Use the Explorer JSON envelope with `digitalTwinsFileInfo: { "fileVersion": "1.0.0" }`, `digitalTwinsModels`, and `digitalTwinsGraph: { "digitalTwins": [...], "relationships": [...] }`. Leave `digitalTwinsModels` empty when the models are already loaded; otherwise include the definitions. Explain the prerequisite. Do not substitute Import Jobs API NDJSON.

Check JSON syntax, finite numeric values, exact model references, inherited property types, map entry structure, unique IDs, relationship names and endpoints, and containment cycles. Check ledger agreement and numerical balances separately. Distinguish these checks from official DTDL-parser validation and actual Azure import.

Verify the format against current [Explorer documentation](https://learn.microsoft.com/en-us/azure/digital-twins/how-to-use-azure-digital-twins-explorer#importexport-graph) or a recent export. To import: upload models if needed, select Import Graph in Twin Graph, open `graph.json`, review and Save, then query `SELECT * FROM digitaltwins`.

Importing a graph does not clear unrelated twins already in the instance. `SELECT * FROM digitaltwins` includes those existing twins. Use a design-specific ID prefix and provide a query scoped to that prefix when needed; do not delete existing twins unless requested.
