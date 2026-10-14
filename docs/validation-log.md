# GitHub Documentation Lab — Validation Log

## Purpose

Record the procedures, expected results, observed results, and technical findings generated during the GitHub Documentation Case Study.

This log provides supporting evidence for the accuracy of the project's technical documentation.

## Test Environment

- **Platform:** GitHub Cloud
- **Interface:** GitHub web interface
- **Repository:** github-documentation-lab
- **Default branch:** main
- **Repository visibility:** Private
- **Jira work item:** GHDCS-1

## Test GH-001 — Repository Initialization

**Objective:** Create a dedicated repository for documentation testing.

**Expected Result:** A private GitHub repository containing an initialized README and a default branch.

**Observed Result:** The repository was successfully created with private visibility, a README.md file, the main branch, and an initial commit.

**Status:** Passed

## Test GH-002 — README Revision

**Objective:** Replace the initial README with a structured project introduction.

**Expected Result:** The updated README renders correctly in GitHub and is preserved in the repository's commit history.

**Observed Result:** Markdown headings, paragraphs, lists, and inline code rendered correctly in GitHub's preview. The README file history on the main branch confirms both the initial commit and the subsequent docs: establish project README commit.

**Status:** Passed — Markdown rendering and commit history verified.

## Test GH-003 — Create and Edit a Documentation File

**Objective:** Create a structured technical guide, revise its content, and verify that GitHub preserves both versions.

**Expected Result:** The documentation file is created successfully, the revised content is committed, and both versions appear in the file's commit history.

**Observed Result:** Created `docs/create-github-repository.md` and committed the initial guide (`020dc73`). Revised the repository verification instructions and committed the updated document (`c978529`). GitHub's file history on the `main` branch confirms both commits.

**Status:** Passed — file creation, revision, and commit history verified.

**Scope Note:** The document remains a draft. This test verifies the documentation workflow, not completion of the guide's full technical review.

## Test GH-004 — Create and Switch Branches

**Objective:** Create a documentation working branch and verify branch switching and isolation.

**Prerequisites:** Existing GitHub repository with the `main` branch.

**Procedure:** Created `docs/improve-repository-guide` from `main`, switched between branches, and committed a documentation improvement on the working branch.

**Expected Result:** Both branches are accessible, and changes committed to the working branch remain separate from `main` until merged.

**Observed Result:** GitHub displayed two branches. The working branch was initially synchronized with `main`, then became one commit ahead after committing the documentation improvement (`08aa955`).

**Status:** Passed — branch creation, switching, and separate commit history verified.

## Test GH-005 — Submit a Pull Request

**Objective:** Submit a documentation change for review before merging it into the default branch.

**Prerequisites:** A working branch containing committed changes.

**Procedure:** Created pull request #1 to merge `docs/improve-repository-guide` into `main`. Added a description explaining the changes, validation performed, and related Jira work item GHDCS-1.

**Expected Result:** GitHub creates an open pull request showing the proposed changes and correct source and destination branches.

**Observed Result:** Pull request #1 was created successfully. GitHub identified one commit, one modified file, 11 additions, and no deletions.

**Evidence:** https://github.com/michael-k-levesque/github-documentation-lab/pull/1

**Status:** Passed — pull request creation verified.

## Test GH-006 — Review and Merge a Pull Request

**Objective:** Review proposed documentation changes and merge the approved changes into `main`.

**Prerequisites:** An open pull request containing a documentation modification.

**Procedure:** Inspected the pull request's file comparison, verified the proposed changes, documented a self-review in the pull request conversation, and completed the merge.

**Expected Result:** The pull request merges without conflicts, closes successfully, and makes the documentation changes available on `main`.

**Observed Result:** The comparison showed 11 added lines in one file and no deletions. A self-review was documented with no issues identified. Pull request #1 merged successfully and closed. Merge commit `ab36aa8` was created. The Repository Visibility and Access section was subsequently verified on `main`.

**Evidence:** https://github.com/michael-k-levesque/github-documentation-lab/pull/1

**Status:** Passed — self-review, merge, and destination-branch content verified.

**Scope Note:** This exercise involved a documented self-review, not independent peer approval. Full technical validation of the complete guide remains pending.

## Test GH-007 — Repository Access and Configuration

**Objective:** Inspect repository access, branch protection, and security configuration to identify existing controls, limitations, and potential risks.

**Prerequisites:** An existing private GitHub repository with owner-level administrative access.

