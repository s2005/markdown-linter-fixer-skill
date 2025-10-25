# Release Process

This document describes how to create a new release of the Markdown Linter Fixer Skill.

## Overview

The release process involves:

1. Creating a release branch
2. Updating the version in `marketplace.json`
3. Creating a Pull Request for review
4. Merging the PR
5. Creating and pushing a git tag
6. Creating a GitHub release (which triggers automatic packaging)

## Version Numbering

We follow [Semantic Versioning](https://semver.org/):

- **MAJOR** (X.0.0): Incompatible API changes or major rewrites
- **MINOR** (0.X.0): New features in a backward-compatible manner
- **PATCH** (0.0.X): Backward-compatible bug fixes

Current version is stored in `.claude-plugin/marketplace.json`.

## Creating a Release

### Step 1: Set Version and Create Release Branch

```bash
# Set the new version as environment variable
export MD_FIXER_VERSION="1.5.0"

# Create and checkout a new release branch
git checkout -b release/v$MD_FIXER_VERSION
```

### Step 2: Update Version Number

Update the version in `.claude-plugin/marketplace.json` using jq:

```bash
jq --arg version "$MD_FIXER_VERSION" '.plugins[0].version = $version' .claude-plugin/marketplace.json > .claude-plugin/marketplace.json.tmp && mv .claude-plugin/marketplace.json.tmp .claude-plugin/marketplace.json
```

Or manually edit the file if jq is not available.

### Step 3: Commit and Push Branch

```bash
git add .claude-plugin/marketplace.json
git commit -m "chore: bump version to $MD_FIXER_VERSION"
git push -u origin release/v$MD_FIXER_VERSION
```

### Step 4: Create Pull Request

Create a PR using GitHub CLI:

```bash
gh pr create \
  --title "chore: bump version to $MD_FIXER_VERSION" \
  --body "Updates version to $MD_FIXER_VERSION for upcoming release" \
  --base main \
  --label "release"
```

Or create it via the [GitHub web UI](https://github.com/s2005/markdown-linter-fixer-skill/compare).

### Step 5: Review and Merge PR

1. Review the PR
2. Verify the version number is correct in `.claude-plugin/marketplace.json`
3. Merge the PR to `main`

### Step 6: Create and Push Tag

After the PR is merged:

```bash
# Switch to main and pull the merged changes
git checkout main
git pull origin main

# Create an annotated tag (using the same version)
git tag -a v$MD_FIXER_VERSION -m "Release version $MD_FIXER_VERSION"

# Push the tag to GitHub
git push origin v$MD_FIXER_VERSION
```

### Step 7: Create GitHub Release

Create the release using GitHub CLI:

```bash
gh release create v$MD_FIXER_VERSION --title "v$MD_FIXER_VERSION" --generate-notes
```

Or via the GitHub web UI:

1. Go to [Releases](https://github.com/s2005/markdown-linter-fixer-skill/releases)
2. Click **Draft a new release**
3. Click **Choose a tag** and select `v$MD_FIXER_VERSION`
4. Click **Generate release notes** (optional but recommended)
5. Review the release notes
6. Click **Publish release**

## What Happens After Release

When you create a GitHub release, the **Release Skill** workflow automatically:

1. ✓ Extracts version from `marketplace.json`
2. ✓ Verifies skill structure (SKILL.md, frontmatter, required fields)
3. ✓ Builds the skill zip archive:
   - Contains: `markdown-linter-fixer/SKILL.md`
   - Contains: `markdown-linter-fixer/references/*.md`
   - Validated structure for Claude.ai upload
4. ✓ Attaches `markdown-linter-fixer-skill.zip` to the release
5. ✓ Generates `SKILL_INSTALLATION.md` with instructions
6. ✓ Creates artifacts (retained for 90 days)

## Testing the Release

After the release is published:

1. Download `markdown-linter-fixer-skill.zip` from the release
2. Go to [Claude.ai](https://claude.ai/) → Settings → Capabilities
3. Upload the skill
4. Test with a project containing markdown files
5. Verify the skill works as expected

## Rollback Process

If you need to rollback a release:

```bash
# Delete the tag locally and remotely
git tag -d v1.5.0
git push origin :refs/tags/v1.5.0

# Delete the GitHub release via UI or CLI
gh release delete v1.5.0

# Revert the version bump commit
git revert <commit-hash>
git push origin main
```

## Troubleshooting

### Tag already exists

```bash
# Delete and recreate the tag
git tag -d v1.5.0
git push origin :refs/tags/v1.5.0
git tag -a v1.5.0 -m "Release version 1.5.0"
git push origin v1.5.0
```

### Release workflow failed

1. Check the [Actions](https://github.com/s2005/markdown-linter-fixer-skill/actions) tab
2. Review the workflow logs
3. Fix any issues
4. Re-run the workflow or trigger manually

### Skill zip is invalid

1. Download the artifact from the failed workflow
2. Extract and verify structure
3. Ensure `SKILL.md` has proper frontmatter
4. Check that references directory exists

## Release Checklist

Before creating a release:

- [ ] All changes are committed and pushed
- [ ] Tests pass (if applicable)
- [ ] CHANGELOG.md is updated
- [ ] Version number follows semver
- [ ] No uncommitted changes in working directory

After creating PR:

- [ ] PR has been reviewed
- [ ] Version bump PR is merged to main
- [ ] Tag is created and pushed
- [ ] GitHub release is created

After release:

- [ ] Skill zip is attached to release
- [ ] Installation instructions are generated
- [ ] Skill installs successfully in Claude.ai
- [ ] Skill functionality is tested
- [ ] Release notes are accurate

## Quick Reference

**Complete release process:**

```bash
# Set version
export MD_FIXER_VERSION="1.5.0"

# 1. Create release branch
git checkout -b release/v$MD_FIXER_VERSION

# 2. Update version in marketplace.json
jq --arg version "$MD_FIXER_VERSION" '.plugins[0].version = $version' .claude-plugin/marketplace.json > .claude-plugin/marketplace.json.tmp && mv .claude-plugin/marketplace.json.tmp .claude-plugin/marketplace.json

# 3. Commit and push branch
git add .claude-plugin/marketplace.json
git commit -m "chore: bump version to $MD_FIXER_VERSION"
git push -u origin release/v$MD_FIXER_VERSION

# 4. Create PR
gh pr create --title "chore: bump version to $MD_FIXER_VERSION" \
  --body "Updates version to $MD_FIXER_VERSION for upcoming release" \
  --base main --label "release"

# 5. Review and merge PR via GitHub UI

# 6. Pull merged changes and create tag
git checkout main
git pull origin main
git tag -a v$MD_FIXER_VERSION -m "Release version $MD_FIXER_VERSION"
git push origin v$MD_FIXER_VERSION

# 7. Create GitHub release
gh release create v$MD_FIXER_VERSION --title "v$MD_FIXER_VERSION" --generate-notes
```

## Additional Resources

- [Semantic Versioning](https://semver.org/)
- [GitHub Releases Documentation](https://docs.github.com/en/repositories/releasing-projects-on-github)
- [Claude Skills Documentation](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
