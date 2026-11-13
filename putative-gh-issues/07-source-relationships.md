# [Design] Define relationships between images, captions, text, and source locations

- Local ID: `07`
- Project version: `v0.2.1`
- Publication status: Published as GitHub issue [#7](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/7).
- Work type: Design.
- Design level: Exploration and definition.
- Implementation readiness: Not ready; design work remains.
- Source topic: Images, captions, body text, and source locations.
- Available next action: List source relationships and difficult layouts the design must represent.

## Purpose

Determine how a result can be connected to the source information that gives it meaning. Source navigation must work across text, visual content, and document boundaries.

## Established requirements and evidence

- Source fidelity includes figures, tables, captions, references, and their relationships with body text.
- Users need to connect results to relevant source content.
- No image or table-content exclusion is inherited from earlier work.
- Source-location precision and relationship representation have not been selected.
- These relationships are not automatically user-configurable settings.

## Questions to resolve

- What location precision is needed for navigation and verification?
- How should multi-panel figures, table captions, and body-text references be connected?
- How should relationships span pages or work units?
- Which content needs image preservation, textual representation, or both?
- How should the design represent an uncertain or missing association?

## Expected design output

A conceptual relationship model with layout examples and a source-navigation description. Compare location precision options against intended tasks. This output should establish meaning before selecting storage fields or identifiers.

## Completion criteria

- [ ] Required relationships and source-location precision are documented.
- [ ] Multi-panel, table, cross-reference, and page-spanning cases are covered.
- [ ] Image/text treatment and uncertain associations have reviewed behavior.
- [ ] Navigation and verification needs are reflected in the design documents.

## Related issues and sources

Related work, not mandatory execution order:

- [05: Conflict resolution](05-comparison-and-conflict-resolution.md) uses source checks.
- [08: Representation and handoff](08-representation-and-handoff.md) carries relationships to consumers.
- [11: GUI](11-gui-and-technology.md) exposes source navigation.
- [13: Acceptance criteria](13-acceptance-criteria.md) assesses traceability.
- [Design status: user configurability](../docs/design-status.md#user-configurability-and-design-status).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
