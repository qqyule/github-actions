# Shared GitHub Actions

This repository centralizes reusable GitHub Actions workflows for `qqyule` projects. It contains no model credentials.

## Robin review

Add this caller workflow to each repository that should receive Robin pull-request reviews:

```yaml
name: Robin

on:
  pull_request:
    types: [opened, reopened, ready_for_review]
  issue_comment:
    types: [created]

permissions:
  actions: read
  contents: read
  pull-requests: write

jobs:
  review:
    uses: qqyule/github-actions/.github/workflows/robin-review.yml@main
    secrets:
      LLM_API_KEY: ${{ secrets.LLM_API_KEY }}
      LLM_BASE_URL: ${{ secrets.LLM_BASE_URL }}
      LLM_MODEL: ${{ secrets.LLM_MODEL }}
```

Each calling repository must define `LLM_API_KEY`, `LLM_BASE_URL`, and `LLM_MODEL` as repository secrets. This is required because the account does not have organization-level secrets and secrets are not forwarded automatically to reusable workflows.

Robin configuration, prompts, model-review parameters, and review strategy are maintained in `.github/workflows/robin-review.yml`.
