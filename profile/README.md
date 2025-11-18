# Welcome to SchoutenEnZn 👋

This is the default community health files repository for the SchoutenEnZn organization.

## About This Repository

This `.github` repository contains:
- **Workflow Templates**: Reusable GitHub Actions workflows
- **Issue Templates**: Standardized issue templates
- **Pull Request Templates**: PR templates with changelog reminders
- **Community Health Files**: Default files for all repositories in this organization

## Available Workflows

### 🔍 Changelog Check
Automatically validates that pull requests include changelog updates.

**Features:**
- Checks if CHANGELOG.md was modified in the PR
- Allows skipping via `skip-changelog` in PR description
- Posts helpful comments on PRs missing changelog updates
- Fails the check if changelog is required but missing

### 📦 Release from Changelog
Automatically creates releases based on the CHANGELOG.md file.

**Features:**
- Detects unreleased changes in CHANGELOG.md
- Automatically increments version numbers
- Creates git tags
- Generates GitHub releases with release notes
- Can be triggered manually with custom version

## How to Use

### For Repository Owners

These templates and files are automatically available to all repositories in the SchoutenEnZn organization.

#### Adding Workflows to a Repository

1. Go to your repository's "Actions" tab
2. Click "New workflow"
3. Look for "By SchoutenEnZn" in the workflow templates
4. Choose either:
   - **Changelog Check Workflow** - for PR validation
   - **Release from Changelog Workflow** - for automated releases
5. Commit the workflow file to your repository

#### Setting Up CHANGELOG.md

Create a `CHANGELOG.md` file in your repository root with this format:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- New feature description

### Changed
- Changes to existing functionality

### Deprecated
- Soon-to-be removed features

### Removed
- Removed features

### Fixed
- Bug fixes

### Security
- Security improvements

## [1.0.0] - 2024-01-01

### Added
- Initial release
```

### For Contributors

When creating a pull request:

1. **Update CHANGELOG.md**: Add your changes under the `[Unreleased]` section
2. **Use PR Template**: Fill out all sections of the PR template
3. **Skip Changelog When Appropriate**: Add `skip-changelog` to your PR description for:
   - Documentation-only changes
   - Test-only changes
   - Internal/CI changes that don't affect users

## Best Practices

### Changelog Guidelines

- **Be Clear**: Write clear, concise descriptions
- **User-Focused**: Describe changes from a user's perspective
- **Categorize**: Use the correct category (Added, Changed, Fixed, etc.)
- **Link Issues**: Reference issue numbers when applicable

### Version Management

This organization follows [Semantic Versioning](https://semver.org/):
- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes (backward compatible)

## Customization

Repository owners can override these defaults by:
- Creating their own `.github` directory in their repository
- Adding repository-specific templates or workflows
- These will take precedence over organization defaults

## Support

For questions or issues:
- Check repository-specific documentation
- Open an issue in the relevant repository
- Contact the repository maintainers

---

*These templates help maintain consistency and quality across all SchoutenEnZn projects.*