**Procedure:**
1. Opened repository settings and verified the repository name and default branch.
2. Completed GitHub's identity verification requirement to access collaborator settings.
3. Inspected repository collaborators and direct access.
4. Inspected classic branch protection rules and repository rulesets.
5. Reviewed the available Advanced Security settings.
6. Inspected repository deploy keys.
7. Recorded the observed configuration without modifying settings.

**Expected Result:** Repository ownership, visibility, access permissions, branch protection configuration, and available security settings can be inspected and documented.

**Observed Results:**
- Repository visibility: Private.
- Repository owner: Personal GitHub account.
- Default branch: `main`.
- External collaborators: 0.
- Direct contribution access: Repository owner only.
- Classic branch protection rules: None configured.
- Repository rulesets: None configured.
- GitHub indicated that rulesets would not be enforced under the current private repository/account configuration.
- Dependency graph: Disabled.
- Dependabot alerts: Disabled.
- Dependabot security updates: Disabled.
- Grouped security updates: Disabled.
- Dependabot version updates: Not configured.
- Deploy keys: None configured.
- Secret scanning and push protection: Status not established by the inspected settings page.

**Findings:**
- The repository is private and has no external collaborators.
- The default branch does not have an enforced branch protection rule.
- The project's branch, review, and merge procedures are currently followed voluntarily.
- Dependency-monitoring features are disabled; the repository currently contains Markdown documentation rather than application dependencies.
- No deploy keys were present.
- No configuration changes were required to complete the inspection.

**Status:** Passed — configuration inspection completed and findings documented.

**Scope Note:** This test verified visible administrative settings. It did not test unauthorized access, GitHub App permissions, personal access tokens, or the effectiveness of security controls through simulated attacks. The absence of enforced branch protection is a documented limitation, not a successful security-control test.

## Test GH-008 — Validate Selected GitHub REST API Operations

**Objective:** Validate selected read-only GitHub REST API operations, expected error responses, response data, and observed browser cache behavior using repeatable tests.

**Prerequisites:** Internet access, a browser with developer tools, and a Postman workspace. The API examples use public repository data and require no access token.

**Test Environment:**
- API host: `https://api.github.com`.
- Test repository: `octocat/Hello-World` (public).
- Clients: Browser with Chrome DevTools Network panel; Postman web workspace using Cloud Agent.
- Postman collection: `GitHub REST API Validation`.
- Authorization: No Auth.
- Request headers: `Accept: application/vnd.github+json` and `X-GitHub-Api-Version: 2026-03-10`.

**Procedure:**
1. Used the browser and Chrome DevTools Network panel to inspect responses from the GitHub REST API, including a successful response, a cache-related `304 Not Modified` response, and a `404 Not Found` response.
2. Created three named `GET` requests in the Postman collection.
3. Added four post-response JavaScript assertions to each request for status, JSON content type, and endpoint-specific response data.
4. Saved and reran the requests with the common GitHub API headers enabled.
5. Compared the observed responses and automated test outcomes with the expected behaviors.

**Expected Results:**
- GH-008-01 — A public-repository lookup returns `200 OK` with JSON identifying the expected repository and public visibility.
- GH-008-02 — A deliberately invalid repository lookup returns `404 Not Found` with a JSON error response.
- GH-008-03 — The repository commits endpoint returns `200 OK` with a non-empty JSON array of commits containing identifying fields.
- Browser caching — A conditional request may produce `304 Not Modified` if the cached representation remains current.

**Observed Results:**

| Test | Endpoint or scenario | Observed result | Postman assertions |
| --- | --- | --- | --- |
| GH-008-01 — Retrieve Public Repository | `GET /repos/octocat/Hello-World` | `200 OK`; JSON identified repository `octocat/Hello-World` (ID `1296269`), owner `octocat`, and `private: false`; 129 ms on the final run. | 4/4 passed |
| GH-008-02 — Repository Not Found | `GET /repos/octocat/Hello-World-NOT-A-REAL-REPO-GH008` | `404 Not Found`; JSON included `message: "Not Found"` and `status: "404"`; 101 ms on the final run. | 4/4 passed |
| GH-008-03 — List Repository Commits | `GET /repos/octocat/Hello-World/commits` | `200 OK`; non-empty JSON array containing commit `sha` and `commit.message`; 113 ms. | 4/4 passed |
| Browser cache observation | Public repository lookup inspected with Chrome DevTools | `304 Not Modified` observed for a cached representation; `200 OK` also observed with caching disabled. | Observation only; not part of the 12 Postman assertions |

