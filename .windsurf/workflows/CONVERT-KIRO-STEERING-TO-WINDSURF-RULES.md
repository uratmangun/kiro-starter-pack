---
description: Converts Kiro steering rules from .kiro/steering directory to Windsurf rules format in .windsurf/rules directory
---

You are a rule conversion specialist that converts Kiro steering files to Windsurf rules format.

## Conversion Process

1. **Analyze Source Directory**
   - Examine all `.md` files in `.kiro/steering/` directory
   - Identify files with `inclusion: always` frontmatter (these are active rules)
   - Note the content structure and formatting of each file

2. **Prepare Target Directory**
   - Ensure `.windsurf/rules/` directory exists
   - Create the directory if it doesn't exist using: `mkdir -p .windsurf/rules`

3. **Convert Each Steering File**
   For each file in `.kiro/steering/`:
   
   a. **Read the source file** and extract:
      - YAML frontmatter (especially `inclusion` field)
      - Main content body
      - File structure and formatting
   
   b. **Transform the content**:
      - Keep the same filename (e.g., `shell-preferences.md`)
      - **Convert YAML frontmatter** from Kiro format to Windsurf rules format:
        
        **For `inclusion: always`:**
        ```yaml
        ---
        name: "[Descriptive Rule Name]"
        trigger: always_on
        description: "[Natural language description of the rule's purpose]"
        ---
        ```
        
        **For `inclusion: fileMatch` with patterns:**
        Create separate rule files for each glob pattern:
        ```yaml
        ---
        trigger: glob
        description: "[Natural language description of the rule's purpose for pattern1]"
        globs: "pattern1"
        ---
        ```
        
        ```yaml
        ---
        trigger: glob
        description: "[Natural language description of the rule's purpose for pattern2]"
        globs: "pattern2"
        ---
        ```
        ```
        
        **Glob Pattern Examples:**
        
        Basic File Extension Patterns:
        ```yaml
        ---
        trigger: glob
        description: "JavaScript development standards"
        globs: "*.js"
        ---
        ```
        ```yaml
        ---
        trigger: glob
        description: "Python coding guidelines"
        globs: "*.py"
        ---
        ```
        ```yaml
        ---
        trigger: glob
        description: "TypeScript development rules"
        globs: "*.ts"
        ---
        ```
        ```yaml
        ---
        trigger: glob
        description: "Documentation formatting standards"
        globs: "*.md"
        ---
        ```
        
        Directory-based Patterns:
        ```yaml
        ---
        trigger: glob
        description: "Source code TypeScript standards"
        globs: "src/**/*.ts"
        ---
        ```
        ```yaml
        ---
        trigger: glob
        description: "Test file Python standards"
        globs: "tests/*.py"
        ---
        ```
        ```yaml
        ---
        trigger: glob
        description: "Documentation standards"
        globs: "docs/**/*.md"
        ---
        ```
        
        Complex Pattern Examples:
        ```yaml
        ---
        trigger: glob
        description: "Source code development standards"
        globs: "src/**/*.{js,ts,py}"
        ---
        ```
        
        Example for Supabase config (create separate files):
        
        File: `supabase-directory.md`
        ```yaml
        ---
        trigger: glob
        description: "Applies Supabase project configuration rules for files in supabase directory"
        globs: "supabase/**/*"
        ---
        ```
        
        File: `supabase-config-files.md`
        ```yaml
        ---
        trigger: glob
        description: "Applies Supabase project configuration rules for supabase.toml files"
        globs: "**/supabase.toml"
        ---
        ```
        
        File: `config-toml-files.md`
        ```yaml
        ---
        trigger: glob
        description: "Applies Supabase project configuration rules for config.toml files"
        globs: "**/config.toml"
        ---
        ```
        
        **How Glob Triggers Work:**
        - **Purpose**: The rule will be applied to all files that match the specified pattern
        - **Activation**: File-pattern-based activation
        - **Use case**: When you want a rule to apply only to specific types of files or files in certain directories
        - **Multiple patterns**: For multiple file types, create separate rules for different patterns or use brace expansion syntax
        
      - Generate appropriate `name` based on file content and purpose
      - For `inclusion: always`:
        - Set `trigger: "always_on"`
        - Set `name` and `description` fields
      - For `inclusion: fileMatch`:
        - Set `trigger: "glob"`
        - Convert `fileMatchPattern` array to `globs` array
        - Set `description` field
      - Create meaningful descriptions summarizing the rule's function
      - Maintain all content formatting and examples
      - Ensure code blocks and syntax highlighting remain intact
   
   c. **Write to target location**:
      - Save to `.windsurf/rules/[filename].md`
      - Preserve original formatting and structure
      - Maintain file permissions

4. **Handle Special Files**
   - Convert files with spaces in names to dash-separated format if needed
   - Ensure all rule files have proper YAML frontmatter
   - Validate that `inclusion: always` is preserved for active rules

5. **Verification Steps**
   - Confirm all source files have been converted
   - Verify target files maintain original content integrity
   - Check that YAML frontmatter is properly formatted
   - Ensure no content is lost during conversion

## File Mapping Examples

```
.kiro/steering/shell-preferences.md → .windsurf/rules/shell-preferences.md
.kiro/steering/spec-generation-standards.md → .windsurf/rules/spec-generation-standards.md
.kiro/steering/supabase-function-deployment.md → .windsurf/rules/supabase-function-deployment.md
```

## Frontmatter Conversion Examples

### Shell Preferences
**From:**
```yaml
---
inclusion: always
---
```
**To:**
```yaml
---
name: "Fish Shell Execution Standards"
trigger: "always_on"
description: "Enforces fish shell syntax for all terminal commands and provides conversion patterns from bash"
---
```

### Spec Generation Standards
**From:**
```yaml
---
inclusion: always
---
```
**To:**
```yaml
---
name: "Kiro Specification Generation Requirements"
trigger: "always_on"
description: "Mandates creation of comprehensive Kiro specifications for all development plans following the three-file format"
---
```

### Supabase Function Deployment
**From:**
```yaml
---
inclusion: always
---
```
**To:**
```yaml
---
name: "Supabase Function Deployment Process"
trigger: "always_on"
description: "Defines the standard process for deploying Supabase functions using Docker container operations"
---
```

## Quality Assurance

After conversion:
- Compare file counts between source and target directories
- Spot-check converted files for content accuracy
- Verify YAML frontmatter is properly converted to Windsurf format
- Ensure all rules have proper `name`, `trigger`, and `description` fields
- Validate that `trigger` is set to "always_on" for files with `inclusion: always`
- Ensure code examples and formatting remain intact
- Test that rules are properly recognized by Windsurf

## Notes

- This conversion maintains the exact content and structure of Kiro steering files
- The primary change is the file location from `.kiro/steering/` to `.windsurf/rules/`
- All development standards, shell preferences, and project-specific rules are preserved
- Files with `inclusion: always` frontmatter become active Windsurf rules