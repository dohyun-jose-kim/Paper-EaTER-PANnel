# Design status

Status: Draft for user review.

Updated: 2026-11-13.

Project version: `v0.2.1`.

## Scope and basis

This document records the current design of `PAPER-LLM-read`. Its basis is the [development README](../readme-dev-v0.1.md) and the user's directions in the current discussion.

The user approved the conceptual diagram and authorized these design drafts. The user also directed that the new design remain independent of the previous project and that its records not be consulted further for this work. Previous extractor evaluations, recommendations, and processing rules are therefore not included as a basis for this design.

This document describes the current understanding. It is not an implementation specification. The design remains incomplete.

## Status terms

| Status | Meaning |
|---|---|
| Established direction | A direction accepted by the user. Details can remain open. |
| Confirmed evidence | A local observation with a stated scope. It does not establish product capability beyond that scope. |
| Provisional design | A proposal for further discussion. It is not a selected implementation. |
| Open decisions | Product design details that still need a decision or supporting information, such as defaults, supported ranges, or implementation mechanisms. This status does not mean that user choice is undecided. |

Design status and user configurability are separate dimensions. For example, letting a user set execution count is an established requirement. The default count and allowed range still need design. A user's choice for a task is not an unresolved product design decision. Internal architecture and security policies are not automatically user settings.

Historical proposals supplied in the task plan are labeled as such. They are not local evidence or current execution instructions. If feedback changes a decision, update its status and basis here and update the corresponding entry in [User choices and remaining design decisions](open-design.md).

## Established direction

| Direction | Current boundary |
|---|---|
| Source fidelity | Deliver scientific paper information to an LLM without omission or distortion. This is the objective, not a verified guarantee. Readable prose alone does not establish fidelity. |
| Information scope | Address text, numbers, symbols, equations, figures, tables, captions, references, and their relationships. The exact treatment of each remains open. |
| User choices and defaults | Provide defaults and let users select models and model combinations, execution count, concurrency, and conflict-resolution policy within supported bounds. Exact defaults, supported choices, and combination constraints still need design. |
| GUI and informed choice | Provide a GUI that helps users understand variables, choices, and the effects of combinations. Let users understand defaults and actively adjust supported settings. Detailed interactions and implementation technology remain design decisions. |
| Deliverable modes | Support all three user-selectable modes: a transcript with source images, a source-aware reading workflow, and both together. Default mode, detailed behavior, and delivery mechanisms still need design. This requirement does not indicate completed implementation. |
| Independent design | Do not inherit the previous project's extractors, architecture, processing sequence, output format, or evaluation boundaries as requirements. Preserve the previous work without changing it. |
| Current work | Gather requirements and develop the design through document review. Project implementation and model evaluation remain pending separate discussion. |
| Environment setup | Install required tools and environments when needed for agreed work. Go setup has been completed. Setup does not settle the implementation language. |
| Future publication | Prepare for a public Git repository. Keep local secrets separate from files intended for publication. |
| Version control workflow | Use project version `v0.2.1`. Create `dev` from `main` and `big-pic-design` from `dev`, then continue current design work on `big-pic-design`. This is the requested branch workflow, separate from the setup observations below. |
| Integration scope | Exclude `caffeine-pour-over` integration from current work. |
| Collaborative review | Present reviewable drafts. Obtain user direction at each agreed checkpoint. Do not treat silence as agreement or repeatedly request approval for accepted decisions. |

## Adaptability

The wrapper should support changes in models and CLI or API access. The design must consider differences in model capability and in the inputs that each access path can deliver.

User model selection and adaptability are established directions. The supported model catalog, model combinations, access mechanisms, defaults, adapter interfaces, and compatibility approach still need design.

## User configurability and design status

| Topic | User configurability or behavior | Design status |
|---|---|---|
| Model selection and combination | Users select a model or supported model combination. | Established choice. Supported models, combinations, capability explanations, access paths, and defaults need design. |
| Execution count | Users set the number of executions for a defined unit of work. | Established choice. Unit of work, range, default, and interaction with model combinations need design. |
| Concurrency | Users set how many executions may run at the same time. | Established choice. Default and resource, access, usage, and cost constraints need design. |
| Conflict-resolution policy | Users select a supported procedure for handling disagreement. | Established choice. Policy set, default, source checks, human review, and treatment of uncertainty need design. Voting is not a selected policy. |
| Deliverable modes | Users choose a transcript with source images, a source-aware reading workflow, or both. | All three modes are required. Default mode, detailed behavior, and delivery mechanisms need design. |
| Input delivery | The workflow must establish what content a model receives. Which input controls users need remains to be designed. | PDF, text, and image paths and verification mechanisms remain design decisions. |
| Source relationships | Users need to connect results to images, captions, body text, and source locations. | Representation, location precision, and navigation behavior need design. They are not automatically configurable settings. |
| Internal representation and handoff format | The selected deliverable must reach its consumer. Which export-format controls users need remains to be designed. | Internal representation and supported handoff formats, including JSON, HTML, and Markdown, remain design decisions. |
| Execution state and provenance | The workflow must address status, failure, cancellation, interruption, resumption, reuse, and input/output records. | User controls, state model, recovery behavior, and provenance detail need design. |
| Security | Keep secrets out of tracked files. Authentication and permission interactions need design. | Environment file exclusions are in place. Authentication, transmission, logging, and GUI content security remain design decisions, not automatically user settings. |
| Implementation technology and GUI | A GUI must support informed, active user choice. | GUI purpose is established. Layout, interactions, frontend technology, and execution-layer technology need design. Go is available as a candidate. |
| Usage and cost | Users need to understand the usage and cost implications of choices. Specific controls remain to be designed. | Subscription/API constraints, reporting, limits, and defaults need design. |
| Acceptance criteria | The product must be assessed for fidelity, reproducibility, and traceability. | Criteria and evaluation methods need design. They are not automatically user settings. |

