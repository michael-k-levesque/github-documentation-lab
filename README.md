# GitHub Documentation Lab

**Technical-writing case study · GitHub workflows · REST API documentation · Postman testing**

A public portfolio project demonstrating how I research software workflows, write task-based technical instructions, verify procedures with working software, and document results in version control.

**Author:** Michael Levesque · [LinkedIn](https://www.linkedin.com/in/mklevesque)

## Start here

| What to review | What it demonstrates |
| --- | --- |
| **[How to Test the GitHub REST API Using Postman](docs/test-github-rest-api-with-postman.md)** | Primary writing sample: audience-focused instructions, prerequisites, annotated testing process, result interpretation, troubleshooting, and limitations |
| **[Postman collection (JSON)](postman/GitHub-REST-API-Validation.postman_collection.json)** | Reusable executable test artifact: three read-only GitHub REST API requests with 12 post-response assertions |
| **[Validation log](docs/validation-log.md)** | Recorded objectives, procedures, expected and observed results, supporting evidence, and boundaries of each test |
| **[How to Create a GitHub Repository](docs/create-github-repository.md)** | Beginner-oriented task guide covering creation, visibility, initialization, verification, and troubleshooting; full novice walkthrough still pending |

## Case study: Documenting a reproducible API test workflow

**The challenge:** API testing instructions need to be usable by someone who did not write the original tests. A successful response alone is not enough: the reader must understand the request, what to inspect, which results are expected, and how to distinguish a genuine failure from an intentionally tested error response.

**My approach:** I created a task-based Postman guide, assembled a reusable collection of public GitHub REST API requests, recorded the results in a structured validation log, and maintained the documentation through branches, commits, and pull requests. The guide covers importing the collection, checking request headers, executing tests individually and together, interpreting responses, and troubleshooting common problems.

**Observed result:** On October 12, 2026, I downloaded the exported collection from GitHub, imported it as a separate copy in Postman, sent all three requests, and ran one local functional collection test. The Postman Collection Runner reported **12 passed, 0 failed, 0 skipped, and 0 errors**. This is an author-led reproduction, not independent peer review.

### Verified test cases

| Test case | Expected HTTP status | Observed result | Assertions |
| --- | --- | --- | --- |
| GH-008-01 — Retrieve Public Repository | `200 OK` | `200 OK` | 4/4 passed |
| GH-008-02 — Repository Not Found | `404 Not Found` | `404 Not Found` (intentional negative test) | 4/4 passed |
| GH-008-03 — List Repository Commits | `200 OK` | `200 OK` | 4/4 passed |
| **Total** | **Three GET requests** | **One successful collection run** | **12/12 passed** |

The test targets GitHub's public `octocat/Hello-World` repository. The `404` response is *expected*: the assertion checks whether GitHub handles a nonexistent repository as documented. HTTP error status and failed Postman assertion are not the same thing.

## Try the API tests yourself

1. Open the [Postman collection JSON](postman/GitHub-REST-API-Validation.postman_collection.json) and download its raw `.json` file.
2. Open Postman, choose **Import**, and select that file. If the collection already exists, choose **Import as Copy**.
3. Select the imported collection and verify its three `GET` requests. No authentication token is required for these public endpoints.
4. Choose **Run** → **Functional** → **Local**, select all three requests, set **Iterations** to `1`, and start the run.
5. Compare the results with the table above and the [validation log](docs/validation-log.md#gh-009--postman-guide-procedure-verification).

For the full procedure, required headers, screenshots-to-capture guidance, test-assertion explanations, and troubleshooting, follow the [Postman testing guide](docs/test-github-rest-api-with-postman.md).

**Requirements and caveats:** You need Postman (web with a working request agent, or desktop) and access to `api.github.com`. The collection is read-only and unauthenticated. GitHub rate limits, network conditions, or API changes can affect future outcomes; the stored JSON does not contain response recordings or guarantee another 12/12 run.

## Documentation workflow and evidence

The repository's commit and pull-request history shows iterative development rather than a finished document uploaded without its working record:

- **Research and drafting:** Task-based Markdown documentation with defined audiences, prerequisites, ordered actions, expected outcomes, and troubleshooting.
- **Version control:** Separate branches, commit messages, pull-request comparisons, self-review, and merges into `main`.
- **Functional validation:** GH-008 API tests and GH-009 collection import/rerun, with results recorded in the [validation log](docs/validation-log.md).
- **Quality and release review:** [GH-010 documentation audit](docs/quality-review-gh-010.md), [GH-011 bounded history/security review](docs/publication-security-review-gh-011.md), and [GH-012 signed-out publication check](docs/validation-log.md#gh-012--public-portfolio-release-check).

The project uses GitHub, Markdown, Postman, GitHub's REST API, and Jira work-item references where applicable.

## Project scope and limitations

This is an **independent portfolio case study**, not official GitHub or Postman documentation. The examples cover selected GitHub web workflows and three unauthenticated, read-only API endpoints—not comprehensive API coverage, authenticated operations, CI integration, or penetration testing.

The **Postman guide** was reproduced successfully in an author-led walkthrough. The **repository-creation guide** has been source-reviewed, but its complete beginner usability walkthrough remains pending. No independent peer review or exhaustive security assurance is claimed. Dates and earlier references to a private repository in the audit records reflect the state when those reviews occurred; the repository is now public.

---

**Primary writing sample:** [Read the Postman REST API testing guide](docs/test-github-rest-api-with-postman.md) · **Technical evidence:** [View the validation log](docs/validation-log.md) · **Professional profile:** [LinkedIn](https://www.linkedin.com/in/mklevesque)
