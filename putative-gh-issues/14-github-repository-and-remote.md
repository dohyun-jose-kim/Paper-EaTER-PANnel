# [Setup] Create the GitHub repository and connect the local remote

- Local ID: `14`
- Project version: `v0.2.1`
- Publication status: Local draft; not published.
- Work type: Repository setup.
- Design level: Setup planning.
- Execution readiness: Repository details and account access must be resolved.
- Source: User request to add repository creation and remote connection as issue 14.
- Available next action: Confirm the proposed owner and visibility before repository creation; the official name and account access are verified.

## Purpose

Create or identify the intended GitHub repository and connect it to this local project. Establish a usable destination for later issue publication and any agreed source push.

## Established requirements and evidence

- The user requested this setup issue. Writing the issue does not create a repository or authorize immediate publication.
- Local inspection found branches `main`, `dev`, and `big-pic-design`, with `big-pic-design` checked out.
- The existing baseline commit is `42389b4`, titled `docs: establish v0.2.1 design baseline`.
- No Git remote was configured at the check before these drafts were written.
- The project is intended for future public hosting. Initial repository visibility has not been selected.
- Local secret files must remain outside published content. The initial design records the .env exclusions and public example file.

## Preparation record (2026-11-13)

The user confirmed the official name as `PEPaper-EaTER-PANnel` and requested preparation for remote setup.

| Item | Prepared state |
|---|---|
| Repository name | `PEPaper-EaTER-PANnel` (confirmed by the user). |
| Local directory | `Paper-EaTER-PANnel`; the directory name may differ from the repository name. No directory rename is required for remote setup. |
| GitHub account | `dohyun-jose-kim`; `gh auth status` verified authentication through the system keyring. |
| Proposed owner | `dohyun-jose-kim`, based on the active account; ownership remains to be confirmed. |
| Target lookup | `gh repo view dohyun-jose-kim/PEPaper-EaTER-PANnel` could not resolve a repository accessible to this account. |
| Proposed remote | `origin`, using the account's configured HTTPS transport. |
| Proposed URL | `https://github.com/dohyun-jose-kim/PEPaper-EaTER-PANnel.git`; this is a prepared destination, not a verified existing remote. |
| Visibility | Still open. Private initially is proposed; future public hosting remains the established direction. |
| Default branch | `main` proposed. |
| Local branches | `main` and `dev` at `42389b4`; current branch `big-pic-design` at `7811d78`. |
| Push scope | No push during preparation. The later initial push scope remains open. Issue drafts exist only on `big-pic-design`. |
| Secret checks | `.env` and `.env.local` are ignored. `.env` does not occur in tracked history. A scan of all 20 reachable historical blobs found no common credential patterns; this is a limited check, not a guarantee. |
| Changes made | Official project name updated in the development README and design documents. Preparation changes remain uncommitted. |

### Prepared commands (not executed)

If the proposed owner and private visibility are accepted, create an empty repository and attach it locally without pushing:

```sh
gh repo create dohyun-jose-kim/PEPaper-EaTER-PANnel --private
git remote add origin https://github.com/dohyun-jose-kim/PEPaper-EaTER-PANnel.git
git remote -v
git ls-remote origin
```

An empty repository can return no refs from a successful `git ls-remote`. If the target already exists at execution time, verify its identity and contents before attaching it. Recheck local remotes before adding `origin`.

After the initial push scope is selected and the prepared document changes are committed, a proposed all-branch publication sequence is:

```sh
git push -u origin main
gh repo edit dohyun-jose-kim/PEPaper-EaTER-PANnel --default-branch main
git push -u origin dev big-pic-design
```

These later commands would publish the design history and local issue drafts as source files. They would not create GitHub issues. No repository creation, remote mutation, commit, or push was performed during preparation.

## Questions to resolve

- Should the active user `dohyun-jose-kim` own the repository, or should it belong to an organization? The official repository name is settled.
- Should it be public immediately or private initially?
- Does the intended repository already exist? If so, is it the correct target for this project?
- Does the verified account have creation access to the selected owner, if an organization is chosen?
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
