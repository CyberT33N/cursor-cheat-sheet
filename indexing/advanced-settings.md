# Advanced Settings for Codebase Indexing

By default, Cursor **indexes all files** in your codebase.

## Customization Options

Expand the **Show Settings** section to:
- Enable or disable **automatic indexing** for new repositories.
- Configure **which files should be ignored** during indexing.

## File Ignore Behavior

- Cursor respects **all `.gitignore` files**, including those in subdirectories.
- You can create a **`.cursorignore` file** for user-specific ignore patterns.
- To prevent committing `.cursorignore`, add it to your **global `.gitignore`**.

## Optimizing Accuracy

If your project contains **large content files** that AI **doesn't need**, excluding them **can improve answer quality**. 