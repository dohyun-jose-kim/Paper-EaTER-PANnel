# [Design] Define comparison units and selectable conflict-resolution policies

- Local ID: `05`
- Project version: `v0.2.1`
- Publication status: Published as GitHub issue [#5](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/5).
- Work type: Design.
- Design level: Design refinement.
- Implementation readiness: Not ready; design work remains.
- Source topic: Comparison and conflict resolution.
- Available next action: Draft disagreement scenarios and candidate policy descriptions.

## Purpose

Define how results are compared and how a user-selected policy handles disagreement. Keep result agreement distinct from verification against the source.

## Established requirements and evidence

- Users must be able to select a supported conflict-resolution policy.
- The product must provide a default and explain supported policies.
- Agreement between results does not establish source fidelity.
- Voting is not a selected policy. Repeated execution does not imply voting.
- No comparison unit or policy set has been selected.

## Questions to resolve

- What should be compared: characters, expressions, regions, passages, structured elements, or task outputs?
- How should the system distinguish disagreement, omission, unreadable content, uncertainty, and unreviewed material?
- When should each policy inspect the source, involve a human reviewer, or preserve an unresolved result?
- Can policies differ by content or task while remaining understandable?
- Does voting have a justified role for any defined case?
- Which policy should be the default, and what error consequences support that choice?

## Expected design output

A comparison-unit definition and a policy comparison with triggers, source-check behavior, reviewer involvement, and result states. Include cases of matching wrong results, conflicting symbols or numbers, missing content, and genuinely unreadable source material. These are design scenarios, not a new model evaluation.

## Completion criteria

- [ ] Comparison units and the supported policy set are defined.
- [ ] Source checks are distinguished from agreement between outputs.
- [ ] Uncertainty, omissions, and unresolved results have explicit treatment.
- [ ] The default and any role for voting have documented rationale.
- [ ] Policy explanations and scenarios are reviewed and recorded.

## Related issues and sources

Related work, not mandatory execution order:

- [03: Execution count](03-execution-count-and-combinations.md) defines the results available to compare.
- [07: Source relationships](07-source-relationships.md) supports source checks.
- [09: Execution lifecycle](09-execution-lifecycle-and-provenance.md) addresses result status.
- [13: Acceptance criteria](13-acceptance-criteria.md) addresses assessment.
- [Design status: user configurability](../docs/design-status.md#user-configurability-and-design-status).

- [Source topic table](../docs/open-design.md#user-choices-and-design-work).
- [Draft index](00-index.md).
