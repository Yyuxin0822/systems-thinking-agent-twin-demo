---
name: environmental-metabolism-modeling
description: Generate and evaluate environmental infrastructure designs through metabolism modeling of input, process, and output twins, stocks, and flows. Use for net-positive infrastructure design, single-system or coupled-system balance and trade-off evaluation, and exporting designs to Azure Digital Twins Explorer.
---

**Goal and Design Requirements**
Design an environmental infrastructure system that meets the stated goal, setting, available area, and population or demand.

Define what success means. For a net-positive goal, specify the resource or outcome, system boundary, and accounting period.

Preserve the stated requirements. Identify assumptions, missing information, and any conflicts that affect feasibility.

**Generative Design**

Design the requested infrastructure through generative environmental metabolism modeling. Consider green infrastructure (ecological/environmental) and architectural infrastructure (built/technological), and determine the assets, connections, capacities, and operating conditions needed to meet the design requirements.

Each twin must represent an identifiable existing or proposed physical or digital asset, or an identifiable assembly of assets. Use input, process, and output to describe assets’ roles relative to the modeled system. Do not create twins for abstract functions or concepts such as “storage,” “consumption,” or “efficiency.” Instead, represent these through the properties, stocks, flows, and operating characteristics of the relevant assets.

For each asset, identify what it receives, transforms, accumulates, and releases:

- **Stocks** are quantities accumulated within an asset at a stated time, including retained resources, living biomass, and materials incorporated into infrastructure. Distinguish stocks from storage or processing capacities.
- **Flows** are transfers between assets, expressed as rates or totals over a stated period. Identify the source, destination, quantity, unit, and time basis.

Include assets outside the site or requested system when they support its design. Identify their location relative to the analysis boundary and account for their contributions and dependencies explicitly. Use containment relationships where asset assemblies or hierarchical decomposition help explain the design.

**Record Stocks and Flows**

Record the stocks and flows used in the design and validation in the structured model and exported instance data. Discussing them in reasoning, prose, or calculations alone does not satisfy this requirement.

Populate the agreed stock and flow maps with named quantities, numeric values, and units. Associate stocks with the relevant asset twins and transfers with the corresponding flow relationships or flow records specified by the agreed schema. Include reference times for stocks and time bases for flows in structured fields wherever supported.

Use evidence, calculations, or clearly labeled assumptions to provide numerical values. Do not invent unsupported values or substitute zero for missing information. If a required quantity cannot be estimated defensibly, record it explicitly as unresolved in an associated structured record and identify the affected balance or performance check as incomplete.

Do not omit a relevant stock or flow because the schema lacks a suitable field. Identify the schema limitation and specify the required extension or linked structured record.

**Validation and Design Revision**

Validation is balance- and co-optimization-driven. Check inputs, outputs, losses, and changes in stock for each asset and for the boundary as a whole, matching stock changes against the flows that cause them over the same period. Do not balance unlike quantities.

Validate from all below perspectives:

- Physical laws and mathematical balance calculations
- Performance evidence, datasets, or available simulation or machine-learned models
- Socio-economic-environmental and spatial constraints
- SEE constraints

Use calculations or tools for numerical checks and state the assumptions and methods. Revise the design where checks reveal problems and push it toward joint improvement across objectives, not only toward feasibility. Report what passes, fails, or remains untested, and claim only the work actually performed.

**A System of Systems**

For a single-system request, validate that system and its supporting dependencies, then proceed to the output.

For multiple systems, first validate each system’s balances and performance. Then evaluate and revise the combined design through exchanges, shared assets, competing demands, and social, economic, and environmental trade-offs across systems and twins. Reflect the complexity needed for a workable multidisciplinary design, while avoiding unnecessary infrastructure and double-counting resources or benefits.

**Output and Completion Check**

Provide the design using the agreed model.json definitions and the corresponding populated twins and relationships for Azure Digital Twins Explorer. Include a concise explanation of the design, assumptions, validation findings, and unresolved issues.

Before delivery, inspect the exported data and verify that:

- Every twin represents an identifiable physical or digital asset or asset assembly.
- Every stock and flow used in a design calculation or validation check has a corresponding populated entry in the exported data.
- Quantities include names, numeric values, units, and the time information needed to interpret them.
- Exported values agree with the calculations and reported findings.
- Missing quantities and schema limitations are explicitly recorded.

An export with stock and flow definitions but no populated stock and flow values is incomplete. Distinguish checks performed locally from a successful import into Azure Digital Twins.
