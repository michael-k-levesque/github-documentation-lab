# GH-011 — Repository History and Publication Security Review

**Review date:** October 12, 2026  
**Reviewed repository:** `michael-k-levesque/github-documentation-lab`  
**Baseline:** `main` at `c5cc530a6da60d538226642496a7af0a8a358185`  
**Decision:** No identified blocker in the inspected repository materials to making this existing repository public. The repository owner changed its visibility to **public** on October 12, 2026.

## Purpose

Determine whether the original GitHub Documentation Lab can be made public for a professional technical-writing portfolio without discarding its genuine Git history. Preserve accurate distinctions between actual checks and security guarantees that cannot be made.

## Inventory and history checked

| Surface | Observed at baseline |
| --- | --- |
| Default branch | `main` |
| Commit history | **29 reachable commits**, including merge history; each commit's changed-file list and available patch reviewed |
| Current tracked files | **Six:** `README.md`, four documents under `docs/`, and one Postman collection JSON under `postman/` |
| Historical changed paths | Only the same six documentation/collection paths appeared in the inspected commits; no observed binary file, uploaded screenshot, executable, or previously deleted credential file |
| Live branches | `main`, `docs/gh-009-postman-api-testing-guide`, `docs/gh-010-quality-review` |
| Branch divergence | Both additional branches were **0 commits ahead** of `main` (already merged) |
| Tags | No Git tags returned by the accessible matching-ref listing |
| GitHub pull requests | Three, **all merged**. Their descriptions, reviews, and discussion comments were inspected; PR #1 includes one recorded author self-review comment |
| Other issues | No separate issue records in the repository issue listing |
| Releases | None |
| GitHub Actions | API returned **0 workflow runs**; current tree contains no `.github/workflows/` files |
| Account identity in commit records | Author email domains were GitHub's `users.noreply.github.com`; committers used `users.noreply.github.com` or GitHub's own `github.com` domain |

## Security and privacy findings

- Inspected all available commit patches and all current tracked text files for recognizable GitHub personal-access tokens, common cloud/API credential prefixes, PEM private-key headers, bearer-token patterns, password/secret assignments, conventional email addresses, and phone-number patterns.
- **No matching embedded credentials, private keys, conventional personal email addresses, or phone-number strings were identified in the reviewed repository content or commit patches.**
- Reviewed the three pull-request descriptions and available review/discussion content; no matching credential patterns were identified.
- The tracked Postman collection defines three unauthenticated **GET** requests to a public GitHub demonstration repository. It includes no saved access tokens or environmental secrets.
- GitHub's GH-007 validation log records an earlier settings inspection: no outside collaborators or deploy keys and no enforced branch protection. These observations are historical, not a fresh live audit of every administrative setting.
- Documentation includes the author's GitHub username, a practice Jira work-item identifier, API examples, dates, and GitHub/official-reference links. Those are intended portfolio context, but the owner should be aware they will become public along with the historical pull-request discussions.
- Publishing does **not** require creating an open-source license. In the absence of a license, ordinary copyright law generally retains the author's rights; GitHub still allows site visitors to view and fork public repositories under its terms.

## Risks and controls

**A. Public history is genuinely public.** GitHub states that changing private to public makes code, activity, and available Actions history/logs visible and allows forks. Returning to private afterward cannot retract copies already obtained by third parties.

**B. Pattern checks are bounded.** This audit reviewed the reachable baseline history and repository surfaces accessible through the connected GitHub API. It is **not** a guarantee about orphaned/unreachable Git objects, inaccessible workflow artifacts, private account-level settings, nonstandard secret formats, unindexed external services, or sensitive information outside the repository. No separate local full-clone forensic scanner or independent audit was run. The artifact endpoint and selected deployment administration endpoints were not available through this connection.

**C. Security scanning after publication.** Review GitHub's Security settings when the repository is public and consider enabling the available secret-scanning/push-protection protections. Do not mistake zero detected patterns for proven absence of all possible secrets.

**D. Portfolio correctness.** Some documents describe the repository as private; those passages recorded actual historical test conditions. The README's current-visibility statement and the GH-010 release status must be updated after changing visibility so a prospective employer is not shown stale current-state claims.

## Result and recommended action

**Review result: Pass with explicitly documented limitations.** No observed content justifies creating a separate repository or rewriting this one's history. The original repository, with its real revision and testing record, is the recommended portfolio source.

**Publication completed:** The user selected the existing-repository/public route after the audit and completed GitHub's repository-visibility confirmation on October 12, 2026. GitHub now reports the repository as **public**. Before distributing the link broadly, confirm from a signed-out browser that the README, both guides, validation log, Postman collection, and closed pull requests are accessible as intended.

## Sources

- [GitHub Docs — Setting repository visibility](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility)
- [GitHub Docs — Removing sensitive data from a repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- [GitHub Docs — Licensing a repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)
- [GitHub Docs — Email addresses reference](https://docs.github.com/en/account-and-profile/reference/email-addresses-reference)
