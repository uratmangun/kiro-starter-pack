---
description: Converts .kiro/hooks files to .windsurf/workflows markdown files with the proper naming convention and content format
---
Please convert all .kiro/hooks files to .windsurf/workflows markdown files. Follow these steps:

1. First, remove all existing files inside /home/uratmangun/CascadeProjects/kiro-starter-pack/.windsurf/workflows
2. Then, for each hook file in /home/uratmangun/CascadeProjects/kiro-starter-pack/.kiro/hooks:
   a. Get the hook name and description from the .kiro/hooks file
   b. Create a markdown file in .windsurf/workflows with the name formatted as lowercase with dashes (e.g., "CREATE COMMIT" becomes "create-commit.md")
   c. Format the content as:
```
---
description: [hook description]
---
[hook prompt content]
```
   d. Save the file to the .windsurf/workflows directory

3. Process all hook files in the .kiro/hooks directory one by one

Ensure all existing workflow files are cleared before starting the conversion process.