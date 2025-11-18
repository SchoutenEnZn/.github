# Complete .github Repository Structure

This document provides a complete overview of the .github repository structure for organization-wide defaults.

## 📂 Directory Tree

```
.github/                                   # Root of special .github repository
│
├── .github/                               # Community health files
│   ├── ISSUE_TEMPLATE/                    # Default issue templates for all repos
│   │   ├── bug_report.md                 # Bug report template
│   │   ├── feature_request.md            # Feature request template
│   │   └── config.yml                    # Issue template configuration
│   │
│   └── PULL_REQUEST_TEMPLATE/            # Default PR templates for all repos
│       └── pull_request_template.md      # PR template with changelog reminder
│
├── workflow-templates/                    # Reusable workflow templates
│   ├── changelog-check.yml               # PR changelog validation workflow
│   ├── changelog-check.properties.json   # Metadata for changelog check
│   ├── release-from-changelog.yml        # Automated release workflow
│   └── release-from-changelog.properties.json  # Metadata for release workflow
│
├── profile/                               # Organization profile
│   └── README.md                         # Shows on organization page
│
├── CHANGELOG.template.md                  # Template for new repositories
├── SETUP_GUIDE.md                        # Step-by-step setup instructions
└── README.md                             # Main documentation (this location)
```

## 📋 File Purposes

### Community Health Files (.github/)

These files are automatically used as defaults for all repositories in the organization that don't have their own versions.

#### Issue Templates
- **bug_report.md**: Standardized template for bug reports
- **feature_request.md**: Standardized template for feature requests
- **config.yml**: Configuration for issue templates (enables/disables blank issues, contact links)

#### Pull Request Template
- **pull_request_template.md**: Default PR template with:
  - Change type selection
  - Changelog update reminder
  - Testing checklist
  - Documentation checklist
  - Code quality checklist

### Workflow Templates (workflow-templates/)

Workflow templates appear in the Actions tab of all repositories in the organization but must be explicitly added by repository maintainers.

#### Changelog Check Workflow
- **changelog-check.yml**: Validates PRs have changelog updates
  - Checks if CHANGELOG.md was modified
  - Allows skip via `skip-changelog` keyword
  - Posts helpful comments
  - Fails CI if required but missing

- **changelog-check.properties.json**: Metadata for the workflow template
  - Name and description
  - Icon
  - Categories
  - File patterns

#### Release Automation Workflow
- **release-from-changelog.yml**: Creates releases from changelog
  - Detects unreleased changes
  - Auto-increments version (semantic versioning)
  - Updates CHANGELOG.md
  - Creates git tags
  - Generates GitHub releases
  - Supports manual triggers

- **release-from-changelog.properties.json**: Metadata for the workflow template
  - Name and description
  - Icon
  - Categories
  - File patterns

### Organization Profile (profile/)

- **README.md**: Appears on the organization's GitHub profile page
  - Welcome message
  - Overview of available workflows
  - Usage instructions
  - Best practices

### Documentation Files

- **README.md**: Main documentation
  - Complete feature overview
  - Usage instructions
  - Configuration guide
  - FAQ

- **SETUP_GUIDE.md**: Step-by-step setup guide
  - Detailed instructions for repository setup
  - Testing procedures
  - Troubleshooting
  - Best practices

- **CHANGELOG.template.md**: Template for repositories
  - Standard format following Keep a Changelog
  - Semantic versioning structure
  - Example entries

## 🔄 How It Works

### Automatic Features

1. **Issue & PR Templates**: Automatically available in all org repositories
2. **Workflow Templates**: Show up in Actions → New Workflow UI
3. **Organization Profile**: Visible on organization page

### Manual Features

1. **Workflows**: Must be added to each repository (security requirement)
   - Available via Actions UI
   - Can be copied manually
   - Repository-specific configuration possible

### Override Mechanism

