# How to Create a GitHub Repository

**Audience:** Beginning GitHub users  
**Platform:** GitHub.com (web interface)  
**Document status:** Draft — validation in progress

## Overview

A GitHub repository stores project files and their revision history. Repositories support version control, collaboration, and documentation management.

This guide explains how to create a repository using the GitHub web interface.

## Prerequisites

You must have a GitHub account and be signed in. You must also have permission to create repositories under the selected account or organization.

## Procedure

1. Open [GitHub](https://github.com) and sign in.
2. Select the **+** menu near the upper-right corner, then select **New repository**. Alternatively, navigate directly to https://github.com/new.
3. Under **Owner**, select the personal account or organization that will own the repository.
4. In **Repository name**, enter a descriptive name. GitHub indicates whether the name is available.
5. Optionally, enter a short explanation of the repository's purpose in **Description**.
6. Under **Choose visibility**, select one of the following:
   - **Public:** Anyone can view the repository.
   - **Private:** Access is restricted to authorized users.
7. Under **Add README**, enable the option if you want GitHub to initialize the repository with a `README.md` file.
8. Under **Add .gitignore**, select an appropriate template if the project requires files to be excluded from version control. Otherwise, retain **No .gitignore**.
9. Under **Add license**, select a license if appropriate for the project. Otherwise, retain **No license**.
10. Review the configuration, then select **Create repository**.

## Expected Result

GitHub opens the newly created repository.

The repository should display the selected name and visibility. If you enabled README initialization, the repository should contain `README.md` and an initial commit.

The default branch name depends on the applicable GitHub configuration.

## Verify the Repository

After creating the repository, confirm that GitHub saved your selected configuration:

1. On the repository's **Code** tab, verify that the owner and repository name are correct.
2. Check the **Public** or **Private** badge beside the repository name. Confirm that it matches the visibility you selected.
3. If you enabled **Add README**, verify that `README.md` appears in the file list and that its contents display correctly.
4. If GitHub created an initial commit, open the repository's commit history and confirm that the commit is recorded.

## Verification Result

The repository opens under the selected owner, displays the chosen visibility, and contains the requested initialization files.

## Repository Visibility and Access

Repository visibility determines who can view a repository. It does not automatically determine who can modify its contents.

- **Public repositories:** Anyone can view the repository and its contents. Only users with appropriate permissions can make changes directly to the repository.
- **Private repositories:** Access is limited to the owner and other authorized users, such as invited collaborators or eligible organization members.

Sharing the URL of a private repository does not grant someone access. Access must be provided through the appropriate GitHub permissions.

Before sharing a repository, confirm that its visibility is appropriate for the information it contains.

## Troubleshooting

### Repository name is unavailable

Choose another name. Repository names must be unique within the selected owner's account.

### Repository creation is not permitted

Verify that you are signed in and have permission to create repositories for the selected owner. Organization policies may restrict repository creation.

### README is missing

Check whether **Add README** was enabled during repository creation. A README can be added afterward.

## Notes

Do not store passwords, access tokens, private keys, or other sensitive information in repository files.

This guide covers GitHub.com through a web browser. GitHub Enterprise installations and future interface revisions may differ.

## Reference

GitHub Docs — Creating a new repository  
https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository
