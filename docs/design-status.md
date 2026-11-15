# Design status

Status: Confirmed requirements recorded; detailed design remains open.

Updated: 2026-11-15.

Project version: `v0.2.1`.

## Resume here: conversation handoff on 2026-11-15

This document and open-design.md preserve the decisions from the current conversation so work can resume without its chat history. Read this section first, then the linked detailed sections. The project remains in design only: no application implementation, CLI trial, or model evaluation has been authorized by this handoff.

**Explicit approval boundary:** the user has NOT finally approved the assistant's last six-stage end-to-end workflow explanation. Do not treat the complete workflow, its buttons, state transitions, or completion/unlock semantics as an approved specification. Earlier individually accepted requirements remain in force. A request to explain a flow, or an acknowledgment of its general behavior, is not approval of all details introduced in that explanation.

### Consolidated accepted decisions

| Topic | Accepted requirement and detail location |
|---|---|
| Pending actions and reruns | Partial/whole-paper rerun, fresh 1/3/5 total independent calls, per-call CLI/model, direct configuration or app proposals approved before execution. See Pending rerun options. |
| Scope interaction | App proposes scope from a pending item; users may directly choose page ranges or document elements. Visually compare candidate coverage. Direct PDF drawing remains deferred. |
| Existing edits | Default to including edited portions for comparison while preserving the current edited document and retaining new outputs separately; offer exclusion per run. Show actual scope. |
| Result retention | Keep previous results until manual deletion. No age/count/storage-based automatic cleanup. |
| Internal representation | Section hierarchy and paragraph-level viewing, content elements, source mapping, relationships, uncertainty, provenance. This is the accepted baseline; future conceptual changes are design updates. |
| Comparison and figures | Structure first, content within aligned elements second. Provenance differences are generation metadata, not content disagreements. Every figure receives human review for identity, completeness, and caption association. |
| Result inspection | Title first; expose structured output and all approval targets, including bibliographic/citation data, content, relationships, uncertainty, provenance, and proposed file/folder names. |
| Local workspace | Accepted source/runs/current/review layout, whole-document and section Markdown, structured JSON, separate figures/tables/equations, BibTeX from confirmed metadata, readable review history. Detailed immutable snapshot mechanism remains a proposal. |
| Naming fields | `<년도>__<저널>__<약칭>__<타이틀>__<기타 사항>`; words inside fields use `-`. Preserve original metadata and scientific signs. |
| Year, journal, abbreviation | Input-version citation year; preprint-version release year; unknown-year if unavailable. Journal uses explicit mapping or full name; current journal mapping is empty. Resource name, then user identifier, then app-proposed abbreviation. DOI belongs to metadata. |
| Title and fallback | Full title by default. Computer chooses character name, known code point, or numbered unknown-symbol placeholder when conversion is needed. Preserve source evidence and scripts/Greek where representable. |
| Naming approval and portability | Conservative portability policy; user confirms the complete final filename, not each conversion step or character. |
| Subject suffix | LLM proposes concise keyword-level subject/category; append preprint/review only when applicable. User may edit. No automatic runtime/approval metadata in filenames. |
| Collision and shortening | Collision `-v<n>` within other-details, distinct from publication version. If sufficient shortening is needed and approved, exact `shortend-file` is last within other-details, after collision token and before extension. Never silently overwrite or truncate. |
| Selection and change set | Select paragraph/figure/table/bibliographic-field candidates, including different calls, and assemble a visible change set for final approval and Apply. Review related elements together. |
| Instance and review protection | One application instance with internal parallel calls/papers. During active review, proposals may be shown but Apply and application updates to the reviewed document are blocked. Other processing continues. |
| Rerun during review | If no suitable result exists, users may rerun while reviewing. This is already established by the earlier rerun requirement, not dependent on acceptance of the six-stage workflow. Preserve existing results and current document; incoming results remain separate candidates. |

### Not approved: the last six-stage workflow

The assistant described: (1) start review, (2) compare/select, (3) rerun if needed, (4) collect a change set, (5) finish review and apply, (6) record application outcomes. This outline combined accepted requirements with new proposals. The user explicitly withheld final approval of the outline as a whole.

In particular, do not implement or record as accepted: `Finish review` / `Back to review` controls; the exact `Reviewing -> Ready to apply -> Applying -> Completed` transitions; the action that freezes a change set; no-change completion or leaving/resuming a review session; the exact document-unlock point and failure behavior. No automatic release or Apply is authorized. Recording approval separately from application success was accepted earlier, but the detailed success/failure workflow and revision mechanism remain proposals.

### Preserved six-stage workflow proposal for the next review

**Status: not finally approved.** Retained at the user's request on 2026-11-15 so the next conversation can present and review the same proposal directly. This section is not an implementation specification. Accepted ingredients are identified; assembling them into this exact workflow remains a proposal.

