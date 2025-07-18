---
description: Automatically generates or updates the README.md file by analyzing the project structure, files, and directories
---
Please analyze the project structure and generate a comprehensive README.md file that includes:

1. Project title and brief description (infer from package.json or context)
2. Installation instructions
3. Usage examples
4. Project structure overview
5. Key features
6. Technologies used (detect from file extensions and dependencies)
7. Configuration instructions (especially for Supabase if detected)
8. Contributing guidelines
9. License information (if available)

If a README.md already exists, please update it while preserving any custom sections that aren't directly related to the project structure. Format the README with proper Markdown syntax including headers, code blocks, and lists.

For Supabase projects, include specific sections about:
- Database schema overview
- Edge Functions (if present)
- Migration instructions
- Local development setup

The README should be professional, clear, and provide enough information for new developers to understand and work with the project.