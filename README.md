# .github

Organization-wide templates and reusable workflows for **SchoutenEnZn** repositories.

## What's This For?

This special `.github` repository provides:
- **Community health files** - Automatically shared across all org repositories (issue templates, PR templates, contributing guidelines)
- **Reusable workflows** - Centralized GitHub Actions for changelog verification and release automation
- **Templates** - CHANGELOG and documentation templates for new repositories

## Quick Start

### Using the Reusable Workflows

**1. Changelog Verification** - Ensure PRs update CHANGELOG.md

Create `.github/workflows/verifyChangelog.yaml` in your repository:

```yaml
name: Changelog Check

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  verify-changelog:
    uses: SchoutenEnZn/.github/.github/workflows/reusable/verifyChangelog.yaml@main
```

**2. Release Automation** - Create releases from CHANGELOG.md

Create `.github/workflows/createRelease.yaml` in your repository:

```yaml
name: Create Release

on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Version (e.g., v1.0.0). Leave blank for latest from CHANGELOG.md'
        required: false
  pull_request:
    types: [closed]

permissions:
  contents: write

jobs:
  create-release:
    if: github.event_name == 'workflow_dispatch' || github.event.pull_request.merged == true
    uses: SchoutenEnZn/.github/.github/workflows/reusable/createRelease.yaml@main
    with:
      version: ${{ github.event.inputs.version }}
```

**3. Set up CHANGELOG.md**

```bash
curl -o CHANGELOG.md https://raw.githubusercontent.com/SchoutenEnZn/.github/main/CHANGELOG.template.md
# Edit to replace REPO_NAME with your repository name
```

> 💡 **More examples:** See `.github/workflows/reusable/EXAMPLES.md`

## How It Works

**Community health files** (issue templates, PR templates, contributing guidelines) are automatically available to all org repositories that don't have their own versions.

**Reusable workflows** require a small caller file in each repository (see Quick Start above). When you update workflows here, all repositories using `@main` get the updates automatically.

## Customization

### Modify Workflows

Edit files in `.github/workflows/reusable/` and push changes. All repos using `@main` will automatically use the updated version.

### Add New Workflows

1. Create workflow file in `.github/workflows/reusable/` with `workflow_call` trigger
2. Document usage in `reusable/EXAMPLES.md`

## FAQ

**Do workflows auto-add to repositories?**  
No. Create a small caller file in each repo (see Quick Start).

**What happens when I update a workflow here?**  
All repos using `@main` get updates automatically on next run.

**Can I customize workflows per repository?**  
Yes. Either copy and modify, or add conditions in the caller workflow.

**How do I pin to a specific version?**  
Use `@v1.0.0` instead of `@main` in the `uses:` line.

**Does the release workflow auto-version?**  
No. You add versioned sections to CHANGELOG.md (e.g., `## [1.0.0] - 2025-12-05`), and the workflow creates the release.

---


**Resources:** [GitHub Actions](https://docs.github.com/en/actions) • [Keep a Changelog](https://keepachangelog.com/) • [Semantic Versioning](https://semver.org/)
