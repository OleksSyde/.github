# .github Repository

This repository contains organization-wide GitHub Actions workflows and other GitHub-related configurations for our organization.

## Contents

- [Branch Protection Workflow](#branch-protection-workflow)
- [Setup](#setup)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)

## Branch Protection Workflow

The main workflow in this repository (`new-repo-protection.yml`) automatically applies branch protection rules to newly created repositories in our organization.

### What it does

When a new repository is created, this workflow:

1. Sets up a Python environment
2. Installs necessary dependencies (PyGithub)
3. Uses the GitHub API to apply branch protection rules to the main branch

### Default Branch Protection Rules

- Requires 1 approving review for pull requests
- Dismisses stale pull request approvals when new commits are pushed
- Requires review from code owners
- Enforces these rules for repository administrators

## Setup

To use this workflow in your organization:

1. Ensure this repository is named `.github` and is public.
2. Create a Personal Access Token (PAT) with `repo` and `admin:org` scopes.
3. Add the PAT as a secret named `ORG_GITHUB_TOKEN` in your organization's settings.
4. Set up a webhook in your organization settings:
    - Payload URL: `https://api.github.com/orgs/YOUR_ORG_NAME/actions/workflows/new-repo-protection.yml/dispatches`
    - Content type: `application/json`
    - Secret: Use a secure random string
    - Events: Select "Repositories" and then "Created"

5. In the organization settings, under "Actions" > "General", ensure "Allow GitHub Actions to create and approve pull requests" is enabled.

## Customization

To customize the branch protection rules:

1. Open the `new-repo-protection.yml` file.
2. Modify the `branch.edit_protection()` function call in the Python script.
3. Commit and push your changes.

## Troubleshooting

If the workflow isn't running or applying rules as expected:

1. Check the Actions tab in this repository for any error messages.
2. Ensure the PAT hasn't expired and has the correct permissions.
3. Verify that the webhook is properly configured and receiving events.
4. Check that the repository where you're expecting rules to be applied was created after this workflow was set up.

For more help, please contact the organization's GitHub administrators.
