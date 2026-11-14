# Design status

Status: Confirmed requirements recorded; detailed design remains open.

Updated: 2026-11-14.

Project version: `v0.2.1`.

## Scope and basis

This document records the current design of `Paper-EaTER-PANnel`. Its basis is the [development README](../readme-dev-v0.1.md) and the user's directions in the current discussion.

The user approved the conceptual diagram and authorized these design drafts. The user also directed that the new design remain independent of the previous project and that its records not be consulted further for this work. Previous extractor evaluations, recommendations, and processing rules are therefore not included as a basis for this design.

This document describes the current understanding. It is not an implementation specification. The design remains incomplete.

## Status terms

| Status | Meaning |
|---|---|
| Established direction | A direction accepted by the user. Details can remain open. |
| Confirmed evidence | A local observation with a stated scope. It does not establish product capability beyond that scope. |
| Provisional design | A proposal for further discussion. It is not a selected implementation. |
| Open decisions | Product design details that still need a decision or supporting information, such as defaults, supported ranges, or implementation mechanisms. This status does not mean that user choice is undecided. |

Design status and user configurability are separate dimensions. For example, letting a user set execution count is an established requirement. The 1/3/5 total-call choices are established; the default still needs design. A user's choice for a task is not an unresolved product design decision. Internal architecture and security policies are not automatically user settings.

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
| Public repository | Repository setup is complete (issue #14). Keep local secrets separate from files intended for publication. |
| Version control workflow | Use project version `v0.2.1`. Create `dev` from `main` and `big-pic-design` from `dev`, then continue current design work on `big-pic-design`. This is the requested branch workflow, separate from the setup observations below. |
| Integration scope | Exclude `caffeine-pour-over` integration from current work. |
| Collaborative review | Present reviewable drafts. Obtain user direction at each agreed checkpoint. Do not treat silence as agreement or repeatedly request approval for accepted decisions. |

## Decisions confirmed on 2026-11-14

Basis: explicit user answers in the design conversation, recorded at the user's request. These are requirements, not implemented or evaluated capabilities. The earlier temporary local discussion memo (`tmp-2026-11-13_0.1.md`) remains preserved; ongoing decisions belong in these design documents.

| Topic | Confirmed decision and remaining boundary | Related issues |
|---|---|---|
| Audience and purpose | Existing LLM users who repeatedly study papers and need precise understanding, including people with limited computer skills. Support understanding comparable to direct reading; this is a goal, not a verified guarantee. | [#1](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/1), [#13](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/13) |
| First version | Wrap LLM-assisted PDF documentation with a minimal GUI. Preserve original language, wording, content order, numbers, equations, figures, tables, captions, and references. Preserve human-readable characters, complete figures, captions, line breaks, and paragraph boundaries; layout cleanup must respect these requirements; do not add translation, summaries, or explanations to the documented source. | [#1](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/1), [#8](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/8) |
| Consumers and handoff | Give equal priority to reading inside the app and use by another LLM. Users download and manually transfer the result. Packaging and image delivery still need design. | [#8](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/8) |
| Inputs and linked material | Start with PDF and reuse existing text; consider OCR where needed. Preserve figures, captions, supplementary figures, and their relationships. If external retrieval is added, list linked material for selection. The latest direction prioritizes local inputs and defers web full-text/supplementary retrieval as a possible later feature; it is not a first-version requirement. | [#6](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/6), [#7](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/7) |
| Execution and visibility | Support multiple papers and parallel LLM calls toward a result. Show queue progress in a near-real-time Dashboard. Users select whole-paper or partial scope and 1/3/5 vote configurations. The vote count is the total number of independent calls for that scope, not a per-model multiplier or repeated turns in one conversation. Each call has a user-selectable CLI and model. Initially populate all calls with the same setting, then allow individual changes; all calls may use the same model. Content-affecting disagreement marks the affected portion pending even when a majority agrees. Scheduling, detailed comparison rules, and limits remain open. Multiple calls do not establish a correct answer. | [#3](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/3), [#4](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/4), [#9](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/9) |
| Review | Mark uncertain items `pending` without stopping ongoing work, other portions, or other papers. Users may review pending items or start independent reruns while remaining work continues. Distinguish processing completion from review completion in the Dashboard. Offer optional in-app conversation with a CLI-based LLM in a workspace while inspecting source images. Include questions and selectable answers during conversation. Show the source image and before/after changes; user selection of `Apply` updates the document and completes review for that item. Conversation alone must not apply a change or complete review. | [#5](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/5), [#9](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/9), [#11](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/11) |
| Environment and access | First version runs locally on macOS with a browser UI and local workspace/CLI execution. Support both Codex CLI and Claude Code; this does not require using both on every task. Authentication and integration feasibility remain to be investigated. Local execution does not imply that model inputs stay on the computer. | [#2](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/2), [#10](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/10), [#11](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/11) |
| UI and later scope | All interface text, including controls, statuses, guidance, and errors, is English. Preserve source-document language. Compare LibreChat and assistant-ui; neither is selected. Multilingual UI is deferred. RAG document search is a possible later feature and a comparison consideration, not a first-version requirement. | [#11](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/11) |

All three product deliverable modes remain required. The first-version documentation scope and optional review chat do not define the complete future source-aware reading mode. Manual downstream handoff is separate from the app's CLI-based review conversation.

`pending` denotes unresolved content review, not queue waiting. Pending review does not pause document or batch processing. Processing can finish while review remains pending, and the Dashboard must distinguish those outcomes. The detailed execution state model, completed-review label, aggregation rules, and treatment of unresolved exports remain open. No retry count, automatic correction policy, numeric limit, or framework is selected here.

The user requested these decisions in both local design documents and related GitHub issue comments. Comments summarize the decisions; this document and open-design.md maintain the consolidated record. Publication status is recorded below after posting.

## Follow-up clarifications on the eleven design topics

Basis: the user's subsequent answers to topics 1–11 and explicit clarification of local storage versus model-service transmission. These refine the earlier decisions above.

- **Execution (topics 1–2):** Users choose whole-paper or partial processing and a 1/3/5 vote configuration at the start. The user clarified that 3 votes means three independent calls in total for the selected scope, not three turns within one conversation and not three calls per selected model. When pending content appears, offer an independent run with a fresh scope, model, and Codex/Claude route selection; either the affected portion or the whole paper may be rerun. Repeated runs aim to increase confidence. Do not infer three distinct models from three votes. The user selected pending review for any content-affecting disagreement, including numbers, signs, omitted text, and figure associations; majority agreement must not automatically finalize that portion or hide dissenting output. Exact comparison/alignment rules remain open. More runs may reveal disagreements; fewer pending items in a single run do not establish higher fidelity. The user confirmed per-call CLI/model selection: initially fill calls with the same setting and allow individual overrides, including repeated use of one model. The initial model/CLI default is not selected. The relationship between rerun proposals and Apply still needs design.
- **Comparable results (topic 2):** Agree on a common result format before execution. Preserve the paper's section organization, including the abstract, with figures separately accessible and connected to their captions. The comparison screen must show the actual PDF region and the different outputs for that region. The common conceptual representation is now accepted as recorded below; detailed schema fields and the alignment mechanism remain to be specified.
- **Input scope (topic 3):** English academic papers, including review papers with variable structure, normally in their online PDF form rather than scans of physical printouts. Expected batches do not exceed ten papers and use local computing. Ten is a workload assumption, not an enforced application limit. OCR support for exceptional inputs remains to be decided.
- **Deferred choices (topics 4 and 6):** Export packaging and source-navigation precision are explicitly on hold. Detailed cancellation, recovery, retry, and resume policies are also deferred; do not silently assign defaults.
- **Workspace (topic 5):** Use one user-designated local storage root. Users can configure a preferred location within their own directory as the default storage path; do not hard-code a project-owned output location. The initial fallback path and behavior when changing this setting remain open. Each processor LLM call sees only one paper (or its selected portion), without context from other papers. A multi-paper batch consists of separate per-paper processing; shared storage must not imply shared processor context. Later cross-paper integration and use are left to the user, not part of the processor workflow. This does not change the established 1/3/5 independent-call configuration. Coding agents/LLMs must be able to modify result files, including final directory and file names. The design must account for renames when tracking results and source links. The on-disk organization within the common root, edit permissions, and whether/how user confirmation applies to filesystem renames remain open; the existing Apply requirement for pending-content corrections remains in force.
- **Security and setup (topics 7 and 9):** Include security, API/login integration planning, installation support, manual user-input steps where needed, and encryption. What is encrypted, credential storage, and concrete authentication mechanisms remain design work. This does not select a first-version API route or a budget/retry policy. Provide an English `ABOUT` page for setup and explanatory guidance; detailed onboarding remains open.
- **Storage and network (topic 8):** Keep files and results locally. The user explicitly permits sending necessary inputs to the selected model service. No external hosting or publishing is requested. Finding full text or supplementary material on the web is a possible later feature, replacing the earlier assumption that selected linked resources must be fetched in the first version. Preserve source links even when retrieval is deferred. Previous execution results are retained until manual deletion by the user; automatic cleanup is not supported. Detailed deletion controls and handling of linked assets remain open.
- **UI (topic 10):** Build the application's own screens, using a chat interface such as LibreChat where needed. LibreChat and assistant-ui remain candidates, not a mandate to adopt an entire chat platform as the application shell.
- **Acceptance (topic 11):** Preserve human-readable characters, entire figures, captions, line breaks, and paragraph boundaries. This narrows the earlier permission to reflow PDF layout. The distinction between visual wrapping and meaningful line breaks needs examples and an explicit rule; no destructive normalization is authorized by default. Reference cases, assessment method, and thresholds remain open.

## Pending rerun options clarified on 2026-11-14

Basis: the user requested several choices within pending review and accepted app-proposed reruns as one optional route.

- Offer partial rerun and whole-paper rerun (the user's total rerun). Whole-paper scope refers to the affected paper, not the batch.
- Let users select 1/3/5 total independent calls for the rerun and configure CLI/model per call. Scope and call count are separate settings.
- Also offer an app-proposed rerun: propose the scope and CLI/model configuration, then obtain user approval before execution. Users may instead configure a rerun directly; the proposal route is not mandatory.
- A pending item is the starting point for a scope recommendation, not a scope unit alongside page range or document element. The app must offer recommendations using those units or other supported units. Users can accept or modify a recommendation, or directly select a scope without first requesting one. Additional scope units and recommendation rules remain open.
- The scope-selection UI must let users visually compare candidate scopes and the source content each includes before choosing. This requirement applies to app recommendations and direct user selection. The concrete layout and visual encoding remain design decisions.
- Execution approval does not apply document changes or complete content review. The existing Apply requirement remains in force. Detailed alignment of rerun outputs and generation of change proposals still need design.
- When a rerun scope includes user-edited content, show the overlap and let the user choose for that execution: include the edited portions for comparison, or exclude them from processing. The confirmed default is to include them, preserve the current edited document, and retain the new outputs separately for comparison. Only user-selected changes confirmed with Apply update the current document. Exclusion must be reflected in the displayed effective processing scope; a whole-paper selection with exclusions is not an unrestricted whole-paper rerun. The result-retention policy below also applies to these outputs.
- The pending action list is not exhaustive. Detailed controls, partial-selection interaction, defaults, and any future allowance for automatic extra calls without approval remain open. This decision does not authorize such automatic calls.

## Result retention clarified on 2026-11-14

Basis: the user selected preservation of previous results with manual deletion only.

Retain previous execution results until the user manually deletes them. Do not automatically delete results based on age, execution count, or storage usage. Detailed deletion controls and handling of linked assets remain to be designed. This decision concerns local execution results; it does not define retention by external model services.

## Accepted internal representation

The user accepted the proposed common internal representation as the current design baseline. Future changes belong to explicit design updates; the baseline is not an unresolved choice.

- Document structure preserves the source order and section hierarchy, including the abstract. Body text is organized into sections and paragraphs, not stored conceptually as one undifferentiated body block. Users must be able to view content at paragraph granularity within its section context.
- Content elements cover text, equations, figures, tables, captions, and references. Figures remain separately accessible.
- Source mapping associates elements with their PDF pages and regions.
- Relationships represent figure-caption links, in-text citation-reference links, and other source relationships.
- Uncertainty records reading uncertainty, possible omissions, and the associated source locations without adding commentary to the transcribed source.
- Provenance identifies the run, CLI, model, and processing scope for each result.

Outputs are aligned using corresponding source regions for comparison. Differences in section or paragraph segmentation must be handled; uncertain correspondence is marked pending for review. Detailed alignment algorithms, field definitions, identifier conventions, serialization details within the accepted file formats, and source-coordinate conventions still require specification within this accepted baseline. Export formats and packaging remain deferred. Acceptance of this representation does not authorize implementation or model evaluation.

## Comparison layers and figure review

Basis: the user distinguished structure from content within that structure, clarified provenance as metadata, and accepted human review of every figure because figures are important.

- Compare in two conceptual layers: first align document structure and element relationships, then compare content within corresponding elements. Paragraph content includes sentences, characters, numbers, and symbols. Detailed alignment and disagreement rules remain open.
- Provenance is metadata about generation conditions. Different run, CLI, or model values are not themselves source-content disagreements. Metadata remains available for traceability; source mapping and relationships still require correctness checks.
- Every figure must receive human review, even when automated comparisons find no disagreement. Review checks figure identity against the source, inclusion of the complete figure area, and the correct caption association. Automated checks may assist but do not replace this review.
- Figures awaiting human review remain pending without blocking processing. The UI must distinguish mandatory figure review from a detected discrepancy; pending does not by itself mean that a figure is incorrect.
- Detailed figure-review controls remain to be designed, including confirmation when no correction is needed. Actual document corrections still require Apply. This requirement does not extend mandatory review to all tables or equations.

## Structured result inspection and approval

Basis: the user clarified that inspection and approval must cover everything in the selected result that is subject to approval, not only the figure and caption. The internal structured output should be available in this interface.

- Let users select a result and inspect the full approval scope through its structured representation. Include the extracted paper title, section/paragraph content and other content elements, source mapping, relationships, uncertainty, provenance, citation information, and proposed result file/folder names or renames where present.
- Distinguish source-derived bibliographic information (such as title and citation fields) from execution provenance metadata and proposed filesystem changes. Their presence in one inspection interface does not make them the same data category.
- Make every item subject to approval visible and inspectable before approval, including proposed changes and relevant current values. Do not restrict inspection to figure/caption previews or apply changes outside the displayed approval scope. A structured tree, panels, or other navigation may be designed; showing structured output does not require a raw JSON-only interface.
- Compare source-derived information with the corresponding source. Show proposed file/folder names and renames as changes to generated result artifacts, rather than as paper content. Citation fields, naming rules, and citation formats still require detailed design.
- Detailed approval granularity, control labels, and whether content approval and filesystem changes share a transaction remain open. The earlier figure-only confirmation UI is superseded by this broader inspection requirement. Mandatory human review of every figure remains in force; this does not establish a mandatory separate approval for every text element.

## Naming convention and proposed workspace structure

Confirmed: the first section of result inspection is the paper title. Bibliographic information supports both citation and file naming. The user specified the filename stem `<년도>_<저널>_<약칭>__<타이틀>_<기타 사항>` (year, journal, abbreviation, title, other details). Preserve this order and the double underscore before title. The abbreviation field uses the paper-stated name of a method, tool, database, or similar named resource first, preserving its original spelling. If no such name is available, use a user-defined short paper identifier. If neither is available, the app proposes a short identifier for user review in the filename approval interface. An app-proposed identifier must be distinguished from a name stated in the paper; it is not inferred source metadata. Selection among multiple eligible named resources remains to be designed. Optional-field handling, filesystem-safe normalization, and collision handling remain to be specified; do not invent missing metadata.

The user requested a concrete directory and file-format proposal, including separately stored paper elements and understandable metadata for proposed and approved changes. This reopens discussion of the local workspace layout and file extensions; it does not settle downstream export packaging.

Confirmed year rule: use the publication year in the official citation information for the input paper version. For a preprint, use the release year of the input preprint version. If the year cannot be established, use the literal filename value unknown-year and request user confirmation. Show the selected year and source evidence in the approval interface, with user correction available. Do not substitute PDF creation or download year.

DOI is included in bibliographic metadata. Record the DOI associated with the input version when available, with source evidence; do not invent a DOI or silently substitute a DOI for another version. DOI is not an additional filename field under the accepted naming convention. Detailed DOI validation and representation of related-version identifiers remain to be designed; external lookup is not authorized by this metadata requirement.

Confirmed journal naming rule: use a journal abbreviation only when a matching entry exists in the explicit mapping table config/journal-abbreviations.json. The table maps full journal names to filename abbreviations and is initially an empty JSON object, so the current fallback is the full journal name. Do not infer or generate abbreviations when no mapping matches. Matching normalization and future table maintenance remain detailed design work.

For the filename journal field, replace spaces with underscores after selecting the mapped value or full-name fallback. Preserve the full journal name with its original spaces in bibliographic metadata. For example, with the empty table, Nature Methods becomes Nature_Methods in the filename. For preprints, use the input version's repository name (such as bioRxiv, medRxiv, or arXiv); if the journal/repository cannot be identified, use unknown-journal and request user confirmation. The method/tool/database abbreviation field remains separate from this journal mapping.

The user accepted the proposed workspace layout and file formats as the current design baseline. Use a per-paper directory named with the specified stem, source/ for the input PDF, runs/<run-id>/calls/<call-id>/result/ for independently retained call outputs, current/ for the current approved result, and review/ for proposals and decision history. manifest.json holds stable paper identifiers and path mappings; run.json records execution scope, configuration, and status; provenance.json records each call's generation conditions.

The common result layout is accepted:

- <paper-name>.md: a readable whole-paper document starting with the title.
- document.json: section/paragraph hierarchy, stable element IDs, source mapping, relationships, and uncertainty.
- bibliography.json: extracted bibliographic fields including DOI when available, source evidence, and uncertainty; citation.bib is generated from confirmed bibliographic information.
- sections/<section-id>.md: section-level text. Paragraphs remain individually addressable by stable IDs, but are not separate files by default.
- figures/<figure-id>/: figure image, caption.md, and figure.json for source mapping and relationships. Preserve original image formats where feasible; use PNG for rendered PDF regions.
- tables/<table-id>/: table.json for cells, merged-cell structure, and notes, plus a source image. CSV is an optional additional representation for simple tables.
- equations/<equation-id>/: a .tex expression, source image, and JSON for source mapping and uncertainty.

Review proposals are stored as review/proposals/<proposal-id>.json; review/events.jsonl records decisions and application outcomes; review/review-summary.md provides a human-readable account. Approval records identify the selected run/call, exact result revision, element IDs and scope, current/proposed values, source evidence, proposed renames, decision and timestamp, and application outcome. User approval and successful application are distinct events. Stable identifiers and revisions preserve traceability across path changes. The UI must make these records understandable without requiring users to read raw JSON.

This is an accepted design baseline, not implemented behavior. Detailed field definitions, selection among multiple eligible abbreviation candidates, missing-field handling for other fields, filename normalization, collision handling, and concurrency behavior remain to be specified. Downstream export packaging remains deferred. Previous results remain until manual deletion.

## Full-title filename conversion

Confirmed: use the input version's full title, preserving case, numbers, and scientific notation; replace spaces with underscores in filenames. Preserve the original title before conversion in bibliographic metadata. Do not automatically summarize or truncate; if the target filesystem length limit is exceeded, propose an alternative for user confirmation.

Use an explicit conservative mapping table. config/filename-title-mapping.json records the accepted formatting/preservation requirements and separately labels candidate mappings as proposals. The candidate code-point tokens for portability-sensitive characters are not a universal filesystem standard or an approved final replacement vocabulary. Actual validity depends on the target filesystem; validation, reserved names, trailing characters, collisions, and mapping-table versioning remain detailed design work.

Any filename conversion must be shown with the original title, the proposed filename, changed characters or notation, and the reason, then confirmed by the user before application. Confirmation may be part of the existing naming approval interface; this does not require a separate modal for each character. Unknown or unsupported cases require a reviewed fallback, never silent deletion or guessed scientific meaning.

Preserve Greek letters, Unicode subscripts/superscripts, and other representable mathematical notation. Do not silently transliterate Greek letters or flatten scripts, accents, combining marks, or mathematical typography. Some PDF notation uses positioning rather than Unicode characters; retain source evidence and structured notation and request confirmation of a filename representation if faithful direct conversion is unavailable. Do not assume every unusual Unicode character is invalid in a filename. Full-title preservation and conversion approval are requirements; candidate replacement tokens still need review.

Documentation upkeep: reconcile accepted decisions from this conversation into the existing README, decision record, and open-design tracker, including superseded statements. The user requested completeness and consistency of these documents, not a separate feature-list artifact. Documented requirements are not claims of implemented features.

## Documentation checkpoint and deferred selection UI

The user has supplied enough product direction to prepare technical design proposals. This is not a decision-complete implementation specification. The user explicitly requested documentation only, with no implementation.

Direct drawing of a selection region on the PDF remains deferred. Subsequent user clarification establishes page-range and document-element selection, app recommendations based on pending items, independent direct selection, and visual comparison of candidate scopes. This supersedes the earlier unapproved status of page-range selection. It does not approve silently accepting an app recommendation or executing it without user approval. Detailed selection controls and source mapping remain to be designed.

Remaining user constraints include automatic extra-call allowances. Result retention is settled as manual deletion only; detailed deletion controls remain to be designed. The agent should propose comparison/alignment, detailed schema fields within the accepted internal representation, CLI integration, security/encryption mechanisms, layout, and evaluation methods. Export packaging/source-navigation precision and detailed recovery policies remain explicitly deferred. These open questions do not prevent recording the confirmed requirements.

## GitHub decision-comment publication

Published on 2026-11-14 at the user's request. Each product-design issue remains open; setup issue #14 was not changed. At the time of comment publication, the local document edits had not yet been committed or pushed.

| Issue | Published record |
|---|---|
| #1 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/1#issuecomment-6872051097) |
| #2 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/2#issuecomment-6872051805) |
| #3 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/3#issuecomment-6872052578) |
| #4 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/4#issuecomment-6872053323) |
| #5 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/5#issuecomment-6872053907) |
| #6 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/6#issuecomment-6872054638) |
| #7 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/7#issuecomment-6872055468) |
| #8 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/8#issuecomment-6872056222) |
| #9 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/9#issuecomment-6872057043) |
| #10 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/10#issuecomment-6872057688) |
| #11 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/11#issuecomment-6872058361) |
| #12 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/12#issuecomment-6872059061) |
| #13 | [Decision comment](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/13#issuecomment-6872059874) |

## Adaptability

The wrapper should support changes in models and CLI or API access. The design must consider differences in model capability and in the inputs that each access path can deliver.

User model selection and adaptability are established directions. Codex CLI and Claude Code are selected first-version access routes. The model catalog, combinations, defaults, adapter interfaces, API scope, and compatibility approach still need design.

## User configurability and design status

| Topic | User configurability or behavior | Design status |
|---|---|---|
| Model selection and combination | Users select a model or supported model combination. | Established choice. Codex CLI and Claude Code are required; model catalog, combinations, capability explanations, integration, and defaults need design. |
| Execution count | Users set the number of executions for a defined unit of work. | Established choice. Whole-paper/partial scope and 1/3/5 configurations are established. Per-call CLI/model selection with identical initial settings and individual overrides is established. Exact partial units and initial defaults need design. |
| Concurrency | Users set how many executions may run at the same time. | Established choice. Default and resource, access, usage, and cost constraints need design. |
| Conflict-resolution policy | Users select a supported procedure for handling disagreement. | Established choice. Policy set, default, comparison triggers, and source checks need design. The pending review and user-confirmed Apply flow is established above. Voting through 1/3/5 configurations is established. Content-affecting disagreement marks the affected portion pending regardless of majority agreement; detailed detection and alignment rules remain open. |
| Deliverable modes | Users choose a transcript with source images, a source-aware reading workflow, or both. | All three modes are required. Default mode, detailed behavior, and delivery mechanisms need design. |
| Input delivery | The workflow must establish what content a model receives. Which input controls users need remains to be designed. | PDF, text, and image paths and verification mechanisms remain design decisions. |
| Source relationships | Users need to connect results to images, captions, body text, and source locations. | Representation, location precision, and navigation behavior need design. They are not automatically configurable settings. |
| Internal representation and handoff format | The selected deliverable must reach its consumer. Which export-format controls users need remains to be designed. | The conceptual internal representation is accepted, including section and paragraph structure, content elements, source mapping, relationships, uncertainty, and provenance. Detailed schema fields and serialization conventions within the accepted local file formats remain to be specified. Handoff formats, including JSON, HTML, and Markdown, remain deferred design decisions. |
| Execution state and provenance | The workflow must address status, failure, cancellation, interruption, resumption, reuse, and input/output records. | Near-real-time Dashboard and optional pending review chat are established. State model, recovery, remaining controls, and provenance detail need design. |
| Security | Keep secrets out of tracked files. Authentication and permission interactions need design. | Environment file exclusions are in place. Authentication, transmission, logging, and GUI content security remain design decisions, not automatically user settings. |
| Implementation technology and GUI | A GUI must support informed, active user choice. | Local macOS browser UI, English interface, and in-app CLI review are established. LibreChat and assistant-ui are candidates; layout and integration need design. Go is available as a candidate. |
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

Use of existing subscriptions is the initial preference. API use remains an option. Codex CLI and Claude Code are selected access routes. Account setup, API support in the first version, billing arrangements, and fallback behavior remain open; automatic paid fallback is not selected.

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

The supplied task plan refers to earlier tool research. This draft does not carry earlier tool recommendations or extractor evaluations into the new design. No researched tool is an adopted dependency. A preliminary UI documentation review occurred during the current discussion. The user retained only LibreChat and assistant-ui as comparison candidates; no runtime, footprint, or CLI integration test has been performed.

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
