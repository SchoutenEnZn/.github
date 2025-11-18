# Visual Guide: What You Get

This document shows exactly what users will see and how the .github repository features work across your organization.

## 🏢 Organization Profile Page

When users visit `https://github.com/SchoutenEnZn`, they will see:

```
╔════════════════════════════════════════════════════════════════╗
║ # Welcome to SchoutenEnZn 👋                                   ║
║                                                                 ║
║ This is the default community health files repository for      ║
║ the SchoutenEnZn organization.                                 ║
║                                                                 ║
║ ## Available Workflows                                         ║
║                                                                 ║
║ ### 🔍 Changelog Check                                         ║
║ Automatically validates that pull requests include changelog   ║
║ updates...                                                      ║
╚════════════════════════════════════════════════════════════════╝
```

*Source: `profile/README.md`*

## 📝 Creating an Issue

When creating an issue in **any** repository (without custom templates):

```
╔════════════════════════════════════════════════════════════════╗
║ New Issue                                              [Submit] ║
╟────────────────────────────────────────────────────────────────╢
║ Choose a template:                                             ║
║                                                                 ║
║ 🐛 Bug Report                                                  ║
║    Report a bug or issue                                       ║
║                                                     [Get started]║
║                                                                 ║
║ ✨ Feature Request                                             ║
║    Suggest an idea or new feature                              ║
║                                                     [Get started]║
║                                                                 ║
║ 📝 Open a blank issue                                          ║
╚════════════════════════════════════════════════════════════════╝
```

*Source: `.github/ISSUE_TEMPLATE/`*

### Bug Report Template

When user clicks "Bug Report":

```
---
name: Bug Report
about: Report a bug or issue
title: '[BUG] '
labels: ['bug']
---

## Description
A clear and concise description of the bug.

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

## Expected Behavior
[...]

## Actual Behavior
[...]

## Environment
- OS: [e.g., Windows 10]
- Browser: [e.g., Chrome 96]
- Version: [e.g., 1.0.0]
```

## 🔀 Creating a Pull Request

When creating a PR in **any** repository (without custom template):

```
╔════════════════════════════════════════════════════════════════╗
║ Create Pull Request                                            ║
╟────────────────────────────────────────────────────────────────╢
║ ## Description                                                 ║
║ <!-- Provide a clear description of your changes -->           ║
║                                                                 ║
║ ## Type of Change                                              ║
║ - [ ] Bug fix                                                  ║
║ - [ ] New feature                                              ║
║ - [ ] Breaking change                                          ║
║ - [ ] Documentation update                                     ║
║                                                                 ║
║ ## Changelog                                                   ║
║ - [ ] I have updated the CHANGELOG.md file                     ║
║ - [ ] No changelog update needed (add `skip-changelog` below)  ║
║                                                                 ║
║ ## Testing                                                     ║
║ - [ ] I have added tests                                       ║
║ - [ ] Tests pass locally                                       ║
║                                                                 ║
║ ## Checklist                                                   ║
║ - [ ] My code follows the style guidelines                     ║
║ - [ ] I have performed a self-review                           ║
╚════════════════════════════════════════════════════════════════╝
```

*Source: `.github/PULL_REQUEST_TEMPLATE/pull_request_template.md`*

## ⚙️ Actions Tab - New Workflow

When a repository admin goes to Actions → New Workflow:

```
╔════════════════════════════════════════════════════════════════╗
║ Choose a workflow                                      [Search] ║
╟────────────────────────────────────────────────────────────────╢
║                                                                 ║
║ By SchoutenEnZn                                                ║
║ ───────────────                                                ║
║                                                                 ║
║ 📋 Changelog Check Workflow                       [Configure]  ║
║    Validates that pull requests include changelog updates      ║
║    or skip label                                               ║
║    Categories: Automation · Code Review                        ║
║                                                                 ║
║ 📦 Release from Changelog Workflow                [Configure]  ║
║    Automatically creates releases based on the CHANGELOG.md    ║
║    file                                                        ║
║    Categories: Automation · Deployment                         ║
║                                                                 ║
╚════════════════════════════════════════════════════════════════╝
```

