# [Design] Investigate PDF, text, and image delivery to models

- Local ID: `06`
- Project version: `v0.2.1`
- Publication status: Local draft; not published.
- Work type: Design.
- Design level: Exploration and definition.
- Implementation readiness: Not ready; design work remains.
- Source topic: PDF, text, and image input delivery.
- Available next action: List input paths and the evidence needed to distinguish available files from received content.

## Purpose

Determine how source content reaches a model and what evidence can support a claim that it was received or inspected.

## Established requirements and evidence

- The design must address PDF, text, and image input paths.
- A local file path alone does not establish delivery to a model.
- Saving an image or adding a Markdown link does not establish that a receiving model can inspect it.
- No project input-delivery trial has been performed. The path and verification mechanism remain undefined.

## Questions to resolve

- Which paths are available through the intended CLI/API access mechanisms?
- Is preprocessing needed, and what information could it omit or change?
- What can establish receipt of text or images? What remains unknown about actual inspection?
- How do context limits, image scaling, and document boundaries affect delivery?
- How can the workflow retain context across pages and work units?
- Which input controls or explanations does the user need?

## Expected design output

An input-path inventory with known capabilities, limitations, and evidence gaps. Propose how to represent receipt and inspection scope without overstating what can be verified. Identify any future trial needed to resolve a gap; this issue draft does not authorize running it.

## Completion criteria

- [ ] Relevant input paths and preprocessing choices are documented.
- [ ] Available source, received input, and inspected scope are distinguished.
- [ ] Context and image-quality constraints are described.
- [ ] A delivery approach and evidence strategy are reviewed, with unresolved verification limits stated.
- [ ] Required follow-up investigation is identified and linked.

## Related issues and sources

Related work, not mandatory execution order:

- [02: Models and access](02-models-and-access.md) identifies access capabilities.
- [03: Execution count](03-execution-count-and-combinations.md) addresses work-unit context.
- [08: Handoff](08-representation-and-handoff.md) addresses delivery to downstream consumers.
- [10: Security](10-authentication-and-security.md) addresses transmission.
- [Development README: conceptual pipeline](../readme-dev-v0.1.md#provisional-conceptual-pipeline).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