Multiple executions do not imply concurrent execution or voting. Matching outputs do not establish fidelity. Output comparison and checking against the source have different purposes.

## Provisional design

The user approved the [conceptual diagram in the development README](../readme-dev-v0.1.md#provisional-conceptual-pipeline) as a starting point. The diagram separates these roles:

| Conceptual role | Purpose | Unresolved boundary |
|---|---|---|
| Input delivery | Make relevant source content available to a model. | Input paths, processing units, context, and verification of received content. |
| Model execution | Perform the requested operation with the user's supported model and execution settings. | Supported choices, defaults, units of work, constraints, and execution interfaces. |
| Comparison and source check | Identify disagreement and check information against the paper using the selected supported policy. | Comparison units, policy set and default, source access, automated checks, and human review. |
| Handoff | Provide the user's selected deliverable mode to its intended user or model. | Default mode, detailed behavior, formats, source links, and actual delivery of text and images. |

These roles do not prescribe required stages, interfaces, or an execution order. Source links, execution state, security, usage, and cost apply across the roles.

All three deliverable modes are required user choices: a transcript with source images, a source-aware reading workflow, and both together. Their implementation remains to be designed. Saving an image or adding a Markdown image link does not establish that a receiving model can inspect the image.

## Technology candidates

Go was proposed as a candidate. The user requested its installation to try it. Go is installed, but it is not the final language selection. Rust and Python remain alternatives. No application framework or dependency set is selected.

A GUI is an established requirement. It must help users understand variables, choices, defaults, and the effects of combinations so that they can actively adjust supported settings. Control layout, explanations, and interaction details still need design.

The screen implementation is not limited to static HTML or a particular language or framework. React, TypeScript, and other suitable technologies may be used. Frontend technology can be selected separately from the execution layer, where Go remains a candidate. This does not select React, TypeScript, or any other framework. GUI implementation technology and handoff formats such as HTML, JSON, or Markdown are separate decisions.

## Access preference

Use of existing subscriptions is the initial preference. API use remains an option. No provider, account route, billing arrangement, or automatic fallback from subscription access to paid API access is selected.

Current authentication, available models, usage limits, and costs have not been verified for a project workflow. A local environment file does not establish authentication. Required variable names and the method for loading `.env` remain open.

## Confirmed evidence and limitations

These observations concern this project's initial setup. They are not model or fidelity evaluations.

| Item | Basis | Confirmed scope and limitation |
|---|---|---|
| Go installation | User terminal output and a local `go version` check on 2026-11-13. | `go version go1.27.4 darwin/arm64`. This confirms the available toolchain command. No project build or application behavior has been tested. |
| Git initialization | User report and local Git status on 2026-11-13. | Local repository on `main`, with no commits at the time of the check. This does not indicate publication. |
| Environment file exclusions | Local `.gitignore`, Git status, and ignore checks. | `.env` and `.env.*` are excluded, except `.env.example`. `.DS_Store` is also excluded. These rules do not establish security of all future files or Git history. |
| Environment placeholders | Files created during initial setup. | `.env` and `.env.example` initially contain comments only. No credential or application configuration schema was supplied. |
| Design review | User direction in the current discussion. | The conceptual diagram, user configuration with defaults, GUI purpose, and all three deliverable modes were accepted. This establishes requirements, not implemented capability. Detailed design decisions remain open. |

No model run, input-delivery trial, or source-fidelity evaluation has been performed for this project. No evidence establishes that the proposed workflow avoids all omissions or distortions. Reproducibility and traceability also need explicit acceptance criteria.

## Research background

The supplied task plan refers to earlier tool research. This draft does not carry earlier tool recommendations or extractor evaluations into the new design. No researched tool is an adopted dependency. No new external tool comparison was performed for these drafts.

Future research should address a specific open design question. Findings must distinguish documented capability from behavior verified for the intended workflow.

## Deferred proposals

The supplied task plan contains the following historical proposals. They remain discussion material and do not constrain the independent design.

| Proposal | Current status |
|---|---|
| Terra checks page images and extracted text together. | Deferred. The model, input path, and need for extracted text remain open. No superiority claim is established. |
| Start an evaluation with six pages and expand it to 16 pages. | Deferred. This is not an approved evaluation protocol or sample requirement. Future evaluation must follow the selected workflow and acceptance criteria. |

## Review boundary

These documents are now at the design-document review checkpoint. The user should check the boundary between established direction and provisional design, identify missing requirements, and correct any interpretation that changes the intended workflow.

The user can set the order and priority of the remaining questions in [User choices and remaining design decisions](open-design.md). Review must distinguish established user choices from details such as defaults, constraints, and implementation mechanisms. Approval of this draft does not settle those details or authorize project implementation or model evaluation. Document completion and design completion are separate milestones.