*Source: `workflow-templates/*.yml` and `workflow-templates/*.properties.json`*

## ✅ Changelog Check in Action

### Scenario 1: PR Without Changelog

```
╔════════════════════════════════════════════════════════════════╗
║ Pull Request #42                                               ║
║ Add user authentication feature                                ║
╟────────────────────────────────────────────────────────────────╢
║                                                                 ║
║ Checks:                                                        ║
║ ❌ Check for Changelog Entry — Failed                          ║
║                                                                 ║
║ ────────────────────────────────────────────────────────────── ║
║                                                                 ║
║ 💬 github-actions[bot] commented:                              ║
║                                                                 ║
║ ## ⚠️ Changelog Update Required                                ║
║                                                                 ║
║ This pull request doesn't appear to include a changelog        ║
║ update.                                                        ║
║                                                                 ║
║ Please update the `CHANGELOG.md` file with a description of    ║
║ your changes, or add `skip-changelog` to the PR description    ║
║ if this change doesn't require a changelog entry.              ║
║                                                                 ║
║ ### How to update the changelog:                               ║
║ 1. Add an entry under the `## [Unreleased]` section            ║
║ 2. Use the format: `- Description of change (#PR_NUMBER)`      ║
║ 3. Categorize under: Added, Changed, Fixed, etc.               ║
║                                                                 ║
╚════════════════════════════════════════════════════════════════╝
```

### Scenario 2: PR With Changelog

```
╔════════════════════════════════════════════════════════════════╗
║ Pull Request #42                                               ║
║ Add user authentication feature                                ║
╟────────────────────────────────────────────────────────────────╢
║                                                                 ║
║ Checks:                                                        ║
║ ✅ Check for Changelog Entry — Passed                          ║
║                                                                 ║
║ Files changed:                                                 ║
║ • src/auth.js                                                  ║
║ • CHANGELOG.md                                                 ║
║                                                                 ║
╚════════════════════════════════════════════════════════════════╝
```

### Scenario 3: Skipped Changelog

```
╔════════════════════════════════════════════════════════════════╗
║ Pull Request #43                                               ║
║ Update documentation for API endpoints                         ║
║                                                                 ║
║ Description:                                                   ║
║ Updated the README with better API examples.                   ║
║                                                                 ║
║ skip-changelog                                                 ║
╟────────────────────────────────────────────────────────────────╢
║                                                                 ║
║ Checks:                                                        ║
║ ✅ Check for Changelog Entry — Passed (skipped)                ║
║                                                                 ║
╚════════════════════════════════════════════════════════════════╝
```

## 🚀 Release Automation in Action

### When Changes are Merged

```
╔════════════════════════════════════════════════════════════════╗
║ Actions                                                        ║
╟────────────────────────────────────────────────────────────────╢
║                                                                 ║
║ Create Release from Changelog                                  ║
║ ────────────────────────────────────────────────────────────── ║
║                                                                 ║
║ ⏳ check-changelog                                             ║
║    ✅ Checkout code                                            ║
║    ✅ Check if changelog has unreleased version                ║
║    ✅ Extract version and release notes                        ║
║        📦 Version: 1.2.3                                       ║
║        📝 Release notes extracted                              ║
║                                                                 ║
║ ⏳ create-release                                              ║
║    ✅ Checkout code                                            ║
║    ✅ Configure git                                            ║
║    ✅ Update CHANGELOG.md                                      ║
║        ✅ Updated CHANGELOG.md with version 1.2.3              ║
║    ✅ Commit changelog update                                  ║
║        ✅ Committed and pushed changelog update                ║
║    ✅ Create git tag                                           ║
║        ✅ Created and pushed tag v1.2.3                        ║
║    ✅ Create GitHub Release                                    ║
║        ✅ Created release: https://github.com/.../v1.2.3       ║
║                                                                 ║
╚════════════════════════════════════════════════════════════════╝
```

### New Release Created

```
╔════════════════════════════════════════════════════════════════╗
║ Releases                                            [+ Draft]  ║
╟────────────────────────────────────────────────────────────────╢
║                                                                 ║
║ v1.2.3                                          Latest release ║
║ Release 1.2.3                                                  ║
║ @github-actions[bot] released this · 2 minutes ago             ║
║                                                                 ║
║ ### Added                                                      ║
║ - New user authentication feature (#42)                        ║
║ - Support for OAuth2 providers (#45)                           ║
║                                                                 ║
║ ### Fixed                                                      ║
║ - Fixed session timeout issue (#47)                            ║
║                                                                 ║
║ Assets:                                                        ║
║ 📎 Source code (zip)                                           ║
║ 📎 Source code (tar.gz)                                        ║
║                                                                 ║
╚════════════════════════════════════════════════════════════════╝
```

## 📂 Repository File Structure After Setup

After a repository adds both workflows:

```
my-repository/
├── .github/
│   └── workflows/
│       ├── changelog-check.yml          # ← Added from template
│       └── release-from-changelog.yml   # ← Added from template
├── src/
│   └── ...
├── CHANGELOG.md                         # ← Created using template
├── README.md
└── ...
```

## 🔄 Complete Workflow Flow

```
Developer Creates PR
         │
         ▼
    ┌────────────────┐
    │ PR Opened      │
    └────────┬───────┘
             │
             ▼
    ┌────────────────────────┐
    │ Changelog Check Runs   │
    └────────┬───────────────┘
             │
             ├─── No changelog update
             │    │
             │    ▼
             │    ❌ Check fails
             │    💬 Bot comments
             │    📝 Developer updates
             │
             └─── Has changelog OR skip-changelog
                  │
                  ▼
                  ✅ Check passes
                  👍 Ready for review
                  
Developer Merges PR to Main
         │
         ▼
    ┌────────────────────────┐
    │ Release Workflow Runs  │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Detects Unreleased     │
    │ Changes in Changelog   │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Increments Version     │
    │ (1.2.2 → 1.2.3)        │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Updates CHANGELOG.md   │
    │ [Unreleased] →         │
    │ [1.2.3] - 2024-11-18   │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Creates Git Tag v1.2.3 │
    └────────┬───────────────┘
             │
             ▼
    ┌────────────────────────┐
    │ Creates GitHub Release │
    │ with Release Notes     │
    └────────────────────────┘
             │
             ▼
         🎉 Done!
```

## 🎯 What Each User Type Sees

### Organization Admins
- ✅ Can edit this .github repository
- ✅ Updates apply to all repositories
- ✅ Manage workflow templates
- ✅ Customize templates

### Repository Maintainers
- ✅ See workflow templates in Actions UI
- ✅ Can add workflows with one click
- ✅ Inherit issue/PR templates automatically
- ✅ Can override with custom versions

### Contributors
- ✅ See standardized issue templates
- ✅ See PR template with changelog reminder
- ✅ Get automatic feedback on PRs
- ✅ Clear contribution guidelines

### Users/Visitors
- ✅ See organization profile README
- ✅ Standardized issue reporting
- ✅ Consistent experience across repos

## 📊 Summary of Features

| Feature | Location | Automatic? | Override? |
|---------|----------|------------|-----------|
| Organization Profile | profile/README.md | ✅ Yes | ❌ No |
| Issue Templates | .github/ISSUE_TEMPLATE/ | ✅ Yes | ✅ Yes |
| PR Template | .github/PULL_REQUEST_TEMPLATE/ | ✅ Yes | ✅ Yes |
| Changelog Check Workflow | workflow-templates/ | ❌ No (opt-in) | ✅ Yes |
| Release Workflow | workflow-templates/ | ❌ No (opt-in) | ✅ Yes |

## 🎨 Customization Examples

Users can customize by:

**1. Using different branch names:**
```yaml
# In their workflow file
on:
  push:
    branches:
      - develop  # Instead of main
```

**2. Adding more skip keywords:**
```yaml
# In their changelog-check.yml
grep -qi "skip-changelog\|no-change\|docs-only"
```

**3. Different version increments:**
```yaml
# In their release-from-changelog.yml
MINOR=$((MINOR + 1))  # Increment minor instead of patch
```

---

**This visual guide shows the complete user experience across the organization!**