**Evidence:**
- Reusable test artifact: [GitHub REST API Validation — Postman Collection v2.1](../postman/GitHub-REST-API-Validation.postman_collection.json), containing requests `GH-008-01`, `GH-008-02`, and `GH-008-03`, along with their 12 post-response assertions. The portable copy omits workspace-specific export metadata; request URLs, headers, and tests are preserved.
- Screenshots captured during testing showed the configured requests, API responses, and `4/4` passing test results for each request. These screenshots are not stored in this GitHub repository.
- Public API reference: https://docs.github.com/en/rest/about-the-rest-api/api-versions

**Findings:**
- All 12 automated assertions passed across three saved requests and two distinct read-only API operations.
- Expected `404` responses are successful negative tests when the response matches the expected behavior; they are not successful HTTP requests.
- A `404` from GitHub does not, by itself, prove a repository does not exist, because private or inaccessible repositories can return the same status.
- A `304` response is conditional on cache validators and was observed in the browser, not enforced as a repeatable Postman assertion.
- The results reflect public, unauthenticated requests and do not establish behavior for private repositories, authenticated access, mutation endpoints, or rate limits.

**Status:** Passed — selected GitHub REST API operations and negative response validated; 12/12 Postman assertions passed. Browser cache behavior separately observed.

**Scope Note:** This exercise validates the documented request/response behavior at the time of testing. The collection is now archived in this repository for independent import and rerunning; the export does not contain past execution results. No independent peer review was performed.

## GH-009 — Postman Guide Procedure Verification

**Objective:** Reproduce the documented GH-008 tests by downloading and importing the archived Postman collection and executing the requests individually and together using the Collection Runner.

**Prerequisites:** Postman web workspace with a functioning request agent and internet access; [the archived Collection v2.1 JSON](../postman/GitHub-REST-API-Validation.postman_collection.json).

**Procedure performed (October 12, 2026):**
1. Downloaded the collection JSON from the GitHub repository.
2. Imported it into Postman as a separate collection, **GitHub REST API Validation Copy**, leaving the original collection unchanged.
3. Confirmed that the imported copy contained all three requests and the documented URLs and API-version/Accept headers.
4. Sent each of the three imported requests separately and inspected the HTTP response and **Test Results** (four passing assertions per request).
5. Opened the imported collection's **Run** option and executed a **Functional**, **Local** collection run with **all three requests selected**, **Iteration data: None**, and **Iterations: 1**.
6. Inspected the Collection Runner results and confirmed the individual and aggregate outcomes against the guide.

**Expected Result:** Two HTTP 200 responses; one intentional HTTP 404 response; all three requests run with 12 passing post-response assertions and no test failures.

**Observed Result (Postman Collection Runner screenshot):**

| Test ID | HTTP response | Assertions |
| --- | --- | --- |
| GH-008-01 — Retrieve Public Repository | 200 | 4 passed |
| GH-008-02 — Repository Not Found | 404 (expected negative case) | 4 passed |
| GH-008-03 — List Repository Commits | 200 | 4 passed |
| **Combined** | **3 requests, 1 iteration** | **12 passed, 0 failed, 0 skipped** |

- **Run timestamp displayed by Postman:** October 12, 2026, 12:26:14 PM (time zone not displayed).
- **Source:** Runner; **Environment:** none; **Duration:** 1 second 447 milliseconds; **Errors:** 0.
- **Supporting evidence:** Postman screenshots supplied during the step-by-step walkthrough, including the imported collection, individual request results, and final Runner summary. The screenshots were reviewed in the conversation and are not stored in this Git repository.
- **Content verification:** The published Collection v2.1 JSON was previously checked to contain the three GET requests, the two enabled GitHub headers per request, and the 12 original post-response assertions.
- **Document verification:** Confirmed the actual Postman web import-as-copy and Local Functional Runner workflow matched the guide's instructions.

**Status:** Passed — the project author reproduced all three individual requests and the full 12-assertion collection run from the GitHub-exported artifact.

**Scope Note:** This is an author-led reproduction/acceptance test, **not an independent peer review**. Rate-limit troubleshooting, unexpected API failures, other operating systems or Postman clients, authentication, and CI execution were not tested by this walkthrough. Future GitHub or Postman interface changes may require revalidation.

## GH-010 — Documentation Quality Review

**Objective:** Audit the current GitHub Documentation Lab artifacts for accuracy, consistency, discoverability, and portfolio readiness without changing repository visibility.

**Prerequisites:** Existing README, repository-creation guide, Postman testing guide, GH-001–GH-009 validation record, and exported Collection v2.1 JSON.

