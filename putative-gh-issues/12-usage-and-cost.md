# [Design] Define subscription and API usage visibility and cost controls

- Local ID: `12`
- Project version: `v0.2.1`
- Publication status: Local draft; not published.
- Work type: Design.
- Design level: Exploration and definition.
- Implementation readiness: Not ready; design work remains.
- Source topic: Subscription usage and API costs.
- Available next action: List the usage information and user controls needed before choosing provider-specific limits.

## Purpose

Help users understand the usage and cost consequences of model, count, and concurrency choices.

## Established requirements and evidence

- Existing subscriptions are the initial preference; API access remains possible.
- Users need understandable usage and cost implications.
- No automatic paid fallback, budget, limit, or reporting mechanism is selected.
- Subscription use must not be converted to API cost without a valid basis.
- Current account limits and billing terms have not been verified for a project workflow.

## Questions to resolve

- What usage information can each access path report, estimate, or not disclose?
- How should the interface distinguish measured usage, estimates, and unknowns?
- Which controls are needed before additional usage or charges occur?
- What budget or usage limits should users be able to set, and what defaults are appropriate?
- What should happen when access or usage limits are reached?
- How should retries, repeats, concurrent operations, and reuse affect reporting?

## Expected design output

Usage-information requirements and proposed control behavior, including cases where reliable estimates are unavailable. Identify account and provider facts that need verification when access paths are selected. Do not insert speculative prices, quotas, or budget values.

## Completion criteria

- [ ] Measured, estimated, and unknown usage are distinguished.
- [ ] User controls, defaults, and limit-reached behavior are reviewed.
- [ ] Subscription and API routes remain distinct in reporting and billing assumptions.
- [ ] Repeats, concurrency, recovery, and reuse are covered.
- [ ] Required external evidence and unresolved limits are documented.

## Related issues and sources

Related work, not mandatory execution order:

- [02: Models and access](02-models-and-access.md) identifies access routes.
- [03: Execution count](03-execution-count-and-combinations.md) defines requested work.
- [04: Concurrency](04-concurrency.md) addresses simultaneous work.
- [09: Lifecycle](09-execution-lifecycle-and-provenance.md) addresses recovery and reuse.
- [11: GUI](11-gui-and-technology.md) explains usage to users.
- [Design status: access preference](../docs/design-status.md#access-preference).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
