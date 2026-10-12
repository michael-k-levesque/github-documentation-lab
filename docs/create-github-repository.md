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

Confirm that the repository name and owner are correct, the visibility matches your selection, and any requested initialization files exist.

If you initialized the repository with a README, open the file and confirm that its contents are displayed.

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
