# PEPaper-EaTER-PANnel

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

## Version control workflow

The development branch structure is `main` -> `dev` -> `big-pic-design`. Create `dev` from `main` and `big-pic-design` from `dev`. Continue the current design work on `big-pic-design`. The project version and this document's revision number are separate.

## Public repository and secrets

The project is intended for a future public Git repository. The local repository is initialized on `main`. Keep local secrets in `.env`. The repository's `.gitignore` excludes `.env` and its variants, except `.env.example`. The example file must contain only comments or placeholders, never credentials. Required variable names will be added when the configuration requirements are known.

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

Comparison between outputs and checking against the source have different purposes. Agreement between outputs does not establish source fidelity. The comparison unit, review responsibilities, and handling of uncertainty remain open.

## User choices and defaults

The product must provide defaults and let users change supported settings. Providing these choices is an established direction. The exact defaults, supported ranges, and combination constraints still need design.

| Variable | User choice | Remaining design decisions |
|---|---|---|
| Model selection and combination | Select the model or supported combination of models. | Supported models and combinations, capability differences, access paths, and defaults. |
| Execution count | Set the number of model executions for a defined unit of work. | Unit of work, supported range, default, and interaction with model combinations. |
| Concurrency | Set how many executions may run at the same time. | Default and limits from access, resources, usage, and cost. |
| Conflict-resolution policy | Select a supported procedure for handling disagreement between results. | Supported policies, default, source checks, human review, and treatment of unresolved content. |

Execution count, concurrency, and conflict-resolution policy are independent variables. Multiple executions do not require concurrent execution or voting. The supported choices and their defaults must be distinguished from the values a user selects for a task.

The wrapper should support changes in models and in CLI or API access. Existing subscriptions are an initial access preference. API use remains an option. The supported model catalog, access mechanisms, implementation technologies, and handoff formats still need design.

## GUI and informed choice

A GUI is part of the established product direction. It must help users understand variables, available choices, and the effects of their combinations. Users must be able to understand the defaults and actively adjust supported settings for their task. Control layout, explanations, and interaction details still need design.

The screen implementation is not limited to static HTML or a specific language or framework. React, TypeScript, and other suitable technologies may be used. Frontend technology can be selected separately from the execution layer, where Go remains a candidate. GUI technology and handoff formats such as HTML, JSON, or Markdown are separate decisions.

## User-selectable deliverable modes

The product must support all three modes and let the user choose:

1. A faithful transcript with source images for another LLM.
2. A source-aware reading workflow that checks the paper while performing a requested task.
3. Both.

Support for these modes is an established requirement, not a claim of completed implementation. The default mode, detailed behavior, and handoff mechanisms still need design. The design must also determine how to connect images, captions, body text, and source locations. Internal representation and handoff formats, including JSON, HTML, and Markdown, remain design decisions.

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
