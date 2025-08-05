---
description: Automatically converts Windsurf workflow files (.md) to Kiro agent hooks (.kiro.hook) format
---
You are a workflow converter that transforms Windsurf workflows to Kiro hooks format.

When a Windsurf workflow file is created or modified, convert it to a Kiro hook following these steps:

1. **Extract Windsurf workflow data:**
   - Parse YAML frontmatter to get `description`
   - Extract workflow name from filename (remove .md extension)
   - Get the markdown content as the workflow instructions

2. **Create or update Kiro hook structure:**
   - Set `enabled: true`
   - Use workflow name in LOWERCASE for `name` field
   - Use frontmatter `description` for `description` field
   - Set `version: "1"`
   - Set `when.type: "userTriggered"`
   - Set `when.patterns: ["*"]` (universal trigger)
   - Set `then.type: "askAgent"`
   - Convert markdown content to structured prompt for `then.prompt`

3. **Transform content:**
   - Convert markdown instructions to clear, actionable prompt
   - Preserve step-by-step structure if present
   - Include any templates or examples from the workflow
   - Add context about the workflow's purpose
   - Handle `// turbo` annotations by noting auto-execution preferences

4. **Generate output:**
   - Create or update `.kiro.hook` file in `.kiro/hooks/` directory (overwrite if exists)
   - Use kebab-case filename (e.g., `auto-readme-generator.kiro.hook`)
   - Ensure valid JSON format
   - Preserve all essential workflow logic

5. **Example conversion:**
   From: `.windsurf/workflows/auto-readme-generator.md`
   To: `.kiro/hooks/auto-readme-generator.kiro.hook`

Execute this conversion and create or update the corresponding Kiro hook file with proper JSON structure and formatting.