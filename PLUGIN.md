# Markdown Linter Fixer Plugin

A Claude Code plugin that provides systematic markdown linting and fixing capabilities through agent skills.

## Overview

This plugin extends Claude Code with the `markdown-linter-fixer` agent skill, enabling Claude to automatically diagnose, fix, and verify markdown formatting issues across your projects using markdownlint-cli2.

## What This Plugin Provides

### Skills

- **markdown-linter-fixer**: Model-invoked agent skill that Claude autonomously uses when markdown linting tasks are detected

The skill is automatically activated when users:

- Ask about "markdown linting issues"
- Mention "fixing MD029 errors"
- Request to "scan markdown files"
- Say "I have ordered list numbering problems"
- Ask to "set up markdown linting"

## Installation

### Via Marketplace (Recommended)

```bash
# Add the marketplace
/plugin marketplace add https://github.com/s2005/markdown-linter-fixer-skill

# Install the plugin
/plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
```

### Via Interactive Menu

```bash
# Open the plugin interface
/plugin

# Select "Browse Plugins" → markdown-linter-fixer → Install
```

### For Local Development

```bash
# Clone the repository
git clone https://github.com/s2005/markdown-linter-fixer-skill.git

# Add as local marketplace
/plugin marketplace add ./markdown-linter-fixer-skill

# Install the plugin
/plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
```

After installation, restart Claude Code to activate the plugin.

## Usage

Once installed, Claude automatically uses the skill when appropriate. Simply ask Claude to help with markdown tasks:

```text
Fix all markdown linting errors in my project
```

```text
Set up markdown linting for my documentation
```

```text
I have ordered list numbering issues in my markdown files
```

Claude will invoke the skill automatically and follow the structured workflow to diagnose, fix, and verify markdown issues.

## Features

### 6-Phase Workflow

1. **Environment Setup**: Verifies markdownlint-cli2 installation and configuration
2. **Diagnostic Assessment**: Scans root and recursive markdown files
3. **Issue Analysis**: Categorizes errors by type with frequency analysis
4. **Automatic Fixes**: Applies auto-fix for correctable issues
5. **Manual Fixes**: Guides through remaining corrections with reference documentation
6. **Verification**: Confirms completion and generates detailed reports

### Special Focus on MD029 Errors

The skill includes comprehensive guidance for MD029 (ordered list item prefix) errors, which are often caused by improper indentation of content between list items:

- Explains the root cause: content breaking list continuity
- Provides 4-space indentation rules for code blocks and paragraphs
- Shows clear wrong ❌ vs correct ✅ examples
- Includes real-world before/after fixes

### Configuration Awareness

- Respects existing `.markdownlint.json` configuration files
- Creates sensible defaults when none exist (disables MD013 line length)
- Never overrides project-specific rules without permission

## Requirements

The skill requires `markdownlint-cli2` to be installed. Claude will check for it and guide installation if needed:

```bash
# Global installation
npm install -g markdownlint-cli2

# Or local to project
npm install --save-dev markdownlint-cli2
```

## Plugin Structure

```tree
.
├── .claude-plugin/
│   ├── plugin.json          # Plugin manifest
│   └── marketplace.json     # Marketplace catalog
└── skills/
    └── markdown-linter-fixer/
        ├── SKILL.md         # Main skill instructions
        └── references/
            └── MD029-Fix-Guide.md  # Detailed MD029 guide
```

## Team Workflows

### Repository-Level Installation

Configure the plugin for automatic installation across your team by adding to `.claude/settings.json`:

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

Team members who trust the repository will automatically have the plugin installed.

## Verification

After installation, verify the plugin is active:

```bash
# Check installed plugins
/plugin

# Look for "markdown-linter-fixer" in the list
```

The skill will be available immediately for Claude to invoke when markdown-related tasks are detected.

## Troubleshooting

### Plugin Installation Issues

#### Marketplace Not Found

If you get an error when adding the marketplace:

```bash
# For GitHub repository
/plugin marketplace add https://github.com/s2005/markdown-linter-fixer-skill

# For local directory (use absolute path)
/plugin marketplace add D:/mcp/claude/markdown-linter-fixer-skill
```

