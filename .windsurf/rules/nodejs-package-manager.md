---
name: "Node.js Package Manager Standards"
trigger: always_on
description: "Enforces use of bun or pnpm for Node.js dependency management, prohibits npm and yarn"
---

# Node.js Package Manager Standards

## Required Package Managers

**MANDATORY**: Use either `bun` or `pnpm` for all Node.js dependency management. Never use `npm` or `yarn`.

### Preferred Order
1. **bun** - Fastest performance, built-in bundler
2. **pnpm** - Efficient disk usage, strict dependency resolution

### Installation Commands

```bash
# Using bun
bun install
bun add <package>
bun remove <package>
bun run <script>

# Using pnpm  
pnpm install
pnpm add <package>
pnpm remove <package>
pnpm run <script>
```

### Project Detection

- If `bun.lock` exists, use `bun`
- If `pnpm-lock.yaml` exists, use `pnpm`
- If both exist, prefer `bun`
- Never generate `package-lock.json` or `yarn.lock`

### Script Execution

Always use the detected package manager for running scripts:
- `bun dev` instead of `npm run dev`
- `pnpm build` instead of `npm run build`

This ensures consistent dependency resolution and optimal performance across the project.