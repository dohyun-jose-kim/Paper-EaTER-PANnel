# Paper-EaTER-PANnel

Project version: `v0.2.1`.

Development README, revision 0.1. This revision identifies the document, not a software release.

## Purpose

This project aims to deliver information from scientific papers to an LLM without omission or distortion. Source fidelity is the primary objective. This objective is not a claim that the project can guarantee error-free delivery.

The design must address text, numbers, symbols, equations, figures, tables, captions, references, and their relationships. A readable output alone does not establish fidelity. The design must also address how a user or model can check information against the source.

## Current stage

The project is in requirements gathering and design discussion. Requirements remain incomplete. Project implementation and model evaluation have not started. Initial development environment setup is complete.

Required tools and local environments may be installed when needed for agreed work. No environment is required for the current document edits. Environment setup does not select the final implementation language or authorize model evaluation.

Go remains a candidate for the implementation. The local installation was verified on 2026-11-13: `go version go1.27.4 darwin/arm64`. For setup on another Mac with Homebrew, install and verify it with:

```sh
brew install go
go version
```

See the [Homebrew Go formula](https://formulae.brew.sh/formula/go) and the [Go installation guide](https://go.dev/doc/install). The installation request does not authorize project implementation or evaluation.

This project has an independent design scope. The previous project's extractors, processing sequence, output format, and evaluation boundaries do not constrain this design. Previous work remains unchanged and can provide historical evidence.

Integration with `caffeine-pour-over` is outside the current scope.

## First-version scope confirmed on 2026-11-14

Build a minimal local macOS web app, used through a browser, wrapping LLM-assisted PDF documentation. Support both Codex CLI and Claude Code through local execution. All interface text is English; multilingual UI is deferred. LibreChat and assistant-ui are comparison candidates, not selected dependencies. Possible later RAG document search informs that comparison but is outside the first-version requirement.

Serve existing LLM users who repeatedly study papers in depth, including users with limited computer skills. Reuse existing PDF text and consider OCR where necessary. Initial inputs are English online academic PDFs, normally not physical-print scans, in expected batches of up to ten papers (not a hard application cap). Preserve original wording, content order, human-readable characters, complete figures, captions, equations, tables, references, line breaks, and paragraph boundaries. Layout cleanup must respect those requirements; visual-wrap handling remains to be designed. Do not add translation, summaries, or explanations to the documented source.

Support reading the result in the app and manually downloading it for another LLM with equal priority. Keep files and results locally; input transmission to the selected model service is explicitly permitted. Preserve external links. Web full-text/supplementary retrieval is a possible later feature; if added, use a selection list before retrieval. Exact export formats, supported external material, and source-navigation precision remain open.

Use one user-designated local storage root. Users can configure a preferred location within their own directory as the default storage path; do not hard-code a project-owned output location. The initial fallback path and behavior when changing this setting remain open.

Each processor LLM call sees only one paper or its selected portion; batches keep paper contexts separate. Later cross-paper integration and use are left to the user.

Support multiple papers and parallel calls with a near-real-time queue Dashboard. Users choose whole-paper or partial scope and 1/3/5 vote configurations. Vote count is the total independent calls for that scope: 3 votes means three calls, not three turns in one conversation or three calls per model. Pending items can trigger a user-selected independent run of a portion or the whole paper, with fresh model and CLI choices. Users assign the CLI and model per call. Initially populate calls with the same setting, allowing individual changes or the same model for all calls.

The pending review interface must offer partial rerun and whole-paper rerun (total rerun), with a fresh choice of 1/3/5 total independent calls and per-call CLI/model settings. An app-proposed rerun is another available option: the app proposes the scope and CLI/model configuration, and the user reviews and approves the configuration before execution. This proposal route is optional; users can configure a rerun directly. Additional pending actions and the detailed interaction remain open. Approval to execute a rerun is separate from Apply confirmation for document changes; automatic extra calls without user approval are not authorized by this requirement.

When a rerun scope overlaps user-edited content, show the overlap and let users choose whether to include those portions for comparison or exclude them from processing. Default to inclusion: preserve the current edited document and retain new outputs separately for comparison. Only user-selected changes confirmed with Apply update the document. Show any exclusions in the effective processing scope, including for whole-paper selections. Retain previous execution results until the user manually deletes them. Do not automatically delete results based on age, execution count, or storage usage. Detailed deletion controls and handling of linked assets remain to be designed.

Content-affecting disagreement marks the affected portion pending regardless of majority agreement, preserving divergent outputs for review. Initial CLI/model defaults and detailed comparison rules remain open. Mark uncertain items `pending` without stopping ongoing work, remaining portions, or other papers. Review or independent reruns may occur while processing continues. Dashboard distinguishes processing completion from review completion.

Comparison first aligns structure, then examines content within corresponding elements, including sentences and characters within paragraphs. Provenance records generation metadata; different CLI/model values do not themselves constitute content disagreement. Every figure requires human review against the source for identity, complete area coverage, and caption association, even when automated comparisons agree. Figures awaiting review remain pending without blocking processing. The UI must distinguish required figure review from a detected discrepancy. Confirmation controls for figures needing no correction remain to be designed; corrections still require Apply.

Result inspection starts with the paper title. Bibliographic information supports citation and naming. The user-defined filename stem is `<년도>_<저널>_<약칭>__<타이틀>_<기타 사항>`; the abbreviation uses a paper-stated method/tool/database or similar resource name first, then a user-defined short identifier if no such name exists, and finally an app-proposed identifier for user review if neither is available. Preserve original resource names and distinguish proposed identifiers from source-derived names. Other field details and filesystem normalization remain to be specified. The local workspace baseline is accepted: a per-paper directory containing source/, runs/, current/, and review/, with Markdown/JSON documents, separate figure/table/equation assets, BibTeX from confirmed bibliographic metadata, and readable proposal/approval records. Approval decisions and successful application are recorded separately, referencing stable IDs and revisions. Paragraphs are addressable within section files rather than separate files by default. See the detailed layout in docs/design-status.md. Precise metadata fields remain to be specified; downstream export packaging remains deferred.

For the filename year, use the official citation publication year for the input paper version; for a preprint, use the release year of the input version. If unavailable, use unknown-year and request user confirmation. Show the year and its source evidence for review and correction. DOI is included in bibliographic metadata when available, with source evidence; it is not an additional filename field.

For the filename journal field, use an abbreviation only when config/journal-abbreviations.json contains a matching entry; otherwise use the full journal name. The table is initially empty. Replace spaces in this filename field with underscores, preserving the full name in bibliographic metadata. Preprints use the input repository name; unidentified journals/repositories use unknown-journal with user confirmation. This journal mapping is separate from the method/tool/database abbreviation field.

The filename title uses the full title of the input version, preserving case, numbers, and scientific notation, with spaces replaced by underscores. Preserve the original title in bibliographic metadata. Filename conversions require user confirmation of the original and proposed values. Preserve Greek letters and subscript/superscript notation where representable; do not silently transliterate, flatten, delete, summarize, or truncate. Unsupported notation and filesystem-limit cases require reviewed alternatives. config/filename-title-mapping.json records the design rules and explicitly provisional character mappings; exact replacements and filesystem validation remain detailed design work.

The result-selection and approval interface must expose the internal structured output and all items subject to approval, not only figure/caption previews. This includes the extracted paper title, structured content, source mapping, relationships, uncertainty, provenance, citation information, and proposed result file/folder names or renames where present. Users must be able to inspect the approval scope and proposed changes before approval. Distinguish source-derived bibliographic information, execution metadata, and filesystem proposals. Detailed fields, citation formats, naming rules, approval granularity, and interface controls remain to be designed.

Offer optional in-app CLI-based review chat in a workspace with source images and intermediate questions/choices. Show before/after changes; user confirmation through `Apply` updates the document and completes that item's review. The complete state model remains open; review pending is distinct from execution waiting.

The accepted common internal representation preserves the source section hierarchy (including the abstract), with body text organized into paragraphs within sections and available for paragraph-level viewing. It covers text, equations, figures, tables, captions, references, source page/region mapping, relationships, uncertainty, and run/CLI/model/scope provenance. Figures remain separately accessible. Outputs are aligned by corresponding source regions, with uncertain correspondence marked pending. This is the current conceptual design baseline; future changes require design updates. Detailed schema fields, serialization conventions within the accepted local file formats, and alignment algorithms remain to be specified. Compare outputs alongside their source PDF region. Agents must be able to edit and rename result files/directories; permissions and rename tracking need design. Use application-specific screens with chat UI where needed and an `ABOUT` page for guidance. Security, encryption scope, login, and setup details remain design work.

Direct PDF region drawing is deferred. Partial rerun scope can be selected by page range or document element. The app must offer scope recommendations for a pending item, and users must also be able to select a scope directly without first requesting a recommendation. The selection UI must support visual comparison of candidate scopes and their source coverage, for both app recommendations and user selections. Other scope units, recommendation rules, and the detailed UI remain to be designed. Current work is documentation and design only; implementation is explicitly excluded.

All three overall product modes below remain required. First-version review chat is separate from manual downstream handoff and does not settle the full reading-workflow design. See [confirmed decisions](docs/design-status.md#decisions-confirmed-on-2026-11-14) and the [numbered remaining questions](docs/open-design.md#remaining-design-sequence).

## Version control workflow

The development branch structure is `main` -> `dev` -> `big-pic-design`. Create `dev` from `main` and `big-pic-design` from `dev`. Continue the current design work on `big-pic-design`. The project version and this document's revision number are separate.

## Public repository and secrets

The public repository is [Paper-EaTER-PANnel](https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel), with `main` as its default branch and current design work on `big-pic-design`. Keep local secrets in `.env`. The repository's `.gitignore` excludes `.env` and its variants, except `.env.example`. The example file must contain only comments or placeholders, never credentials. Required variable names will be added when the configuration requirements are known.

Environment files do not load automatically. The loading method remains a design decision. Do not place secrets in source files, documentation, logs, or generated outputs. Before publication, check the files selected for publication and the Git history for secrets. Ignore rules do not remove files that Git already tracks or secrets in earlier commits.

## Provisional conceptual pipeline

The diagram below is an agreed starting point for discussion. It separates conceptual roles. It does not specify required execution stages, interfaces, or a fixed execution order. All three handoff modes are required user choices in the planned product. They are not yet implemented.

```text
Provisional conceptual pipeline

                    [Scientific paper]
                            |
                    [Input delivery]
                   PDF / text / images
                            |
                    [Model execution]
                            |
               [Comparison and source check]
                            |
                         [Handoff]
                            |
              +-------------+-------------+
              |             |             |
       [Transcript and  [Source-aware    [Both]
        source images]   reading workflow]

Cross-cutting concerns:
Source links | Execution state | Security | Usage and cost

Independent variables:
Execution count | Concurrency | Conflict-resolution policy
```

Input delivery must distinguish available source files from the text and images that a model actually receives. Saving an image or placing its link in Markdown does not establish that a receiving model can inspect it.

Comparison between outputs and checking against the source have different purposes. Agreement between outputs does not establish source fidelity. The comparison unit and policy details remain open. The first-version pending review and user-confirmed Apply flow is established above.

## User choices and defaults

The product must provide defaults and let users change supported settings. Providing these choices is an established direction. The 1/3/5 total-call choices are established; initial defaults, other limits, and compatibility constraints still need design.

| Variable | User choice | Remaining design decisions |
|---|---|---|
| Model selection and combination | Select the model or supported combination of models. | Specific models and combinations, capability differences, integration for both required CLIs, API scope, and defaults. |
| Execution count | Set the number of model executions for a defined unit of work. | Precise partial-work units and initial defaults; 1/3/5 total independent calls with per-call CLI/model assignment are established. |
| Concurrency | Set how many executions may run at the same time. | Default and limits from access, resources, usage, and cost. |
| Conflict-resolution policy | Select a supported procedure for handling disagreement between results. | Supported policies, default, source-check triggers, and unresolved-result handling beyond the established pending review flow. |

Execution count, concurrency, and conflict-resolution policy are independent variables. Multiple executions do not require concurrent execution or voting. The supported choices and their defaults must be distinguished from the values a user selects for a task.

The wrapper should support changes in models and in CLI or API access. Existing subscriptions are an initial access preference. API use remains an option. Codex CLI and Claude Code are required first-version access routes. Specific models, integration mechanisms, API scope, implementation technologies, and handoff formats still need design.

## GUI and informed choice

A GUI is part of the established product direction. It must help users understand variables, available choices, and the effects of their combinations. Users must be able to understand the defaults and actively adjust supported settings for their task. Control layout, explanations, and interaction details still need design.

The screen implementation is not limited to static HTML or a specific language or framework. React, TypeScript, and other suitable technologies may be used. Frontend technology can be selected separately from the execution layer, where Go remains a candidate. GUI technology and handoff formats such as HTML, JSON, or Markdown are separate decisions.

## User-selectable deliverable modes

The product must support all three modes and let the user choose:

1. A faithful transcript with source images for another LLM.
2. A source-aware reading workflow that checks the paper while performing a requested task.
3. Both.

Support for these modes is an established requirement, not a claim of completed implementation. The default mode, detailed behavior, and handoff mechanisms still need design. The design must also determine how to connect images, captions, body text, and source locations. The conceptual internal representation is accepted as described above. Detailed schema fields and serialization conventions within the accepted local file formats remain to be specified; handoff formats, including JSON, HTML, and Markdown, remain deferred design decisions.

## Collaborative design process

The user and the agent develop the design through staged review. Records distinguish **Established direction**, **Confirmed evidence**, **Provisional design**, and **Open decisions**. Evidence records distinguish locally checked records from user-provided history.

Design status and user configurability are separate dimensions. A user-selectable variable can be an established requirement while its supported range and default remain design decisions. Internal architecture and security policies are not automatically user settings.

The review sequence covers document structure and the diagram, this README, the design documents, and final consistency checks. Each checkpoint requires user direction before the next stage. Silence does not count as agreement. Accepted decisions do not need repeated approval.

When feedback changes a decision, the documents must update its status and basis. New requirements or differences in interpretation remain open until resolved. Completing these documents does not complete the project design or authorize implementation or evaluation.

## Related documents

The following design documents are drafts for user review:

- [Design status](docs/design-status.md): established direction, evidence and limitations, provisional design, candidates, and deferred proposals.
- [User choices and remaining design decisions](docs/open-design.md): intended user controls and behavior, unresolved details, and information needed to decide.

[Previous project README](../PAPER-pdf-transit/README.md) is retained as an optional historical reference. It is not a basis for the current design drafts. This link requires the sibling project and may not resolve in a standalone public repository.