| Stage | Proposed interaction and application behavior | Decision boundary |
|---|---|---|
| 1. Start review | Open the document and protect its current content against application updates. Show incoming candidates separately. Other papers and internal parallel calls continue. | Single instance and blocking Apply during active review are accepted. Review-entry event and lock lifecycle need design. |
| 2. Compare and select | Show the title first, then structured bibliographic/content/source/relationship/uncertainty/provenance fields and file/folder proposals. Compare structure before content. Review every figure. Select paragraph, figure, table, or bibliographic-field candidates across calls; show dependencies such as figure-caption together. | These inspection and selection requirements are accepted; exact screen layout and dependency controls are proposals. |
| 3. Rerun if no suitable candidate | During review choose partial/whole-paper scope, visually compare page/element scope candidates, choose 1/3/5 total independent calls and per-call CLI/model, then approve execution. Default to reprocessing edited portions for comparison while preserving them; exclusion is selectable. Continue reviewing while calls run. Show new outputs as separate candidates without replacing current content or previous selections. | Rerun during review and its configuration are accepted. Detailed rerun UI and execution scheduling remain to be designed. Rerun never permits Apply during active review. |
| 4. Assemble a change set | Collect selected modifications and display current values, candidates, source evidence, and linked dependencies. Selecting a candidate does not approve/apply it. Newly arriving suggestions are not automatically inserted. | Element selection and visible change-set approval are accepted. Exact change-set schema, dependency enforcement, and incorporation controls need design. |
| 5. Finish review and confirm application | Proposed `Finish review` freezes the selected change set and enters `Ready to apply`, showing the exact changes. Retain document protection; do not unlock it for arbitrary writes. Proposed `Apply` can apply only that fixed set after final confirmation. Proposed `Back to review` returns to editing the selection or rerunning and clears ready-to-apply status. | This transition, freeze mechanism, and button arrangement are NOT approved. It is a proposal for leaving active review, not an exception allowing Apply while active review continues. |
| 6. Record application outcome | Record the approval separately from actual application success. On success, record the new result revision and applied changes, then release protection. On failure, do not claim completion. | Approval/application distinction is accepted. Exact revision mechanism, unlock point, failure states, and recovery actions are NOT approved; detailed recovery remains deferred. |

Proposed state sketch, retained for discussion only:

```text
Reviewing (Apply blocked; current document protected)
  | compare/select; rerun returns additional candidates
  | Finish review [proposed]
  v
Ready to apply (fixed change set; document still protected)
  | Back to review [proposed] -> Reviewing
  | Apply [proposed transition after active review ends]
  v
Applying (only the approved set may write)
  | success [exact completion/unlock behavior unapproved]
  v
Completed
```

Branches from the prior explanation (current status noted individually):

- Complete review without modifying content when an inspected item needs no correction; the control and completion scope remain undefined.
- Leave or postpone a review while preserving proposals/selections; lock release and resumption behavior remain undefined.
- Historical proposal: apply a subset while other items remain pending. The later decision below now permits an explicit override route; its detailed state transitions remain unapproved.
- Keep new suggestions separate after a change set is fixed; incorporating one would require returning to review. The precise freezing/version contract remains a proposal.

These branches must not be inferred from the existing requirement that pending review does not block unrelated processing. Do not introduce automatic unlock, automatic application, or model retries as part of documenting this sketch.

Historical opening question (deferred by the later decision below; do not request approval before the flowchart and UX review):

> 검토 중에는 문서를 보호하고 rerun·비교·선택을 계속할 수 있습니다. 제안한 전환은 `Finish review`로 선택한 change set을 고정한 뒤, 최종 확인 화면에서 `Apply`하거나 `Back to review`로 돌아가는 방식입니다. `Finish review`와 `Apply`를 분리하는 이 방식부터 확인해 주시겠습니까?

Present the six-stage table when useful, but ask for one focused decision at a time. Explicitly state that the preserved flow is a proposal awaiting approval; do not ask the user to reapprove the already accepted ingredients.

### Next design discussion and work boundary

Defer the transition out of active review until a complete flowchart and sufficiently composed functions/UI support evaluation of the user experience. Preserve the six-stage proposal for that review. Ask one focused question at a time when that review resumes. Do not reopen the already accepted naming, preservation, rerun, single-instance, or active-review blocking requirements.

Other remaining work: concrete Unicode vocabulary/validation coverage, numbering scopes, suffix details and shortening strategy; structured schema fields/source coordinates; alignment criteria and figure completeness checks; permissions/deletion dependencies; instance scope and multiple tabs; CLI integration feasibility, security/encryption, onboarding, and evaluation criteria. The technical refinement section records proposals, not completed investigations or implemented features. Export packaging, detailed navigation precision, direct PDF drawing, multilingual UI, web retrieval, and RAG retain their existing deferred/later status. The later termination-choice decision opens that part of lifecycle design; detailed recovery mechanisms remain open.

Historical publication checkpoint: the initial handoff used commit 22eb17d as its baseline; the consolidated handoff was subsequently committed as b99f15b. Later follow-up decisions are recorded below. Use Git history for the current commit status. They have not been pushed or published as GitHub issue updates. Local issue drafts and prior published comments are historical records; these consolidated local design documents contain the later decisions. The temporary memo is preserved and is not the authoritative current decision record.

## Follow-up decision: pending override and deferred workflow approval

Status: user-confirmed product behavior on 2026-11-15; detailed interaction and state transitions remain open.

