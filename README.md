# .github

This is a special repository recognized by GitHub for organization-wide defaults and community health files.

## 📁 Repository Structure

```
.github/
├── .github/
│   ├── ISSUE_TEMPLATE/           # Default issue templates
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── config.yml
│   ├── PULL_REQUEST_TEMPLATE/    # Default PR templates
│   │   └── pull_request_template.md
│   └── workflows/                # Centralized workflow files
│       ├── createRelease.yaml
│       └── verifyChangelog.yaml
├── profile/
│   └── README.md                  # Organization profile page
├── CHANGELOG.template.md          # Template for new repositories
├── CONTRIBUTING.md                # Contributing guidelines
├── PULL_REQUEST_TEMPLATE.md       # Root-level PR template
└── README.md                      # This file
```

## 🚀 What's Included

### 📋 Community Health Files

These files are automatically available to all repositories in the **SchoutenEnZn** organization:

#### **Issue Templates**
- 🐛 **Bug Report** - Structured template for reporting bugs with environment details
- ✨ **Feature Request** - Standardized format for proposing new features

#### **Pull Request Template**
Comprehensive PR template that includes:
- Change type classification
- Changelog update reminder with skip option
- Testing checklist
- Documentation requirements
- Code quality checks

#### **Contributing Guidelines** (`CONTRIBUTING.md`)
Standard contribution workflow for all repositories

### 🔧 Centralized Workflows

#### **Verify CHANGELOG Updated** (`.github/workflows/verifyChangelog.yaml`)
Ensures PRs update the CHANGELOG.md file before merging.

**What it does:**
- ✅ Verifies CHANGELOG.md was modified in the PR
- ✅ Fails the check if changelog is missing
- ✅ Compares against the base branch to detect changes

**How to use in your repositories:**

Create `.github/workflows/changelog-check.yml` in your repository:

```yaml
name: Changelog Check

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  verify-changelog:
    uses: SchoutenEnZn/.github/.github/workflows/verifyChangelog.yaml@main
```

That's it! The workflow will automatically run on all PRs.

---

#### **Create Release** (`.github/workflows/createRelease.yaml`)
Automatically creates GitHub releases from CHANGELOG.md versions.

**What it does:**
- ✅ Extracts version numbers from CHANGELOG.md
- ✅ Generates release notes from changelog entries
- ✅ Creates GitHub releases with tags
- ✅ Can be triggered manually with a custom version

**How to use in your repositories:**

Create `.github/workflows/release.yml` in your repository:

