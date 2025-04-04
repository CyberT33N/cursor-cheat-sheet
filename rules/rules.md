# Cursor Rules

This section explains how to use rules to customize AI behavior in Cursor.

## Project Rules

Project rules offer a powerful and flexible system with path-specific configurations. Project rules are stored in the `.cursor/rules` directory and provide granular control over AI behavior in different parts of your project.

### How They Work

- **Semantic Descriptions:** Each rule can include a description of when it should be applied.
- **File Pattern Matching:** Use glob patterns to specify which files/folders the rule applies to.
- **Automatic Attachment:** Rules can be automatically included when matching files are referenced.
- **Reference Files:** Use `@file` in your project rules to include them as context when the rule is applied.

You can reference rule files using `@file`, allowing you to chain multiple rules together.

You can create a new rule using the command palette with `Cmd + Shift + P > New Cursor Rule`. By using project rules, you also get the benefit of version control since it's just a file.

### Example Use Cases

- Framework-specific rules for certain file types (e.g., SolidJS preferences for `.tsx` files).
- Special handling for auto-generated files (e.g., `.proto` files).
- Custom UI development patterns.
- Code style and architecture preferences for specific folders.

## Global Rules

Global rules can be added by modifying the **Rules for AI** section under **Cursor Settings > General > Rules for AI**.

This is useful if you want to specify rules that should always be included in every project, like output language, length of responses, etc.

### List
- https://cursor.directory/rules

## .cursorrules File

For backward compatibility, you can still use a `.cursorrules` file in the root of your project. However, this feature will eventually be removed. We recommend migrating to the new **Project Rules** system for better flexibility and control. 