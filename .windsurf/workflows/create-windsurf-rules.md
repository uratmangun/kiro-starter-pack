---
description: Creates comprehensive Windsurf rules following the official schema with proper YAML frontmatter and markdown structure
---

You are a Windsurf rules generator that creates well-structured rule files following the official schema.

## Rule Creation Process

1. **Understand the Rule Requirements**
   - Ask the user what coding standard, practice, or constraint they want to enforce
   - Clarify the rule's purpose, scope, and when it should be applied
   - Identify specific technologies, frameworks, or scenarios where the rule applies

2. **Generate Rule Filename**
   - Create a lowercase filename with hyphens (e.g., `use-bun-or-pnpm-for-nodejs-dependency-manager.md`)
   - Ensure the name clearly describes the rule's purpose
   - Keep it concise but descriptive (max 60 characters)

3. **Create YAML Frontmatter**
   - Add required `trigger` field with activation modes:
     - `manual` - Rule activated via @mention in Cascade's input box
     - `always_on` - Rule always applied (Always On)
     - `model_decision` - Model decides whether to apply rule (Model Decision)
     - `glob` - Applied to files matching specified glob pattern
   - Add required `description` field (50-150 characters)
   - Add optional `globs` field (required only for `glob` trigger type)
   - Write a complete sentence describing what the rule enforces
   - Keep it concise but informative

4. **Structure the Rule Content**
   Follow this standard format:
   
   ```markdown
   # [Rule Title]
   
   ## [Main Concept/Overview]
   
   **MANDATORY**: Clear statement of what must be done or avoided.
   
   ### [Sub-sections as needed]
   - Specific guidelines
   - Examples with code blocks
   - Configuration details
   - Best practices
   
   ### [Common Patterns]
   
   ```language
   // Good example
   code_example_here
   
   // Bad example  
   code_example_here
   ```
   
   ### [Additional Guidelines]
   
   - Bullet points with specific rules
   - References to tools or commands
   - Exception handling (if any)
   
   [Closing statement explaining the benefit/rationale]
   ```

5. **Include Essential Elements**
   - Clear mandatory statements using **MANDATORY** or **REQUIRED**
   - Code examples showing correct and incorrect usage
   - Specific commands, file patterns, or configurations
   - Rationale explaining why the rule exists
   - Exception handling for edge cases

6. **Choose Appropriate Trigger**
   - `always_on`: Rule applies to all code changes and interactions
   - `manual`: Rule only applies when explicitly mentioned via @mention
   - `model_decision`: Rule applies when the model decides it's relevant based on context
   - `glob`: Rule applies to files matching the specified glob pattern

7. **Create the Rule File**
   - Save to `.windsurf/rules/[rule-name].md`
   - Ensure proper YAML frontmatter formatting
   - Validate Markdown syntax
   - Test the rule by referencing it in conversations

## Schema Compliance Checklist

- [ ] YAML frontmatter with `trigger` and `description` fields
- [ ] Lowercase filename with hyphens
- [ ] Clear mandatory statements
- [ ] Code examples with proper syntax highlighting
- [ ] Logical section organization
- [ ] Specific, actionable guidelines
- [ ] Rationale for the rule
- [ ] File saved in `.windsurf/rules/` directory

## Example Rule Structure

```markdown
---
trigger: always_on
description: "Enforces use of TypeScript for all new JavaScript files to improve code quality and maintainability"
---

# TypeScript Usage Standards

## Required Language

**MANDATORY**: Use TypeScript for all new JavaScript files. Avoid plain JavaScript except for legacy code maintenance.

### File Extensions

- Use `.ts` for TypeScript files
- Use `.tsx` for React components with TypeScript
- Never create new `.js` or `.jsx` files

### Configuration

```json
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true
  }
}
```

### Migration Strategy

- Convert existing `.js` files to `.ts` when making significant changes
- Add proper type annotations for function parameters and return types
- Use interfaces for object structures

This ensures better code quality, improved IDE support, and reduced runtime errors.
```

The workflow will help create consistent, well-structured rules that integrate seamlessly with Windsurf's rule system.
