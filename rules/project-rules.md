# Project Rules

Project rules offer a powerful and flexible system with path-specific configurations. Project rules are stored in the `.cursor/rules` directory and provide granular control over AI behavior in different parts of your project.

## How They Work

- **Semantic Descriptions:** Each rule can include a description of when it should be applied.
- **File Pattern Matching:** Use glob patterns to specify which files/folders the rule applies to.
- **Automatic Attachment:** Rules can be automatically included when matching files are referenced.
- **Reference Files:** Use `@file` in your project rules to include them as context when the rule is applied.

You can reference rule files using `@file`, allowing you to chain multiple rules together.

You can create a new rule using the command palette with `Cmd + Shift + P > New Cursor Rule`. By using project rules, you also get the benefit of version control since it's just a file.

## Example Use Cases

- Framework-specific rules for certain file types (e.g., SolidJS preferences for `.tsx` files).
- Special handling for auto-generated files (e.g., `.proto` files).
- Custom UI development patterns.
- Code style and architecture preferences for specific folders. 