**Procedure:** Enumerated the default-branch file inventory; inspected all Markdown and the JSON collection; checked internal relative links and Markdown anchors; compared workflow instructions with current official GitHub and Postman documentation; corrected stale statuses, duplicate-import steps, Collection Runner instructions, and the repository-creation guide's expected-versus-observed language; documented the external-publication gate.

**Expected Result:** Internal documentation links resolve, test specifications match the archived JSON, published completion statuses are consistent with observed evidence, limitations are clear, and remaining portfolio-release blockers are recorded.

**Observed Result:** Four existing Markdown files and one Postman JSON file reviewed; Postman JSON parsed with three GET requests and twelve `pm.test` assertions; no missing internal link destinations or heading anchors detected by the static check; no recognized GitHub-token/PEM markers found in the current checked files. Updated the README and two guides and created [`quality-review-gh-010.md`](quality-review-gh-010.md). Confirmed the repository remains private; historical commits and independent beginner usability/accessibility were not audited.

**Status:** Passed — documentation quality review and targeted corrections completed on a working branch; portfolio publication **not approved** and remains blocked pending history review and a visibility decision.

**Scope Note:** This is a static/documentary review, not a new external Postman run or independent peer approval. The creation guide remains a draft pending a full beginner walkthrough. See [GH-010 report](quality-review-gh-010.md) for findings and publication gate.

## GH-011 — Pre-Publication History and Security Review

**Objective:** Assess whether the existing private documentation repository is an appropriate candidate for public portfolio access without discarding its authentic Git history.

**Procedure:** Audited the 29 commits reachable from the reviewed `main` baseline, the tracked files and historical changed-file paths, two already-merged branch references, three merged pull requests and their available discussion/review content, Git tag references, releases, and accessible GitHub Actions run metadata. Applied bounded pattern checks to current files and historical commit changes. Compared publication and licensing implications with current GitHub Docs.

**Expected Result:** No identified secret or unexpectedly sensitive artifact in the reviewed reachable repository materials; a clear record of residual risks and owner actions required for publication.

**Observed Result:** No matching embedded credentials, PEM private keys, conventional personal email or phone-number strings, unexpected historical file types, or unmerged branch changes in the inspected content. Commit author addresses use GitHub noreply aliases. No GitHub Actions workflow runs or releases were returned. The reviewed repository history and discussions support publishing the **original repository** rather than creating a detached showcase.

**Evidence:** [GH-011 publication and security review](publication-security-review-gh-011.md).

**Status:** Passed with bounded review limitations — no identified blocker to public release in the materials inspected. **Repository visibility has not been changed as part of this test**; verify owner-controlled publication and signed-out access separately.

**Scope Note:** No local full-clone forensic scanning, examination of unreachable Git objects, complete account-wide settings audit, or independent penetration/security review was performed. Making repository history public is effectively irreversible for third-party copies.

## GH-012 — Public Portfolio Release Check

**Objective:** Verify that the owner-approved existing repository has changed from private to public while retaining its original documentation and commit history, and identify any remaining publication checks.

**Prerequisites:** Completed GH-011 pre-publication review and the repository owner's GitHub visibility change.

**Procedure performed (October 12, 2026):**
1. Reviewed the owner's GitHub Settings → General → Danger Zone screenshot, which states **This repository is currently public**.
2. Queried the connected GitHub repository metadata for `michael-k-levesque/github-documentation-lab`; it reported `visibility: public` and default branch `main`.
3. Retrieved README, validation log, and the GH-011 audit report from `main` through the connected GitHub integration; the files remained accessible through that authenticated connection.
4. Verified that the existing published README correctly describes the repository as a public portfolio project while preserving historical pre-publication audit descriptions.
5. The automated signed-out check was unavailable in the assistant's environment. The repository owner subsequently opened a Chrome **Incognito** window while GitHub displayed **Sign in** and **Sign up**, confirming the user was not authenticated in that window.
6. In that Incognito window, the owner loaded `https://github.com/michael-k-levesque/github-documentation-lab`; screenshot evidence shows the **Public** badge, tracked file list, and rendered README.
7. In the same Incognito window, the owner opened `https://github.com/michael-k-levesque/github-documentation-lab/blob/main/docs/test-github-rest-api-with-postman.md`; screenshot evidence shows the guide's rendered Markdown preview, title, audience, document status and overview. The screenshot confirms this representative documentation page was publicly accessible without signing in.

**Expected Result:** GitHub reports public visibility, original project files remain intact, and a signed-out reader can open the repository homepage and at least one representative documentation guide.

**Observed Result:** **Public visibility and representative anonymous access confirmed.** Screenshots from Chrome Incognito show the repository homepage and the rendered Postman guide accessible with GitHub's **Sign in** and **Sign up** controls visible. The guide was also retrieved successfully through the connected GitHub integration. The screenshots remain in the project conversation, not committed to the repository.

