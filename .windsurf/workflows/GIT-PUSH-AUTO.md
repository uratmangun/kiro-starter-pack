---
description: Automatically stages all changes, creates a commit with proper conventional commit format based on commit-messages.md guidelines, and pushes to remote repository
---
Please perform the following git operations in sequence:

1. Run `git add .` to stage all changes
2. Generate an appropriate commit message following the conventional commit format specified in .kiro/steering/commit-messages.md, including:
   - Appropriate emoji based on the type of changes
   - Conventional commit type (feat, fix, docs, etc.)
   - Scope if relevant
   - Clear, imperative description under 50 characters
   - Use the guidelines and examples from the commit-messages.md file
3. Run `git commit -m "[generated message]"` with the generated message
4. Run `git push` to push changes to remote

Analyze the staged changes to determine the most appropriate commit type and generate a meaningful commit message that follows the established guidelines.