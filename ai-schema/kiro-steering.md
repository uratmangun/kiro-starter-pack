# Steering - Kiro Documentation

## What is Steering?

Steering gives Kiro persistent knowledge about your project through markdown files in `.kiro/steering/`. Instead of explaining your conventions in every chat, steering files ensure Kiro consistently follows your established patterns, libraries, and standards.

## Key Benefits

**Consistent Code Generation** - Every component, API endpoint, or test follows your team's established patterns and conventions.

**Reduced Repetition** - No need to explain project standards in each conversation. Kiro remembers your preferences.

**Team Alignment** - All developers work with the same standards, whether they're new to the project or seasoned contributors.

**Scalable Project Knowledge** - Documentation that grows with your codebase, capturing decisions and patterns as your project evolves.

## Default Steering Files

Kiro automatically creates three foundational files that establish core project context:

**Product Overview** (`product.md`) - Defines your product's purpose, target users, key features, and business objectives. This helps Kiro understand the "why" behind technical decisions and suggest solutions aligned with your product goals.

**Technology Stack** (`tech.md`) - Documents your chosen frameworks, libraries, development tools, and technical constraints. When Kiro suggests implementations, it will prefer your established stack over alternatives.

**Project Structure** (`structure.md`) - Maps your codebase organization, naming conventions, file placement rules, and architectural patterns. This ensures new code follows your existing project layout.

## Creating Custom Steering Files

Beyond the default files, you can create specialized steering files for specific aspects of your project. Each file should focus on a particular domain or concern, making them easier to maintain and more targeted in their guidance.

## Inclusion Modes

Steering files support three inclusion modes that control when and how Kiro accesses their content:

## Always Included (Default)

Files without frontmatter are automatically included in every Kiro interaction. This is ideal for core project knowledge that should always be available.

```markdown
# API Standards

All API endpoints must follow REST conventions...
```

## Conditional Inclusion

Use frontmatter to specify when files should be included based on file patterns or project context:

```markdown
---
include_when:
  - "**/*.test.js"
  - "**/*.spec.ts"
---

# Testing Standards

All tests must follow these patterns...
```

## Manual Inclusion

Files marked as manual inclusion are only loaded when explicitly referenced:

```markdown
---
include: manual
---

# Database Migration Guide

Step-by-step process for database changes...
```

## File References

Reference other steering files or project files to create interconnected documentation:

```markdown
# Component Guidelines

See also: [API Standards](api-standards.md)

For examples, check: [Button Component](../src/components/Button.tsx)
```

## Best Practices

### Keep Files Focused
Each steering file should address a specific concern or domain. This makes them easier to maintain and more effective at guiding Kiro's behavior.

### Use Clear Examples
Include concrete code examples that demonstrate your preferred patterns. Kiro learns better from examples than abstract descriptions.

### Update Regularly
Steering files should evolve with your project. When you establish new patterns or change existing ones, update the relevant steering files.

### Leverage Conditional Inclusion
Use conditional inclusion to provide context-specific guidance. This keeps irrelevant information from cluttering Kiro's context while ensuring relevant knowledge is available when needed.

## Common Steering File Strategies

**Component Patterns** (`components.md`) - Document your component architecture, prop patterns, styling approaches, and reusability guidelines. Include examples of well-structured components and common patterns to follow.

**API Design** (`api-design.md`) - Establish REST conventions, error handling patterns, authentication approaches, and response formats. Include examples of well-designed endpoints and common API patterns.

**Database Schema** (`database.md`) - Document table relationships, naming conventions, migration patterns, and data modeling approaches. Include schema examples and relationship patterns.

**Testing Strategy** (`testing.md`) - Define testing approaches, mock patterns, assertion styles, and coverage expectations. Include examples of well-written tests and testing utilities.

**Code Style** (`style.md`) - Establish formatting rules, naming conventions, file organization, and code structure preferences. Include examples of well-formatted code and style guidelines.

**Security Guidelines** (`security.md`) - Document authentication patterns, authorization requirements, data validation rules, input sanitization standards, and vulnerability prevention measures. Include secure coding practices specific to your application.

**Deployment Process** (`deployment-workflow.md`) - Outline build procedures, environment configurations, deployment steps, and rollback strategies. Include CI/CD pipeline details and environment-specific requirements.

Custom steering files are stored in `.kiro/steering/` and become immediately available across all Kiro interactions.

---

*Source: [Kiro Documentation - Steering](https://kiro.dev/docs/steering/)*
*Page updated: July 14, 2025*
