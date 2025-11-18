# Example Workflow Files for Using Reusable Workflows

This directory contains example workflows that demonstrate how to use the centralized reusable workflows from this repository in your own projects.

## Changelog Verification

Create `.github/workflows/verifyChangelog.yaml` in your repository:

```yaml
name: Changelog Check

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  verify-changelog:
    uses: SchoutenEnZn/.github/.github/workflows/verifyChangelog.yaml@main
```

## Release Creation

Create `.github/workflows/createRelease.yaml` in your repository:

```yaml
name: Create Release

on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Version number (e.g., v1.0.0). Leave blank to use latest from CHANGELOG.md.'
        required: false
  pull_request:
    types:
      - closed

permissions:
  contents: write

jobs:
  create-release:
    # Only run on merged PRs or manual dispatch
    if: github.event_name == 'workflow_dispatch' || github.event.pull_request.merged == true
    uses: SchoutenEnZn/.github/.github/workflows/createRelease.yaml@main
    with:
      version: ${{ github.event.inputs.version }}
```

## Quick Setup Commands

Copy-paste these commands to quickly set up both workflows in your repository:

```bash
mkdir -p .github/workflows

# Create changelog verification workflow
cat > .github/workflows/verifyChangelog.yaml << 'EOF'
name: Changelog Check

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  verify-changelog:
    uses: SchoutenEnZn/.github/.github/workflows/verifyChangelog.yaml@main
EOF

# Create release workflow
cat > .github/workflows/createRelease.yaml << 'EOF'
name: Create Release

on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Version number (e.g., v1.0.0). Leave blank to use latest from CHANGELOG.md.'
        required: false
  pull_request:
    types:
      - closed

permissions:
  contents: write

jobs:
  create-release:
    if: github.event_name == 'workflow_dispatch' || github.event.pull_request.merged == true
    uses: SchoutenEnZn/.github/.github/workflows/createRelease.yaml@main
    with:
      version: ${{ github.event.inputs.version }}
EOF

# Commit the workflows
git add .github/workflows/
git commit -m "Add changelog verification and release workflows"
git push
```
