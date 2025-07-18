---
inclusion: manual
---

# Commit Message Guidelines

When generating commit messages, always follow the conventional commit format with appropriate emojis:

## Format
```
<emoji> <type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

## Types and Emojis
- ✨ `feat`: A new feature
- 🔧 `fix`: A bug fix
- 📚 `docs`: Documentation only changes
- 💎 `style`: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- ♻️ `refactor`: A code change that neither fixes a bug nor adds a feature
- ⚡ `perf`: A code change that improves performance
- ✅ `test`: Adding missing tests or correcting existing tests
- 📦 `build`: Changes that affect the build system or external dependencies
- ⚙️ `ci`: Changes to CI configuration files and scripts
- 🔨 `chore`: Other changes that don't modify src or test files
- ⏪ `revert`: Reverts a previous commit

## Examples
- ✨ feat(auth): add OAuth2 login functionality
- 🔧 fix(api): resolve null pointer exception in user service
- 📚 docs(readme): update installation instructions
- ♻️ refactor(utils): simplify date formatting helper
- ✅ test(auth): add unit tests for login validation
- 📦 build(deps): upgrade React to v18.2.0

## Rules
1. Use lowercase for type and description
2. Keep the description under 50 characters when possible
3. Use imperative mood ("add" not "added" or "adds")
4. Include scope when relevant (component, module, or area affected)
5. Always start with the appropriate emoji
6. No period at the end of the description
7. Use body for additional context if needed (separate with blank line)

## Breaking Changes
For breaking changes, add `!` after the type/scope and include `BREAKING CHANGE:` in the footer:
```
💥 feat(api)!: remove deprecated user endpoints

BREAKING CHANGE: The /api/v1/users endpoint has been removed. Use /api/v2/users instead.
```