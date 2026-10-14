# How to Create a GitHub Repository

**Audience:** Beginning GitHub users  
**Platform:** GitHub.com (web interface)  
**Document status:** Updated against GitHub Docs and the author's October 2026 hands-on repository-creation walkthrough (8 of 8 checks passed for the tested configuration). Independent beginner usability review and optional-path testing remain pending.

## Overview

A GitHub repository stores project files and their revision history. Repositories support version control, collaboration, and documentation management.

This guide explains how to create a repository using the GitHub web interface. The initial GH-001 setup and a later, separately recorded GHDCS-2 practice walkthrough demonstrate successful initialization under the configurations tested. These tests do not establish that every option, account type, or future interface variation has been verified.

## Prerequisites

You must have a GitHub account and be signed in. You must also have permission to create repositories under the selected account or organization. For a first practice run, choose an account you control and use **Private** visibility unless you specifically intend to publish the contents.

## Procedure

These instructions describe creation of a **new, blank repository**. GitHub can also create repositories from templates, but template-based creation was not part of the recorded walkthrough. See [GitHub's template procedure](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) if that is your goal.

1. Open [GitHub](https://github.com) and sign in.
2. Select the **+** menu near the upper-right corner, then choose **New repository**. Alternatively, open [github.com/new](https://github.com/new) directly. **The direct URL was used in the documented test; the + menu path is supported by GitHub Docs but was not separately tested in that session.**
3. In the **General** section, under **Owner**, select the personal account or organization that should own the repository.
4. In **Repository name**, enter a short, descriptive name. GitHub indicates whether that name is available under the selected owner.
   - GitHub's documented limit is **100 characters**.
   - Use ASCII letters, digits, periods (`.`), hyphens (`-`), or underscores (`_`). Avoid spaces and other characters.
   - If GitHub reports the name is unavailable, choose a different one.
5. Optionally, enter a concise description in **Description**.
6. In the **Configuration** section, open **Choose visibility** and select:
   - **Public:** Anyone on the internet can view the repository.
   - **Private:** Access is restricted to authorized people.
   **Check the actual selection.** Do not assume the default choice is Private.
7. Under **Add README**, switch the toggle to **On** if you want GitHub to initialize the repository with a `README.md` file and an initial commit.
8. Under **Add .gitignore**, select a template only if the project needs one. Otherwise leave **No .gitignore**.
9. Under **Add license**, choose a license only if it is appropriate for your project. Otherwise leave **No license**. Public visibility does not itself grant a reuse license.
10. Review the owner, name, visibility, README toggle, and optional files. Then select **Create repository**.
11. Wait for GitHub to open the new repository's **Code** page before proceeding to [Verify the Repository](#verify-the-repository).

### Example: safe beginner practice configuration

This is an example for someone following the same controlled exercise—not a required setting for every project.

| Field | Practice value |
| --- | --- |
| Owner | An account you control |
| Repository name | `documentation-walkthrough-sandbox` (or another available, non-sensitive name) |
| Description | `Temporary repository for testing and validating GitHub documentation procedures.` |
| Choose visibility | **Private** |
| Add README | **On** |
| Add .gitignore | **No .gitignore** |
| Add license | **No license** |

The practice configuration above was successfully used in an author-led walkthrough. **Do not upload sensitive information or change existing repositories for this exercise.**

**If you are importing an existing Git repository:** GitHub advises leaving the optional initialization files unselected to avoid introducing merge conflicts. You can add a README, `.gitignore`, or license after importing.

## Expected Result

GitHub opens the newly created repository.

The repository should display the selected owner, name, and visibility. If you enabled README initialization, the file list should contain `README.md`, with a corresponding initial commit. In the documented practice run, GitHub displayed the **Private** badge, the `main` branch, one branch, and one initial commit.

The default branch name depends on the applicable GitHub configuration. If you did not initialize the repository with a README, license, or other file, GitHub may instead display **Quick setup** with instructions for adding files or pushing an initial commit.

## Verify the Repository

After creating the repository, confirm that GitHub saved your selected configuration:

1. On the repository's **Code** tab, verify that the owner and repository name are correct.
2. Check the **Public** or **Private** badge beside the repository name. Confirm that it matches the visibility you selected.
3. If you enabled **Add README**, verify that `README.md` appears in the file list and that its contents display correctly.
4. Confirm that the repository page shows a commit count. If needed, open **Commits** to inspect the history and confirm the initial commit; a successful practice run displayed **1 Commit**.
5. Confirm that the branch selector shows the branch GitHub actually created (in the recorded practice run it was `main`). Do not assume that every account uses `main` by default.

## Successful Verification Looks Like

A correctly created repository opens under the selected owner, displays the chosen visibility, and contains any initialization files you requested. If you created an empty repository, it will not yet have a commit history.

**Recorded test:** In the GHDCS-2 author-led walkthrough, all eight planned repository-creation and initial-verification checks passed: owner, accepted repository name, description, private visibility, README enabled, no optional .gitignore/license, successful creation, and the expected repository page with `main` and one initial commit. The result is based on pre-creation and post-creation screenshots and repository metadata. It does **not** represent independent usability testing of a beginner who received no assistance.

## Repository Visibility and Access

Repository visibility determines who can view a repository. It does not automatically determine who can modify its contents.

- **Public repositories:** Anyone can view the repository and its contents. Only users with appropriate permissions can make changes directly to the repository.
- **Private repositories:** Access is limited to the owner and other authorized users, such as invited collaborators or eligible organization members.

Sharing the URL of a private repository does not grant someone access. Access must be provided through the appropriate GitHub permissions.

Before sharing a repository, confirm that its visibility is appropriate for the information it contains.

## Troubleshooting

### Repository name is unavailable or rejected

Choose another name. Repository names must be unique within the selected owner's account, at most 100 characters long, and use GitHub's permitted characters. Recheck the selected owner and the availability indicator.

### Repository creation is not permitted

Verify that you are signed in and have permission to create repositories for the selected owner. Organization policies may restrict repository creation.

### README is missing

Check whether **Add README** was enabled during repository creation. A README can be added afterward. If you intentionally created an empty repository, GitHub may show a **Quick setup** screen rather than a README and initial commit.

### Repository is public when you expected private

Check the repository visibility badge before placing content in it. Stop and review [GitHub's visibility-change guidance](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility) before changing settings; making a public repository private does not undo previous public exposure.

## Notes

Do not store passwords, access tokens, private keys, or other sensitive information in repository files.

This guide covers GitHub.com through a web browser. GitHub Enterprise installations and future interface revisions may differ.

## Reference

- [GitHub Docs — Creating a new repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository)
- [GitHub Docs — About the repository README file](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
- [GitHub Docs — Creating a repository from a template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)
- [GitHub Docs — About repositories and visibility](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories)
