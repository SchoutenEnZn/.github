# Quick Reference Card

A one-page reference for using the SchoutenEnZn .github repository features.

## 📦 What's Included

```
✅ Changelog Check Workflow     - Validates PR changelog updates
✅ Release Automation Workflow  - Creates releases from changelog
✅ Issue Templates              - Bug reports & feature requests
✅ Pull Request Template        - With changelog reminder
✅ Organization Profile         - Welcome page for org
✅ Documentation                - Setup guides & references
```

## 🚀 Quick Start (5 minutes)

### For Repository Maintainers

1. **Create CHANGELOG.md** (copy from `CHANGELOG.template.md`)
2. **Add Workflows:**
   - Go to Actions → New Workflow
   - Add "Changelog Check Workflow"
   - Add "Release from Changelog Workflow"
3. **Done!** ✅

### For Contributors

1. **Make changes** to code
2. **Update CHANGELOG.md** under `[Unreleased]`
3. **Create PR** (template auto-fills)
4. **Merge** after approval
5. **Release created automatically** 🎉

## 📝 CHANGELOG.md Format

```markdown
## [Unreleased]

### Added
- New feature (#42)

### Fixed
- Bug fix (#43)
```

**Categories:** Added, Changed, Deprecated, Removed, Fixed, Security

## 🔄 Common Workflows

### Adding a Feature
```bash
# 1. Create branch
git checkout -b feature/new-thing

# 2. Implement feature
# ... code changes ...

# 3. Update changelog
echo "### Added" >> CHANGELOG.md
echo "- New feature description (#PR)" >> CHANGELOG.md

# 4. Create PR
# 5. Merge → Release auto-created! 🎉
```

### Fixing a Bug
```bash
# 1. Create branch
git checkout -b fix/bug-name

# 2. Fix bug
# ... code changes ...

# 3. Update changelog
echo "### Fixed" >> CHANGELOG.md
echo "- Fixed bug description (#PR)" >> CHANGELOG.md

# 4. Create PR
# 5. Merge → Release auto-created! 🎉
```

### Documentation Changes
```bash
# 1. Make changes to docs
# 2. Create PR with `skip-changelog` in description
# 3. Merge (no release created)
```

## ⚙️ Workflow Behavior

### Changelog Check (PR Validation)

| Scenario | Result |
|----------|--------|
| CHANGELOG.md updated | ✅ Pass |
| `skip-changelog` in PR description | ✅ Pass (skipped) |
| No changelog & no skip | ❌ Fail + Bot comment |

**Alternative skip keywords:**
- `skip-changelog`
- `no-changelog`
- `[skip changelog]`

### Release Automation

| Trigger | Behavior |
|---------|----------|
| Merge to main with unreleased changes | 🚀 Auto-create release |
| Merge to main without changes | ℹ️ No release |
| Manual trigger | 🎯 Create with custom version |

**Version Increment:** Patch version incremented by default (1.2.3 → 1.2.4)

## 🎯 When to Skip Changelog

Add `skip-changelog` to PR description when:
- ✅ Documentation-only changes
- ✅ Test-only changes  
- ✅ CI/CD configuration changes
- ✅ Code formatting/linting
- ✅ Internal refactoring (no user impact)

Don't skip for:
- ❌ Bug fixes
- ❌ New features
- ❌ Breaking changes
- ❌ Performance improvements
- ❌ Security fixes

## 🔒 Required Permissions

Workflows need these permissions (already configured):
```yaml
permissions:
  contents: write       # Create tags, releases
  pull-requests: write  # Comment on PRs
```

## 📂 File Locations

```
Repository Root
├── CHANGELOG.md                         # ← Create this
└── .github/
    └── workflows/
        ├── changelog-check.yml          # ← Add from template
        └── release-from-changelog.yml   # ← Add from template
```

## 🎨 Customization Cheat Sheet

### Change target branch
```yaml
# In workflow file
on:
  push:
    branches:
      - develop  # Add your branch
```

### Add skip keywords
```yaml
# In changelog-check.yml, line ~40
grep -qi "skip-changelog\|your-keyword"
```

### Change version increment
```yaml
# In release-from-changelog.yml, line ~80
MINOR=$((MINOR + 1))  # Increment minor version
PATCH=0               # Reset patch to 0
```

### Customize categories
Edit CHANGELOG.md structure - workflow extracts content as-is

## 🆘 Troubleshooting

| Problem | Solution |
|---------|----------|
| Changelog check fails but I updated CHANGELOG.md | Ensure file is named exactly `CHANGELOG.md` in root |
| Release not created after merge | Check `[Unreleased]` section has entries |
| Wrong version number | Check existing git tags, or use manual trigger |
| Permission errors | Verify workflow has `contents: write` permission |
| Workflow not visible in Actions | Check it's in `.github/workflows/` directory |

## 📋 PR Checklist Template

When creating a PR, ensure:
- [ ] Code changes are complete
- [ ] CHANGELOG.md updated (or `skip-changelog` added)
- [ ] Tests pass locally
- [ ] Code follows style guidelines
- [ ] Documentation updated (if needed)
- [ ] PR template filled out

## 🔗 Quick Links

- **Setup Guide:** [SETUP_GUIDE.md](SETUP_GUIDE.md)
- **Full Documentation:** [README.md](README.md)
- **Structure Overview:** [STRUCTURE.md](STRUCTURE.md)
- **Visual Guide:** [VISUAL_GUIDE.md](VISUAL_GUIDE.md)
- **Changelog Template:** [CHANGELOG.template.md](CHANGELOG.template.md)

## 📞 Getting Help

1. Check [README.md](README.md) for detailed docs
2. Review [SETUP_GUIDE.md](SETUP_GUIDE.md) for step-by-step instructions
3. Look at [VISUAL_GUIDE.md](VISUAL_GUIDE.md) for examples
4. Ask repository maintainers
5. Open issue in this .github repository

## 💡 Pro Tips

1. **Update changelog in each PR** - Don't batch changes
2. **Use clear descriptions** - Help future maintainers
3. **Link to issues/PRs** - Use (#42) notation
4. **Keep [Unreleased] section clean** - Remove empty categories
5. **Review auto-generated releases** - Edit if needed
6. **Use semantic versioning** - MAJOR.MINOR.PATCH
7. **Test locally first** - Ensure changes work before PR
8. **Read bot comments** - They provide helpful guidance

## 📈 Version Control

This organization follows [Semantic Versioning](https://semver.org/):

```
MAJOR.MINOR.PATCH (e.g., 2.1.3)
  │     │     │
  │     │     └─── Bug fixes (backward compatible)
  │     └─────── New features (backward compatible)
  └──────────── Breaking changes
```

**Examples:**
- `1.0.0 → 1.0.1` - Bug fix (PATCH)
- `1.0.1 → 1.1.0` - New feature (MINOR)
- `1.1.0 → 2.0.0` - Breaking change (MAJOR)

## ✅ Success Criteria

You're doing it right when:
- ✅ Every PR updates changelog or has skip keyword
- ✅ Releases happen automatically after merges
- ✅ Release notes are clear and accurate
- ✅ Version numbers follow semantic versioning
- ✅ Contributors know what to do (clear templates)
- ✅ No manual release process needed

---

**Print this page and keep it handy! 📄**

---

*Last updated: 2024-11-18*
*Repository: [SchoutenEnZn/.github](https://github.com/SchoutenEnZn/.github)*