- **Review exit and Apply:** decide this interaction after drawing the complete flowchart and composing the functions sufficiently to assess the user experience. The six-stage workflow remains a proposal. Do not request isolated approval of `Finish review` and `Apply` before that review.
- **Default:** resolve all pending items before finalization.
- **Exception:** permit the user to proceed with pending items remaining. This is supported but not recommended. Require an explicit override confirmation that states that pending regions remain. Exact English command/button wording is not selected.
- **Fallback for an unselected pending item in this explicit override:** if identical candidates form a strict majority (more than one half, such as 2/3 or 3/5), select that result. Display a popup-style notification stating which result will be selected and that the basis is majority agreement.
- **No strict majority:** select the result of query 1 by its original query order, not completion order. Display a warning that this is an arbitrary fallback because no strict majority could be established. Do not describe it as the best or verified result.
- This fallback addresses items for which the user has not chosen a candidate. It does not authorize replacing an explicit user selection. Show the chosen result and selection basis in the override interaction; detailed grouping and confirmation order remain to be designed.
- Ordinary disagreement detection still marks affected content pending even when a majority agrees. Majority agreement does not automatically finalize content. The new fallback applies only to the explicit user override route, not normal processing or unsolicited Apply.
- The active-review Apply block remains in force. Permission to proceed with pending items does not define when the review lock is released or authorize writes during active review.

Remaining specification: candidate equivalence and voting scope across reruns; denominator when calls fail or results are missing; behavior if query 1 has no usable result; aggregate notification layout; and final status/provenance for overridden items. The existing mandatory human review of every figure remains recorded. Whether this exception can bypass that requirement must be resolved explicitly; do not silently mark unreviewed figures as human-reviewed. Distinguish applying only selected changes from finalizing with fallback-selected pending content in the future flowchart.

## Follow-up decision: joint approval and completion levels

Status: user clarification on 2026-11-15.

- **Joint approval:** approve content changes and file/folder renames together. The final approval view must expose both. This resolves the separate-versus-joint approval choice; it does not yet specify filesystem transaction, rollback, or recovery mechanisms.
- **Distinct completion levels:** processing completion, review completion, and Apply completion are separate states. None alone means final completion. All must be complete before the final completed state is shown. Exact item aggregation and treatment of explicitly overridden pending items remain to be specified; override must not silently be represented as human review.
- **Review interruption/resumption:** the user requested clarification, not a policy decision. Explain leaving the review screen, switching papers, or closing the app with selections not yet applied, and distinguish persistence of selections from continued protection of the current document. Selection retention, lock lifecycle, and recovery behavior are not newly approved here.
- **Related changes (historical clarification):** at this point the user had not selected a dependency policy. The later follow-up below provisionally adopts the proposed criterion. The agent should propose criteria and concrete examples for linked changes (e.g. figure identity and caption association, citation and reference target). Do not treat this as approval to bundle every related element or to modify dependent content automatically. Joint inspection of related elements remains accepted.

## Follow-up decision: override help, termination choices, and provisional dependencies

Status: user-confirmed requirements on 2026-11-15, with the dependency policy explicitly provisional.

### Override process help

The user accepted the pending override route and its strict-majority / original-query-1 fallback notifications. Place a `<?>` help icon beside the override notification/confirmation. It opens a concise explanation of the complete override process with a compact diagram: normal pending resolution; explicit override confirmation; preserve explicit selections; for unselected items, strict majority selects the matching result, otherwise query 1 is the arbitrary fallback; disclose the chosen result and basis before approved application. This is explanatory help, not a substitute for the required notification or warning. Exact popup/help layout and Apply transitions remain open; do not present the unapproved six-stage workflow as finalized.

### One-stop termination

Inform users that closing the visible app/browser interface does not necessarily terminate processing. Provide one place to choose the termination behavior rather than silently deciding to keep running or immediately terminate:

| Choice | Required behavior / explanation |
|---|---|
| Continue in background | Keep processing in the background after the visible interface closes. Inform the user that processing continues. |
| Force termination | Stop without background continuation. Distinguish abrupt termination from orderly shutdown; do not promise complete preservation of in-flight work. |
| Prepare for recovery, then exit | Allow a short wait to save recoverable state and perform orderly shutdown before exiting. Explain that termination is delayed for this preparation. |

The user selected this one-stop choice model. Exact labels, default choice, close/quit triggers, CLI subprocess handling, persistence/checkpoint granularity, timeout behavior, and recovery guarantees require technical design and platform feasibility checks. Do not claim browser-close interception is implemented or universally available. Unexpected process/OS termination is distinct from a user-requested orderly shutdown.

Selection persistence and active-review document protection must be considered in this lifecycle design. The prior suggestion to persist all selections and preserve protection through interruption/restart is not independently approved by this termination decision. Existing active-review Apply blocking remains accepted; exit/restart lock semantics remain open. Other papers and reruns may continue when background processing is chosen, within existing execution approvals.

### Provisional linked-change policy

Adopt the proposed dependency criterion provisionally: if applying only one change would make content or a relationship inconsistent, present the necessary changes together. Show the included elements and the reason for grouping, then obtain user confirmation. An independent caption typo correction need not be bundled with figure replacement; a figure identity correction requiring a caption reassociation should expose both changes together. A citation identifier change requiring a reference-target update should expose the linked changes together. Do not silently edit dependent content or bundle all related elements indiscriminately. Detailed dependency detection and transaction/recovery rules remain design work. This policy is provisional, not a final immutable decision.