Any repository can override defaults by creating:
- `.github/ISSUE_TEMPLATE/` - Custom issue templates
- `.github/PULL_REQUEST_TEMPLATE/` - Custom PR templates
- `.github/workflows/` - Repository-specific workflows

## 🎯 Usage Scenarios

### Scenario 1: New Repository Setup

1. Repository inherits issue/PR templates automatically ✅
2. Developer goes to Actions → New Workflow
3. Selects "Changelog Check Workflow"
4. Selects "Release from Changelog Workflow"
5. Creates CHANGELOG.md using template
6. Everything configured! 🎉

### Scenario 2: Existing Repository

1. Already has custom templates (keeps them) ✅
2. Can still add workflow templates selectively
3. Can override specific templates as needed
4. Gradual adoption possible

### Scenario 3: Organization-Wide Update

1. Update workflow templates in this .github repo
2. Repositories see updated templates in Actions UI
3. Repositories can update their workflows
4. Centralized management ✅

## 📊 Feature Matrix

| Feature | Automatic | Manual | Override |
|---------|-----------|--------|----------|
| Issue Templates | ✅ | ❌ | ✅ |
| PR Templates | ✅ | ❌ | ✅ |
| Workflow Templates | ❌ | ✅ | ✅ |
| Organization Profile | ✅ | ❌ | ❌ |

**Legend:**
- ✅ Automatic: Applied without action
- ✅ Manual: Requires explicit action
- ✅ Override: Repository can customize
- ❌ Not applicable

## 🔒 Security Considerations

### Workflow Permissions

Both workflows require specific permissions:

```yaml
permissions:
  contents: write      # Create tags, releases, update files
  pull-requests: write # Comment on PRs
```

### Why Workflows Aren't Automatic

GitHub intentionally requires workflows to be explicitly added to repositories because:
- Workflows can execute arbitrary code
- They have access to repository secrets
- They can modify repository content
- Security risk if automatically inherited

## 🎨 Customization Options

### Organization-Level (This Repository)

**To customize for all repos:**
1. Edit files in this repository
2. Changes apply to all repos immediately (templates)
3. Workflows show updated version in Actions UI

### Repository-Level

**To customize for one repo:**
1. Copy template to repository
2. Modify as needed
3. Local version takes precedence

### Examples of Customization

**Different branch names:**
```yaml
# In workflow files
on:
  push:
    branches:
      - develop  # Add your branch
```

**Different skip keywords:**
```yaml
# In changelog-check.yml
if echo "$PR_BODY" | grep -qi "skip-changelog\|no-change"; then
```

**Different version increment:**
```yaml
# In release-from-changelog.yml
MINOR=$((MINOR + 1))  # Instead of PATCH
PATCH=0
```

## 📈 Benefits

### For Organization

- ✅ Consistent workflows across all repositories
- ✅ Centralized updates and maintenance
- ✅ Reduced setup time for new repositories
- ✅ Standardized contribution guidelines
- ✅ Better changelog maintenance
- ✅ Automated release process

### For Contributors

- ✅ Clear contribution guidelines
- ✅ Standardized issue/PR templates
- ✅ Automatic changelog reminders
- ✅ Consistent experience across repos

### For Maintainers

- ✅ Automated release creation
- ✅ Changelog enforcement
- ✅ Less manual work
- ✅ Consistent versioning
- ✅ Better documentation

## 🚀 Next Steps

1. ✅ Review this structure
2. ✅ Test in a sample repository
3. ✅ Gather feedback from team
4. ✅ Roll out to production repositories
5. ✅ Document organization-specific conventions
6. ✅ Train team members on workflows

## 📚 Additional Resources

- [GitHub Community Health Files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [Workflow Templates](https://docs.github.com/en/actions/using-workflows/creating-starter-workflows-for-your-organization)
- [Keep a Changelog](https://keepachangelog.com/)
- [Semantic Versioning](https://semver.org/)

---

**This structure provides a complete, ready-to-use solution for organization-wide workflow and template management.**
