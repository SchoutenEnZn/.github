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
│   └── PULL_REQUEST_TEMPLATE/    # Default PR templates
│       └── pull_request_template.md
├── workflow-templates/            # Reusable workflow templates
│   ├── changelog-check.yml
│   ├── changelog-check.properties.json
│   ├── release-from-changelog.yml
│   └── release-from-changelog.properties.json
├── profile/
│   └── README.md                  # Organization profile page
└── README.md                      # This file
```

## 🚀 Features

### Workflow Templates

#### 1. **Changelog Check** (`changelog-check.yml`)
Validates that pull requests include changelog updates.

**What it does:**
- ✅ Checks if CHANGELOG.md was modified in the PR
- ✅ Allows skipping via `skip-changelog` keyword in PR description
- ✅ Posts helpful comments on PRs missing changelog updates
- ✅ Fails CI if changelog is required but missing

**Usage in repositories:**
1. Go to Actions → New workflow
2. Select "Changelog Check Workflow" from templates
3. Commit to `.github/workflows/changelog-check.yml`

#### 2. **Release from Changelog** (`release-from-changelog.yml`)
Automatically creates releases based on CHANGELOG.md changes.

**What it does:**
- ✅ Detects unreleased changes in CHANGELOG.md
- ✅ Automatically increments version numbers (semantic versioning)
- ✅ Updates CHANGELOG.md with version and date
- ✅ Creates git tags
- ✅ Generates GitHub releases with release notes
- ✅ Can be triggered manually with custom version

**Triggers:**
- Automatically on push to main/master branch
- Manually via workflow dispatch with optional version input

**Usage in repositories:**
1. Go to Actions → New workflow
2. Select "Release from Changelog Workflow" from templates
3. Commit to `.github/workflows/release-from-changelog.yml`

### Issue Templates

Pre-configured issue templates for:
- 🐛 **Bug Reports**: Structured bug reporting with environment details
- ✨ **Feature Requests**: Standardized feature proposal format

### Pull Request Template

A comprehensive PR template that includes:
- Change type classification
- Changelog reminder with skip option
- Testing checklist
- Documentation updates
- Code quality checklist

## 📝 CHANGELOG.md Format

Repositories using these workflows should maintain a CHANGELOG.md file:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- New feature description (#123)

### Changed
- Changes to existing functionality (#124)

### Fixed
- Bug fixes (#125)

### Security
- Security improvements (#126)

## [1.0.0] - 2024-01-01

### Added
- Initial release
```

## 🔧 How It Works

### Organization-Wide Defaults

GitHub automatically uses files from this `.github` repository as defaults for all repositories in the **SchoutenEnZn** organization that don't have their own versions.

**What's shared:**
- Issue templates
- Pull request templates
- Workflow templates (available in Actions UI)

**What's NOT automatic:**
- Workflows must be manually added to each repository (via Actions UI or copy-paste)
- This is by design - workflows need explicit opt-in for security reasons

### Repository-Specific Overrides

Any repository can override these defaults by creating its own:
- `.github/ISSUE_TEMPLATE/` directory
- `.github/PULL_REQUEST_TEMPLATE/` directory
- Workflow files in `.github/workflows/`

## 📋 Step-by-Step Setup Guide

### For New Repositories

1. **Create CHANGELOG.md**
   ```bash
   # Copy the template format above into CHANGELOG.md
   # Commit to your repository root
   ```

2. **Add Changelog Check Workflow**
   - Go to repository → Actions → New workflow
   - Find "Changelog Check Workflow"
   - Commit to `.github/workflows/changelog-check.yml`

3. **Add Release Automation Workflow**
   - Go to repository → Actions → New workflow
   - Find "Release from Changelog Workflow"
   - Commit to `.github/workflows/release-from-changelog.yml`

4. **Configure Branch Protection** (Recommended)
   - Go to Settings → Branches
   - Add rule for main/master
   - Require "Check for Changelog Entry" status check to pass

### For Existing Repositories

1. **Review existing CHANGELOG.md** or create one
2. **Add workflows** as described above
3. **Update documentation** to mention changelog requirements
4. **Test** by creating a test PR

## 🎯 Workflow Usage Examples

### Making a PR with Changelog

1. Make your code changes
2. Update CHANGELOG.md under `[Unreleased]`:
   ```markdown
   ## [Unreleased]
   
   ### Fixed
   - Fixed login issue when username contains special characters (#42)
   ```
3. Create PR - changelog check will pass ✅

### Making a PR without Changelog

For changes that don't need changelog (docs, tests, CI):

1. Make your changes
2. In PR description, add: `skip-changelog`
3. Changelog check will pass ✅

### Creating a Release

**Automatic (recommended):**
1. Merge PRs with changelog updates to main
2. Release workflow automatically triggers
3. New version is created based on semantic versioning
4. Release notes are extracted from changelog

**Manual:**
1. Go to Actions → Release from Changelog
2. Click "Run workflow"
3. Optionally specify version (e.g., "2.1.0")
4. Release is created

## 🔒 Permissions

The release workflow requires:
- `contents: write` - To create tags and releases
- `pull-requests: write` - To interact with PRs (changelog check)

These are configured in the workflow files.

## 🛠️ Customization

### Modify Workflows

To customize for your organization:

1. Clone this repository
2. Edit workflow templates in `workflow-templates/`
3. Update properties files (`.properties.json`) for metadata
4. Commit changes
5. Templates will be available to all org repositories

### Add More Templates

You can add additional workflow templates:

1. Create `workflow-templates/your-workflow.yml`
2. Create `workflow-templates/your-workflow.properties.json`
3. Templates appear in Actions UI for all repos

## 📚 Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Keep a Changelog](https://keepachangelog.com/)
- [Semantic Versioning](https://semver.org/)
- [Community Health Files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)

## 🤝 Contributing

To improve these templates:

1. Fork this repository
2. Make your changes
3. Test in a sample repository
4. Submit a pull request

## ❓ FAQ

**Q: Why aren't workflows automatically added to repositories?**  
A: For security reasons, GitHub requires workflows to be explicitly added to each repository. However, the templates make this easy via the Actions UI.

**Q: Can I use different changelog formats?**  
A: Yes, but you may need to modify the workflow scripts that parse CHANGELOG.md.

**Q: What if I want to skip releases for some merges?**  
A: The release workflow only triggers when there are unreleased changes in CHANGELOG.md. If no changes are detected, no release is created.

**Q: Can I customize version numbering?**  
A: Yes, use the manual workflow dispatch with a specific version number.

## 📄 License

These templates are provided as-is for use within the SchoutenEnZn organization.
