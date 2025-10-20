# Markdown Linter Fixer

A Claude Agent Skill that systematically fixes linting issues in markdown files using markdownlint-cli2.

## Overview

This skill provides Claude with structured workflows to diagnose, fix, and verify markdown formatting issues across projects. It focuses on the most common real-world issues, especially MD029 errors caused by improper indentation of content within ordered lists.

## What This Skill Does

The Markdown Linter Fixer skill enables Claude to:

- **Verify and install** markdownlint-cli2 if needed
- **Scan markdown files** at root level and recursively through subdirectories
- **Categorize errors** by type with frequency analysis
- **Apply automatic fixes** for correctable issues
- **Guide manual corrections** with detailed reference documentation
- **Focus on MD029 errors** - the most common issue with lists containing code blocks
- **Generate comprehensive reports** showing what was fixed and what remains

## Why This Skill?

Markdown linting errors are common in documentation, especially when combining:

- Ordered lists with code blocks
- Mixed content (paragraphs, blockquotes, nested lists)
- Technical documentation with examples

The **MD029 error** (ordered list item prefix) is particularly common and confusing. This skill includes a comprehensive guide explaining the root cause: **improper indentation** of content between list items, not just numbering inconsistencies.

## Quick Links

- **[Installation & Troubleshooting Guide](INSTALLATION.md)** - Complete installation guide with troubleshooting
- **[Plugin Documentation](PLUGIN.md)** - Plugin-specific features and configuration
- **[Changelog](CHANGELOG.md)** - Version history and release notes

## Installation

**Quick start for Claude Code:**

```bash
# Add the marketplace
/plugin marketplace add https://github.com/s2005/markdown-linter-fixer-skill

# Install the plugin
/plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace

# Restart Claude Code
```

**For complete installation instructions**, including:

- Local development setup
- Team deployment
- Manual installation (Claude.ai/Desktop/API)
- Troubleshooting
- Uninstallation with known bug workarounds

See **[INSTALLATION.md](INSTALLATION.md)**.

### Prerequisites

The skill requires `markdownlint-cli2` to be installed. Claude will check for it and guide installation if needed:

```bash
# Global installation
npm install -g markdownlint-cli2

# Or local to project
npm install --save-dev markdownlint-cli2
```

## Usage

Once installed, Claude automatically activates this skill when you:

- Ask about "markdown linting issues"
- Mention "fixing MD029 errors"
- Request to "scan markdown files"
- Say "I have ordered list numbering problems"
- Ask to "set up markdown linting"

### Slash Command

The plugin provides a unified slash command for markdown linting:

**Command Format:**

```bash
/mdlinter [mode] [scope]
```

**Arguments:**

- `mode` (optional): Either `check` or `fix`
  - `check` - Scan and report issues without making changes (DEFAULT)
  - `fix` - Scan and automatically fix all issues
  - If not specified or invalid, safely defaults to `check` mode
- `scope` (optional): Target file(s), folder, or pattern. Defaults to all markdown files in the project.

**Examples:**

```bash
# Check all files (default mode)
/mdlinter

# Explicitly check all files
/mdlinter check

# Fix all files
/mdlinter fix

# Check only README.md (default mode)
/mdlinter README.md

# Explicitly check only README.md
/mdlinter check README.md

# Fix files in docs folder
/mdlinter fix docs/

# Check multiple specific files
/mdlinter check README.md CONTRIBUTING.md
```

The check mode is useful for CI/CD or pre-commit checks, while fix mode runs the complete workflow to resolve all issues. For safety, the command always defaults to check mode when mode is not specified.

### Example Requests

**Simple cleanup:**

```text
Fix all markdown linting errors in my project
```

**Setup from scratch:**

```text
Set up markdown linting for my documentation
```

**Specific MD029 issues:**

```text
I have ordered list numbering issues in my markdown files with code blocks
```

**Comprehensive scan:**

```text
Scan all markdown files and create a report of issues
```

## Plugin Structure

```tree
.
├── .claude-plugin/
│   ├── plugin.json                 # Plugin manifest
│   └── marketplace.json            # Marketplace catalog
├── skills/                         # Skills directory
│   └── markdown-linter-fixer/      # Skill directory
│       ├── SKILL.md                # Main skill instructions
│       └── references/
│           └── MD029-Fix-Guide.md  # Detailed MD029 indentation guide
├── examples/                       # Example files
├── PLUGIN.md                       # Plugin documentation
├── README.md                       # This file
└── LICENSE                         # MIT License
```

### Progressive Disclosure Design

Following Anthropic's recommendations, this skill uses progressive disclosure:

1. **Level 1**: Metadata (`name` + `description`) - Always loaded (~50 words)
2. **Level 2**: SKILL.md body - Loaded when skill is triggered (~2,000 words)
3. **Level 3**: MD029-Fix-Guide.md - Loaded only when needed (~1,500 words)

