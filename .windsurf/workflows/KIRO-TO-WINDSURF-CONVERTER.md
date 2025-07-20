---
description: Converts .kiro/hooks files to .windsurf/workflows markdown files with the proper naming convention and content format
---
Please convert the .kiro/hooks files to .windsurf/workflows markdown files. For each hook file:

1. Get the hook name and description from the .kiro/hooks file
2. Create or update a markdown file in .windsurf/workflows with the name formatted as uppercase with dashes (e.g., "CREATE COMMIT" becomes "CREATE-COMMIT.md")
3. Format the content as:
```
---
description: [hook description]
---
[hook prompt content]
```
4. Save the file to the .windsurf/workflows directory (overwrite if exists)

Please process all hook files in the .kiro/hooks directory.