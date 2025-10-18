# Installation and Troubleshooting Guide

Quick reference for installing and troubleshooting the Markdown Linter Fixer plugin.

## Quick Start

### 1. Add the Marketplace

```bash
/plugin marketplace add https://github.com/s2005/markdown-linter-fixer-skill
```

### 2. Install the Plugin

```bash
/plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
```

### 3. Restart Claude Code

Restart Claude Code for the plugin to take effect.

### 4. Install markdownlint-cli2

```bash
npm install -g markdownlint-cli2
```

### 5. Verify Installation

```bash
/plugin
```

Look for "markdown-linter-fixer" in the enabled plugins list.

## Installation Methods

### Method 1: From GitHub (Recommended)

```bash
# Add marketplace
/plugin marketplace add https://github.com/s2005/markdown-linter-fixer-skill

# Install plugin
/plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace

# Restart Claude Code
```

### Method 2: Interactive Menu

```bash
# Open plugin interface
/plugin

# Navigate: Browse Plugins → markdown-linter-fixer → Install
# Restart Claude Code
```

### Method 3: Local Development

```bash
# Clone repository
git clone https://github.com/s2005/markdown-linter-fixer-skill.git

# Add local marketplace (use absolute path)
/plugin marketplace add D:/path/to/markdown-linter-fixer-skill

# Install plugin
/plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace

# Restart Claude Code
```

## Prerequisites

### Node.js and npm

The plugin requires `markdownlint-cli2`, which needs Node.js and npm.

**Check if installed:**

```bash
node --version
npm --version
```

**Install Node.js:**

