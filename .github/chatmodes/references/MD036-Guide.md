# Markdown Style Guide

## MD036 Rule - No Emphasis as Heading

**Rule**: Never use bold text (`**text**`) as a heading substitute. Always use proper markdown heading syntax.

### ❌ Wrong

```markdown
**Configuration File Check**

Some content here...
```

### ✅ Correct

```markdown
#### Configuration File Check

Some content here...
```

### Heading Level Guidelines

- Use `#` through `######` for headings (h1-h6)
- Maintain proper heading hierarchy:
  - `#` Main title (h1)
  - `##` Major sections (h2)
  - `###` Subsections under h2 (h3)
  - `####` Subsections under h3 (h4)
- Never skip heading levels (e.g., don't jump from h2 to h4)

### Common Violations to Avoid

1. **Bold text on standalone lines** - These should be headings
2. **Section dividers using bold** - Use proper heading levels instead
3. **Emphasis for structure** - Use headings for document structure, bold only for emphasis within content

### When Creating/Modifying Markdown Files

- Always use heading syntax (`####`) for section titles
- Reserve bold text (`**text**`) for emphasis within paragraphs only
- Run `markdownlint-cli2` to verify before committing