### Latest resume point

User-selected work order: first review usage scenarios using the integrated flowchart and wireframes; then decide result acceptance boundaries (mandatory inspection, override scope, and completion distinctions). See the [issue audit](open-design.md#pre-implementation-issue-audit-and-agreed-work-order--2026-11-15). This sequence does not approve unresolved workflow transitions.

Preserve the six-stage workflow as an unapproved proposal, and defer review-exit/Apply approval until the complete flowchart and composed UI/functions support UX evaluation. The next design artifact should integrate override help, the provisional dependency groups, joint content/rename approval, distinct completion levels, and one-stop termination into that reviewable flow. Do not request isolated approval of the old six-stage proposal as if these later decisions did not exist. Documentation does not authorize implementation or model execution.

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

Confirmed: the first section of result inspection is the paper title. Bibliographic information supports both citation and file naming. The user specified the filename stem `<년도>__<저널>__<약칭>__<타이틀>__<기타 사항>` (year, journal, abbreviation, title, other details). Preserve this order and use double underscores between all fields. Within each field, join words with hyphens by replacing spaces; preserve original field values in metadata. This supersedes the earlier space-to-underscore rule. Do not rewrite scientific minus signs or existing meaningful notation as word separators. The abbreviation field uses the paper-stated name of a method, tool, database, or similar named resource first, preserving its original spelling. If no such name is available, use a user-defined short paper identifier. If neither is available, the app proposes a short identifier for user review in the filename approval interface. An app-proposed identifier must be distinguished from a name stated in the paper; it is not inferred source metadata. Selection among multiple eligible named resources remains to be designed. Optional-field handling, filesystem-safe normalization, and collision handling remain to be specified; do not invent missing metadata.

The user requested a concrete directory and file-format proposal, including separately stored paper elements and understandable metadata for proposed and approved changes. This reopens discussion of the local workspace layout and file extensions; it does not settle downstream export packaging.

Confirmed year rule: use the publication year in the official citation information for the input paper version. For a preprint, use the release year of the input preprint version. If the year cannot be established, use the literal filename value unknown-year and request user confirmation. Show the selected year and source evidence in the approval interface, with user correction available. Do not substitute PDF creation or download year.

DOI is included in bibliographic metadata. Record the DOI associated with the input version when available, with source evidence; do not invent a DOI or silently substitute a DOI for another version. DOI is not an additional filename field under the accepted naming convention. Detailed DOI validation and representation of related-version identifiers remain to be designed; external lookup is not authorized by this metadata requirement.

Confirmed journal naming rule: use a journal abbreviation only when a matching entry exists in the explicit mapping table config/journal-abbreviations.json. The table maps full journal names to filename abbreviations and is initially an empty JSON object, so the current fallback is the full journal name. Do not infer or generate abbreviations when no mapping matches. Matching normalization and future table maintenance remain detailed design work.

For the filename journal field, replace spaces with hyphens after selecting the mapped value or full-name fallback. Preserve the full journal name with its original spaces in bibliographic metadata. For example, with the empty table, Nature Methods becomes Nature-Methods in the filename. For preprints, use the input version's repository name (such as bioRxiv, medRxiv, or arXiv); if the journal/repository cannot be identified, use unknown-journal and request user confirmation. The method/tool/database abbreviation field remains separate from this journal mapping.

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

Confirmed: use the input version's full title, preserving case, numbers, and scientific notation; replace spaces with hyphens in filenames. Preserve the original title before conversion in bibliographic metadata. Do not automatically summarize or truncate; if the target filesystem length limit is exceeded, propose an alternative for user confirmation.

Use an explicit conservative mapping table. config/filename-title-mapping.json records the accepted formatting/preservation requirements and separately labels candidate mappings as proposals. The candidate code-point tokens for portability-sensitive characters are not a universal filesystem standard or an approved final replacement vocabulary. Actual validity depends on the target filesystem; validation, reserved names, trailing characters, collisions, and mapping-table versioning remain detailed design work.

Any filename conversion must be shown with the original title, the proposed filename, changed characters or notation, and the reason, then confirmed by the user before application. Confirmation may be part of the existing naming approval interface; this does not require a separate modal for each character. Unknown or unsupported cases require a reviewed fallback, never silent deletion or guessed scientific meaning.

Preserve Greek letters, Unicode subscripts/superscripts, and other representable mathematical notation. Do not silently transliterate Greek letters or flatten scripts, accents, combining marks, or mathematical typography. Some PDF notation uses positioning rather than Unicode characters; retain source evidence and structured notation and request confirmation of a filename representation if faithful direct conversion is unavailable. Do not assume every unusual Unicode character is invalid in a filename. Full-title preservation and conversion approval are requirements; candidate replacement tokens still need review.

Documentation upkeep: reconcile accepted decisions from this conversation into the existing README, decision record, and open-design tracker, including superseded statements. The user requested completeness and consistency of these documents, not a separate feature-list artifact. Documented requirements are not claims of implemented features.

## Technical refinement draft: naming, revisions, comparison, and review

Status: engineering proposals for review, except subsections explicitly labeled Confirmed, which record subsequent user decisions. The latest approval boundary is in Resume here above. This section does not authorize application implementation, CLI/model trials, or deferred recovery/export work.

### Naming pipeline and source preservation

Keep three separate values: source title (with source evidence), structured title (including mathematical spans where needed), and approved filename. Do not reconstruct metadata by splitting underscores in filenames. Store the year, journal, resource abbreviation, title, and other-details fields explicitly; underscores may occur within every field.

Proposed sequence:

1. Collect each field with source page/region, extraction uncertainty, and origin (`source`, `user`, or `app_proposal`). Resolve the input version before selecting its year or DOI.
2. Select journal mapping by exact full-name match initially. No fuzzy matching, automatic case folding, or web lookup. Preserve both the matched key and original value; the current empty mapping produces full names.
3. Apply the explicit title rules once, in a deterministic order, using a pinned mapping revision. Keep unknown notation unresolved rather than inventing text. Apply field-specific rules before joining the filename stem.
4. Assemble the complete stem and extension; validate every actual directory/file component and the complete destination path. Validation applies to other fields too, but title mappings must not silently alter a journal or resource name.
5. Show original text, source rendering, proposed filename, and a change list. Obtain approval for the exact candidate and destination, including ordinary space substitutions when present. Revalidate at application time.
6. Record approved and applied outcomes separately. If validation fails or the destination changed, retain the current files and return the proposal for review. Processing can continue under stable internal IDs while final naming is pending; pending artifacts remain in runs/, not presented as approved current/ content.

### Unicode and mapping vocabulary

Confirmed: the user selected the conservative portability policy. Propose conversions for characters or names that can cause problems in other major environments even when accepted locally. Also validate the actual target volume. This is the selected policy, not a user-selectable two-policy feature. Preserve representable scientific notation; conservative portability does not imply ASCII-only filenames. Detailed platform coverage and validation rules require specification and verification, and universal compatibility is not guaranteed. The computer builds the candidate; the user reviews the complete final proposal before application.

Use character-name tokens first when conversion is needed, with explicit `[U+XXXX]` tokens as the fallback when a reliable name representation is unavailable. Neither form is an abbreviation of scientific meaning. Never infer that a slash means division or that a vertical bar means an absolute value. For code points above U+FFFF, use the full uppercase hexadecimal value if this token scheme is approved.

| Input class | Proposed handling | Review evidence |
|---|---|---|
| ASCII space U+0020 | Replace each occurrence with `-`; do not collapse repeated spaces silently | Original and proposed title |
| Greek letters and mathematical Unicode | Preserve where representable; no transliteration | Rendered title and original code points |
| Unicode superscripts/subscripts | Preserve; never apply NFKC/NFKD to source or display values | Source and rendered text |
| Combining marks or canonically equivalent sequences | Keep original sequence; optional NFC comparison key only for diagnostics, never as a rewrite | Code-point difference if relevant |
| PDF-positioned scripts or stacked formulas | Retain structured spans and source rendering; request a reviewed filename representation | Formula/title crop and explicit fallback |
| `/`, `\`, `:`, `*`, `?`, `"`, `<`, `>`, `|` | Character-name token first, then code-point fallback, only when target validation or a selected portability policy requires conversion | Rule and reason; user confirmation |
| NBSP, tabs, newlines, zero-width or directional controls | Flag for inspection; no blanket whitespace stripping or control removal | Visible escaped representation and source |
| Unknown/private-use/replacement glyph | Propose known-code-point fallback where available, otherwise numbered unknown-symbol placeholder; no application before review | Source crop, code point, missing-font/extraction status |
| Literal text resembling `[U+002F]` | Keep as literal source text; do not decode from a filename | Transformation event distinguishes literal from generated tokens |

The filename is not a reversible encoding. Different source strings can produce the same candidate, so preserve the original and conversion events and run collision checks. No rule may silently overwrite another result. Mapping-table edits produce a new revision; previously approved filenames do not change automatically.

A naming proposal contains: `proposal_id`, `paper_id`, `base_revision`, field inputs and origins, source references, `mapping_revision`, `mapping_digest`, requested destination, proposed filename, changed spans with code points and rule IDs, validation findings, and the target revision/digest to approve. Positions refer explicitly to the stored original string; rendered glyph groups and PDF spans are separately referenced. Invalid/unresolved candidates cannot be applied.

### Confirmed fallback precedence

The user selected character-name notation as the default conversion fallback (for example, `[solidus]`). If a reliable, unambiguous name representation is unavailable, use an explicit Unicode code-point token such as `[U+002F]`. If both the character name and code point are unidentified, use a numbered placeholder such as `[unknown-symbol-01]`. The computer selects the appropriate fallback level and constructs the complete proposed filename automatically. The user reviews and confirms the final proposal before application, regardless of which fallback levels were used. Do not request separate approval at each fallback step or for each individual character. Show all conversions and their levels within the final proposal. Preserve the original title and link each unresolved placeholder to its source location/image in metadata; do not conflate distinct unresolved occurrences. Placeholder approval authorizes the filename representation, not a claim that the scientific notation has been identified. Number allocation scope and stability across revisions remain to be specified. This supersedes the earlier code-point-first recommendation. Directly representable Greek letters, scripts, and other scientific notation remain preserved; the fallback policy does not require converting every special character.

Use a maintained character-name vocabulary; the mapping file now proposes name tokens for its existing characters and preserves code-point alternatives. Exact spelling/casing/word separators for labels other than the illustrated `[solidus]`, and the conditions for an unavailable name representation, still require detailed specification. An unidentified glyph does not have a known code point merely because it looks unusual; unresolved glyphs and positioned formulas require source inspection and a reviewed representation, including a numbered unknown-symbol placeholder when both identifiers are unavailable. The conservative portability policy is selected; precise platform coverage and validation cases remain detailed design work.

### Length, collisions, and unresolved naming fields

Validate the actual target filesystem and complete path rather than imposing a guessed universal character limit. Include extension, directory depth, and Unicode encoding in the check. A full title repeated in a folder and file can make path constraints more restrictive. Do not truncate either occurrence silently.

Collision checks compare actual destination entries and report case/canonical-equivalence ambiguities conservatively. A matching content digest may suggest an existing paper but must not silently merge records; DOI equality is not proof of an identical input version. Offer an existing record for inspection or a disambiguated candidate for approval, without overwriting.

Confirmed `<기타 사항>` behavior: use an LLM-proposed, maximally concise subject/category descriptor at the specificity of the paper's author-provided keywords, grounded in the paper. Preserve the distinction between source keywords and a generated catalog label in metadata. A general paper uses the subject alone; append preprint and/or review-paper information only when applicable, after the subject. Publication status and article type are separate attributes; a preprint can also be a review. The separator before this field is `__`, superseding the earlier single underscore. Do not automatically append an ordinary-paper label, Run ID, CLI/model, or approval status. Users may enter or edit identifying text. The app may propose version or collision disambiguation information when needed, and the complete filename is reviewed, editable, and approved by the user. An empty user field prompts a concise LLM proposal rather than silently omitting the suffix. The user's tentative mention of `v` does not define a universal fallback token. If a reliable subject cannot be proposed, show the uncertainty for final review; no fixed fallback or invented classification is selected. The hyphen joins words within the suffix; exact vocabulary, missing-keyword inference, and quantitative length limits still require design; do not invent a numeric cap. For an unavoidable length limit, offer a shorter user-approved path or the accepted shortening exception with a terminal shortend-file marker, retaining the complete title in metadata. Multiple method/tool/database names are presented as choices with source evidence; do not select one solely by occurrence count. These policy choices still require review.

### Confirmed collision suffix

The user selected `v<n>` for filename collision disambiguation. Propose appending `-v<n>` to the other-details field, preserving the full title and the `__` field separators. The computer detects the collision and proposes an available candidate; the user reviews the complete filename before application. Never overwrite an existing result. A collision suffix is naming metadata, not evidence of a published/preprint version or an execution revision. Keep its purpose separate from source-version information in metadata. Starting number, allocation scope, handling an existing version token, and final availability checks require specification; no automatic duplicate-paper merge is authorized.

### Confirmed shortening exception

When length constraints require shortening, the user permits a sufficiently shortened filename proposal, subject to final-result review. Append the exact literal `shortend-file` as the final token inside the existing other-details field, immediately before the extension. It is not a separate filename field. Preserve this user-specified spelling; do not silently correct it to `shortened-file`. Use the intra-field hyphen separator, and place the marker after any collision suffix: `...__<topic>-v<n>-shortend-file.ext`. The marker belongs to the other-details field as naming metadata, not to the original title or a publication type.

Shorten enough to satisfy the actual destination's filename and full-path limits with the extension, collision suffix, marker, and intended directory structure included. Do not merely remove one character or truncate automatically at a fixed guessed limit. Generate a concise, identifiable candidate and show the full original title, proposed name, and length/validation outcome together. The user may edit and approve the complete result; no shortening is applied silently. Preserve the unshortened title, approved filename, and exception reason in metadata. Whether particular directory names also need shortening is determined by path validation; the approved title remains unchanged in bibliographic content. Exact shortening strategy and any numeric headroom remain detailed design.

### Confirmed element selection and change-set approval

The user accepted selection of results per paragraph, figure, table, and bibliographic field, with the selected changes assembled into one visible change set for final approval and Apply. Users may combine elements from different independent calls. Show related dependencies, such as a figure and its caption, together for review. Before Apply, show the complete selected changes and their scope; individual candidate selection is not approval or application. This defines the user-facing approval unit; detailed dependency enforcement and transaction behavior remain engineering design. The subsequent review-lock requirement below prevents application-controlled updates to the document during active review; the release-to-Apply transition remains to be designed.

### Confirmed single-instance execution and review lock

Run only one application instance at a time; parallel paper processing and LLM calls occur within that instance, including CLI subprocesses as needed. This is not a single-OS-process requirement. Instance-lock scope and multiple-browser-tab behavior still require detailed design.

While a document is under active review, it must not be updated. The app may generate, retain, and show additional change proposals, including results from parallel processing or reruns, but Apply to that document is blocked while review remains active. Candidate selection and proposal inspection remain available. Keep proposals separate from the document's current content; other documents and processing tasks can continue.

The block must be enforced by the application write path, not only by disabling a UI button. This includes application-mediated agent/CLI writes to the reviewed document; route generated candidates to separate outputs. Technical protection against external filesystem edits remains a separate design concern, not a guarantee supplied by single-instance execution.

The exact action that ends active review and permits final approved Apply is not yet selected. Do not infer an automatic unlock, auto-apply, or a bypass for the reviewing tab. Preserve the accepted change-set approval model, with application only after an explicitly designed transition out of active review. This supersedes the earlier assumption that ordinary parallel work may update the reviewed base document and require the user to repeatedly re-review it.

### Revision and approval contract

Propose stable `paper_id`, `run_id`, `call_id`, `element_id`, and immutable `revision_id` values, independent of filenames. A new extraction first has call-local element IDs. Alignment relates them to canonical elements; uncertain matches do not inherit a canonical ID automatically. Record split/merge lineage explicitly rather than reusing one ID for multiple new paragraphs.

Each approval proposal identifies its base revision, candidate revision, element/metadata/rename targets, differences, and required dependencies. Provide a readable structured view and source evidence before approval. Keep generation provenance distinct from bibliographic facts and content changes.

- `Approve review`: record inspection of the exact visible revision where no edit is needed. This is a proposed control, not a final UI label.
- `Apply`: approve and apply the displayed change set. The existing requirement remains; record application success separately from approval.
- Defensive proposal: if the base changes outside active review, or an external edit bypasses application controls, mark the proposal stale and refresh the comparison before any later Apply. During active review, normal application updates are blocked by the confirmed review lock; stale handling must not replace that lock. Never apply approval to a different revision.
- A content/asset change invalidates dependent review conclusions, including figure completeness or caption-link approval; unrelated elements keep their review records. A pure path rename does not invalidate scientific review when content identity is unchanged, but the rename itself remains an explicit operation.
- External agent edits are detected using revision/digest checks and shown as new candidate changes. They must not silently bypass content approval. Direct-edit detection mechanisms remain to be specified.
- Do not promise an atomic transaction across arbitrary filesystems. Preflight content and rename operations; publish the new current revision only when the required writes succeed. Record failure/partial application without misreporting review completion. Detailed recovery remains deferred.

Propose revision snapshots under current/revisions/<revision-id>/ with a manifest pointer to the active revision. This is an extension of the accepted current/ layout and requires review; previous approved results must remain available until manual deletion regardless of the mechanism selected. Deleting a run must show referenced current assets and review evidence; propose refusing deletion of shared referenced assets unless a reviewed preservation/copy plan exists. Retention of a deletion audit event is a further proposal, not authority to retain deleted source content.

### Structural alignment and content comparison

Align candidates using source-document identity, page/region overlap, element type, reading order, and section context. Text similarity is supporting evidence only. Allow one-to-many and many-to-one alignment for paragraph splits/merges. Do not force a match when columns, repeated captions, or overlapping regions create ambiguity. Thresholds require reference cases and remain unspecified.

After alignment, compare sentence/character content, numeric values as written, signs, scripts, units, equation structure, table cell/merged-cell structure, and element relationships. Preserve raw text. A separate diagnostic comparison view may identify encoding or visual-wrap differences, but must not silently reflow, dehyphenate, or remove source differences. Equivalent-looking equations are not automatically equivalent scientific content.

| Finding | Proposed review treatment |
|---|---|
| Different generation CLI/model | Metadata difference; not a content disagreement |
| Paragraph split with complete aligned content | Structural difference shown separately; resolve source paragraph boundaries if uncertain |
| Missing element, numeric/sign/script change, or wrong relationship | Content disagreement: pending even if a majority agrees |
| Uncertain source alignment or unreadable single-call content | Pending with the uncertainty reason |
| Identical outputs | Report agreement; do not label source fidelity verified |
| Any figure, including identical outputs | Mandatory human review remains pending until reviewed |

Figure review includes identity, complete panels/labels/caption, and source association. Show all relevant source regions for multi-page content. The source inventory itself can be incomplete: missing-figure detection requires page coverage checks, not just review of extracted figures. Propose a coverage summary of pages and detected figure candidates for human inspection; the exact completeness procedure remains to be reviewed.

### Review interface and processing state

Propose a title-first header with bibliographic fields and naming preview, a section/paragraph/element navigation tree, source and selected-output panes, and a change/approval panel. Show provenance and uncertainty alongside the relevant item. A raw structured view is optional; it does not replace the readable view. Result selection supports choosing candidates per element as well as inspecting a whole call, with dependencies such as figure-caption links included visibly in any change set.

Rerun scope previews distinguish selected output targets, additional read-only context, and user-edited exclusions. Context may be needed to interpret a caption or equation, but must come only from the same paper; reading context does not grant permission to change it. Show page range and element-based candidates visually. A figure candidate includes its complete panels and caption by default in the proposal; boundary selection still requires user approval.

Propose two independent status dimensions: processing (`queued`, `running`, `finished`, `failed`) and review (counts of pending, reviewed, stale, and approved-not-applied items). These are a draft display model, not finalized retry/recovery semantics. A single item may have several pending reasons, such as mandatory figure review plus disagreement. Completing a run must not clear any review reasons automatically. Show failed/missing calls in a 3/5-call group; never treat absent results as agreement. Do not silently add replacement calls.

### Adapter, security, and evaluation design backlog

Propose a common CLI adapter contract: availability/authentication check, model selection, one-paper input manifest, execution request, output collection, structured validation, and capability/error reporting. This is a required-capability list, not verified behavior of Codex CLI or Claude Code. Compare both CLIs using official documentation before selecting invocation or authentication mechanisms. No API fallback, credential format, model catalog, or transport has been chosen.

The browser/server boundary should be designed around local access, workspace-scoped file operations, source-aware sanitization, and redacted logs. A local browser connection does not authorize arbitrary filesystem access. Propose avoiding shell interpolation of paper metadata and treating extracted HTML/Markdown as untrusted display data. Credential storage and encryption need a separate threat model and platform review; no encryption claim is established here.

Before implementation, prepare reference examples for Unicode titles, many-to-many paragraph alignment, omitted figures, split captions, stale approvals, filename collisions, and edited-content reruns. Evaluate fidelity, traceability, review completeness, and naming correctness separately. No sample-size threshold, runtime benchmark, or model experiment is authorized by this draft.

### Design examples and review gates

| Example | Expected design outcome |
|---|---|
| `α₂ dynamics` | Candidate `α₂-dynamics`; preserve Greek/subscript; show space conversion for approval |
| `x² versus x2` | Preserve the distinction in title and content comparison |
| `A/B` | If conversion is required: `A[solidus]B`; code-point fallback `A[U+002F]B`; confirmation required |
| Literal `A[U+002F]B` | No decoding; collision with generated candidate requires review |
| PDF-positioned superscript with plain extracted `x2` | Do not accept flattened title silently; show source and request representation review |
| Very long title | No automatic truncation; retain full metadata and propose a reviewed alternative |
| Revision changes after approval preview | Stale proposal; refresh before Apply |
| Two calls omit the same figure | Agreement does not establish coverage; source inventory review remains needed |

The next review can accept or modify (1) detailed portability validation rules and character-name vocabulary within the accepted conservative policy and name-first fallback order, (2) detailed topic-suffix vocabulary and unavailable-topic handling within the accepted subject-first rule, and (3) revision/approval granularity. These questions are distinct from already accepted full-title preservation and confirmation of the final conversion proposal. CLI feasibility, security mechanisms, and evaluation criteria remain separate investigations; export packaging, direct PDF drawing, and detailed recovery stay deferred.

### Technical sources and limits

Unicode distinguishes canonical from compatibility equivalence; compatibility normalization can remove distinctions in mathematical characters and scripts. This supports avoiding NFKC/NFKD for source preservation; the product-specific approval design is our proposal. [Unicode UAX #15](https://www.unicode.org/reports/tr15/).

Windows filename rules include reserved characters/names, trailing-character constraints, and filesystem-dependent limits. They inform the selected conservative portability policy, not universal macOS rules. Target-volume validation on macOS is still required. [Microsoft: Naming Files, Paths, and Namespaces](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file).


## Decision reconciliation after commit 22eb17d

The conversation since the committed baseline has been reconciled with the README, this decision record, open-design.md, and the filename mapping design. No separate feature-list artifact was requested. These records distinguish confirmed naming behavior from engineering proposals.

| Topic | Confirmed current rule |
|---|---|
| Field boundaries | `<년도>__<저널>__<약칭>__<타이틀>__<기타 사항>`; words within fields use `-` instead of spaces. Original metadata and meaningful scientific signs remain preserved. |
| Fallback | Computer selects character-name notation, known Unicode code-point notation, then numbered unknown-symbol notation as needed. Source evidence remains linked. |
| Confirmation | User inspects/edits/approves the complete final filename; no intermediate per-level or per-character prompts. |
| Portability | Conservative portability is selected, with actual-destination validation; no ASCII-only rule or universal compatibility guarantee. |
| Topic suffix | LLM proposes a concise source-grounded subject/category; preprint/review information follows only when applicable. User editing remains available. Runtime metadata is not inserted automatically. |
| Collision | Use `-v<n>` within other-details, separate from actual publication-version metadata; never overwrite. If shortening applies, the collision token precedes shortend-file. |
| Shortening | Permit sufficient shortening only through final-result approval. `shortend-file` is the exact terminal token inside other-details; preserve the full source title and exception record. |
| Unchanged journal mapping | The journal-name table is still empty; full journal names are used until an explicit matching entry exists. |

Audit corrections: removed remaining journal space-to-underscore statements; updated proposed multiword character-name tokens to hyphens; clarified collision-token placement relative to the shortening marker; added the confirmed topic-suffix policy to the mapping design. Exact token vocabulary, validation coverage, counter allocation and stability, and shortening algorithms remain detailed design. Revision snapshots, stale-approval handling, alignment algorithms, figure coverage checks, CLI/security mechanisms, and evaluation procedures remain engineering proposals or investigations, not newly accepted requirements. No application implementation or model trial has been performed.

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
