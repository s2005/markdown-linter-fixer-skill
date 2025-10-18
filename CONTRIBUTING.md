# Contributing to Markdown Linter Fixer Skill

Thank you for your interest in contributing! This document provides guidelines for contributing to the Markdown Linter Fixer skill.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Skill Development Guidelines](#skill-development-guidelines)
- [Testing](#testing)
- [Pull Request Process](#pull-request-process)

## Code of Conduct

This project follows a Code of Conduct to ensure a welcoming environment:

- Be respectful and inclusive
- Welcome newcomers and help them learn
- Focus on constructive feedback
- Respect differing viewpoints and experiences

## Getting Started

### Prerequisites

- Claude.ai account (Pro, Max, Team, or Enterprise)
- Basic understanding of Markdown
- Familiarity with markdownlint-cli2 (helpful but not required)
- Git for version control

### Setting Up Development Environment

1. Fork the repository
2. Clone your fork:

   ```bash
   git clone https://github.com/s2005/markdown-linter-fixer-skill.git
   cd markdown-linter-fixer-skill
   ```

3. Create a feature branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

## How to Contribute

### Types of Contributions

We welcome several types of contributions:

1. **Bug Reports**: Found an issue? Report it!
2. **Feature Requests**: Have an idea? Suggest it!
3. **Documentation**: Improve README, guides, or comments
4. **Code**: Fix bugs or implement features
5. **Examples**: Add new usage examples or test cases

### Reporting Bugs

When reporting bugs, please include:

- Clear, descriptive title
- Steps to reproduce the issue
- Expected behavior vs actual behavior
- Claude version and environment (Claude.ai, Claude Code, API)
- Relevant error messages or screenshots
- Example markdown files that trigger the issue (if applicable)

**Bug Report Template:**

```markdown
**Description:**
Brief description of the issue

**Steps to Reproduce:**
1. Step one
2. Step two
3. Step three

**Expected Behavior:**
What should happen

**Actual Behavior:**
What actually happens

**Environment:**
- Claude version: [e.g., Sonnet 4]
- Platform: [e.g., Claude.ai, Claude Code]
- markdownlint-cli2 version: [if applicable]

**Additional Context:**
Any other relevant information
```

### Suggesting Features

Feature suggestions should include:

- Clear use case and motivation
- How it fits with the skill's purpose
- Example of how it would work
- Potential implementation approach (optional)

## Skill Development Guidelines

### Skill Structure

Follow the established structure:

```tree
markdown-linter-fixer/
├── SKILL.md                    # Main instructions (imperative voice)
└── references/
    └── MD029-Fix-Guide.md      # Additional reference material
```

### Writing Style for SKILL.md

- Use **imperative/infinitive form** (verb-first instructions)
- Write objective, instructional language
- Example: "To accomplish X, do Y" (not "You should do X")
- Be clear and concise
- Use progressive disclosure (keep main file lean)

### Adding New Features

When adding features to the skill:

1. **Update SKILL.md** if it affects the main workflow
2. **Create reference files** for detailed guidance (keep SKILL.md lean)
3. **Update README.md** with new capabilities
4. **Add examples** showing how to use the feature
5. **Test thoroughly** in Claude environment

### Modifying MD029-Fix-Guide.md

When updating the MD029 guide:

- Keep the `<!-- markdownlint-disable MD029 -->` header
- Maintain the structure: Problem → Solution → Examples
- Include both ❌ wrong and ✅ correct examples
- Focus on practical, real-world scenarios
- Use clear before/after comparisons

### Progressive Disclosure

Follow Anthropic's progressive disclosure principle:

1. **Metadata (name/description)**: Brief, clear, trigger-focused
2. **SKILL.md**: Essential workflow and instructions
3. **Reference files**: Detailed documentation loaded as needed

Keep token usage efficient by:

- Moving detailed info to reference files
- Using clear file references in SKILL.md
- Letting Claude decide when to load additional content

## Testing

### Manual Testing

Test your changes by:

1. **Packaging the skill:**

   ```bash
   cd markdown-linter-fixer
   zip -r ../markdown-linter-fixer.zip SKILL.md references/
   ```

2. **Installing in Claude:**
   - Upload via Claude.ai Settings → Profile → Skills
   - Or use Claude Code plugin system

3. **Testing scenarios:**
   - Clean project setup
   - Fixing existing issues
   - MD029-specific problems
   - Edge cases and error handling

### Test Cases

Ensure your changes work with:

- Empty projects (no markdown files)
- Single markdown file
- Multiple files in subdirectories
- Files with various MD*** errors
- Files with correct formatting (no changes needed)
- Projects with existing `.markdownlint.json`
- Projects without markdownlint-cli2 installed

### Quality Checklist

Before submitting:

- [ ] SKILL.md uses imperative voice
- [ ] Changes are documented in README.md
- [ ] Examples are included for new features
- [ ] Tested in Claude environment
- [ ] No unnecessary duplication between SKILL.md and references
- [ ] Progressive disclosure principles followed
- [ ] Clear, concise descriptions in metadata

## Pull Request Process

### Before Submitting

1. Test your changes thoroughly
2. Update documentation
3. Add examples if introducing new features
4. Ensure SKILL.md follows style guidelines
5. Verify the skill packages correctly

### PR Guidelines

1. **Create focused PRs**: One feature or fix per PR
2. **Write clear titles**: Describe what the PR does
3. **Provide context**: Explain why the change is needed
4. **Reference issues**: Link to related issues
5. **Include test results**: Show the skill working in Claude

**PR Template:**

```markdown
**Description:**
Brief description of changes

**Motivation:**
Why is this change needed?

**Changes:**
- Change 1
- Change 2
- Change 3

**Testing:**
How was this tested?
- [ ] Tested in Claude.ai
- [ ] Tested in Claude Code
- [ ] Tested with sample projects
- [ ] Edge cases covered

**Screenshots/Examples:**
[If applicable]

**Related Issues:**
Closes #123
```

### Review Process

1. Maintainers will review your PR
2. Address any feedback or requested changes
3. Once approved, your PR will be merged
4. Your contribution will be credited in releases

## Style Guide

### Markdown Style

- Use ATX-style headers (`#` not underlines)
- Use fenced code blocks with language tags
- Include blank lines around lists and code blocks
- Keep lines readable (but MD013 is disabled)
- Use proper list indentation (4 spaces)

### Documentation Style

- Write in present tense
- Be concise but complete
- Use examples liberally
- Include both success and error cases
- Link to relevant external resources

### Code Comments

When including code examples in SKILL.md or references:

- Explain the "why" not just the "what"
- Use inline comments for complex logic
- Provide context for command-line examples
- Show expected output when helpful

## Release Process

Releases are managed by maintainers:

1. Version bump in README.md
2. Update CHANGELOG.md (if exists)
3. Create GitHub release with packaged skill
4. Tag with semantic version (e.g., v1.3.1)

## Recognition

Contributors are recognized:

- In GitHub contributors list
- In release notes for significant contributions
- In README.md acknowledgements (for major features)

## Questions?

- **Issues**: For bug reports and feature requests
- **Discussions**: For questions and general discussion
- **Email**: [Optional: Add contact email]

## Resources

- [Anthropic Skills Documentation](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
- [Agent Skills Blog Post](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- [Anthropic Skills Repository](https://github.com/anthropics/skills)
- [markdownlint-cli2 Documentation](https://github.com/DavidAnson/markdownlint-cli2)

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to make Claude better at fixing markdown linting issues!
