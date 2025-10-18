<!-- markdownlint-disable MD029 -->
# Fixing MD029 Markdownlint Errors: Ordered List Item Prefix

> **Note:** This documentation file has markdownlint rules disabled at the top because it intentionally contains examples of problematic markdown code that would otherwise trigger linting errors. This is a common practice in documentation that demonstrates what NOT to do.

## Problem Description

The MD029 markdownlint rule triggers the following error:

```text
MD029/ol-prefix: Ordered list item prefix [Expected: 1; Actual: 2; Style: 1/1/1]
```

This error occurs when markdownlint detects what it perceives as separate ordered lists instead of a continuous numbered list.

## Root Cause

The primary cause of MD029 errors is **improper indentation of content between ordered list items**. When code blocks, paragraphs, or other content appear between list items without proper indentation, Markdown parsers interpret this as breaking the list continuity.

### Example of Problematic Code

<!-- markdownlint-disable MD029 MD032 -->

```markdown
1. First item

```bash
some code here
```

2. Second item  <!-- This triggers MD029 error -->

```text

<!-- markdownlint-enable MD029 MD032 -->

In the above example, the code block breaks the list, causing item 2 to be seen as starting a new list.

## Solution: Proper Indentation

### For Code Blocks

Indent code blocks with **4 spaces** (or more, depending on nesting level) to maintain list continuity:

```markdown
1. First item

    ```bash
    some code here
    ```

2. Second item  <!-- No MD029 error -->

3. Third item

    ```bash
    another code block
    ```

4. Fourth item
```

### For Paragraphs

Indent continuation paragraphs with **at least 1 space** (typically 4 spaces for consistency):

```markdown
1. First item

    This is a continuation paragraph that belongs to item 1.
    It should be indented to maintain list continuity.

2. Second item

    Another continuation paragraph.

3. Third item
```

### For Mixed Content

You can mix different types of content by maintaining proper indentation:

```markdown
1. First step

    ```bash
    command --option value
    ```

    This command does something important.

2. Second step

    ```bash
    another-command --flag
    ```

    Additional explanation here.

3. Final step
```

## Indentation Rules

| Content Type | Indentation Required |
|--------------|---------------------|
| Code blocks (fenced) | 4 spaces minimum |
| Code blocks (indented) | 8 spaces minimum |
| Paragraphs | 4 spaces (recommended) |
| Blockquotes | 4 spaces + `>` |
| Nested lists | 4 spaces per level |

## Common Mistakes to Avoid

<!-- markdownlint-disable MD029 MD032 MD031 -->

### ❌ Wrong: No indentation

```markdown
1. Item one

```bash
code here
```

2. Item two  <!-- MD029 error -->
```text

### ❌ Wrong: Insufficient indentation

```markdown
1. Item one

  ```bash
  code here  <!-- Only 2 spaces, not enough -->
  ```

2. Item two  <!-- MD029 error -->
```text

<!-- markdownlint-enable MD029 MD032 MD031 -->

### ✅ Correct: Proper indentation
```markdown
1. Item one

    ```bash
    code here  <!-- 4 spaces indentation -->
    ```

2. Item two  <!-- No error -->
```

## Alternative Solutions (Not Recommended)

While the following approaches can technically resolve MD029 errors, they are not recommended as they affect readability and functionality:

### Using Only "1." for All Items

```markdown
1. First item
1. Second item  <!-- Auto-numbered by renderer -->
1. Third item
```

### Disabling the Rule

```markdown
<!-- markdownlint-disable MD029 -->
1. First item
2. Second item
3. Third item
```

### Ignoring MD029 Errors in Specific Sections

Sometimes you need to intentionally include examples of problematic markdown (like in this documentation file). In such cases, you can disable the MD029 rule for specific sections:

```markdown
<!-- markdownlint-disable MD029 MD032 -->

1. Item one

```bash
code here
```

2. Item two  <!-- This would normally trigger MD029 error -->

<!-- markdownlint-enable MD029 MD032 -->
```text

**When to use this approach:**
- In documentation files showing examples of problematic code
- When demonstrating what NOT to do
- In code examples that are meant to illustrate errors

**Note:** This documentation file itself uses `<!-- markdownlint-disable MD029 -->` at the top to prevent errors from the intentional "bad examples" shown throughout the document.

## Best Practices

1. **Always use 4-space indentation** for content within list items
2. **Maintain consistent indentation** throughout the document
3. **Test your markdown** with a preview to ensure proper rendering
4. **Use fenced code blocks** (```) rather than indented code blocks when possible
5. **Keep list items logically grouped** - if content doesn't belong to a list item, consider restructuring

## Real-World Example

Here's a common scenario showing how proper indentation fixes MD029 errors:

### Before (with MD029 errors):

```markdown
1. Clone the repository

```bash
git clone https://github.com/example/project.git
```

2. Install dependencies  <!-- MD029 error here -->

```bash
npm install
```

3. Run the application  <!-- MD029 error here -->
```

### After (MD029 errors fixed):

```markdown
1. Clone the repository

    ```bash
    git clone https://github.com/example/project.git
    ```

2. Install dependencies  <!-- No error -->

    ```bash
    npm install
    ```

3. Run the application  <!-- No error -->

    ```bash
    npm start
    ```
```

## Verification

After applying the fixes, run markdownlint to verify:

```bash
markdownlint your-file.md
```

You should see no MD029 errors in the output.

## Conclusion

The key to fixing MD029 errors is understanding that Markdown requires proper indentation to maintain list continuity. By indenting code blocks and other content with 4 spaces, you ensure that the markdown parser recognizes them as part of the list items rather than separate elements that break the list.
