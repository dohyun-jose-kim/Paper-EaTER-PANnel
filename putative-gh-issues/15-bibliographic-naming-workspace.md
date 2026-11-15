# [Design] Define bibliographic naming, workspace layout, and approved rename behavior

Published: https://github.com/dohyun-jose-kim/Paper-EaTER-PANnel/issues/15

## Purpose

Own the bibliographic naming and local workspace design that currently spans representation (#8), lifecycle (#9), and GUI (#11) without complete naming-specific completion criteria. This is design work, not implementation authorization.

## Accepted baseline

- Filename stem: `<year>__<journal>__<short-name>__<full-title>__<other-details>`; spaces within fields become `-`. Preserve original metadata separately.
- Year comes from the input version's official citation or preprint release year. DOI remains bibliographic metadata. Journal abbreviations require an explicit mapping; the current table is empty, so use full names.
- Short-name precedence: paper-stated method/tool/database name, then user-defined identifier, then an app proposal.
- Preserve full title and scientific notation where representable. Conversion fallback: character name → Unicode code point → `[unknown-symbol-01]`. Computer chooses the level; user reviews the complete converted name and changes.
- Concise other-details describe subject/category; append preprint/review only when applicable. Do not insert Run ID, CLI/model, or approval status.
- Collision uses `-v<n>` in other-details; no overwrite. Shortening requires confirmation and the exact final token `shortend-file` inside other-details.
- Accepted workspace baseline: source/runs/current/review, original PDF, per-call results/provenance, Markdown/JSON, confirmed-metadata BibTeX, and separate figure/table/equation assets. Keep earlier results until manual deletion.
- Content changes and file/folder renames are approved together. Approval is distinct from successful application.

## Remaining design

Replacement vocabulary; representability and actual destination validation; mapping versions/matching; multiple eligible short names; unavailable subject; collision allocation; shortening strategy; stable identity through renames; linked asset deletion; and failed/partial content-plus-rename application. No universal filesystem limit or completed converter is claimed.

## Completion criteria

- [ ] Bibliographic field provenance, precedence, missing values, and multiple candidates are specified with examples.
- [ ] Unicode preservation/conversion, fallback levels, user confirmation, and portability validation are reviewed with scientific notation cases.
- [ ] Collision and shortening proposals include full destination/extension validation and no-overwrite behavior.
- [ ] Directory/file responsibilities, stable references, and manual deletion dependencies are specified, coordinated with #8 and #9.
- [ ] Joint content/rename approval and failure/recovery scenarios are reviewed, coordinated with #9 and #11.
- [ ] Naming/workspace acceptance cases are linked to #13, and accepted versus provisional decisions remain explicit.

## Scope and coordination

#8 owns content representation and handoff; this issue owns names and local workspace organization. #9 owns lifecycle/recovery mechanisms; this issue supplies rename-specific requirements. #11 owns screen composition; this issue supplies naming approval content. #13 owns assessment design.

The next user-selected sequence is flowchart/wireframe scenario review, then result acceptance boundaries. Local design documents are `docs/design-status.md`, `docs/open-design.md`, and `config/filename-title-mapping.json`; latest local commits `a71eefc`/`cf81c7e` are not yet pushed. This issue states the relevant baseline directly rather than relying on unpublished links.
