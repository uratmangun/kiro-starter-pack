---
description: Creates a simple blog post about the project by analyzing its structure, features, and purpose
---

This workflow analyzes your project and generates a simple blog post highlighting its key features, tech stack, purpose, and development methodology using Kiro specifications.

1. **Analyze project structure**: Examine the project files to understand the tech stack and architecture by finding key files like package.json, README.md, and source code files.

2. **Read project README**: Extract project information from README if it exists, otherwise generate blog post from project analysis.

3. **Check package.json for dependencies**: Identify the tech stack from package.json by looking for popular frameworks and libraries like react, vue, angular, svelte, next, nuxt, vite, webpack, tailwind, typescript, supabase, firebase, mongodb, postgres.

4. **Analyze Kiro specifications**: Examine the .kiro/specs directory to understand the development methodology:
   - List all specification directories
   - Read requirements.md, design.md, and tasks.md files from each spec
   - Analyze how spec-driven development was used in the project
   - Document the development workflow and planning approach

5. **Analyze project type**: Determine if it's a web app, API, CLI tool, etc. based on file structure and dependencies.

6. **Create demo content**: Prepare repository embedding format for all projects:
   - Get repository URL from GitHub CLI or git remote
   - Use repository embedding format: `{% embed repository_url %}`

7. **Create blog post**: Generate a comprehensive blog post with the following structure:

# [PROJECT_NAME]

## Introduction
Brief introduction about the project and its purpose.

## What is [PROJECT_NAME]?
Description based on README or project analysis - describe the project's purpose and main functionality.

## Tech Stack & Architecture
List of technologies found in the project:
- Frontend/UI technologies
- Backend/Database technologies  
- Development Tools

## Development Methodology: Kiro Specifications
This project follows spec-driven development using Kiro specifications:
- **Requirements**: User stories and acceptance criteria for each feature
- **Design**: Technical architecture and implementation approach
- **Tasks**: Discrete, trackable implementation steps

### Specifications Created:
[List all specs found in .kiro/specs with brief descriptions]

## Key Features
1. **Feature 1**: Describe a key feature
2. **Feature 2**: Describe another feature
3. **Feature 3**: Describe additional functionality

## Demo
{% embed https://github.com/[username]/[repo-name] %}

## Getting Started
Installation and setup instructions based on project type.

## Conclusion
Summary of the development experience and key takeaways.

## Technical Deep Dive
### Project Structure
List key source files and their purposes.

### Key Dependencies
List main dependencies from package.json.

### Development Workflow
Describe the development process.

8. **Save the blog post** as BLOG.md in the PITCH folder.

The blog post should be comprehensive, professional, and ready for customization and publishing.

## Enhanced Workflow Steps:

### Kiro Specs Analysis Process:
1. List all directories in .kiro/specs/
2. For each spec directory, read the three core files:
   - requirements.md: Extract user stories and acceptance criteria
   - design.md: Document technical approach and architecture decisions
   - tasks.md: List implementation tasks and their completion status
3. Summarize the spec-driven development approach used
4. Highlight how specifications guided the development process

### Demo Creation Process:
1. **Get repository URL**:
   - Use `gh repo view --json url -q .url` to get the repository URL
   - If GitHub CLI is not available, extract repository URL from git remote: `git remote get-url origin`
   - Use repository embedding format for all projects: `{% embed repository_url %}`

### Blog Post Enhancement:
- Include a dedicated section about the Kiro specification methodology
- List all specifications created with brief descriptions of their purpose
- Add repository embedding for demo content
- Emphasize the spec-driven development workflow as a key project feature