# Uninstall Test: Plugin and Marketplace Removal

This document provides step-by-step instructions for completely uninstalling the markdown-linter-fixer plugin and removing its marketplace.

## Prerequisites

- Claude Code is installed and accessible via CLI
- Marketplace is configured
- Plugin is currently installed

## Step 1: Check Current Status

First, verify what's currently installed:

```bash
claude plugin marketplace list
```

**Expected Output:**

```text
Configured marketplaces:

  ❯ markdown-linter-fixer-marketplace
    Source: Directory (/path/to/markdown-linter-fixer-skill)
```

Check plugin status:

### Option 1: Simple list with status (Recommended)

```bash
jq -r '.enabledPlugins | to_entries[] | "\(.key): \(if .value then "enabled" else "disabled" end)"' ~/.claude/settings.json
```

### Option 2: Formatted table

```bash
echo "INSTALLED PLUGINS:" && jq -r '.enabledPlugins | to_entries[] | "  [\(if .value then "V" else " " end)] \(.key | split("@")[0]) (from: \(.key | split("@")[1]))"' ~/.claude/settings.json
```

### Option 3: Check specific plugin

```bash
jq -r --arg plugin "markdown-linter-fixer@markdown-linter-fixer-marketplace" '.enabledPlugins[$plugin] // "not installed"' ~/.claude/settings.json
```

Look for `markdown-linter-fixer@markdown-linter-fixer-marketplace` in the output.

### Alternative Methods for Listing Plugins

**1. List all plugins with status:**

```bash
jq -r '.enabledPlugins | to_entries[] | "\(.key): \(if .value then "enabled" else "disabled" end)"' ~/.claude/settings.json
```

**Expected Output:**

```text
example-skills@anthropic-agent-skills: enabled
markdown-linter-fixer@markdown-linter-fixer-marketplace: enabled
```

**2. Formatted table view:**

```bash
echo "INSTALLED PLUGINS:" && jq -r '.enabledPlugins | to_entries[] | "  [\(if .value then "V" else " " end)] \(.key | split("@")[0]) (from: \(.key | split("@")[1]))"' ~/.claude/settings.json
```

**Expected Output:**

```text
INSTALLED PLUGINS:
  [V] example-skills (from: anthropic-agent-skills)
  [ ] document-skills (from: anthropic-agent-skills)
  [V] markdown-linter-fixer (from: markdown-linter-fixer-marketplace)
```

**3. Check if specific plugin exists:**

```bash
jq -r --arg plugin "markdown-linter-fixer@markdown-linter-fixer-marketplace" '.enabledPlugins[$plugin] // "not installed"' ~/.claude/settings.json
```

**Expected Output:**

```text
true
```

**4. Get raw JSON (for scripting):**

```bash
jq '.enabledPlugins' ~/.claude/settings.json
```

**Expected Output:**

```json
{
  "example-skills@anthropic-agent-skills": true,
  "markdown-linter-fixer@markdown-linter-fixer-marketplace": true
}
```

**5. Count total plugins:**

```bash
jq '.enabledPlugins | length' ~/.claude/settings.json
```

**Expected Output:**

```text
3
```

## Step 2: Disable the Plugin (Optional)

Before uninstalling, you can optionally disable the plugin:

```bash
claude plugin disable markdown-linter-fixer@markdown-linter-fixer-marketplace
```

**Expected Output:**

```text
✔ Plugin disabled successfully
```

## Step 3: Uninstall the Plugin

Remove the plugin completely:

```bash
claude plugin uninstall markdown-linter-fixer@markdown-linter-fixer-marketplace
```

**Expected Output:**

```text
✔ Plugin uninstalled successfully
```

## Step 4: Remove the Marketplace

Remove the marketplace from your configuration:

```bash
claude plugin marketplace remove markdown-linter-fixer-marketplace
```

**Expected Output:**

```text
✔ Marketplace removed successfully
```

## Step 5: Manual Cleanup (REQUIRED - Temporary Workaround)

