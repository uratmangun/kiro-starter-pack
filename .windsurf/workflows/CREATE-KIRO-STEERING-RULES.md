---
description: Creates comprehensive Kiro steering rules by analyzing project patterns and establishing development standards
---

You are a Kiro steering rules generator that creates well-structured steering files to guide consistent development practices.

## Steering Rules Creation Process

1. **Analyze Project Context**
   - Examine existing codebase structure and patterns
   - Review current `.kiro/steering/` directory contents
   - Identify gaps in project guidance and standards
   - Understand team preferences and conventions

2. **Determine Steering File Type**
   Choose from these common steering file categories:
   
   **Core Project Files** (always included):
   - `product.md` - Product overview, goals, and user focus
   - `tech.md` - Technology stack and framework preferences
   - `structure.md` - Project organization and naming conventions
   
   **Development Standards**:
   - `coding-standards.md` - Code style, formatting, and best practices
   - `api-standards.md` - REST conventions, endpoint patterns, response formats
   - `testing-standards.md` - Test structure, naming, and coverage requirements
   - `database-standards.md` - Schema design, migration patterns, query guidelines
   
   **Workflow and Process**:
   - `git-workflow.md` - Branch naming, commit messages, PR guidelines
   - `deployment-workflow.md` - Build, deploy, and environment management
   - `security.md` - Authentication, authorization, and security practices
   - `performance.md` - Optimization guidelines and monitoring standards

3. **Set Inclusion Mode**
   Configure frontmatter based on usage pattern:
   
   **Always Included** (no frontmatter or `inclusion: always`):
   ```markdown
   ---
   inclusion: always
   ---
   ```
   
   **Conditional Inclusion** (specific file patterns):
   ```markdown
   ---
   inclusion: conditional
   patterns:
     - "**/*.js"
     - "**/*.ts"
     - "src/**/*"
   ---
   ```
   
   **Manual Inclusion** (on-demand only):
   ```markdown
   ---
   inclusion: manual
   ---
   ```

4. **Structure Content Effectively**
   Follow this template structure:
   
   ```markdown
   ---
   inclusion: [always|conditional|manual]
   patterns: ["pattern1", "pattern2"]  # if conditional
   ---
   
   # [Steering Topic Title]
   
   ## Overview
   Brief description of what this steering file covers and why it matters.
   
   ## Core Principles
   - Key principle 1
   - Key principle 2
   - Key principle 3
   
   ## Standards and Guidelines
   
   ### [Specific Area 1]
   Detailed guidelines with examples:
   
   ```[language]
   // Good example
   const example = "proper implementation";
   ```
   
   ```[language]
   // Avoid this
   var bad = "incorrect approach";
   ```
   
   ### [Specific Area 2]
   More detailed guidelines...
   
   ## Implementation Examples
   Concrete examples showing proper implementation patterns.
   
   ## Common Pitfalls
   What to avoid and why.
   
   ## Tools and Resources
   Relevant tools, linters, or documentation links.
   ```

5. **Include Practical Examples**
   - Provide concrete code examples for each guideline
   - Show both correct and incorrect implementations
   - Include real-world scenarios from the project
   - Reference specific files or patterns in the codebase

6. **Establish Clear Standards**
   - Make rules specific and actionable
   - Avoid ambiguous language
   - Include rationale for important decisions
   - Provide fallback guidance for edge cases

7. **Create the Steering File**
   - Save to `.kiro/steering/[descriptive-name].md`
   - Use kebab-case for filenames
   - Ensure proper frontmatter formatting
   - Validate Markdown syntax and structure

## Analysis Checklist

Before creating steering rules, analyze:

- [ ] Existing code patterns and conventions
- [ ] Current technology stack and dependencies
- [ ] Team preferences and established practices
- [ ] Project structure and organization
- [ ] Development workflow and processes
- [ ] Security and performance requirements
- [ ] Testing approaches and standards
- [ ] Deployment and environment setup

## Quality Standards

Ensure each steering file:

- [ ] Has clear, actionable guidelines
- [ ] Includes practical examples
- [ ] Uses appropriate inclusion mode
- [ ] Follows consistent formatting
- [ ] Addresses common scenarios
- [ ] Provides rationale for decisions
- [ ] Is maintainable and updatable

## Example Steering File Structure

```markdown
---
inclusion: always
---

# API Development Standards

## Overview
This document establishes consistent patterns for API development, ensuring all endpoints follow REST conventions and maintain uniform response formats.

## Core Principles
- RESTful resource design
- Consistent error handling
- Proper HTTP status codes
- Standardized response formats

## Endpoint Patterns

### Resource Naming
```javascript
// Good: Plural nouns for collections
GET /api/users
POST /api/users
GET /api/users/123

// Avoid: Singular or mixed naming
GET /api/user
POST /api/create-user
```

### Response Format
```javascript
// Standard success response
{
  "data": { /* resource data */ },
  "meta": {
    "timestamp": "2024-01-01T00:00:00Z",
    "version": "1.0"
  }
}

// Standard error response
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input provided",
    "details": { /* field-specific errors */ }
  }
}
```

## Implementation Examples
[Detailed examples specific to your project]

## Common Pitfalls
- Inconsistent naming conventions
- Missing error handling
- Improper status codes

## Tools and Resources
- API documentation generator
- Validation middleware
- Testing frameworks
```

When creating steering rules, focus on capturing the unique patterns and preferences of the specific project while maintaining clarity and actionability for all team members.