```yaml
name: Create Release

on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Version (e.g., v1.0.0). Leave blank for latest from CHANGELOG.md'
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

### 📝 CHANGELOG Template

`CHANGELOG.template.md` provides a starting point for new repositories following [Keep a Changelog](https://keepachangelog.com/) format.

**To use:**
```bash
cp CHANGELOG.template.md CHANGELOG.md
# Edit to match your repository name
```

## 🔧 How It Works

### Organization-Wide Defaults

GitHub automatically uses files from this `.github` repository as defaults for all repositories in the **SchoutenEnZn** organization that don't have their own versions.

**Automatically shared:**
- Issue templates (`.github/ISSUE_TEMPLATE/`)
- Pull request templates (`.github/PULL_REQUEST_TEMPLATE/`)
- Contributing guidelines (`CONTRIBUTING.md`)

**Not automatically shared:**
- Workflows in `.github/workflows/` must be manually copied to each repository
- This is by design for security reasons

### Repository-Specific Overrides

Individual repositories can override these defaults by creating their own versions of any file.

## 📋 Quick Start Guide

### For New Repositories

1. **Set up CHANGELOG.md**
   ```bash
   curl -o CHANGELOG.md https://raw.githubusercontent.com/SchoutenEnZn/.github/main/CHANGELOG.template.md
   # Edit the file to replace REPO_NAME with your repository name
   ```

2. **Add Changelog Verification**
   
   Create `.github/workflows/verifyChangelog.yaml`:
   ```yaml
   name: Changelog Check
   
   on:
     pull_request:
       types: [opened, synchronize]
   
   jobs:
     verify-changelog:
       uses: SchoutenEnZn/.github/.github/workflows/verifyChangelog.yaml@main
   ```

3. **Add Release Workflow** (Optional)
   
   Create `.github/workflows/createRelease.yml`:
   ```yaml
   name: Create Release
   
   on:
     workflow_dispatch:
       inputs:
         version:
           description: 'Version (e.g., v1.0.0)'
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
   ```

4. **Enable Branch Protection** (Recommended)
   - Go to Settings → Branches
   - Add rule for `main` branch
   - Require "Verify CHANGELOG Updated" status check to pass

### For Existing Repositories

1. Review or create `CHANGELOG.md` using the template
2. Add the workflow files as shown in the "For New Repositories" section
3. Update your documentation to mention changelog requirements

> **💡 Tip:** See `.github/workflows/EXAMPLES.md` in this repository for more workflow examples and configurations.

## 💡 Workflow Usage

### Working with Changelogs

**Making a PR with Changelog Update:**

1. Make your code changes
2. Update `CHANGELOG.md` under the `[Unreleased]` section:
   ```markdown
   ## [Unreleased]
   
   ### Fixed
   - Fixed login issue with special characters (#42)
   ```
3. Create PR → Changelog check passes ✅

**Making a PR without Changelog Update:**

The current workflow **requires** changelog updates. If you need to skip the check:
- Modify the workflow in your repository to add skip logic
- Or temporarily disable the check for specific PRs

### Creating Releases

**Option 1: Automatic (on PR merge)**
1. Ensure CHANGELOG.md has a versioned section (e.g., `## [1.0.0] - 2025-11-18`)
2. Merge the PR
3. The workflow automatically creates a GitHub release

**Option 2: Manual trigger**
1. Go to Actions → Create Release
2. Click "Run workflow"
3. **Leave version blank** to use the latest version from CHANGELOG.md
4. **Or specify a version** (e.g., `v1.2.3`) for manual control

**CHANGELOG format for releases:**
```markdown
## [1.0.0] - 2025-11-18

### Added
- New authentication system (#45)

### Fixed
- Critical security vulnerability (#46)
```

## 🛠️ Customization

### Modifying Workflows

To customize the reusable workflows:

1. Clone this repository
2. Edit files in `.github/workflows/`:
   - `verifyChangelog.yaml` - Changelog verification logic
   - `createRelease.yaml` - Release creation and versioning
3. Commit and push changes
4. **All repositories using the workflows automatically get the updates!** 🎉

### Adding More Workflows

You can add additional centralized workflows:

1. Create new workflow files in `.github/workflows/` using `workflow_call` trigger
2. Document them in this README and in `EXAMPLES.md`
3. Repositories can reference them using the `uses:` syntax

## 📚 Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Keep a Changelog](https://keepachangelog.com/)
- [Semantic Versioning](https://semver.org/)
- [Community Health Files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)

## 🤝 Contributing

To improve these templates:

1. Create a branch in this repository
2. Make your changes
3. Test in a sample repository
4. Open a pull request

## ❓ FAQ

**Q: Are workflows automatically added to repositories?**  
A: No. You need to create a workflow file in each repository that **references** the centralized workflow using `uses: SchoutenEnZn/.github/.github/workflows/workflowName.yaml@main`.

**Q: Can I customize the workflows for my repository?**  
A: Yes! You can either:
- Copy the workflow to your repo and modify it directly
- Or add parameters/conditions in your caller workflow

**Q: What happens when you update workflows in this repository?**  
A: All repositories using `@main` automatically get the updates on their next workflow run! Use `@v1.0.0` tags for stability.

**Q: How do I update to use the latest workflow version?**  
A: If you're using `@main`, it updates automatically. If using a tagged version like `@v1.0.0`, change it to the new tag or `@main`.

**Q: Does the release workflow automatically version my releases?**  
A: The workflow reads version numbers from your CHANGELOG.md. You need to add versioned sections manually (e.g., `## [1.0.0] - 2025-11-18`).

**Q: Can I trigger releases manually?**  
A: Yes! Use the workflow dispatch option in the Actions tab and optionally specify a version number.

**Q: Can I test workflow changes before they affect all repos?**  
A: Yes! Use a branch or tag reference like `@feature-branch` or `@test-v1` instead of `@main` while testing.