⚠️ **TEMPORARY WORKAROUND**: This manual step is required until [Claude Code issue #9537](https://github.com/anthropics/claude-code/issues/9537) is resolved. Once the bug is fixed, Step 5 will no longer be necessary.

**IMPORTANT**: Due to [Claude Code issue #9537](https://github.com/anthropics/claude-code/issues/9537), the CLI commands do not automatically clean up the `settings.json` configuration file. **You must manually edit this file.**

### Known Bug Details

- **Bug**: Plugin marketplace removal doesn't clean up settings.json, causing marketplace to reinstall
- **Impact**: Marketplace automatically reinstalls on next Claude Code startup
- **Root Cause**: CLI commands modify runtime state but don't update persistent settings.json
- **Issue**: <https://github.com/anthropics/claude-code/issues/9537>
- **Status**: Open as of October 2025
- **Workaround**: Manual editing required (see commands below)

### Files to Manually Edit

Edit the following files to remove leftover configuration:

1. **Global settings**: `~/.claude/settings.json`
2. **Project settings**: `.claude/settings.json` (if present in your repository)
3. **Local settings**: `.claude/settings.local.json` (if present in your repository)

### What to Remove

Open `~/.claude/settings.json` in a text editor and remove these entries:

**Remove from `enabledPlugins`:**

```json
"enabledPlugins": {
  "markdown-linter-fixer@markdown-linter-fixer-marketplace": false  // ← Remove this line
}
```

**Remove from `extraKnownMarketplaces`:**

```json
"extraKnownMarketplaces": [
  {
    "name": "markdown-linter-fixer-marketplace"  // ← Remove this entire entry
  }
]
```

**Example of clean settings.json:**

```json
{
  "enabledPlugins": {
    // other plugins...
  },
  "extraKnownMarketplaces": [
    // other marketplaces...
  ]
}
```

### Manual Cleanup Commands

**IMPORTANT**: These commands are temporary workarounds until the bug is fixed.

#### Option 1: Check What Needs Cleaning (All Platforms)

First, verify the stale entry exists:

```bash
# Check for plugin entry in settings.json
cat ~/.claude/settings.json | grep "markdown-linter"
```

**Expected output (showing the bug):**

```text
"markdown-linter-fixer@markdown-linter-fixer-marketplace": true
```

Even though you removed the marketplace, this entry remains!

#### Option 2: Using jq (Recommended - All Platforms)

If you have `jq` installed, use this automated cleanup:

```bash
# Backup settings.json first
cp ~/.claude/settings.json ~/.claude/settings.json.backup

# Remove the plugin entry using jq
jq 'del(.enabledPlugins["markdown-linter-fixer@markdown-linter-fixer-marketplace"])' \
  ~/.claude/settings.json > ~/.claude/settings.json.tmp && \
  mv ~/.claude/settings.json.tmp ~/.claude/settings.json

# Verify it's gone
cat ~/.claude/settings.json | grep "markdown-linter"
```

**Expected output after cleanup:**

```text
(no output - entry is removed)
```

#### Option 3: Manual Edit (Windows)

```bash
# Open in Notepad (Windows)
notepad "%USERPROFILE%\.claude\settings.json"

# Find and DELETE the line containing:
# "markdown-linter-fixer@markdown-linter-fixer-marketplace": true

# Save and close
```

#### Option 4: Manual Edit (macOS/Linux)

```bash
# Using nano
nano ~/.claude/settings.json

# Using VS Code
code ~/.claude/settings.json

# Using vim
vim ~/.claude/settings.json

# Find and DELETE the line containing:
# "markdown-linter-fixer@markdown-linter-fixer-marketplace": true

# Save and exit
```

### Verification After Manual Cleanup

```bash
# Verify the entry is completely removed
cat ~/.claude/settings.json | grep "markdown-linter"

# Should return nothing if cleanup was successful
```

## Step 6: Verify Cleanup

Check that the marketplace is no longer listed:

```bash
claude plugin marketplace list
```

**Expected Output:**

The `markdown-linter-fixer-marketplace` should NOT appear in the list.

**If it still appears**: You didn't complete Step 5 (manual cleanup). The marketplace configuration remains in `settings.json`.

## Step 7: Restart Claude Code

Restart Claude Code (if running) to ensure all changes take effect

## Step 8: Final Verification

Verify complete removal:

```bash
# Should NOT list markdown-linter-fixer-marketplace
claude plugin marketplace list

# Should NOT list markdown-linter-fixer plugin
jq -r '.enabledPlugins | to_entries[] | "\(.key): \(if .value then "enabled" else "disabled" end)"' ~/.claude/settings.json | grep markdown-linter-fixer
```

## Troubleshooting

### Issue: Marketplace Reinstalls After Restart

**Symptom**: After restarting Claude Code, `markdown-linter-fixer-marketplace` reappears in marketplace list.

**Cause**: Step 5 (manual cleanup) was not completed. The `settings.json` file still contains marketplace configuration.

**Solution**:

1. Check `~/.claude/settings.json` for `extraKnownMarketplaces` entries
2. Remove the marketplace entry manually
3. Restart Claude Code again

### Issue: Cannot Remove Marketplace

**Symptom**: `claude plugin marketplace remove` fails with an error.

**Solution**:

1. Ensure you're using the correct marketplace name: `markdown-linter-fixer-marketplace`
2. Check the marketplace exists: `claude plugin marketplace list`
3. Try removing with exact name from the list

## Re-installation Instructions

To reinstall the plugin after testing uninstall:

```bash
# Add marketplace
claude plugin marketplace list
claude plugin validate ./
claude plugin marketplace add ./
claude plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
```

**Note**: Restart Claude Code after reinstalling.

## What This Test Demonstrates

This test demonstrates:

1. The official uninstall commands work for removing plugin runtime state
2. **TEMPORARY**: The [known bug #9537](https://github.com/anthropics/claude-code/issues/9537) requires manual cleanup (Step 5)
3. Without Step 5 (manual cleanup), the marketplace will reinstall automatically on restart
4. **Current workaround**: Complete removal requires both CLI commands AND manual settings.json editing
5. **Future**: Once bug #9537 is resolved, Step 5 will no longer be necessary

### Why Manual Cleanup is Required (Until Bug is Fixed)

The bug causes:

- CLI commands update **runtime state** (what you see in `plugin marketplace list`)
- CLI commands DO NOT update **persistent state** (`~/.claude/settings.json`)
- On restart, Claude Code reads settings.json and reinstalls the marketplace

**When the bug is fixed**: The CLI commands will automatically clean both runtime AND persistent state, eliminating the need for manual cleanup.

## Related Documentation

- [INSTALLATION.md - Uninstalling section](../INSTALLATION.md#uninstalling)
- [Claude Code Issue #9537](https://github.com/anthropics/claude-code/issues/9537)
- [Plugin Documentation](../PLUGIN.md)
