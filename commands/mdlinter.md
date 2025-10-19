---
description: Check or fix markdown linting issues with optional scope
---

# Markdown Linter - {{ARGUMENTS}}

Use the `markdown-linter-fixer` skill to check or fix markdown linting issues.

**Command format:** `/mdlinter [mode] [scope]`

**Arguments:**

- Mode (optional): `{{ARGUMENTS}}`
  - First argument can be either `check` or `fix`
  - `check` - scan and report issues WITHOUT making changes (DEFAULT if not specified or invalid)
  - `fix` - scan and automatically fix all issues
  - **Safety default**: If no mode is provided or an invalid mode is given, defaults to `check` mode

- Scope (optional):
  - Can be specified as second argument (or first if mode is omitted)
  - Can be: a specific file, multiple files (space-separated), a folder, or a glob pattern
  - If not provided, operates on ALL markdown files in the project

**Examples:**

- `/mdlinter` - check all files (default mode)
- `/mdlinter check` - explicitly check all files
- `/mdlinter fix` - fix all files
- `/mdlinter README.md` - check only README.md (default mode)
- `/mdlinter check README.md` - explicitly check only README.md
- `/mdlinter fix docs/` - fix all files in docs folder
- `/mdlinter check README.md CONTRIBUTING.md` - check specific files

**Workflow based on mode:**

**IMPORTANT**: If mode is not specified or is invalid, always use CHECK mode as the safe default.

**For CHECK mode:**

1. Verify markdownlint-cli2 installation
2. Check for existing configuration files
3. Run diagnostic scans on the specified scope
4. Categorize and analyze all errors by type
5. Generate comprehensive report
6. IMPORTANT: Do NOT execute auto-fix (--fix flag)
7. Do NOT make any manual fixes to files
8. ONLY scan and report the issues found

**For FIX mode:**

1. Verify markdownlint-cli2 installation
2. Check/create configuration files
3. Run diagnostic scans on the specified scope
4. Apply automatic fixes using --fix flag
5. Handle any remaining manual fixes (especially MD029 issues)
6. Verify all issues are resolved
7. Provide comprehensive summary report

**Report should include:**

- Total files scanned
- All errors found by type (MD001, MD029, MD032, etc.)
- File names and line numbers for each error
- Count of each error type
- Which errors are auto-fixable vs require manual intervention
