# User choices and remaining design decisions

Status: Confirmed requirements incorporated; remaining design work tracked.

Updated: 2026-11-15.

Project version: `v0.2.1`.

## Resume checkpoint on 2026-11-15

Read [the conversation handoff](design-status.md#resume-here-conversation-handoff-on-2026-11-15) before continuing. It consolidates the accepted requirements and distinguishes them from unapproved proposals. The last six-stage workflow explanation was NOT finally approved by the user. Earlier individual decisions remain valid.

The [preserved six-stage proposal](design-status.md#preserved-six-stage-workflow-proposal-for-the-next-review) includes the step-by-step behavior, proposed state sketch, unapproved branches, and an opening review question for the next conversation. It was retained at the user's request without promoting it to an approved design.

Review exit and Apply transitions are deferred until a complete flowchart and composed functions/UI allow UX assessment. `Finish review`, `Back to review`, change-set freezing, no-change completion, and exact unlock/failure transitions remain proposals. Proceeding with pending items is now permitted as an explicit, non-recommended override; resolving all pending items before finalization remains the default. See the [follow-up decision](design-status.md#follow-up-decision-pending-override-and-deferred-workflow-approval). Rerun during review is already supported by the accepted requirements; it does not unlock the document or automatically apply new candidates. Do not treat the six-stage explanation as an accepted state machine.

This tracker and design-status.md are the current local record; historical issue drafts/comments have not been synchronized with these latest decisions. Documentation only; implementation and model evaluation remain outside the authorized scope.

## Purpose and use

This document separates user choices and intended product behavior from remaining design decisions for `Paper-EaTER-PANnel`. Read it with [Design status](design-status.md) and the [development README](../readme-dev-v0.1.md).

The product must provide defaults and let users change supported settings. Model selection and combinations, execution count, concurrency, conflict-resolution policy, and all three deliverable modes are established user choices. The 1/3/5 total-call choices and per-call CLI/model controls are established. Initial defaults, other limits, compatibility constraints, and implementation mechanisms still need design. A user's choice for a task is not an unresolved product design decision.

A GUI is required to help users understand these variables, available choices, and the effects of combinations. It must support informed, active use of defaults and settings. Screen implementation is not limited to static HTML or a specific language or framework. React, TypeScript, and other suitable technologies may be used. Frontend technology and execution-layer technology can be selected separately.

The table does not define an implementation schedule, schema, interface, or evaluation protocol. Intended behavior is not a claim of completed implementation. Internal architecture, security policies, and acceptance criteria are not automatically user settings. The user can change the order and priority of the remaining design discussions. No previous project's architecture or evaluation boundary is a requirement here.

## User choices and design work

The [confirmed decisions](design-status.md#decisions-confirmed-on-2026-11-14) are the decision record for the current discussion. Do not reopen the local macOS browser app, English UI, both CLI routes, equal human/LLM consumer priority, manual downstream handoff, source-preserving documentation, user-confirmed review changes, or local storage with permitted selected-model input transmission as unanswered questions.

The [follow-up clarifications](design-status.md#follow-up-clarifications-on-the-eleven-design-topics) record the latest answers and supersede earlier assumptions about first-version web retrieval and unrestricted layout reflow.

The full product retains three deliverable modes. The first version focuses on PDF documentation and optional in-app review conversation, not a complete specification of every future reading task. Existing PDF text must be reused; OCR need and implementation remain to be investigated. LibreChat and assistant-ui are the only current UI comparison candidates. Multilingual UI is deferred; RAG search remains a possible later extension.

## Pending rerun controls

Confirmed: pending review offers partial rerun and whole-paper rerun, a fresh 1/3/5 total-call selection, and per-call CLI/model configuration. An app-proposed scope and CLI/model configuration, reviewed and approved by the user before execution, is another optional route. Users can also configure reruns directly. Scope, call count, and configuration route are separate choices, not mutually exclusive actions. See the [decision record](design-status.md#pending-rerun-options-clarified-on-2026-11-14).

Confirmed scope selection: offer page-range and document-element selection. Use a pending item to propose an appropriate scope; it is not a competing scope unit. Users can accept or modify the proposal, or select a scope directly without requesting a proposal. The UI must support visual comparison of candidate scopes and the source content each includes, for both recommended and directly selected scopes.

Confirmed handling of user edits: when the rerun scope overlaps user-edited content, show that overlap and offer a per-execution choice to include the edited portions for comparison or exclude them from processing. Default to inclusion while preserving the current edited document and retaining new outputs separately. Only selected changes confirmed with Apply update the document. If portions are excluded, show the effective processing scope, including exclusions from a whole-paper selection.

Remaining design: additional scope units, recommendation rules, source mapping, detailed visual comparison and partial-selection interaction, additional pending actions, other defaults, and detailed alignment and change proposals for rerun outputs. Confirmed retention policy: preserve previous execution results until the user manually deletes them; no automatic cleanup by age, execution count, or storage usage. Detailed deletion controls and handling of linked assets remain open. Execution approval is separate from Apply for document changes. Automatic extra calls without approval are not authorized by this decision; any future allowance remains open.

## Internal representation baseline

The [common internal representation](design-status.md#accepted-internal-representation) is accepted: section hierarchy and paragraph-level viewing, content elements, source mapping, relationships, uncertainty, and provenance. Body text retains section and paragraph structure. Source-region correspondence supports output alignment; uncertain correspondence is pending. Future conceptual changes require a design update. Remaining work specifies fields, identifiers, serialization, coordinate conventions, and alignment algorithms within this baseline; export packaging remains deferred.

## Comparison and mandatory figure review

Confirmed: compare structure first, then content within aligned elements, including sentences and characters within paragraphs. Provenance describes generation metadata; CLI/model differences alone are not content disagreements. Every figure requires human review of its identity, completeness, and caption association, regardless of automated agreement. Awaiting figure review is pending and must not block processing; distinguish it from a detected discrepancy in the UI.

Remaining design: alignment and comparison rules, visual figure/source comparison, review confirmation without a correction, and aggregation of review status. Corrections retain the Apply requirement. Mandatory human review of every table or equation has not been established.

## Structured result approval interface

Confirmed: users select a result and inspect its internal structured output and all items subject to approval. The scope includes extracted paper title, content and structure, source mapping, relationships, uncertainty, execution provenance, citation information, and proposed output file/folder names or renames where present. Make approval scope and changes inspectable; do not limit the interface to figure/caption previews. Distinguish bibliographic metadata, execution metadata, and filesystem proposals. Mandatory figure review remains required.

Remaining design: navigation of the structured result, detailed bibliographic fields and citation formats, naming rules, approval granularity, and transaction boundaries. Content changes and file/folder renames now require joint approval; transaction/rollback mechanisms remain open. Raw JSON display and a particular screen layout are not selected. Visibility of all approval targets does not imply a separate mandatory approval for every element.

## Naming and workspace layout

Confirmed filename stem: `<년도>__<저널>__<약칭>__<타이틀>__<기타 사항>`. The title is the first section in result inspection; bibliographic information also supplies naming fields. Confirmed abbreviation precedence: use the paper-stated method/tool/database or similar resource name, preserving original spelling; if absent, use the user-defined short identifier; if neither exists, the app proposes an identifier for user review. Distinguish app proposals from source-derived names. Selection among multiple eligible resource names, other missing/optional values, filename normalization, and collisions need specification. The user requested a concrete local directory and extension proposal, including proposed/approved-change metadata that people can understand. See the [proposal and decision record](design-status.md#naming-convention-and-proposed-workspace-structure). Local layout and extension discussion is now active; downstream export packaging remains deferred. The user accepted the source/runs/current/review layout and proposed file formats as the current baseline. This includes section Markdown files with addressable paragraphs, separate figure/table/equation assets, structured document and bibliographic metadata, BibTeX generated from confirmed metadata, and machine-readable approval events with a human-readable summary. Approval and successful application are distinct records. Remaining work concerns precise fields and implementation mechanisms, not whether to adopt this baseline.

## Publication year and DOI

Confirmed: the filename year is the publication year in the official citation information for the input version; for a preprint, use that input version's release year. If unavailable, use unknown-year and request user confirmation. The approval interface shows the year and its source evidence and permits correction. PDF creation/download dates are not substitutes. DOI belongs in bibliographic metadata when available, with source evidence; it does not add a filename field. Detailed DOI validation and handling of identifiers for related versions remain design work.

## Journal filename field and mapping table

Confirmed: use a mapped journal abbreviation only if config/journal-abbreviations.json contains a matching entry; otherwise use the full journal name. The mapping file exists as an empty JSON object, so no abbreviations currently match. Replace spaces in the filename journal field with hyphens; preserve the original full name in bibliographic metadata. Use the input repository name for preprints, or unknown-journal with user confirmation if unidentified. The method/tool/database abbreviation field remains distinct. Detailed matching normalization and future mapping-table maintenance remain to be designed. No automatic abbreviation generation is selected.

## Full-title conversion and documentation upkeep

Confirmed: full input-version title, original case/numbers/notation, spaces replaced with hyphens, and the original title preserved in metadata. No automatic truncation or summarization. Conversions require user confirmation of the original and proposed name; unsupported notation and length-limit cases require reviewed fallback proposals. Preserve Greek letters and subscripts/superscripts where representable; no silent transliteration, flattening, or compatibility normalization. Source-rendered notation must remain inspectable when plain Unicode cannot express it faithfully. See the [decision record](design-status.md#full-title-filename-conversion) and config/filename-title-mapping.json. Candidate character replacements are explicitly proposals, not yet approved conversion rules.

Remaining naming design: replacement vocabulary, target-filesystem validation, collisions, detailed topic-suffix vocabulary and unavailable-topic handling, multiple abbreviation candidates, and mapping-table versioning. Maintain the existing design documents against conversation decisions; no separate feature-list document is requested.

## Technical refinement draft now available

The [technical refinement draft](design-status.md#technical-refinement-draft-naming-revisions-comparison-and-review) supplies concrete proposals for Unicode/filename handling, mapping versions, collision/length validation, stable IDs and immutable revisions, approval scope and stale-result checks, structural alignment, content comparison, figure coverage, and UI/state separation. It also defines the investigation boundaries for CLI adapters, security, and acceptance examples.

These are reviewable engineering proposals, not newly accepted decisions or implemented capabilities. Naming conversion always retains the already accepted user-confirmation requirement. The mapping JSON now carries proposed categories, ordering, approval fields, and design examples; it is not an executable converter. Review next: detailed validation rules for the selected conservative portability policy and name-token vocabulary (name-first/code-point-second precedence is now confirmed), detailed topic-suffix rules, then revision/approval granularity. CLI integration feasibility and security mechanisms still need focused research. Deferred export/recovery topics have not been silently settled.

## Confirmed fallback precedence

When filename conversion is required, use character-name notation first (for example `[solidus]`), and explicit Unicode code-point notation such as `[U+002F]` if a reliable name representation is unavailable. If neither name nor code point is identifiable, use a numbered placeholder such as `[unknown-symbol-01]`. The computer selects the appropriate fallback level and constructs the complete proposed filename automatically. The user reviews and confirms the final proposal before application, regardless of which fallback levels were used. Do not request separate approval at each fallback step or for each individual character. Show all conversions and their levels within the final proposal. Preserve the original title and link placeholders to source location/image metadata; approval of a filename does not resolve uncertainty about the scientific content. Numbering scope and revision stability remain to be designed. Preserve directly representable scientific notation; unknown glyphs must not receive invented code points. The mapping file records this accepted precedence with proposed labels and code-point alternatives. Exact vocabulary formatting and unavailable-name conditions remain detailed design; the conservative portability policy is selected. Include cross-environment filename risks as conversion triggers and validate the actual destination. Detailed platform coverage and validation rules remain open; no ASCII-only conversion or universal compatibility guarantee is implied.

## Concise subject suffix

Confirmed: the filename uses `__` before the other-details suffix. An LLM proposes a very short subject/category descriptor at the specificity of the paper's provided keywords, grounded in the source. For general papers, use the subject alone; append preprint/review information after it only where applicable. Treat preprint status and review article type separately. Users can enter/edit identifying information, and the app can propose version/collision disambiguation when needed. Review and approve the complete filename; do not insert runtime or approval metadata automatically. An empty entry should receive a subject proposal, not automatic omission. No universal `v` fallback is established. Remaining design: exact vocabulary, missing-keyword handling, unavailable-subject representation, and justified length constraints. Preserve source keywords separately from the generated label.

## Collision suffix

Confirmed: use `-v<n>` at the end of the other-details field to disambiguate colliding filenames, without shortening the full title or overwriting an existing result. The computer proposes a candidate and the user confirms the complete final filename. Treat the collision counter separately from the input paper's publication/preprint version and execution revisions. Starting number, allocation scope, existing-version-token handling, and application-time collision checks remain detailed design.

## Shortening exception

Confirmed: when length constraints require shortening, propose a sufficiently shortened name and put the exact literal `shortend-file` last within the existing other-details field (not a separate field), before the extension and after any collision suffix (for example `...__topic-v2-shortend-file.pdf`). Include the marker, extension, collision suffix, and actual directory path in validation. The user reviews and approves the complete proposed result; no silent truncation. Preserve the original full title and record the approved name and exception reason in metadata. Detailed shortening strategy and numeric headroom remain open; do not invent a universal limit.

## Change-set approval

Confirmed: select candidates per paragraph, figure, table, and bibliographic field, including selections from different calls. Assemble them into a visible change set for final approval and Apply. Show related elements such as figure/caption together for review. Selection alone neither approves nor applies changes. Remaining design: dependency enforcement, transaction boundaries, and the transition from active review (Apply blocked) to final approved application.

## Single instance and active-review protection

Confirmed: only one application instance runs at a time; it may execute parallel papers/calls and CLI subprocesses internally. While a document is being reviewed, proposals can still be generated and shown, but Apply to that document is blocked. Preserve the current document and keep candidate outputs separate; other work continues. Application write paths must enforce the block, including app-mediated agent writes, rather than relying on a disabled UI button alone.

Remaining design: instance-lock scope, multiple-tab behavior, entry/exit rules for active review, explicit release-to-Apply interaction, and handling external filesystem modifications. No automatic unlock or Apply is authorized. A stale-revision check is a defensive mechanism outside this protection, not permission to update a document during review.

## Pending override: confirmed behavior and remaining detail

Default: resolve every pending item before finalization. Users may explicitly override this default after confirmation that pending regions remain. For an unselected pending item, choose a strict-majority result (more than half; e.g. 2/3 or 3/5) and show which result is selected and why in a popup-style notification. Without a strict majority, choose query 1 by original query order and warn that the choice is arbitrary. This does not replace explicit user selections or authorize automatic finalization during ordinary processing.

The [decision record](design-status.md#follow-up-decision-pending-override-and-deferred-workflow-approval) retains the unresolved details: voting scope/equivalence, missing results and unavailable query 1, notification and confirmation layout, override status/provenance, and the relationship to mandatory figure review. Review exit and Apply remain deferred for joint flowchart/UX review. Partial application and finalization with fallback-selected content must be shown as distinct cases in that design.

## Joint approval, completion, and clarification checkpoint

Confirmed: content changes and file/folder renames are approved together, with both visible in final approval. Processing, review, and Apply each have their own completion state; all must be complete for final completion. Their aggregation and the status of explicit pending overrides still need design.

The user requested a concrete explanation of review interruption/resumption before choosing selection-persistence and document-protection behavior. Selection persistence and document-protection behavior across interruption remain unresolved. The later termination decision below establishes close/exit choices. For linked changes, the later follow-up provisionally adopts grouping when separate application would make content or relationships inconsistent, with visible reasons and user confirmation; this is not a universal bundling rule. See the [decision record](design-status.md#follow-up-decision-joint-approval-and-completion-levels).

## Latest checkpoint: help and termination

Confirmed: add a `<?>` help icon beside pending-override notification/confirmation, with a concise explanation and compact diagram of the whole override process. Keep the required selection notification and arbitrary-fallback warning.

Confirmed: provide one-stop termination choices, informing users that closing the interface does not necessarily stop processing: continue in background; force termination without background processing; or wait for recoverable-state preparation and orderly exit. Defaults, close/quit triggers, subprocess shutdown, checkpoints, timeouts, and recovery guarantees remain to be designed. Selection persistence and review protection across exit/restart are not settled solely by this choice model.

Provisionally accepted: group necessary linked changes when separate application would break content/relationship consistency; show grouping reasons and included items for user confirmation. See the [latest decision record](design-status.md#follow-up-decision-override-help-termination-choices-and-provisional-dependencies).

Next: prepare an integrated flowchart and UI/function composition for UX review, preserving the unapproved status of review-exit/Apply transitions. Include override/help, dependencies, joint content/rename approval, separate completion levels, and termination choices. Detailed recovery was previously deferred; this follow-up opens the termination-choice requirements without settling all recovery mechanisms.

## Current checkpoint

The user has provided enough direction for technical proposals; not every remaining engineering question requires a user answer now. Documentation is authorized; implementation is explicitly excluded.

- **Deferred by the user:** direct PDF region drawing, output packaging/source-navigation precision, detailed cancellation/recovery policies, multilingual UI. Web retrieval and RAG remain later possibilities.
- **Still requiring user constraints when relevant:** automatic extra-call allowances and details of the partial-selection interaction.
- **Agent proposals required:** detailed schema fields within the accepted internal representation, comparison/alignment, CLI integration and setup, encryption/authentication mechanisms, UI composition, and quality-assessment methods.
- **Selection requirements now confirmed:** page-range and document-element selection, app recommendations based on pending items, independent direct selection, and visual comparison of candidate scopes. Direct PDF region drawing remains deferred. Recommendation rules and detailed controls still need design; recommendations must not silently become approved execution scope.

## Remaining design sequence

These numbers identify discussion topics, not GitHub issue numbers or a mandatory implementation order. Topics 1–11 have received initial answers; the remaining questions below refine those answers. Export packaging and detailed source navigation in topic 4, and recovery policies in topic 6, remain deferred. Local directory layout and file formats from topic 4 have since been accepted. Ask one question at a time, reuse answers across topics, and distinguish a request for a proposal from permission for automatic decisions.

| No. | Topic and related GitHub issues | User intent or constraints still needed | Agent investigation and design work |
|---|---|---|---|
| 1 | Execution counts and model roles — [#3](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/3), [#2](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/2) | Established: whole-paper/partial scope, 1/3/5 vote configurations, and independent pending reruns with fresh model/CLI selection. Vote count means total independent calls for the selected scope: 3 votes is three calls, not three turns in one conversation or three calls per model. Established: users assign a CLI and model to each call; initially all calls share the same setting and individual calls can be changed. Reusing one model for every call is allowed. Direct PDF region drawing is deferred. Page-range/document-element selection, app scope recommendations, direct selection, and visual scope comparison are established. Initial CLI/model defaults and detailed selection controls need design. | Propose partial work units, cross-unit context, and justified defaults with examples preserving total-call semantics and user-controlled per-call assignment. Supporting both CLIs does not imply calling both each time. |
| 2 | Comparison, integration, and pending decisions — [#5](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/5) | Established: a pre-agreed common format, paper sections including abstract, separately accessible figures, and PDF-region/output comparison. Established: any content-affecting disagreement marks the affected portion pending, even when a majority agrees. Still needed: precise structure-first alignment/content comparison rules and unreadable or single-run uncertainty triggers. Every figure requires human review regardless of agreement; provenance differences are metadata differences. Approved reruns are supported; automatic extra calls without approval are not authorized. | Define comparison units and detection rules consistent with pending review for content-affecting disagreement; do not replace this with majority-based automatic finalization. Preserve the agreed source-image, in-app chat, before/after, and user-confirmed Apply flow. Agreement is not source verification; 1/3/5 voting is selected, with pending review rather than majority-based finalization of disputed content. |
| 3 | Input coverage and workload — [#6](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/6), [#7](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/7) | Established: English online academic PDFs, including reviews; normally not physical-print scans; expected batches up to ten using local computing. Still needed: representative lengths/layouts and exceptional input support. Ten is not a hard cap. | Investigate text/image delivery, OCR, preprocessing, image scaling, context limits, and evidence of received versus inspected content. Treat web retrieval as a possible later extension; preserve links in local inputs. |
| 4 | Output and source navigation — [#8](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/8), [#7](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/7) | Explicitly deferred: export formats, packaging, and source-navigation precision. The conceptual internal representation is accepted, including section hierarchy and paragraph-level viewing; detailed schema fields and serialization conventions within the accepted local formats remain to be specified. | Specify the accepted internal representation for text, equations, tables, images, captions, references, uncertainty, and provenance; revisit output packages when that deferred topic resumes. Design page/region navigation and pending export treatment. Manual transfer is settled; packaging is not. |
| 5 | Workspace, retention, and reuse — [#9](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/9) | Established: one user-designated local storage root, configurable as the default path within the user's own directory; each processor call sees one paper or its selected portion only. Batches keep paper contexts separate. Later cross-paper integration is left to the user. Agents can edit result files and rename final directories/files. Still needed: initial fallback path, behavior when changing the default, implementation details of the accepted directory layout, permissions, rename approval controls, history fields, manual deletion controls, and reuse. Previous execution results must be retained until manual deletion; automatic cleanup is excluded. | Propose per-paper context isolation within shared storage, rename-safe provenance, history, and reuse conditions. Do not introduce cross-paper processor context or an integrated multi-paper workflow. Future RAG remains optional and outside current processing scope. |
| 6 | Queue and recovery — [#4](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/4), [#9](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/9) | Established: pending review does not stop ongoing work, other portions, or other papers. Review and independent reruns may occur while remaining processing continues. Dashboard distinguishes processing completion from review completion. Detailed cancellation, failure, retry, and resume behavior remains deferred. | Design states, dependencies, concurrency constraints, retries, and recovery scenarios. Separate execution waiting from review pending; define document-level status and completed-review labels. |
| 7 | Usage and automatic-call limits — [#12](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/12), [#2](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/2) | Usage/retry limits and first-version API scope remain unanswered. New requirements for security, encryption, API/login planning, and manual input steps are tracked under topics 8–9. | Verify route-specific capabilities/limits and propose measured, estimated, and unknown usage displays. Do not assume paid fallback or invent budgets. Model and call-multiplier settings are required context, not verified cost estimates. |
| 8 | Transmission and deletion — [#10](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/10) | Established: local storage; necessary input transmission to the selected model service is explicitly allowed. Web full-text/supplement retrieval is a possible later feature. Established result retention: manual deletion only, with no automatic cleanup. Still needed: sensitivity, detailed deletion controls and handling of linked assets, and encryption scope. | Map data flows, authentication, permissions, logging/redaction, and safe rendering. Local execution does not imply local model processing. |
| 9 | Installation and onboarding — [#11](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/11), [#10](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/10) | Established: an ABOUT page for guidance, setup/security planning, and manual input steps where needed. Detailed installation/login/update experience remains open. | Propose macOS installation, login guidance, launch, update, and missing/unavailable CLI behavior for nontechnical users. Verify feasible integration for both Codex CLI and Claude Code. |
| 10 | Screens and implementation technology — [#11](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/11) | Established: own application screens with chat UI such as LibreChat where needed. Still needed: concrete source/result/chat layout; compare LibreChat and assistant-ui without assuming a full-platform adoption. | Compare LibreChat and assistant-ui for footprint, CLI integration, questions/forms, source images, Dashboard integration, and later RAG potential. Propose frontend and execution-layer choices; no framework or language is selected. |
| 11 | First-version acceptance — [#13](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/13), [#1](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/1) | Established: preserve human-readable characters, entire figures, captions, line breaks, and paragraph boundaries. Still needed: meaningful versus visual line-break rules, reference cases, reviewers, and assessment method. | Propose representative cases, references, review procedures, omission/distortion categories, and justified thresholds. Distinguish fidelity, reproducibility, and traceability. Evaluation design does not authorize model runs. |

## Decision records and next review

When a design question is resolved, record the decision and its basis in [Design status](design-status.md). Update the numbered sequence to show remaining design work without renumbering established discussion references. Keep supported choices and defaults distinct from the values a user selects for a task. Selecting a default does not remove user choice. Selecting one variable does not resolve related variables.

Fidelity means preserving the intended source information. Reproducibility concerns consistency under stated conditions. Traceability concerns the ability to connect a result to its source and processing history. Agreement between repeated outputs does not establish fidelity. Observing no errors in a sample does not guarantee error-free delivery.

The next review should identify missing topics, incorrect status assignments, and any confusion between user controls and internal design. The user does not need to resolve every remaining detail before accepting these documents as an accurate record of the current design discussion.

The user requested decision comments on related GitHub issues as well as these local documents. Posting a decision summary does not complete a design issue; publication references are recorded in design-status.md. The temporary discussion memo remains unchanged. Subsequent answers should update the decision record and the corresponding remaining question together.

## Pre-implementation issue audit and agreed work order — 2026-11-15

The user selected the next work order: (1) inspect user scenarios through an integrated flowchart and wireframes, then (2) decide result acceptance boundaries, including mandatory inspection, permitted override scope, and distinct completion labels. This is design work, not authorization to implement or run model evaluations. Preserve unsettled transitions as proposals in the visual artifacts.

Read-only audit of the live GitHub issue bodies and completion criteria: #1–13 remain open; #14 is closed. No additional design issue currently satisfies all its existing completion criteria. Partial design progress is not implementation completion. No GitHub issue was edited or created during this audit.

| Issues | Suggested update classification | Remaining boundary |
|---|---|---|
| #1, #3, #5, #7, #8, #9, #11 | Partial design completion; update accepted requirements and outstanding work | Full flows/defaults, comparison/alignment, source navigation, schema/handoff, lifecycle and reviewed wireframes remain incomplete as applicable |
| #2, #4, #10, #12 | Requirements clarified; technical investigation/design remains | Capability evidence/defaults, scheduling/limits, authentication/security, usage reporting and limits |
| #6 | Input scope clarified; delivery investigation remains | Receipt/inspection evidence, preprocessing and input-path feasibility |
| #13 | Definitions and assessment principles established; acceptance design remains | Mode-specific criteria, reference cases, error classification and justified evaluation method |
| #14 | Complete; retain closed state | Repository setup only |

Priority body corrections: #3 still says no unit/count range is selected; #5 says voting and comparison units are unselected; #8 must distinguish the accepted conceptual internal representation/local formats from unresolved detailed schema and deferred export packaging; #9 must record manual-only retention and the accepted completion levels/termination choices without claiming a complete state machine. Earlier decision comments do not remove obsolete statements in issue bodies. #1/#8/#11/#13 span all three product modes: preserve that scope while distinguishing first-version work from deferred modes; do not close them merely because first-version requirements are recorded.

Recommended new issue candidate (not issued or user-approved): `[Design] Define bibliographic naming, workspace layout, and approved rename behavior`. Existing #8 addresses representation/handoff, #9 lifecycle/provenance, and #11 GUI; none explicitly owns completion criteria for the complete naming/workspace policy. Track original bibliographic metadata and evidence, field precedence, journal mapping, Unicode/fallback confirmation, collision/shortening, accepted directory/file layout, and joint content/rename approval with failure behavior. Cross-link existing issues and give each requirement one primary owner. New issuance is not logically mandatory if an existing issue is explicitly expanded to own these criteria; explicit coverage is necessary.

Do not create duplicate issues solely for override (#5), termination (#9), flowcharts/wireframes (#1/#11), or acceptance criteria (#13). These can be updated in place. Optional future splits must preserve parent completion criteria and traceability. Local commits are not yet pushed, so GitHub updates must not present unpushed branch links as already published evidence.

### Audit publication follow-up

The user subsequently authorized publication: comments were posted on #1–13 and the naming/workspace candidate was issued as [#15](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/15). The read-only audit statements above describe the earlier audit, not the current publication state. See the [publication record](design-status.md#issue-publication-and-vector-flowchart--2026-11-15). The first [HTML/SVG flowchart](diagrams/review-workflow.html) is now available for review; detailed wireframes and acceptance decisions remain next.

## Current visual checkpoint — 2026-11-15

The user accepted the [V2.1 responsibility diagram](diagrams/app-data-flow-v2.1.html) and its connector cleanup as the visual baseline. [Standalone SVG](diagrams/app-data-flow-v2.1.svg). Earlier V1/V2/V3 artifacts remain available; the requested V2.1 label follows V3 chronologically. Acceptance concerns layout and connection clarity, not the still-unapproved review-exit/Apply transitions.

Next: develop review-to-final-confirmation wireframes and inspect user scenarios. Then decide result acceptance boundaries. Remaining decisions include pending override versus mandatory figure review, missing calls/query-1 failure, overridden completion status, selection persistence and protection across shutdown/resume, and partial content/rename application failure. Detailed schema/alignment and CLI/authentication feasibility remain technical design work. No product implementation is authorized by the diagrams.
