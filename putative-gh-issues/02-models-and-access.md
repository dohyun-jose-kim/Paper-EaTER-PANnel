# [Design] Define model choices and adaptation to CLI and API changes

- Local ID: `02`
- Project version: `v0.2.1`
- Publication status: Published as GitHub issue [#2](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/2).
- Work type: Design.
- Design level: Design refinement.
- Implementation readiness: Not ready; design work remains.
- Source topic: Models and access changes.
- Available next action: List the capabilities the workflow needs and the access questions to investigate.

## Purpose

Define how users choose supported models and understand their relevant differences. Keep the wrapper adaptable when models or access mechanisms change.

## Established requirements and evidence

- Users must be able to select a model or supported model combination.
- The wrapper must accommodate changes in models and CLI/API access.
- Existing subscriptions are the initial preference. API access remains possible.
- No supported model catalog, default model, or compatibility interface has been selected.
- No project workflow has verified current authentication, model availability, or usage limits.

## Questions to resolve

- Which reading, visual interpretation, and task capabilities must the catalog describe?
- Which models and access paths should be supported initially, and what evidence supports inclusion?
- Which combinations are meaningful, and which capability differences should the GUI explain?
- How should the system handle an unavailable model, changed CLI/API behavior, or an unsupported input type?
- What compatibility information must the wrapper retain? What would require a user decision rather than a silent change?
- What should the default model or combination be?

## Expected design output

A supported-capability and access comparison, a proposed catalog and default, and a description of the adaptation boundary. Distinguish provider documentation, observed behavior, and unverified assumptions. Any future research should answer these questions; this draft does not select or install providers.

## Completion criteria

- [ ] Supported models and access paths are selected with stated capability evidence.
- [ ] Supported combinations and default choices are explained.
- [ ] Unavailability, incompatible inputs, and access changes have defined intended behavior.
- [ ] GUI explanations distinguish capability, access, and usage constraints.
- [ ] Reviewed decisions and remaining evidence gaps are recorded in the design documents.

## Related issues and sources

Related work, not mandatory execution order:

- [03: Execution count](03-execution-count-and-combinations.md) defines the execution meaning of combinations.
- [06: Input delivery](06-input-delivery.md) addresses what models receive.
- [10: Authentication and security](10-authentication-and-security.md) addresses access credentials.
- [12: Usage and cost](12-usage-and-cost.md) addresses access limits and charges.
- [Design status: adaptability](../docs/design-status.md#adaptability).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
