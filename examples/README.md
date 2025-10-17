# Example Markdown Files

This directory contains example markdown files for testing the Markdown Linter Fixer skill.

## Files

### with-md029-errors.md

A markdown file with intentional MD029 errors. Use this to test the skill's ability to:

- Detect MD029 errors
- Identify improperly indented code blocks
- Generate accurate diagnostic reports

**Common errors in this file:**

- Code blocks not indented within list items
- Paragraphs breaking list continuity

### with-md029-fixed.md

The corrected version showing proper 4-space indentation. Compare with the error version to understand:

- How proper indentation maintains list continuity
- The correct way to include code blocks in lists
- The difference between broken and continuous lists

## Usage

### Testing the Skill

1. Copy these files to a test directory
2. Ask Claude to scan for markdown linting issues
3. Compare the fixes Claude applies with the fixed version
4. Verify the skill correctly identifies and fixes MD029 errors

### Example Commands

**In Claude.ai or Claude Code:**

```text
Scan the examples directory and fix all markdown linting issues
```

```text
Check with-md029-errors.md and explain the issues found
```

```text
Fix MD029 errors in with-md029-errors.md and show me the differences
```

### Expected Behavior

When running the skill on `with-md029-errors.md`, you should see:

1. **Diagnostic Phase**:
   - Reports multiple MD029 errors
   - Identifies lines where code blocks break lists

2. **Auto-Fix Phase**:
   - Attempts automatic fixes
   - May not resolve all issues (indentation requires understanding)

3. **Manual Fix Phase**:
   - Loads MD029-Fix-Guide.md
   - Explains proper 4-space indentation
   - Guides through manual corrections

4. **Verification Phase**:
   - Re-scans the file
   - Confirms all MD029 errors resolved
   - Provides summary report

## Creating Your Own Test Cases

To create additional test files:

1. Write markdown with various errors
2. Run markdownlint-cli2 to verify errors exist
3. Document the expected errors
4. Create a fixed version for comparison

## Common Test Scenarios

### Scenario 1: Simple List with Code

Test basic ordered lists with code blocks

### Scenario 2: Nested Lists

Test multiple levels of indentation

### Scenario 3: Mixed Content

Test lists with code blocks, paragraphs, and blockquotes

### Scenario 4: Multiple Error Types

Test files with MD029 plus other errors (MD032, MD047, etc.)

## Verification

After the skill fixes a file, verify:

```bash
# Should show no errors
markdownlint-cli2 with-md029-errors.md

# Compare with expected result
diff with-md029-errors.md with-md029-fixed.md
```

## Tips

- Use these examples when contributing to the skill
- Create new examples for edge cases you discover
- Document any issues you find during testing
- Share your test cases in pull requests
