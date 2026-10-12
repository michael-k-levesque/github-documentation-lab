# GitHub Documentation Lab

An independent technical-writing project focused on developing, testing, and validating GitHub documentation using real software workflows.

**Portfolio case study:** This repository shows the actual documentation-development process: version-controlled task guides, branching and pull-request exercises, a reusable Postman REST API test collection (three requests / twelve assertions), and a validation log distinguishing observed results from remaining limitations. Tests were performed by the project author; no independent peer review is claimed.

## Project Purpose

This repository provides a controlled practice environment for researching GitHub functionality, documenting technical procedures, and verifying instructions before incorporating them into a professional documentation portfolio.

## Project Objectives

- Develop accurate, task-based GitHub documentation.
- Practice repository setup, file management, and version control.
- Test branching, commits, pull requests, and review workflows.
- Create troubleshooting and configuration guides.
- Explore the GitHub REST API using Postman.
- Apply consistent formatting, terminology, and documentation quality standards.

## Documentation Structure

- `README.md` — Project introduction, documentation index, and testing instructions.
- [`docs/create-github-repository.md`](docs/create-github-repository.md) — Draft task-based GitHub repository creation guide (full technical review pending).
- [`docs/validation-log.md`](docs/validation-log.md) — Test procedures, observed results, and limitations for GH-001 through GH-009.
- [`docs/test-github-rest-api-with-postman.md`](docs/test-github-rest-api-with-postman.md) — GH-009 Postman testing guide (**author-led reproduction passed October 12, 2026; no independent peer review**).
- [`postman/GitHub-REST-API-Validation.postman_collection.json`](postman/GitHub-REST-API-Validation.postman_collection.json) — Importable Postman collection with automated REST API checks.
- [`docs/quality-review-gh-010.md`](docs/quality-review-gh-010.md) — GH-010 documentation quality review and original release-gate findings.
- [`docs/publication-security-review-gh-011.md`](docs/publication-security-review-gh-011.md) — GH-011 review of reachable commit history, pull-request discussions, current files, and publication risks.

## Run the GitHub REST API tests in Postman

The GH-008 case study includes three **read-only, unauthenticated** requests against GitHub's public `octocat/Hello-World` repository, with **four post-response assertions per request**.

| Request | Behavior under test | Expected HTTP status | Assertions |
| --- | --- | --- | --- |
| GH-008-01 — Retrieve Public Repository | Verify the repository identity and public visibility | `200 OK` | 4 |
| GH-008-02 — Repository Not Found | Verify GitHub's expected error response for a deliberately invalid repository name | `404 Not Found` | 4 |
| GH-008-03 — List Repository Commits | Verify the commits response is a non-empty JSON array with commit identifiers and messages | `200 OK` | 4 |

### Prerequisites

- Postman desktop or web app capable of sending HTTP requests (the Postman web app may require an available agent).
- Internet access to `https://api.github.com`.
- **No API key, personal access token, or repository access is required** for these public requests. GitHub's unauthenticated rate limits still apply.

### Import and execute

1. Open the [Postman collection JSON](postman/GitHub-REST-API-Validation.postman_collection.json) on GitHub and use **Raw** to download it (or save the raw JSON as a `.json` file).
2. In Postman, choose **Import** and select the downloaded JSON file. If Postman displays **Collection exists**, choose **Import as Copy** to avoid overwriting the original collection.
3. In **Collections**, expand the newly imported **GitHub REST API Validation** collection (or **GitHub REST API Validation Copy**) and open the first request. Verify that `Accept: application/vnd.github+json` and `X-GitHub-Api-Version: 2026-03-10` are enabled.
4. Click **Send**, then open **Test Results** to see that request's four automated assertions. Repeat for the other two saved requests.
5. To execute the entire suite, select the newly imported collection, choose **Run**, set **Functional**, **Local**, **Iterations: 1**, and confirm all three requests are selected before choosing **Start run**. Expect **12 passing assertions** when GitHub returns the documented responses. The `404` in GH-008-02 is intentional and should pass its assertions.

For a detailed walkthrough, including error interpretation, test assertions, troubleshooting, and evidence collection, see the [GH-009 Postman testing guide](docs/test-github-rest-api-with-postman.md). **GH-009 was reproduced on October 12, 2026: the archived collection imported successfully and all 12 assertions passed in a local functional collection run.** This was an author-led walkthrough, not independent peer review.

The exported collection contains the request definitions and test scripts; **it does not include stored response snapshots or independently certify future test runs**. The observed results and testing limitations are recorded in [GH-008 of the validation log](docs/validation-log.md#test-gh-008--validate-selected-github-rest-api-operations).

## Documentation Standards

Documentation will be developed using the following principles:

- Clear, audience-appropriate instructions.
- Verified technical procedures.
- Defined prerequisites and expected results.
- Consistent terminology and formatting.
- Accessible, maintainable content.
- Version-controlled revisions.

## Project Status

**Documentation reviewed; publication decision pending.**

GH-001 through GH-009 have recorded workflow outcomes, including GH-009's successful import-and-rerun verification. GH-010 reviewed documentation quality. GH-011 found no identified blocker in the reviewed reachable history or repository discussions to publishing this **existing** repository, with the limits documented in the [publication security review](docs/publication-security-review-gh-011.md). The repository-creation guide remains a draft pending a separate end-to-end beginner walkthrough.

**Visibility at last review:** Private. Public access must be enabled by the repository owner in GitHub settings and verified from a signed-out browser before sharing the link. Once visibility changes, this statement and the older historical status notes should be read in light of the publication date.

## Project Context

This repository is part of an independent technical-writing portfolio project. It is not affiliated with or endorsed by GitHub or Atlassian.
