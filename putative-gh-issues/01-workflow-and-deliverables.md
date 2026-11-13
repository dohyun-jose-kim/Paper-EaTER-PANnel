# [Design] Define workflows for all three deliverable modes

- Local ID: `01`
- Project version: `v0.2.1`
- Publication status: Published as GitHub issue [#1](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/1).
- Work type: Design.
- Design level: Design refinement.
- Implementation readiness: Not ready; design work remains.
- Source topic: User workflow and final deliverable.
- Available next action: Draft the user journey and result boundary for each mode.

## Purpose

Define what the user does and receives in each required mode. A shared understanding of the workflow is needed before selecting handoff mechanisms or designing detailed screens.

## Established requirements and evidence

- Support a faithful transcript with source images.
- Support a source-aware reading workflow that checks the paper while performing a requested task.
- Support both together as a third user-selectable mode.
- Provide a default while preserving user choice. All three modes are required; their inclusion is not a question for this issue.
- These are agreed requirements, not implemented capabilities.

## Questions to resolve

- For each mode, what starts the task, what does the user supply, and what marks completion?
- Who consumes the result: the user, another model, or another application?
- When does the workflow inspect the source or request user review?
- In the combined mode, how do saved material and task-specific reading relate?
- What should be saved for reuse, and what remains specific to one task?
- Which mode should be the default, and what task evidence supports that choice?

## Expected design output

A flow description for each mode, with input, user actions, source checks, result boundaries, and handoff expectations. Include representative usage scenarios and a default-mode proposal with its rationale. Coordinate format details with issue 08 rather than selecting a schema here.

## Completion criteria

- [ ] All three required modes have distinct, reviewable user flows.
- [ ] Result consumers, completion boundaries, and reuse expectations are stated.
- [ ] The default-mode decision and its rationale are recorded.
- [ ] Remaining cross-topic questions are linked and explicitly resolved or deferred through review.
- [ ] The reviewed decisions are reflected in the project design documents.

## Related issues and sources

Related work, not mandatory execution order:

- [08: Representation and handoff](08-representation-and-handoff.md) defines delivery details.
- [11: GUI and technology](11-gui-and-technology.md) turns the flows into user interactions.
- [13: Acceptance criteria](13-acceptance-criteria.md) defines how results will be assessed.
- [Development README: deliverable modes](../readme-dev-v0.1.md#user-selectable-deliverable-modes).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
