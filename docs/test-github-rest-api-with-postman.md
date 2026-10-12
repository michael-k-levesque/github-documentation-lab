# How to Test the GitHub REST API Using Postman

**Audience:** Technical writers, QA analysts, support engineers, and developers who need to reproduce and document REST API behavior.  
**Platform:** Postman (web or desktop), GitHub REST API  
**Document status:** Validated walkthrough — GH-009 reproduced from the archived collection on October 12, 2026; independent peer review not performed  
**Case study:** GH-009, based on the completed GH-008 test suite  
**Last reviewed:** October 2026

## Overview

This guide explains how to import a reusable Postman collection, send three read-only requests to GitHub's public REST API, interpret the responses, and evaluate the automated test results. It also shows how to distinguish an intentionally failing HTTP request from a failed test assertion.

The project uses three real requests and 12 post-response assertions recorded during GH-008. The archived collection is the executable test artifact; the [GH-008 validation log](validation-log.md#test-gh-008--validate-selected-github-rest-api-operations) records the original observations. A new reader's results may differ if the API, network, or public repository changes.

### Learning objectives

After completing this guide, you should be able to:

1. Import a Postman Collection v2.1 JSON file without changing its request definitions.
2. Inspect the HTTP method, URL, headers, authorization, and post-response scripts.
3. Execute individual requests and a functional collection run.
4. Identify the expected `200 OK` and `404 Not Found` response bodies.
5. Explain what each of the 12 automated assertions verifies, and what it *does not* prove.
6. Capture reproducible test evidence and diagnose common failures.

## Before you begin

### Prerequisites

- An account or installation that can open Postman. The Postman web app must have an available request-sending agent; the desktop app can send supported HTTP requests directly.
- Internet access to `https://api.github.com`.
- The [GitHub REST API Validation Postman collection](../postman/GitHub-REST-API-Validation.postman_collection.json).
- Basic familiarity with HTTP methods, status codes, JSON objects, and JSON arrays.

**Authorization:** No Auth. All three saved requests use publicly accessible GitHub endpoints. You do **not** need a personal access token or write access to the private documentation-lab repository.

**Safety:** The collection performs only `GET` operations. Do not add authentication tokens to this example or publish environment files containing secrets. Avoid repeatedly running tests while rate limited.

### Test configuration

The saved collection contains three requests, each with the same enabled headers:

| Header | Value | Purpose |
| --- | --- | --- |
| `Accept` | `application/vnd.github+json` | Requests GitHub's recommended JSON representation. |
| `X-GitHub-Api-Version` | `2026-03-10` | Pins a supported GitHub REST API version to make the intended contract explicit. |

The collection uses literal URLs and requires **no environment variables**. If Postman displays additional *generated/hidden headers*, leave them unchanged unless troubleshooting a specific issue.

## 1. Import the collection

1. Open the [collection JSON](../postman/GitHub-REST-API-Validation.postman_collection.json) in GitHub and use **Raw** to obtain the original JSON file. Download or save it with a `.json` extension, without copying the rendered GitHub page.
2. Open a Postman workspace. Select **Import** (some versions label the entry point **Use resources or import**).
3. Select the saved JSON file, or drag the file into the import dialog.
4. Finish importing. Under **Collections**, confirm that **GitHub REST API Validation** appears.
5. Expand the collection and confirm the three saved requests listed below.

**If the collection already exists:** Importing may create a second copy, depending on the workspace and import choice. Select the newly imported collection for this exercise so you do not accidentally modify your previous test evidence.

### Imported requests

| Test ID | Saved request name | Method and endpoint | Expected status |
| --- | --- | --- | --- |
| GH-008-01 | Retrieve Public Repository (200 OK) | `GET https://api.github.com/repos/octocat/Hello-World` | `200 OK` |
| GH-008-02 | Repository Not Found (404) | `GET https://api.github.com/repos/octocat/Hello-World-NOT-A-REAL-REPO-GH008` | `404 Not Found` |
| GH-008-03 | List Repository Commits (200 OK) | `GET https://api.github.com/repos/octocat/Hello-World/commits` | `200 OK` |

These requests test **two GitHub REST API operations** (retrieve repository and list commits) and **two response scenarios** (successful lookup and deliberately invalid lookup).

## 2. Inspect a saved request before sending it

Use **GH-008-01 — Retrieve Public Repository (200 OK)** as the starting example.

1. Select the request from the collection.
2. Confirm the method is **GET** and the URL matches the table above.
3. Open **Authorization**; verify the effective request authorization is **No Auth**.
4. Open **Headers**; verify both headers in **Test configuration** are enabled and their values match exactly. Check for conflicting duplicate headers if you edited the request.
5. Open **Scripts → After response** (some Postman versions call this **Post-response**). Confirm that four `pm.test(...)` blocks are present.
6. Do not change the script or endpoint during the first run.

### Anatomy of a post-response assertion

An excerpt from GH-008-01:

```javascript
pm.test("GH-008-01: HTTP status is 200", function () {
    pm.response.to.have.status(200);
});
```

- `pm.test(name, function)` registers a named assertion, so its outcome appears in **Test Results**.
- `pm.response` refers to the response for the request just sent.
- `to.have.status(200)` checks the HTTP status, independently of whether Postman was able to display JSON.
- Other assertions use `pm.expect(...)` to compare values parsed from `pm.response.json()`.

**Important:** A script proves only the conditions it actually checks. For example, confirming that the response is a non-empty commits array does not verify the entire commit history, the API's pagination behavior, or authentication rules.

## 3. Send the positive repository request (GH-008-01)

1. With GH-008-01 open, select **Send**.
2. In the response panel, confirm the HTTP status is `200 OK`.
3. Open **Body** and use the JSON view. Locate the repository identity and visibility fields.
4. Open **Test Results** and confirm that four tests passed.

The four saved assertions require:

| Assertion | Required result |
| --- | --- |
| HTTP status | `200` |
| Response content type | `Content-Type` includes `application/json` |
| Repository identity | `id: 1296269`; `name: "Hello-World"`; `full_name: "octocat/Hello-World"`; `owner.login: "octocat"` |
| Visibility | `private: false` |

Example *selected* fields (not the complete API response):

```json
{
  "id": 1296269,
  "name": "Hello-World",
  "full_name": "octocat/Hello-World",
  "private": false,
  "owner": {
    "login": "octocat"
  }
}
```

**Expected outcome:** `200 OK` and **4/4 passed**.

**Interpretation:** The assertions establish that the response matched the saved test's expected identity, content type, and visibility. The fixed repository ID is useful for this case study, but may require maintenance if the test fixture changes; do not reuse it for arbitrary repositories.

## 4. Send the expected-error request (GH-008-02)

1. Select **GH-008-02 — Repository Not Found (404)**.
2. Confirm that its URL contains `Hello-World-NOT-A-REAL-REPO-GH008` and that authorization and headers match the saved configuration.
3. Select **Send**.
4. Check the HTTP status, response JSON, and **Test Results**.

The four saved assertions require:

| Assertion | Required result |
| --- | --- |
| HTTP status | `404` |
| Response content type | `Content-Type` includes `application/json` |
| Error message | `message` equals `"Not Found"` |
| Error status field | `status` equals the string `"404"` |

Example *selected* fields:

```json
{
  "message": "Not Found",
  "status": "404"
}
```

**Expected outcome:** HTTP `404 Not Found` **and 4/4 passed**. A red HTTP status indicator in Postman is expected here and does not by itself mean that an automated test failed.

**Interpretation:** The deliberate invalid URL produces a negative test case. A `404` response cannot *generally* establish that a GitHub repository is nonexistent: the GitHub REST API can also conceal private or inaccessible resources with `404`. Here the invented repository path is the intended test fixture.

**Maintenance caution:** The assertion expects the JSON `status` value as a **string**. If GitHub changes the response shape, record the observed body first and then review the assertion rather than silently changing the expected result.

## 5. Send the commits request (GH-008-03)

1. Select **GH-008-03 — List Repository Commits (200 OK)**.
2. Confirm the URL ends in `/repos/octocat/Hello-World/commits`.
3. Select **Send**.
4. Confirm a `200 OK` response and examine the JSON.

The response should begin with a JSON **array**, not a single repository object. A typical abbreviated structure is:

```json
[
  {
    "sha": "example-commit-identifier",
    "commit": {
      "message": "Example commit message"
    }
  }
]
```

This illustrative snippet explains the response structure; it is **not** a saved GitHub response or proof of a particular commit.

The four saved assertions require:

| Assertion | Required result |
| --- | --- |
| HTTP status | `200` |
| Response content type | `Content-Type` includes `application/json` |
| Collection shape | JSON is a non-empty array |
| First commit fields | First entry contains non-empty string `sha` and `commit.message` |

**Expected outcome:** `200 OK` and **4/4 passed**.

**Interpretation:** The test checks the first returned commit's basic shape. It does **not** assert that all commits have been returned, validate all entries, verify commit signatures, or follow pagination links.

## 6. Run the entire collection

Use a collection run to execute all three saved requests as one test suite.

1. In **Collections**, select **GitHub REST API Validation**.
2. Select **Run** (depending on the Postman layout, this may appear in the collection's menu).
3. Choose a **Functional** run and a local/manual execution method where the interface offers these options.
4. Confirm all three requests are selected and use **one iteration**. Keep the default request order for comparison with this guide.
5. Start the run.
6. Review the summary and expand any failed assertion to inspect its name, expected value, and actual value.

### Collection acceptance criteria

| Measurement | Expected |
| --- | --- |
| Requests executed | 3 |
| Post-response assertions evaluated | 12 |
| Passing assertions | 12 |
| Failing assertions | 0 |
| HTTP status mix | Two `200` responses; one intentional `404` response |
| Unauthorized write operations | None |

**Recorded GH-009 walkthrough (October 12, 2026):** The collection downloaded from GitHub was imported in Postman as a separate copy, each request was sent individually (4/4 assertions passed), and a Local Functional collection run completed one iteration with **3 requests, 12/12 assertions passed, 0 failures, and 0 errors** (1.447 seconds total). This observation is documented in the [GH-009 validation log](validation-log.md#gh-009--postman-guide-procedure-verification). The result does not guarantee the same outcome on future executions.

A collection run result and an individually sent request are both valid ways to inspect tests, but they are different evidence artifacts. If the Collection Runner is unavailable in your client, send each saved request separately and record all three results. Do not imply that a batch run took place.

## 7. Interpret results and common HTTP behaviors

### Test result versus HTTP status

- **HTTP status** describes GitHub's response to the request.
- **Assertion result** describes whether the response matched the expected conditions written in Postman's script.
- A deliberate `404` can have **passing assertions**.
- A `200` response can still have **failing assertions** if its JSON or fields differ from expectations.

### Why a browser may show `304 Not Modified`

GH-008 also observed a `304` status when inspecting requests in Chrome DevTools, followed by `200` with caching disabled. A conditional request can return `304` when a cache validator indicates the representation has not changed. The response may have no JSON body to parse. **The Postman collection does not assert `304`**, and this browser-only observation does not count among the 12 assertions.

### Rate limits and public endpoints

GitHub's documented primary unauthenticated REST API rate limit is **60 requests per hour** for the originating IP address. Repeated requests or a shared network/agent can affect remaining allowance. Check response headers such as `x-ratelimit-remaining` and `x-ratelimit-reset` if the response changes unexpectedly. A rate-limit response may be `403` or `429`; it is *not* a passing GH-008 test. Do not immediately keep retrying.

## 8. Troubleshooting

| Symptom | Likely explanation | Recommended action |
| --- | --- | --- |
| Request does not send | Postman agent is unavailable, a proxy blocks traffic, or the network is offline. | Verify connectivity and the selected agent. In the web app, choose an available agent; alternatively, try Postman desktop. |
| `401`, unexpected `403`, or unexpected `404` | Credentials, rate limiting, wrong URL, missing access, or endpoint behavior differ from the intended public test. | Confirm **No Auth**, the exact URL, enabled headers, response body, and rate-limit headers. Do not assume every `404` means the resource is absent. |
| `403` or `429` after multiple runs | A GitHub primary or secondary rate limit may have been reached. | Inspect `retry-after`, `x-ratelimit-remaining`, and `x-ratelimit-reset`; pause according to GitHub's guidance instead of repeatedly retrying. |
| `200`, but one or more assertions fail | A response field, content type, or the expected fixture no longer matches the saved script. | Open **Test Results**, identify the exact assertion, inspect the JSON, and compare with the test contract. Keep a record before changing expectations. |
| Script throws an exception instead of listing four results | The body was not parseable JSON, or a nested field was absent when `pm.response.json()` or another expression ran. | Inspect status and raw response body first. Do not treat a script exception as a passing response. |
| Imported collection or script is missing | The wrong file was imported or a different duplicate collection is open. | Reimport the v2.1 JSON artifact and confirm all three requests and four assertions per request are present. |
| `304` or no JSON body in a browser | Conditional cache behavior rather than the expected fresh representation. | Inspect conditional request headers and caching in browser DevTools; do not apply the JSON-body assertions to a bodyless `304`. |
| Expected `404` displays a red status badge | GitHub correctly returned an HTTP error response by design. | Look at **Test Results**; the negative test passes when all four assertions pass. |
| Different response times | Network and service conditions fluctuate. | Record the observed duration, but do not use GH-008's historical response times as pass/fail thresholds. |

### A safe way to investigate failed assertions

1. Record the request ID and time of the run.
2. Capture the request method, URL, active headers, HTTP status, and response body (redact secrets if present).
3. Identify whether the failure is **transport**, **HTTP**, **data-contract**, or **test-script** related.
4. Reproduce the result once after addressing an identified issue; avoid repeated retries under a rate limit.
5. Record the observed behavior separately from your interpretation.
6. If you change a test expectation, explain the reason and preserve the revision in version control.

## 9. Capture evidence for a documentation case study

Use the following test record for a new run (do not substitute GH-008's historical results):

| Field | What to record |
| --- | --- |
| Test identifier | GH-008-01, GH-008-02, or GH-008-03 |
| Execution date/time | Include time zone |
| Client/agent | Postman web with selected agent, or Postman desktop |
| Environment | No Environment (unless you intentionally configured one) |
| Request | HTTP method, URL, and API version |
| Expected result | Expected HTTP status and assertion outcomes |
| Observed result | Actual status, pass/fail counts, and relevant JSON fields |
| Evidence | Redacted screenshot, run report, or documented response details |
| Outcome | Passed, Failed, or Blocked |
| Deviations | Any unexpected behavior, with troubleshooting and retest notes |

**Evidence discipline:** The JSON collection stores request definitions and scripts; it does **not** store screenshot evidence or execution results. GH-008's original manual runs were observed as **12/12 passed**. The author separately reproduced the workflow for GH-009 on October 12, 2026, and recorded the results in the [validation log](validation-log.md#gh-009--postman-guide-procedure-verification). Screenshots were reviewed during the walkthrough but are not committed to this repository. This is not independent peer approval.

## 10. Boundaries and next-level improvements

This small suite is intentionally safe and narrowly scoped. It does not test authenticated private repositories, token handling, write operations, webhook delivery, pagination, response schema completeness, all API fields, access-control enforcement, or CI execution.

Future extensions could add:

- A schema-based contract test to check the type and presence of additional response fields.
- Pagination tests for commit lists and careful handling of the `Link` response header.
- Parameterized collection variables for interchangeable public test repositories, with fixture-aware expectations.
- A clean CI run with captured logs and proper secrets management **if** authenticated scenarios are added.

Those extensions are **not** part of the current GH-008 evidence or the importable collection, and should not be represented as completed testing.

## Related project resources

- [Importable Postman collection](../postman/GitHub-REST-API-Validation.postman_collection.json)
- [GH-008 validation log](validation-log.md#test-gh-008--validate-selected-github-rest-api-operations)
- [GitHub Documentation Lab README](../README.md)

## Official references

- [Postman — Import data into Postman](https://learning.postman.com/docs/getting-started/importing-and-exporting/importing-data/)
- [Postman — Write scripts to test API response data](https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-scripts/)
- [Postman — Test your API using the Collection Runner](https://learning.postman.com/docs/tests-and-scripts/running-collections/intro-to-collection-runs/)
- [GitHub — REST API versions](https://docs.github.com/en/rest/about-the-rest-api/api-versions)
- [GitHub — REST API rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api)
- [GitHub — Troubleshooting the REST API](https://docs.github.com/en/rest/using-the-rest-api/troubleshooting-the-rest-api)