Download from [nodejs.org](https://nodejs.org/) (LTS version recommended)

### markdownlint-cli2

**Global installation (recommended):**

```bash
npm install -g markdownlint-cli2
```

**Local installation:**

```bash
npm install --save-dev markdownlint-cli2
```

**Verify installation:**

```bash
markdownlint-cli2 --version
```

## Common Issues

### Issue 1: Marketplace Not Found

**Error:** "Cannot find marketplace at URL"

**Solutions:**

1. Check the URL is correct:

   ```bash
   /plugin marketplace add https://github.com/s2005/markdown-linter-fixer-skill
   ```

2. For local paths, use absolute paths:

   ```bash
   /plugin marketplace add D:/full/path/to/markdown-linter-fixer-skill
   ```

3. Ensure the repository has `.claude-plugin/marketplace.json`

### Issue 2: Plugin Not Showing

**Error:** Plugin doesn't appear after adding marketplace

**Solutions:**

1. List marketplaces:

   ```bash
   /plugin marketplace list
   ```

2. Verify marketplace.json exists in `.claude-plugin/` directory

3. Check plugin name in marketplace.json is `markdown-linter-fixer`

### Issue 3: Plugin Not Loading

**Error:** Plugin installed but not working

**Solutions:**

1. **Verify installation:**

   ```bash
   /plugin
   ```

   Look for "markdown-linter-fixer" in the list

2. **Check if enabled:**
   Make sure it's not in "Disabled" status

3. **Restart Claude Code:**
   Plugins require restart after installation

4. **Reinstall if needed:**

   ```bash
   /plugin uninstall markdown-linter-fixer@markdown-linter-fixer-marketplace
   /plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
   ```

### Issue 4: Skill Not Activating

**Error:** Claude doesn't use the skill when expected

**Understanding model-invoked skills:**

Skills are automatically activated by Claude based on context. They are NOT slash commands.

**How to trigger the skill:**

Use explicit keywords in your requests:

✅ **Good requests:**

- "Fix all markdown linting errors in my project"
- "Scan markdown files for MD029 errors"
- "Set up markdown linting for my documentation"
- "I have ordered list numbering issues"

❌ **Ambiguous requests:**

- "Clean up my files"
- "Fix my docs"
- "Check everything"

**Force activation:**

```text
Use the markdown-linter-fixer skill to scan and fix all markdown files
```

**Verify skill loaded:**

Skills should be available automatically. Check `/help` for any markdown-related guidance.

### Issue 5: markdownlint-cli2 Not Found

**Error:** "markdownlint-cli2: command not found"

**Solutions:**

1. **Install globally:**

   ```bash
   npm install -g markdownlint-cli2
   ```

2. **Or install locally:**

   ```bash
   npm install --save-dev markdownlint-cli2
   ```

3. **Verify installation:**

   ```bash
   markdownlint-cli2 --version
   ```

4. **If npm not found, install Node.js:**
   - Download from [nodejs.org](https://nodejs.org/)
   - Restart terminal after installation
   - Try installing markdownlint-cli2 again

### Issue 6: Permission Errors

**Error:** "EACCES: permission denied" during npm install

**On Windows:**

```bash
# Run terminal as Administrator
# Or install locally:
npm install --save-dev markdownlint-cli2
```

**On macOS/Linux:**

```bash
# Option 1: Use sudo (not recommended for security)
sudo npm install -g markdownlint-cli2

# Option 2: Configure npm prefix (recommended)
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
npm install -g markdownlint-cli2
```

### Issue 7: Skill Files Missing

**Error:** Claude reports it cannot find SKILL.md or reference files

**Check directory structure:**

```tree
.claude-plugin/
  ├── plugin.json
  └── marketplace.json
skills/
  └── markdown-linter-fixer/
      ├── SKILL.md
      └── references/
          └── MD029-Fix-Guide.md
```

**Verify plugin.json:**

```json
{
  "name": "markdown-linter-fixer",
  "version": "1.2.0",
  "skills": [
    {
      "name": "markdown-linter-fixer",
      "path": "skills/markdown-linter-fixer"
    }
  ]
}
```

**Reinstall if structure is wrong:**

```bash
/plugin uninstall markdown-linter-fixer@markdown-linter-fixer-marketplace
/plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
```

## Verification Checklist

After installation, verify everything is working:

- [ ] Marketplace added: `/plugin marketplace list`
- [ ] Plugin installed: `/plugin` shows "markdown-linter-fixer"
- [ ] Plugin enabled: Not in "Disabled" status
- [ ] Claude Code restarted
- [ ] markdownlint-cli2 installed: `markdownlint-cli2 --version`
- [ ] Test with request: "Scan markdown files for errors"

## Team Installation

For automatic installation across your team:

### Add to Repository Settings

Create or edit `.claude/settings.json` in your repository:

```json
{
  "marketplaces": [
    {
      "url": "https://github.com/s2005/markdown-linter-fixer-skill",
      "name": "markdown-linter-fixer-marketplace"
    }
  ],
  "plugins": [
    {
      "name": "markdown-linter-fixer",
      "marketplace": "markdown-linter-fixer-marketplace",
      "enabled": true
    }
  ]
}
```

Team members who trust the repository folder will automatically:

1. Have the marketplace added
2. Have the plugin installed
3. Be able to use the skill immediately

## Uninstalling

### Disable Temporarily

```bash
/plugin disable markdown-linter-fixer@markdown-linter-fixer-marketplace
```

### Remove Completely

```bash
/plugin uninstall markdown-linter-fixer@markdown-linter-fixer-marketplace
```

### Remove Marketplace

```bash
/plugin marketplace remove markdown-linter-fixer-marketplace
```

## Getting Help

### Check Logs

Claude Code logs may contain error details:

- Look for plugin loading errors
- Check skill activation messages
- Review any file access issues

### Report Issues

If you encounter problems:

1. **Check existing issues:** [GitHub Issues](https://github.com/s2005/markdown-linter-fixer-skill/issues)
2. **Create new issue** with:
   - Your operating system
   - Claude Code version
   - Steps to reproduce
   - Error messages or logs
   - What you expected vs what happened

### Documentation

- **Plugin Guide:** [PLUGIN.md](PLUGIN.md)
- **Main README:** [README.md](README.md)
- **Claude Code Plugins:** [Official Docs](https://docs.claude.com/en/docs/claude-code/plugins)
- **Agent Skills:** [Skills Documentation](https://docs.claude.com/en/docs/claude-code/skills)

## Quick Reference

### Useful Commands

```bash
# Plugin management
/plugin                                    # Open plugin menu
/plugin marketplace list                   # List marketplaces
/plugin marketplace add <url>              # Add marketplace
/plugin install <name>@<marketplace>       # Install plugin
/plugin disable <name>@<marketplace>       # Disable plugin
/plugin enable <name>@<marketplace>        # Enable plugin
/plugin uninstall <name>@<marketplace>     # Uninstall plugin

# Tool verification
markdownlint-cli2 --version               # Check if installed
node --version                            # Check Node.js
npm --version                             # Check npm
```

### Skill Activation Keywords

Use these phrases to trigger the skill:

- "markdown linting"
- "MD029 errors"
- "fix markdown files"
- "scan markdown documentation"
- "ordered list numbering issues"
- "set up markdown linting"

## Support

- **Issues:** [GitHub Issues](https://github.com/s2005/markdown-linter-fixer-skill/issues)
- **Discussions:** [GitHub Discussions](https://github.com/s2005/markdown-linter-fixer-skill/discussions)
- **Email:** <s2005@users.noreply.github.com>

---

**Version:** 1.2.0
**Last Updated:** October 18, 2025