This keeps Claude's context window efficient while providing comprehensive guidance when required.

## Key Features

### 6-Phase Workflow

1. **Environment Setup**: Verify tools and configuration
2. **Diagnostic Assessment**: Scan files and document issues
3. **Issue Analysis**: Categorize by error type
4. **Automatic Fixes**: Apply auto-fix for correctable issues
5. **Manual Fixes**: Guide through remaining corrections
6. **Verification**: Confirm completion and report results

### MD029 Indentation Focus

The included reference guide focuses on the **root cause** of MD029 errors:

- Explains why improper indentation breaks list continuity
- Provides clear 4-space indentation rules
- Shows ❌ wrong vs ✅ correct examples
- Includes real-world before/after fixes
- Documents when to use `<!-- markdownlint-disable MD029 -->`

### Configuration Awareness

- Respects existing `.markdownlint.json` files
- Creates sensible defaults (disables MD013 line length)
- Never overrides project-specific rules without permission

## Common Scenarios

### Scenario 1: Clean Project Setup

```text
User: "Set up markdown linting for my documentation"
Claude: [Installs markdownlint-cli2, creates config, runs diagnostic, reports results]
```

### Scenario 2: Fix Existing Issues

```text
User: "Fix all markdown linting errors"
Claude: [Scans, categorizes, auto-fixes, guides manual fixes, verifies completion]
```

### Scenario 3: MD029 Focus

```text
User: "My lists with code blocks show MD029 errors"
Claude: [Scans for MD029, loads indentation guide, fixes with proper 4-space indentation]
```

## Configuration

The skill creates `.markdownlint.json` with sensible defaults:

```json
{
  "MD013": false
}
```

This disables the max line length rule while keeping other formatting checks active.

## Development & Contribution

### Building from Source

```bash
# Clone the repository
git clone https://github.com/s2005/markdown-linter-fixer-skill.git
cd markdown-linter-fixer-skill

# The plugin is ready to use - skill is at skills/markdown-linter-fixer/
# For manual installation, package just the skill:
cd skills/markdown-linter-fixer
zip -r ../../markdown-linter-fixer.zip SKILL.md references/
```

### Testing the Skill

1. Install in Claude.ai or Claude Code
2. Test with a project containing markdown files
3. Verify it properly:
   - Detects markdownlint-cli2 availability
   - Scans files correctly
   - Applies fixes appropriately
   - Loads MD029 guide when needed
   - Generates accurate reports

### Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## Technical Details

**Skill Type**: Workflow-based with progressive disclosure  
**Dependencies**: markdownlint-cli2 (npm package)  
**Supported Environments**: GitBash, WSL2, Linux, macOS  
**File Format**: Markdown with YAML frontmatter  
**Reference Files**: 1 (MD029-Fix-Guide.md)

## Best Practices

- **Start with auto-fix**: Let markdownlint-cli2 handle what it can
- **Use the guide**: Load MD029-Fix-Guide.md for indentation issues
- **Preserve content**: All fixes maintain original meaning
- **Report clearly**: Always provide detailed before/after summaries
- **Respect config**: Never override project linting rules

## Security Considerations

This skill:

- ✅ Only reads/writes markdown files
- ✅ Uses standard npm package (markdownlint-cli2)
- ✅ Requires explicit user permission for file modifications
- ✅ Provides clear explanations before executing commands
- ✅ No external network calls (except npm installation)

Always review the skill contents before installing, especially:

- The commands it will execute
- The files it will modify
- The npm packages it requires

## License

MIT License - See [LICENSE](LICENSE) file for details.

## Resources

- [Claude Skills Documentation](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
- [Anthropic Skills Repository](https://github.com/anthropics/skills)
- [markdownlint-cli2 Documentation](https://github.com/DavidAnson/markdownlint-cli2)
- [Markdown Linting Rules (MD029)](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md#md029)

## Acknowledgements

Created following Anthropic's [Agent Skills design pattern](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills).

Special thanks to:

- Anthropic for the [Skills framework](https://github.com/anthropics/skills)
- David Anson for [markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2)
- The CommonMark specification team

## Support

### Reporting Issues

If you encounter problems:

1. **Check existing issues:** [GitHub Issues](../../issues)
2. **Create new issue** with:
   - Your operating system (Windows/macOS/Linux)
   - Claude Code version: `claude --version`
   - Node.js version: `node --version`
   - markdownlint-cli2 version: `markdownlint-cli2 --version`
   - Steps to reproduce
   - Error messages or logs
   - What you expected vs what happened

### Get Help

- **Issues**: Report bugs or request features via [GitHub Issues](../../issues)
- **Discussions**: Ask questions in [GitHub Discussions](../../discussions)
- **Documentation**: See [Claude Skills docs](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)

---

**Version**: 1.4.0
**Last Updated**: October 20, 2025
**Compatibility**: Claude Code, Claude Sonnet 4 and higher with code execution enabled
