# Codebase Indexing in Cursor

This section explains how to index your codebase for more accurate AI assistance and search results.

## Index your Codebase

For **better and more accurate** codebase answers, you can **index your codebase**. Cursor computes **embeddings** for each file in your project, using them to **improve search results and AI responses**.

### How It Works

- When a **project is opened**, Cursor **initializes indexing** for that workspace.
- After the initial setup, Cursor will **automatically index new files** added to your workspace.
- The indexing **status** is available under:
  **Cursor Settings > Features > Codebase Indexing**.

## Advanced Settings

By default, Cursor **indexes all files** in your codebase.

### Customization Options

Expand the **Show Settings** section to:
- Enable or disable **automatic indexing** for new repositories.
- Configure **which files should be ignored** during indexing.

### File Ignore Behavior

- Cursor respects **all `.gitignore` files**, including those in subdirectories.
- You can create a **`.cursorignore` file** for user-specific ignore patterns.
- To prevent committing `.cursorignore`, add it to your **global `.gitignore`**.

### Optimizing Accuracy

If your project contains **large content files** that AI **doesn't need**, excluding them **can improve answer quality**.

## Working with Large Monorepos

For **large monorepos** (hundreds of thousands of files), **strategic indexing** is key.

### Best Practices

- Use `.cursorignore` to let developers configure **which folders and paths** are indexed.
- Add `.cursorignore` to **your global `.gitignore`**.

This helps developers optimize indexing for **their specific work areas**.

## FAQ

### Where can I see all indexed codebases?

There's **no centralized list** of indexed codebases. To check a project's status:
1. Open the project in Cursor.
2. Navigate to **Codebase Indexing settings**.

### How do I delete all indexed codebases?

- **Option 1:** Delete your Cursor **account** from Settings (removes all indexed data).
- **Option 2:** Manually delete **individual codebases** from Codebase Indexing settings.

**Note:** There's **no bulk delete option** without deleting your account. 