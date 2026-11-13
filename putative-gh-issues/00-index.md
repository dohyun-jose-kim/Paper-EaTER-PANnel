# Local GitHub issue drafts

Project version: `v0.2.1`.

Publication status: Published as GitHub issues #1–#14. Product-design issues #1–#13 are open; completed setup issue #14 is closed.

## Purpose and boundaries

This directory contains 14 issue drafts: 13 product-design topics from [User choices and remaining design decisions](../docs/open-design.md), plus the requested GitHub repository and remote setup issue. Each draft is now linked to its published GitHub issue below.

The two-digit IDs remain local references. The GitHub issue links below record the actual assigned numbers; neither numbering scheme defines priority or an implementation schedule. Related-issue links show coordination needs; they do not assert mandatory execution order.

The drafts describe work to do. Their existence does not mean that the work, design review, or implementation is complete. Current work is on `big-pic-design`. Draft creation and issue publication are separate operations; all 14 drafts have now been published at the user’s request.

## Levels of detail and readiness

| Level | Meaning | Current drafts |
|---|---|---|
| Design refinement | User-facing requirements are established. Define the remaining behavior, defaults, limits, and mechanisms. | 01-05 and 11 |
| Exploration and definition | The problem and some requirements are known. Gather missing information and develop an approach before selecting details. | 06-10 and 12-13 |
| Repository setup | Public repository, remote, and branch tracking are configured and verified. | 14 (complete) |

These levels describe the current work, not importance. They are separate from user configurability: an established user choice can still need substantial design. No product-design draft is ready for implementation.

Do not reopen GUI introduction, user control over the established settings, or support for all three deliverable modes. Exact defaults, supported ranges, and combination constraints are still design work. No framework, schema, policy set, evaluation threshold, or sample size is selected by these drafts.

## Issue list

| Local ID | Topic | Level | Available next action |
|---|---|---|---|
| 01 | [User workflow and final deliverable](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/1) | Design refinement | Draft the user journey and result boundary for each mode. |
| 02 | [Models and access changes](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/2) | Design refinement | List the capabilities the workflow needs and the access questions to investigate. |
| 03 | [Execution count and model combinations](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/3) | Design refinement | Draft definitions and examples that distinguish work units, repeats, and model combinations. |
| 04 | [Concurrency](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/4) | Design refinement | Describe serial and concurrent behavior without selecting a numeric default. |
| 05 | [Comparison and conflict resolution](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/5) | Design refinement | Draft disagreement scenarios and candidate policy descriptions. |
| 06 | [PDF, text, and image input delivery](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/6) | Exploration and definition | List input paths and the evidence needed to distinguish available files from received content. |
| 07 | [Images, captions, body text, and source locations](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/7) | Exploration and definition | List source relationships and difficult layouts the design must represent. |
| 08 | [Internal representation and handoff format](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/8) | Exploration and definition | Describe what each consumer must receive before comparing candidate formats. |
| 09 | [Execution state, failure, and recovery](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/9) | Exploration and definition | Draft user-visible scenarios for progress, partial results, interruption, and reuse. |
| 10 | [Authentication, permissions, and secrets](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/10) | Exploration and definition | Map intended access and data flows, separating existing Git exclusions from runtime requirements. |
| 11 | [Implementation technology and GUI](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/11) | Design refinement | Draft screen flows and wireframes for mode selection, settings, and their explanations. |
| 12 | [Subscription usage and API costs](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/12) | Exploration and definition | List the usage information and user controls needed before choosing provider-specific limits. |
| 13 | [Fidelity, reproducibility, and traceability](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/13) | Exploration and definition | Define assessment terms and consequential error categories before proposing an evaluation protocol. |
| 14 | [GitHub repository creation and remote connection](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/14) | Setup complete | Public repository and all three branch upstreams verified. |

## Work that can start now

- **01 and 11:** Draft the three mode workflows and GUI flows or wireframes. Their central requirements are established. Unsettled values must remain labeled rather than silently becoming defaults.
- **03 and 04:** Define execution units, count semantics, and concurrency behavior. Numeric defaults and limits require further rationale.
- **Other design issues:** Begin the listed investigation or scenario-writing action. Do not treat a lack of a final design as a reason to postpone all useful work.
- **14:** Complete. The public repository is `dohyun-jose-kim/Paper-EaTER-PANnel`; `origin` is configured, all three branches are pushed and tracked, and `main` is the default branch.

This readiness assessment is not a mandatory priority order. Starting design work does not authorize implementation, live model evaluation, or external publication.

## Review and completion

Product-design drafts contain established requirements, unresolved questions, expected output, and unchecked completion criteria. Setup issue 14 records the completed repository configuration. Those criteria describe completion of the issue's design or setup work, not completion of this draft-writing task.

Review the scope and evidence before treating a proposal as a decision. Record reviewed decisions in the project design documents. If a broad topic later needs smaller issues, split it around independently reviewable results and retain links to the original topic. Do not invent detailed implementation tickets merely to make all drafts equally long.

Publication checks verified secret exclusions and scanned tracked files and Git history for common credential patterns. Published issue bodies use GitHub links for source documents and actual related issues. A later implementation issue should refer to a reviewed design rather than infer unspecified behavior from this draft.

## Sources

- [Development README](../readme-dev-v0.1.md).
- [Design status](../docs/design-status.md).
- [User choices and remaining design decisions](../docs/open-design.md).
- The user's current directions, including the request for issue 14.

No previous-project evaluation records were used to write these drafts.
