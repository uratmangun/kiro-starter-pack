---
description: Creates a new Windsurf workflow following the official schema guidelines and best practices
---

You are a Windsurf workflow generator that creates well-structured workflow files following the official schema.

## Workflow Creation Process

1. **Understand the Requirements**
   - Ask the user what task or process they want to automate
   - Clarify the workflow's purpose and scope
   - Identify any dependencies or prerequisites

2. **Generate Workflow Name**
   - Create a lowercase filename with hyphens replacing spaces (e.g., `auto-readme-generator.md`)
   - Ensure the name clearly describes the workflow's purpose
   - Check that the name doesn't conflict with existing workflows

3. **Create YAML Frontmatter**
   - Add required `description` field (50-150 characters)
   - Write a complete sentence describing the workflow's purpose
   - Keep it concise but informative

4. **Structure the Content**
   Choose the appropriate content format:
   
   **Step-by-Step Instructions** (most common):
   ```markdown
   1. First step description
   2. Second step description
   3. Third step description
   ```
   
   **Contextual Instructions** (for complex workflows):
   ```markdown
   You are a [role] that will [purpose].
   
   [Detailed context and instructions]
   
   [Specific steps to execute]
   ```
   
   **Template-Based Instructions** (when output format matters):
   ```markdown
   Generate a [output] following this format:
   
   ```
   [template or example]
   ```
   
   [Additional instructions]
   ```

5. **Add Special Annotations (if needed)**
   - Use `// turbo` above steps that should auto-run individually
   - Use `// turbo-all` anywhere in the workflow to auto-run all command steps
   - Only add these annotations for safe, non-destructive operations

6. **Include Best Practices**
   - Make instructions clear and specific
   - Include error handling guidance where appropriate
   - Specify file paths and command syntax precisely
   - Add context about when to use the workflow

7. **Create the Workflow File**
   - Save to `.windsurf/workflows/[workflow-name].md` (lowercase with dashes)
   - Ensure proper YAML frontmatter formatting
   - Validate Markdown syntax

## Schema Compliance Checklist

- [ ] YAML frontmatter with `description` field
- [ ] Lowercase filename with hyphens (no spaces)
- [ ] Clear, actionable instructions
- [ ] Proper Markdown formatting
- [ ] Appropriate use of turbo annotations (if any)
- [ ] File saved in `.windsurf/workflows/` directory

## Example Output Structure

```markdown
---
description: Brief description of what this workflow accomplishes
---

[Clear instructions for the workflow, following one of the content structure patterns above]
```

The workflow will automatically be registered as a slash command based on its filename (e.g., `/create-windsurf-workflow` for this file).
