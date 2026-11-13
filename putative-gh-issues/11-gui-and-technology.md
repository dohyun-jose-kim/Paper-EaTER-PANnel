# [Design] Design the GUI for informed choice and select implementation technologies

- Local ID: `11`
- Project version: `v0.2.1`
- Publication status: Local draft; not published.
- Work type: Design.
- Design level: Design refinement.
- Implementation readiness: Not ready; design work remains.
- Source topic: Implementation technology and GUI.
- Available next action: Draft screen flows and wireframes for mode selection, settings, and their explanations.

## Purpose

Turn the established user choices into an understandable interface. Choose implementation technologies based on the required interaction and integration needs.

## Established requirements and evidence

- A GUI is required. Its introduction is not a decision to reopen.
- Users must understand defaults, variables, supported combinations, and their effects, then actively adjust settings.
- All three deliverable modes must be available as user choices.
- Screen implementation is not limited to static HTML or one language or framework.
- React, TypeScript, and other suitable technologies may be used. Frontend and execution-layer technologies can be selected separately.
- Go is installed as a candidate. No GUI framework or final execution-layer language is selected.

## Questions to resolve

- How should users move from selecting a mode to configuring and starting work?
- How should defaults, available choices, unsupported combinations, and their reasons be explained?
- Which information belongs beside a setting, and which needs a separate explanation or source view?
- How should progress, review, results, and recovery appear in the interaction?
- What deployment and integration needs should guide frontend and execution-layer choices?
- Is a complementary CLI useful, and for which tasks?

## Expected design output

Screen flows and wireframes for the agreed choices, with example explanations and result/review transitions. Include a technology comparison tied to deployment, integration, learning, and maintenance needs. Early wireframes may label unsettled values as undecided; they must not silently turn examples into defaults.

## Completion criteria

- [ ] All three modes and the established settings appear in reviewable user flows.
- [ ] Defaults and combination constraints are explained without obscuring user control.
- [ ] Progress, results, source inspection, and recovery interactions are addressed.
- [ ] Frontend and execution-layer choices have documented rationale.
- [ ] The reviewed GUI design distinguishes established behavior from unresolved details.

## Related issues and sources

Related work, not mandatory execution order:

- [01: Workflows](01-workflow-and-deliverables.md) defines mode behavior.
- [03: Execution settings](03-execution-count-and-combinations.md) defines count semantics.
- [07: Source relationships](07-source-relationships.md) supports source navigation.
- [09: Lifecycle](09-execution-lifecycle-and-provenance.md) defines status and recovery.
- [12: Usage and cost](12-usage-and-cost.md) defines usage explanations.
- [Development README: GUI](../readme-dev-v0.1.md#gui-and-informed-choice).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
