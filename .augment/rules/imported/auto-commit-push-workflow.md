---
type: "always_apply"
---

# Auto Commit and Push Workflow

## Overview

**MANDATORY**: When performing automatic Git operations, follow this standardized workflow for staging changes, generating conventional commit messages with emojis, and pushing to remote.

### Workflow Steps

1. **Status Check**: Run `git status` to see what files have been modified
2. **Stage Changes**: Use `git add .` to include all modified files
3. **Analyze Changes**: Use `git status --porcelain` to get a clean list of modified files, then read the content of modified files to understand what has been changed
4. **Generate Commit Message**: Create a conventional commit message with appropriate emoji
5. **Commit**: Execute `git commit -m "your message here"`
6. **Push**: Execute `git push` to remote repository
7. **Report**: Provide a summary of operations performed

### Commit Message Format

```
<emoji> <type>(<scope>): <description>
[optional body]
[optional footer(s)]
```

### Types and Emojis

- ✨ feat: A new feature
- 🔧 fix: A bug fix
- 📚 docs: Documentation only changes
- 💎 style: Changes that do not affect the meaning of the code
- ♻️ refactor: A code change that neither fixes a bug nor adds a feature
- ⚡ perf: A code change that improves performance
- ✅ test: Adding missing tests or correcting existing tests
- 📦 build: Changes that affect the build system or external dependencies
- ⚙️ ci: Changes to CI configuration files and scripts
- 🔨 chore: Other changes that don't modify src or test files
- ⏪ revert: Reverts a previous commit

### Commit Message Rules

1. Use lowercase for type and description
2. Keep the description under 50 characters when possible
3. Use imperative mood ("add" not "added" or "adds")
4. Include scope when relevant (component, module, or area affected)
5. Always start with the appropriate emoji
6. No period at the end of the description
7. Use body for additional context if needed (separate with blank line)

### Breaking Changes

For breaking changes, add `!` after the type/scope and include `BREAKING CHANGE:` in the footer.

### Example Usage

```bash
git status
git add .
git status --porcelain
git commit -m "✨ feat(auth): add user authentication system"
git push
```

This ensures consistent, descriptive commit messages that follow conventional commit standards while maintaining clear project history.
