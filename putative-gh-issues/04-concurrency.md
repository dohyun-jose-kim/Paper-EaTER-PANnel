# [Design] Define user-controlled concurrency and operating limits

- Local ID: `04`
- Project version: `v0.2.1`
- Publication status: Local draft; not published.
- Work type: Design.
- Design level: Design refinement.
- Implementation readiness: Not ready; design work remains.
- Source topic: Concurrency.
- Available next action: Describe serial and concurrent behavior without selecting a numeric default.

## Purpose

Define how users control simultaneous work and understand its effect on responsiveness and resource use.

## Established requirements and evidence

- Users must be able to set concurrency within supported limits.
- Concurrency is independent of execution count.
- Access, resources, usage, and cost can constrain the setting.
- No numeric default, limit, or scheduling mechanism has been selected.

## Questions to resolve

- Which operations can overlap, and which have dependencies that require an order?
- What does the concurrency setting count?
- How should requested concurrency interact with model, provider, and local resource limits?
- What happens to pending or active work when a limit is reached or an operation fails?
- What default and range can be justified for the intended workflow?
- How should the GUI explain the requested setting and the work actually running?

## Expected design output

A behavior description for serial and concurrent work, an explanation of limiting factors, and a justified default/range proposal. Include scenarios with mixed models and constrained access. Define the observable behavior without prematurely selecting a scheduler implementation.

## Completion criteria

- [ ] The setting's meaning and scope are explicit.
- [ ] Operation dependencies and relevant limiting factors are documented.
- [ ] Pending-work and limit-reached behavior are described.
- [ ] Default, range, and GUI explanations are reviewed.
- [ ] The result is consistent with execution count and recovery decisions.

## Related issues and sources

Related work, not mandatory execution order:

- [03: Execution count](03-execution-count-and-combinations.md) defines total requested work.
- [09: Execution lifecycle](09-execution-lifecycle-and-provenance.md) addresses interruption and failure.
- [12: Usage and cost](12-usage-and-cost.md) addresses usage constraints.
- [Development README: user choices](../readme-dev-v0.1.md#user-choices-and-defaults).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