Make sure:

- The URL is correct and accessible
- For local paths, use absolute paths (not relative)
- The repository contains `.claude-plugin/marketplace.json`

#### Plugin Not Found in Marketplace

If the plugin doesn't appear after adding the marketplace:

1. Check marketplace was added: `/plugin marketplace list`
2. Verify marketplace.json exists in `.claude-plugin/` directory
3. Check the plugin name in marketplace.json matches: `markdown-linter-fixer`

### Plugin Not Loading

If the plugin is installed but not working:

1. **Verify installation**: `/plugin` - Look for "markdown-linter-fixer" in the list
2. **Check status**: Ensure it shows as "Enabled" (not "Disabled")
3. **Restart Claude Code**: Plugins require restart after installation
4. **Check plugin structure**: Verify `.claude-plugin/plugin.json` exists with skills array

### Skill Not Activating

The skill is **model-invoked**, meaning Claude decides when to use it based on task context.

**Common reasons why skills don't activate:**

1. **Ambiguous request**: Be explicit with keywords
   - ✅ "Fix all markdown linting errors in my project"
   - ✅ "Scan markdown files for MD029 errors"
   - ❌ "Clean up my files"

2. **Skill not loaded**: Check if the plugin is enabled

3. **Tool dependency missing**: Ensure markdownlint-cli2 is installed

**How to force activation:**

```text
Use the markdown-linter-fixer skill to scan and fix all markdown files
```

**Verify skill is available:**

Check Claude Code settings or use `/help` to see if markdown-related commands are available.

### markdownlint-cli2 Not Found

The skill requires `markdownlint-cli2` to function.

**Install globally:**

```bash
npm install -g markdownlint-cli2
```

**Or install locally in your project:**

```bash
npm install --save-dev markdownlint-cli2
```

**Verify installation:**

```bash
markdownlint-cli2 --version
```

**If npm is not installed:**

1. Install Node.js from [nodejs.org](https://nodejs.org/)
2. Restart your terminal
3. Install markdownlint-cli2

### Permission Issues

If you get permission errors during npm installation:

**On Windows:**

```bash
# Run as Administrator or use local installation
npm install --save-dev markdownlint-cli2
```

**On macOS/Linux:**

```bash
# Use sudo for global installation
sudo npm install -g markdownlint-cli2

# Or configure npm to use a different directory
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
npm install -g markdownlint-cli2
```

### Skill Files Not Found

If Claude reports skill files are missing:

1. **Check directory structure:**

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

2. **Verify plugin.json has skills reference:**

   ```json
   {
     "skills": [
       {
         "name": "markdown-linter-fixer",
         "path": "skills/markdown-linter-fixer"
       }
     ]
   }
   ```

3. **Reinstall the plugin:**

   ```bash
   /plugin uninstall markdown-linter-fixer@markdown-linter-fixer-marketplace
   /plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
   ```

### Still Having Issues?

1. **Check Claude Code logs** for error messages
2. **Verify plugin compatibility** with your Claude Code version
3. **Report issues** on [GitHub Issues](https://github.com/s2005/markdown-linter-fixer-skill/issues)
4. **Review documentation** at [Claude Code Plugins Guide](https://docs.claude.com/en/docs/claude-code/plugins)

## Uninstalling

```bash
# Disable the plugin
/plugin disable markdown-linter-fixer@markdown-linter-fixer-marketplace

# Or completely remove it
/plugin uninstall markdown-linter-fixer@markdown-linter-fixer-marketplace
```

## Version

**Current Version**: 1.2.0

## License

MIT License - See [LICENSE](LICENSE) file for details.

## Support

- **Issues**: [GitHub Issues](https://github.com/s2005/markdown-linter-fixer-skill/issues)
- **Documentation**: [README.md](README.md)
- **Plugin Guide**: [Claude Code Plugins Documentation](https://docs.claude.com/en/docs/claude-code/plugins)

## See Also

- [Agent Skills Documentation](https://docs.claude.com/en/docs/claude-code/skills)
- [Plugin Marketplaces](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)
- [markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2)
