# [Design] Define internal representation and handoff for the required modes

- Local ID: `08`
- Project version: `v0.2.1`
- Publication status: Local draft; not published.
- Work type: Design.
- Design level: Exploration and definition.
- Implementation readiness: Not ready; design work remains.
- Source topic: Internal representation and handoff format.
- Available next action: Describe what each consumer must receive before comparing candidate formats.

## Purpose

Determine how the product represents source information internally and delivers useful results to users, models, or applications.

## Established requirements and evidence

- All three deliverable modes must be supported.
- Handoffs must address required text, images, and source links.
- JSON, HTML, Markdown, images, and combinations remain options.
- Handoff format and GUI implementation technology are separate decisions.
- No internal schema or export-format selection control has been approved.

## Questions to resolve

- What content and relationships must each mode preserve internally?
- Which capabilities do the intended consumers require?
- How will a receiving model actually obtain and inspect images?
- How should equations, tables, source locations, and uncertain content survive handoff?
- Should users choose export formats, or should the workflow determine them?
- What must remain portable or reusable outside the application?

## Expected design output

A representation requirements description and a format comparison organized by consumer and mode. Propose the handoff boundary and explain any information loss or compatibility limits. A detailed schema should follow the reviewed requirements, not be invented in this draft.

## Completion criteria

- [ ] Each mode has explicit consumer and content requirements.
- [ ] Internal representation is distinguished from external formats and GUI technology.
- [ ] Image delivery, source relationships, and uncertainty are addressed.
- [ ] Supported handoffs and any user format choices are reviewed with rationale.
- [ ] Compatibility and information-preservation limits are documented.

## Related issues and sources

Related work, not mandatory execution order:

- [01: Workflows](01-workflow-and-deliverables.md) defines mode boundaries.
- [06: Input delivery](06-input-delivery.md) addresses actual model inputs.
- [07: Source relationships](07-source-relationships.md) defines relationships to preserve.
- [09: Lifecycle and provenance](09-execution-lifecycle-and-provenance.md) addresses reuse and history.
- [Development README: deliverable modes](../readme-dev-v0.1.md#user-selectable-deliverable-modes).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
