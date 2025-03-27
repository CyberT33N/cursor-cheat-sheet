# Ignore Files in Cursor

Learn how to use `.cursorignore` and `.cursorindexingignore` to control file access and indexing in Cursor.

## Overview

Cursor provides two different ignore files to control how files are handled:

- **`.cursorignore`**: Makes a best-effort attempt to exclude files from both AI features and indexing.
- **`.cursorindexingignore`**: Controls only which files are indexed for search and context (same as the old `.cursorignore`).

As of version **0.46**, `.cursorignore` attempts to exclude files from both **AI access and indexing** (similar to the previously unreleased `.cursorban`). For **indexing-only control**, like the old `.cursorignore`, use `.cursorindexingignore`.

## .cursorignore

The `.cursorignore` is **best-effort**, meaning **we do not guarantee that ignored files will never be sent up**. Bugs may allow ignored files to be accessed in certain cases. If you find any such issues, report them.

### Use cases

- Excluding **sensitive files** from AI access and indexing.
- Ignoring **configuration files** that contain secrets.
- Restricting access to **proprietary code**.

### Effects

Files listed in `.cursorignore` will be excluded from Cursor's AI features:
- Not included in **tab and chat requests**.
- Not included in **AI context features**.
- Not **indexed** for search or context.
- Not **accessible** via `@`-symbols or other context tools.

## .cursorindexingignore

The `.cursorindexingignore` file **automatically inherits all patterns from your `.gitignore`** files.

It only controls **which files are indexed** for search and context. This provides the same indexing control as the old `.cursorignore`.

### Use cases

- Excluding **large generated files** from indexing.
- Skipping indexing of **binary files**.
- Controlling which parts of the codebase are **searchable**.
- **Optimizing** indexing performance.

### Important

Files in `.cursorindexingignore` **can still be manually included** as context or accessed by AI features – they just **won't be automatically indexed** or included in search results.

## File Format

Both `.cursorignore` and `.cursorindexingignore` use the same syntax as `.gitignore`.

### Basic Patterns

```gitignore
# Ignore all files in the `dist` directory
dist/

# Ignore all `.log` files
*.log

# Ignore specific file `config.json`
config.json
```

### Advanced Patterns

Include only `*.py` files in the `app` directory:

```gitignore
# Ignore everything
*

# Do not ignore app
!app/

# Do not ignore directories inside app
!app/*/
!app/**/*/

# Do not ignore Python files
!*.py
```

## Troubleshooting

The ignore file syntax follows `.gitignore` exactly. If you encounter issues:

- Replace **"cursorignore"** with **"gitignore"** in search queries.
- Check **Stack Overflow** for similar patterns.
- Test patterns with:
  ```bash
  git check-ignore -v [file]
  ```
  to understand how matching works.

### Common Gotchas

- Patterns are **matched relative** to the ignore file location.
- **Later patterns override earlier ones**.
- **Directory patterns require a trailing slash (`/`)**.
- **Negation patterns (`!`) must negate a previous pattern**. 