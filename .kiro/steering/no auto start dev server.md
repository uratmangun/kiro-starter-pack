---
inclusion: always
---

# Development Server Manual Start Policy

## Server Startup Behavior

**MANDATORY**: Never automatically start development servers for web applications. Always let the user start them manually.

### Prohibited Actions

- Do not run `npm start`, `bun dev`, `pnpm dev`, or similar commands automatically
- Do not execute `yarn start`, `npm run dev`, or framework-specific dev commands
- Do not start servers for React, Vue, Angular, Next.js, Vite, or other web frameworks
- Do not automatically run `serve`, `http-server`, or local server commands

### Permitted Actions

- Suggest the appropriate command to start the server
- Provide instructions on how to start the development server
- Offer to create or update start scripts in package.json
- Help configure server settings and environment variables

### Framework-Specific Examples

**React/Create React App:**
```bash
# Don't auto-run: npm start
# Instead suggest: "Run 'npm start' to start the development server"
```

**Next.js:**
```bash
# Don't auto-run: bun dev
# Instead suggest: "Run 'bun dev' to start the Next.js development server"
```

**Vite:**
```bash
# Don't auto-run: pnpm dev
# Instead suggest: "Run 'pnpm dev' to start the Vite development server"
```

### Exception Handling

- Build commands (`npm run build`, `bun build`) are allowed
- Test commands (`npm test`, `bun test`) are allowed
- Production server commands may be suggested but not auto-executed

This ensures the user maintains control over when and how development servers are started, preventing unwanted resource usage and allowing proper development workflow management.
