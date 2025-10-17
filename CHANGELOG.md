# Changelog

All notable changes to the Markdown Linter Fixer skill will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2025-10-17

### Added in version 1.1.0

- Comprehensive MD029-Fix-Guide.md focusing on indentation as root cause
- Real-world examples showing proper 4-space indentation
- Table of indentation requirements for different content types
- ❌ Wrong vs ✅ Correct example comparisons
- Documentation on using markdownlint-disable comments
- Detailed troubleshooting section

### Changed

- Updated SKILL.md to emphasize indentation focus for MD029 errors
- Enhanced Phase 3 (Issue Analysis) to note MD029 patterns with code blocks
- Improved Phase 5 (Manual Fixes) with clearer indentation guidance
- Updated Resources section to accurately describe guide contents
- Refined Scenario 3 to mention "lists with code blocks"

### Improved

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

### Upgrading from 1.0.0 to 1.1.0

No breaking changes. Simply replace the old skill package with the new one:

1. Remove old skill from Claude
2. Upload new markdown-linter-fixer.zip
3. All existing workflows continue to work
4. Enhanced MD029 guidance available immediately

---

For detailed information about each release, see the [Releases](../../releases) page.
