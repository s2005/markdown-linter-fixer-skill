# Changelog

All notable changes to the Markdown Linter Fixer skill will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.3.0] - 2025-10-18

### Added in 1.3.0

- MD036-Guide.md reference documentation for proper heading usage
- `.markdownlint-cli2.jsonc` configuration file support with `ignores` array
- Configuration to exclude example files from linting
- Memory note for markdown style guidelines

### Changed in 1.3.0

- Updated SKILL.md to recommend `.markdownlint-cli2.jsonc` instead of `.markdownlint.json`
- Converted bold text subsections to proper markdown headings (####) throughout SKILL.md
- Fixed heading hierarchy in SKILL.md (h2 → h3 → h4)
- Enhanced configuration documentation with `ignores` array usage examples

### Fixed in 1.3.0

- All MD036 (no-emphasis-as-heading) errors in SKILL.md
- All MD001 (heading-increment) errors in SKILL.md
- Markdown linting errors in MD036-Guide.md reference file
- Corrected `.claude-plugin/marketplace.json` source path format

### Improved in 1.3.0

- Better configuration file structure with support for file exclusions
- Comprehensive documentation for avoiding MD036 violations
- All markdown files now pass linting with 0 errors

## [1.2.0] - 2025-10-18

### Added

- Claude Code plugin structure with marketplace support
- `.claude-plugin/marketplace.json` for plugin catalog configuration
- `PLUGIN.md` with comprehensive plugin documentation
- Marketplace installation instructions in README.md
- Skills reference in plugin.json manifest
- Support for `/plugin marketplace add` installation method
- Interactive plugin menu installation support
- Team workflow configuration documentation
- Local development installation guide

### Changed

- Reorganized project as Claude Code plugin with marketplace
- Updated README.md installation section to prioritize marketplace installation
- Renamed manual installation from Option 2 to Option 3
- Enhanced plugin structure diagram to include marketplace.json
- Updated plugin.json to include skills array reference

### Improved

- Easier installation via Claude Code plugin system
- Better team collaboration through repository-level plugin configuration
- More discoverable through marketplace browsing
- Clearer separation between plugin documentation (PLUGIN.md) and skill documentation (README.md)

## [1.1.0] - 2025-10-17

### Added in version 1.1.0

- Comprehensive MD029-Fix-Guide.md focusing on indentation as root cause
- Real-world examples showing proper 4-space indentation
- Table of indentation requirements for different content types
- ❌ Wrong vs ✅ Correct example comparisons
- Documentation on using markdownlint-disable comments
- Detailed troubleshooting section

### Changed in version 1.1.0

- Updated SKILL.md to emphasize indentation focus for MD029 errors
- Enhanced Phase 3 (Issue Analysis) to note MD029 patterns with code blocks
- Improved Phase 5 (Manual Fixes) with clearer indentation guidance
- Updated Resources section to accurately describe guide contents
- Refined Scenario 3 to mention "lists with code blocks"

### Improved in version 1.1.0

- More practical focus on real-world MD029 causes
- Better alignment with actual markdown linting issues developers face
- Clearer explanations of when content breaks list continuity

## [1.0.0] - 2025-10-17

### Added in version 1.0.0

- Initial release of Markdown Linter Fixer skill
- 6-phase workflow for systematic markdown linting
- Environment setup and prerequisites checking
- Diagnostic assessment (root and recursive scans)
- Issue analysis and categorization
- Automatic fixes using markdownlint-cli2 --fix
- Manual fix guidance
- Verification and comprehensive reporting
- MD029 reference guide (initial version)
- Configuration file creation (.markdownlint.json)
- Support for GitBash, WSL2, Linux, macOS

### Features

- Progressive disclosure design (3 levels)
- Automatic markdownlint-cli2 detection
- Sensible configuration defaults (MD013 disabled)
- Clear error reporting at each phase
- Configuration-aware (respects existing configs)
- Common scenario examples
- Integration with Anthropic Skills framework

---

## Version History Summary

- **1.3.0** - Configuration improvements and MD036 documentation
- **1.2.0** - Plugin structure with marketplace support
- **1.1.0** - Enhanced MD029 guide with indentation focus
- **1.0.0** - Initial release with full workflow and basic MD029 guide

## Upcoming Features

Potential future enhancements:

- Support for additional markdownlint rules documentation
- Interactive fix mode with user confirmations
- Batch processing for multiple projects
- Integration with CI/CD pipelines
- Custom rule configuration templates
- Git integration for commit hooks

## Migration Notes

### Upgrading to 1.2.0 (Plugin Structure)

If you previously installed as a standalone skill:

1. Uninstall the old skill from Claude.ai/Desktop
2. Install via Claude Code plugin system:

   ```bash
   /plugin marketplace add https://github.com/s2005/markdown-linter-fixer-skill
   /plugin install markdown-linter-fixer@markdown-linter-fixer-marketplace
   ```

3. All existing workflows continue to work
4. Enjoy easier installation and updates

### Upgrading from 1.0.0 to 1.1.0

No breaking changes. Simply replace the old skill package with the new one:

1. Remove old skill from Claude
2. Upload new markdown-linter-fixer.zip
3. All existing workflows continue to work
4. Enhanced MD029 guidance available immediately

---

For detailed information about each release, see the [Releases](../../releases) page.
