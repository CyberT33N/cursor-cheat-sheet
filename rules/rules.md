# Cursor Rules

This section explains how to use rules to customize AI behavior in Cursor.

## Project Rules

<details><summary>Click to expand..</summary>

Example:

<details><summary>Click to expand..</summary>

```mdc
      ---
      description: This rule prohibits the use of wildcard/star exports in JavaScript and TypeScript files. It requires developers to explicitly list each named export rather than using the catch-all export syntax. This practice improves code clarity, makes dependencies explicit, prevents accidental exports, and enables better static analysis and tree-shaking. The rule applies to all JavaScript and TypeScript files in the project and ensures that the codebase maintains clear and intentional export boundaries.
      globs: ["**/*.{ts,tsx,mjs,mts}"]
      alwaysApply: false
      tags: ["exports", "imports", "clarity", "tree-shaking", "maintainability", "typescript", "javascript"]
      priority: 80
      version: "1.1"
      ---
      
      # No Star Exports in JavaScript/TypeScript
      
      ## Critical Rules
      
      1.  **NEVER** use star/wildcard exports (`export * from './file'`) in JavaScript or TypeScript files. 🚫
      2.  **ALWAYS** explicitly list each named export when re-exporting from another file. ✅
      3.  When exporting from another module, use named exports with destructuring: `export { name1, name2 } from './file'`.
      4.  For default exports being re-exported, use the explicit syntax: `export { default as ComponentName } from './file'`. (Ensure the source file actually has a default export).
      5.  When creating barrel files (index.ts/js), list all exports individually.
      6.  Clearly identify what specific functionality is being exported from each imported module.
      7.  If many exports need to be re-exported, list them systematically, grouped by source file for better organization.
      8.  When refactoring existing code, replace **ALL** star exports with explicit named exports.
      
      ## Examples
      
      <example>
      // ✅ CORRECT - Explicit named exports
      
      // Explicitly list each export being re-exported
      export { EvidentService } from './EvidentServiceClass.ts'
      export { setAbb, resetSpecificAbbs, checkOrCreateAbbs } from './abbreviation.ts'
      export { executeUserSql } from './sql.ts'
      
      // Re-exporting a default export with a specific name
      export { default as UserComponent } from './UserComponent.ts'
      
      // Grouped by source for better organization when there are many exports
      // From authentication module
      export { login, logout, validateToken } from './auth/authentication.ts'
      export { hasPermission, Role, Permission } from './auth/authorization.ts'
      
      // Using aliased exports when needed
      export { default as Button } from './components/Button.ts'
      export { default as TextField } from './components/TextField.ts'
      export { submitForm as sendFormData } from './forms/submission.ts'
      </example>
      
      <example type="invalid">
      // ❌ INCORRECT - Using star exports
      
      // Generic star exports that hide what's actually being exported
      export * from './EvidentServiceClass.ts'
      export * from './abbreviation.ts'
      export * from './sql.ts'
      
      // Star export with default export being re-exported
      export * from './components/Button.ts'
      
      // Star exports in barrel files
      // index.ts
      export * from './models/user.ts'
      export * from './models/post.ts'
      export * from './utils/helpers.ts'
      </example>
      
      ## Why This Rule Is Important
      
      1. **Explicitness and Clarity**: Explicit exports clearly communicate which specific functions, classes, or values are being exported. This makes it easier for developers to understand what a module provides without having to examine the source files.
      
      2. **Better Tree-Shaking**: Bundlers like Webpack and Rollup can more effectively perform tree-shaking (dead code elimination) when exports are explicit. Star exports can prevent proper tree-shaking because the bundler cannot determine which exports are actually used.
      
      3. **Prevents Accidental Exports**: Star exports can inadvertently expose internal implementation details or utilities that were not meant to be part of the public API. Explicit exports ensure only intended functionality is exposed.
      
      4. **Avoids Name Collisions**: When using star exports from multiple modules, name collisions can occur silently, with later exports overriding earlier ones. Explicit exports make such conflicts immediately visible.
      
      5. **Improves Code Navigation**: IDEs and code analysis tools can more easily track explicit imports and exports, improving features like "Go to Definition" and refactoring capabilities.
      
      6. **Better Documentation**: Explicit exports serve as a form of documentation, clearly showing the public API of a module at the export site rather than requiring developers to look through the source files.
      
      ## Implementing This Rule
      
      ### When Creating New Files
      
      When creating new barrel files or modules that re-export from other files:
      
      ```typescript
      // In index.ts, instead of:
      export * from './user-service'
      
      // Do this:
      export { 
        createUser, 
        getUserById, 
        updateUser, 
        deleteUser 
      } from './user-service'
      ```
      
      ### When Refactoring Existing Code
      
      To refactor existing star exports:
      
      1. Identify all exports from the source module:
         ```typescript
         // Check the './user-service.ts' file to see what it exports
         ```
      
      2. Replace the star export with explicit named exports:
         ```typescript
         // Replace:
         export * from './user-service'
         
         // With:
         export { 
           createUser, 
           getUserById, 
           updateUser, 
           deleteUser 
         } from './user-service'
         ```
      
      ### Handling Default Exports
      
      For modules with default exports, ensure you explicitly re-export them using the `default as` syntax. The source module must, of course, have a default export.
      
      ```typescript
      // Source file: ./Button.ts
      // export default class Button { ... }
      
      // Barrel file: ./components/index.ts
      // Instead of (doesn't re-export the default):
      // export * from './Button' 
      
      // Do this:
      export { default as Button } from './Button'
      ```
      
      ## Edge Cases and Exceptions
      
      There are **no exceptions** to this rule. All star exports **MUST** be replaced with explicit named exports, even in the following cases:
      
      1.  **Large Number of Exports**: Even when a module exports many items, they **MUST** all be listed explicitly. This may make the export statement longer but maintains clarity, intentionality, and toolability.
      
      2.  **Re-exporting an Entire API**: When creating a facade or adapter over another library, each re-exported item **MUST** still be listed explicitly.
      
      3.  **Type Exports (TypeScript)**: This rule applies equally to type exports. Since TypeScript **does not allow `export type * from './file';`**, you are already required to use explicit type re-exports: `export type { TypeName1, TypeName2 } from './file'`. This rule reinforces that this explicit practice should be followed for *all* exports, not just types. 
```


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



</details>














<br><br>
___
<br><br>


## Global Rules

<details><summary>Click to expand..</summary>

Global rules can be added by modifying the **Rules for AI** section under **Cursor Settings > General > Rules for AI**.

This is useful if you want to specify rules that should always be included in every project, like output language, length of responses, etc.

### List
- https://cursor.directory/rules

</details>


<br><br>
___
<br><br>


## .cursorrules File

<details><summary>Click to expand..</summary>

For backward compatibility, you can still use a `.cursorrules` file in the root of your project. However, this feature will eventually be removed. We recommend migrating to the new **Project Rules** system for better flexibility and control. 

</details>
