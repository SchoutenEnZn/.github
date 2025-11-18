# Quick Setup Guide

This guide will help you set up changelog-based workflows in your repository.

## Prerequisites

- Repository in the SchoutenEnZn organization
- Admin or write access to the repository
- Basic understanding of GitHub Actions

## Step 1: Create CHANGELOG.md

Copy the `CHANGELOG.template.md` from this repository to your repository root:

1. Copy `CHANGELOG.template.md` to your repository as `CHANGELOG.md`
2. Replace `REPO_NAME` with your actual repository name
3. Update the initial version and date as needed
4. Commit the file

**Example CHANGELOG.md:**
```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - 2024-11-18

### Added
- Initial project setup
```

## Step 2: Add Changelog Check Workflow

1. Go to your repository on GitHub
2. Click on the **Actions** tab
3. Click **New workflow**
4. Scroll down to "By SchoutenEnZn" or search for "changelog"
5. Click **Configure** on "Changelog Check Workflow"
6. Review the workflow file
7. Click **Commit changes** (commit to `.github/workflows/changelog-check.yml`)

**Or manually create** `.github/workflows/changelog-check.yml`:
```yaml
# Copy content from workflow-templates/changelog-check.yml
```

## Step 3: Add Release Automation Workflow

1. Go to the **Actions** tab again
2. Click **New workflow**
3. Find "Release from Changelog Workflow"
4. Click **Configure**
5. Review the workflow file
6. Click **Commit changes** (commit to `.github/workflows/release-from-changelog.yml`)

**Or manually create** `.github/workflows/release-from-changelog.yml`:
```yaml
# Copy content from workflow-templates/release-from-changelog.yml
```

## Step 4: Configure Branch Protection (Recommended)

1. Go to **Settings** → **Branches**
2. Click **Add rule** (or edit existing rule for main/master)
3. Branch name pattern: `main` (or `master`)
4. Check **Require status checks to pass before merging**
5. Search for and select: **Check for Changelog Entry**
6. Click **Create** or **Save changes**

This ensures no PR can be merged without a changelog update (unless skipped).

## Step 5: Test the Setup

### Test Changelog Check

1. Create a new branch
2. Make a code change (without updating CHANGELOG.md)
3. Create a pull request
4. You should see:
   - ❌ Changelog check fails
   - 💬 Bot comment asking for changelog update

5. Now update CHANGELOG.md:
   ```markdown
   ## [Unreleased]
   
   ### Fixed
   - Fixed test issue (#1)
   ```
6. Push the change
7. You should see:
   - ✅ Changelog check passes

### Test Skip Functionality

1. Create another branch with only documentation changes
2. Create a pull request
3. Add `skip-changelog` to the PR description
4. You should see:
   - ✅ Changelog check passes (skipped)

### Test Release Automation

1. Merge a PR with changelog updates to main
2. Go to **Actions** tab
3. You should see "Create Release from Changelog" workflow running
4. After completion, check:
   - **Releases** tab shows new release
   - **Tags** shows new version tag
   - CHANGELOG.md is updated with version and date

## Common Workflows

### Adding a Feature

1. Create feature branch
2. Implement feature
3. Update CHANGELOG.md:
   ```markdown
   ## [Unreleased]
   
   ### Added
   - New user profile page (#42)
   ```
4. Create PR
5. Merge after approval
6. Release is created automatically

### Fixing a Bug

1. Create bugfix branch
2. Fix the bug
3. Update CHANGELOG.md:
   ```markdown
   ## [Unreleased]
   
   ### Fixed
   - Fixed memory leak in data processing (#43)
   ```
4. Create PR
5. Merge after approval
6. Release is created automatically

### Documentation-Only Changes

1. Create branch
2. Update documentation
3. Create PR with `skip-changelog` in description
4. Merge (no release created)

### Manual Release

If you need to create a release with a specific version:

1. Go to **Actions** tab
2. Select "Create Release from Changelog" workflow
3. Click **Run workflow**
4. Enter version (e.g., `2.1.0`)
5. Click **Run workflow**
6. Release is created with specified version

## Troubleshooting

### Changelog Check Fails Even Though I Updated CHANGELOG.md

- Ensure the file is named exactly `CHANGELOG.md` (case-sensitive)
- Ensure the file is in the repository root
- Check that changes were committed and pushed

### Release Workflow Doesn't Trigger

- Ensure there are changes under `[Unreleased]` in CHANGELOG.md
- Check workflow file is in `.github/workflows/release-from-changelog.yml`
- Verify the workflow runs on your main branch (check branch name)

### Version Number Is Wrong

- Check existing git tags in your repository
- The workflow increments the PATCH version by default
- Use manual trigger to specify exact version

### Permission Denied Errors

- Ensure `GITHUB_TOKEN` has correct permissions
- Check workflow file has `permissions:` section:
  ```yaml
  permissions:
    contents: write
    pull-requests: write
  ```

## Advanced Configuration

### Custom Branch Names

If you use branch names other than `main` or `master`:

Edit both workflow files and update:
```yaml
on:
  push:
    branches:
      - main
      - master
      - develop  # Add your branch
```

### Custom Version Increment Logic

Edit `release-from-changelog.yml` to customize version bumping:

```yaml
# Find this section and modify:
PATCH=$((PATCH + 1))  # Change to MINOR or MAJOR as needed
```

### Skip Changelog Keywords

Edit `changelog-check.yml` to add more skip keywords:

```yaml
if echo "$PR_BODY" | grep -qi "skip-changelog\|no-changelog\|skip changelog\|your-custom-keyword"; then
```

## Best Practices

1. **Write Clear Changelog Entries**
   - Be specific about what changed
   - Reference issue/PR numbers
   - Write from user perspective

2. **Update Changelog with Each PR**
   - Don't wait until release time
   - Make it part of your development workflow

3. **Use Semantic Versioning**
   - MAJOR: Breaking changes
   - MINOR: New features (backward compatible)
   - PATCH: Bug fixes (backward compatible)

4. **Review Auto-Generated Releases**
   - Check release notes are accurate
   - Edit if needed for clarity

5. **Keep Unreleased Section Clean**
   - Remove empty subsections
   - Keep only relevant categories

## Need Help?

- Check the [main README](README.md) for detailed documentation
- Review workflow files for comments and configuration options
- Open an issue in this repository for support
- Contact repository maintainers

---

**Next Steps:**
- ✅ Set up CHANGELOG.md
- ✅ Add workflows
- ✅ Configure branch protection
- ✅ Test with a PR
- 🎉 Enjoy automated releases!