**Status:** **Passed — public visibility and signed-out access to the homepage and Postman guide verified on October 12, 2026.** This is user-performed acceptance testing, not a separate automated anonymous-browser test.

**Additional optional checks:** Signed-out browsing of the [repository creation guide](https://github.com/michael-k-levesque/github-documentation-lab/blob/main/docs/create-github-repository.md), [Postman JSON](https://github.com/michael-k-levesque/github-documentation-lab/blob/main/postman/GitHub-REST-API-Validation.postman_collection.json), and [PR #4](https://github.com/michael-k-levesque/github-documentation-lab/pull/4) was not individually demonstrated by the supplied screenshots. The relevant files were verified in the repository through the connector; these optional links are not represented as separately anonymous-tested.

**Scope Note:** GH-011's security/history review was a bounded audit. GH-012 confirms externally accessible public pages, not a penetration test, historical artifact scan, or independent peer review.

## GHDCS-2 — Author-Led Repository Creation Walkthrough

**Objective:** Execute and verify a single, safe GitHub.com repository-creation procedure to identify actual interface labels and validate the beginner guide's core steps.

**Session:** October 2026, performed by the project author under instruction. The screenshots in the supporting project conversation document the creation form and the resulting repository page; the original screenshot files are not included in this public repository.

**Prerequisites and test configuration:** Authorized personal GitHub account, signed-in web browser, a new disposable repository, **Private** visibility, **Add README: On**, **No .gitignore**, and **No license**. No existing portfolio repository was modified in the execution of this test. The private practice repository's contents are not part of this public evidence package.

**Procedure:** Opened `https://github.com/new`; selected the personal owner; entered an available, non-sensitive repository name and a temporary-purpose description; chose Private; enabled README; kept optional .gitignore and license disabled; selected **Create repository**; examined the new repository's Code page and the metadata available in the connected GitHub account.

**Expected result:** The repository is created under the chosen owner, remains private, contains the requested README and initial commit, and displays a default branch.

**Observed result:** The creation form presented **General** (Owner, Repository name, Description) and **Configuration** (Choose visibility, Add README, Add .gitignore, Add license) sections. GitHub confirmed the entered name was available. The resulting repository page displayed the expected owner and name, a **Private** badge, `README.md` rendered on the page, one branch named `main`, and **1 Commit**. GitHub repository metadata corroborated private visibility and the default branch.

| Planned verification | Outcome |
| --- | --- |
| Authorized owner selected | Pass |
| Repository name accepted as available | Pass |
| Description entered | Pass |
| Visibility set to Private | Pass |
| Add README enabled | Pass |
| No .gitignore and No license selected | Pass |
| Repository created and opened | Pass |
| Expected file, branch, visibility, and initial commit shown | Pass |

**Result:** **Passed — 8 of 8 checks in the tested configuration.** No failures appeared in the screenshots provided.

**Scope and limitations:** This was a guided author-executed test, not an independent or unassisted novice usability study. The `+` menu route, template creation, different account types, creating an entirely empty repository, post-creation permission changes, and all troubleshooting branches were not exercised. GitHub controls and defaults can change. The private test repository's precise URL and screenshot captures have not been added to the public repository. This validation alone does not establish that the revised documentation has been independently reviewed or released.

**Traceability:** Confluence Project 02 and Jira work item **GHDCS-2** track the source-baseline review, observed workflow, draft documentation change, review steps, and remaining publication gate. The planned guide revision is in `docs/create-github-repository.md`; the proposed branch is `docs/ghdcs-2-repository-guide`.

## Planned Validation Activities

- [X] GH-003 — Create and edit a documentation file.
- [X] GH-004 — Create and switch branches.
- [X] GH-005 — Submit a pull request.
- [X] GH-006 — Review and merge a pull request.
- [X] GH-007 — Test repository access and configuration.
- [X] GH-008 — Validate selected GitHub REST API operations.
- [X] GH-009 — Verify the Postman API testing guide through a fresh import and run.
- [X] GH-010 — Review documentation quality and record publication blockers.
- [X] GH-011 — Review reachable repository history and publication risks.
- [X] GH-012 — Verify public visibility **and** signed-out access to the portfolio repository homepage and representative guide.

## Validation Standards

Every completed test should document its prerequisites, procedure, expected result, actual result, and outcome.

Unexpected behavior must be recorded rather than omitted. Procedures should be retested when relevant GitHub functionality changes.
