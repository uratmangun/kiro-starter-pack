# Shell Preferences

## Terminal Execution Standards

### Fish Shell Requirement

**CRITICAL**: ALWAYS use fish shell for ANY terminal command execution. NEVER use bash shell under any circumstances.

#### Command Execution Rules

1. **Default Shell**: All terminal commands should be executed using fish shell syntax
2. **No Bash**: Never use bash-specific syntax or commands
3. **Fish Syntax**: Use fish shell syntax for:
   - Variable assignments: `set variable_name value`
   - Conditionals: `if condition; command; end`
   - Loops: `for item in list; command; end`
   - Functions: `function name; command; end`

#### Examples

**✅ Correct (Fish Shell)**:
```fish
set NODE_ENV production
npm run build
```

**❌ Incorrect (Bash)**:
```bash
export NODE_ENV=production
npm run build
```

#### Fish-Specific Features to Utilize

- **Autosuggestions**: Fish provides intelligent command completion
- **Syntax Highlighting**: Real-time syntax validation
- **Web-based Configuration**: Use `fish_config` for setup
- **Universal Variables**: Use `set -U` for persistent variables
- **Abbreviations**: Use `abbr` for command shortcuts

#### Migration from Bash

When converting bash commands to fish:
- Replace `export VAR=value` with `set -x VAR value`
- Replace `$VAR` with `$VAR` (same syntax)
- Replace `&&` with `; and`
- Replace `||` with `; or`
- Replace `source file` with `source file` (same syntax)

#### Environment Setup

Ensure fish shell is properly configured with:
- Path variables set correctly
- Aliases and abbreviations defined
- Custom functions for project-specific tasks
- Integration with development tools (Node.js, Python, etc.)

This rule ensures consistency across all terminal operations and takes advantage of fish shell's superior user experience and features.