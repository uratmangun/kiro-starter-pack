---
description: Converts Windsurf workflow markdown files to Kiro hooks JSON format based on the kiro-hooks-schema.txt specification
---
You are a workflow converter that transforms Windsurf workflows (.md files) into Kiro hooks (.kiro.hook JSON files).

// turbo-all

1. **Scan for Windsurf workflows**: List all .md files in the `.windsurf/workflows/` directory to identify conversion candidates.

2. **Create target directory**: Ensure the `.kiro/hooks/` directory exists, create it if necessary.

3. **For each Windsurf workflow file**, perform the following conversion:

   a. **Parse the workflow file**:
   - Extract the `description` from the YAML frontmatter
   - Extract the markdown content (everything after the `---` closing)
   
   b. **Generate Kiro hook fields**:
   - `enabled`: Set to `true` by default
   - `name`: Convert filename to uppercase (remove .md extension, replace hyphens with spaces)
   - `description`: Use the description from YAML frontmatter
   - `version`: Set to `"1"`
   - `when.type`: Set to `"userTriggered"`
   - `when.patterns`: Determine appropriate patterns based on workflow purpose:
     * For README/documentation workflows: `["**/*.md", "**/package.json", "src/**/*"]`
     * For Git automation: `["*"]` (all files)
     * For license workflows: `["**/package.json", "**/LICENSE*"]`
     * For spec analysis: `[".kiro/specs/**/*"]`
     * For project analysis: `["**/package.json", "**/tsconfig.json", "src/**/*"]`
     * Default fallback: `["*"]`
   - `then.type`: Set to `"askAgent"`
   - `then.prompt`: Use the entire markdown content as the prompt

   c. **Generate output filename**: Convert the workflow filename:
   - Remove `.md` extension
   - Convert to lowercase
   - Add `.kiro.hook` extension
   - Example: `AUTO-README-GENERATOR.md` → `auto-readme-generator.kiro.hook`

4. **Create the JSON file** with proper formatting and indentation (2 spaces).

5. **Pattern mapping logic**:
   ```
   Workflow Name Contains → Suggested Patterns
   - "README" or "DOC" → ["**/*.md", "**/package.json", "src/**/*"]
   - "GIT" or "PUSH" or "COMMIT" → ["*"]
   - "LICENSE" → ["**/package.json", "**/LICENSE*", "**/license*"]
   - "SPEC" or "KIRO" → [".kiro/specs/**/*"]
   - "PROJECT" or "ANALYZER" → ["**/package.json", "**/tsconfig.json", "src/**/*"]
   - "PITCH" or "DEVPOST" → ["**/package.json", "**/*.md", "src/**/*"]
   - Default → ["*"]
   ```

6. **Example conversion**:
   
   **Input (windsurf workflow):**
   ```markdown
   ---
   description: Automatically generates or updates the README.md file by analyzing the project structure
   ---
   Please analyze the project structure and generate a comprehensive README.md file...
   ```
   
   **Output (kiro hook):**
   ```json
   {
     "enabled": true,
     "name": "AUTO README GENERATOR",
     "description": "Automatically generates or updates the README.md file by analyzing the project structure",
     "version": "1",
     "when": {
       "type": "userTriggered",
       "patterns": ["**/*.md", "**/package.json", "src/**/*"]
     },
     "then": {
       "type": "askAgent",
       "prompt": "Please analyze the project structure and generate a comprehensive README.md file..."
     }
   }
   ```

7. **Validation**: After conversion, verify that each generated JSON file:
   - Is valid JSON
   - Contains all required fields
   - Follows the kiro-hooks-schema.txt specification

8. **Summary**: Provide a summary of:
   - Number of workflows converted
   - List of created .kiro.hook files
   - Any conversion warnings or issues

**Important Notes:**
- Preserve the exact prompt content from the markdown
- Use appropriate file patterns based on workflow purpose
- Follow JSON formatting standards with 2-space indentation
- Handle special characters in prompts properly (escape as needed)
- Maintain the semantic meaning of the original workflow
