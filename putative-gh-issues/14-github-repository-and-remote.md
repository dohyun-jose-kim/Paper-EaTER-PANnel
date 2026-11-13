# [Setup] Create the GitHub repository and connect the local remote

- Local ID: `14`
- Project version: `v0.2.1`
- Publication status: Local draft; not published.
- Work type: Repository setup.
- Design level: Setup planning.
- Execution readiness: Repository details and account access must be resolved.
- Source: User request to add repository creation and remote connection as issue 14.
- Available next action: Resolve repository owner, name, visibility, and initial push scope; then verify account access.

## Purpose

Create or identify the intended GitHub repository and connect it to this local project. Establish a usable destination for later issue publication and any agreed source push.

## Established requirements and evidence

- The user requested this setup issue. Writing the issue does not create a repository or authorize immediate publication.
- Local inspection found branches `main`, `dev`, and `big-pic-design`, with `big-pic-design` checked out.
- The existing baseline commit is `42389b4`, titled `docs: establish v0.2.1 design baseline`.
- No Git remote was configured at the check before these drafts were written.
- The project is intended for future public hosting. Initial repository visibility has not been selected.
- Local secret files must remain outside published content. The initial design records the .env exclusions and public example file.

## Questions to resolve

- Which user or organization should own the repository, and what should it be named?
- Should it be public immediately or private initially?
- Does the intended repository already exist? If so, is it the correct target for this project?
- Which authenticated account has the necessary access?
- What remote name and transport should be used? The conventional name origin is a candidate, not an existing configuration.
- Does setup include an initial push? If so, which branches should be pushed and tracked, and which branch should be the remote default?
- Should these local issue drafts be included in the initial published source snapshot?

## Expected setup output

Record the agreed repository identity, visibility, remote configuration, and push scope. During later execution, recheck local state and account access, resolve any target-name conflict, create or use the agreed repository, and connect the remote. Check the content and history selected for publication for secrets.

This issue is operational setup, not product architecture. It is the closest item to a concrete execution procedure, but the repository details are still required. Do not infer that a future public-hosting intention authorizes immediate public creation.

## Completion criteria

- [ ] Repository owner, name, visibility, default branch, and push scope are recorded.
- [ ] The intended repository exists and access is verified.
- [ ] The local remote resolves to the intended repository.
- [ ] Files and history selected for publication have been checked for secrets; local .env files remain excluded.
- [ ] If an initial push is included, the agreed branches and tracking relationships are verified. Otherwise, the no-push outcome is recorded.
- [ ] The resulting URL and configuration are documented without credentials.

## Related issues and sources

Related work, not mandatory execution order:

- [10: Authentication and security](10-authentication-and-security.md) addresses application security; its entire design need not be complete to configure Git hosting.
- [Development README: version control](../readme-dev-v0.1.md#version-control-workflow).
- [Development README: secrets](../readme-dev-v0.1.md#public-repository-and-secrets).
- User direction in the current discussion; read-only local Git inspection.
- [Draft index](00-index.md).
