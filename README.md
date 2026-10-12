# GitHub Documentation Lab

An independent technical-writing project focused on developing, testing, and validating GitHub documentation using real software workflows.

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
- [`docs/validation-log.md`](docs/validation-log.md) — Test procedures and evidence for GH-001 through GH-008.
- [`postman/GitHub-REST-API-Validation.postman_collection.json`](postman/GitHub-REST-API-Validation.postman_collection.json) — Importable Postman collection with automated REST API checks.

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
2. In Postman, choose **Import** and select the downloaded JSON file.
3. Expand **GitHub REST API Validation** and open a request. Verify that the `Accept: application/vnd.github+json` and `X-GitHub-Api-Version: 2026-03-10` headers are enabled.
4. Click **Send**, then open **Test Results** to see the four automated assertions for that request. Repeat for the other two requests, or run the collection in Postman's Collection Runner.
5. Expect **12 passing assertions across the three requests** when GitHub returns the documented responses. The `404` in GH-008-02 is intentional; its assertions should pass.

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

**In Development**

The practice repository has been initialized. Documentation development, workflow testing, and technical validation are ongoing activities.

## Project Context

This repository is part of an independent technical-writing portfolio project. It is not affiliated with or endorsed by GitHub or Atlassian.
