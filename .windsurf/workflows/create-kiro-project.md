---
description: Creates a new Kiro project from the starter pack boilerplate template using GitHub CLI
---

You are a Kiro project generator that creates new projects from the official starter pack template.

## Prerequisites

Before running this workflow, ensure you have:
- GitHub CLI (`gh`) installed and authenticated
- Access to create public repositories on GitHub
- The `uratmangun/kiro-starter-pack` template is accessible

## Project Creation Process

1. **Choose Your Project Name**
   - Select a descriptive name for your project (lowercase, hyphens preferred)
   - Ensure the name doesn't conflict with existing repositories
   - Consider the project's purpose and scope

2. **Navigate to CascadeProjects Directory**
   ```bash
   cd /home/uratmangun/CascadeProjects
   ```

3. **Create Repository from Template**
   ```bash
   gh repo create <your-project-name> --template uratmangun/kiro-starter-pack --public --clone
   ```
   Replace `<your-project-name>` with your chosen project name.

4. **Navigate to Project Directory**
   ```bash
   cd <your-project-name>
   ```

5. **Verify Project Structure**
   Check that the following Kiro directories and files are present:
   - `.kiro/` directory with configuration files
   - `.windsurf/` directory with workflows and rules
   - `README.md` with project documentation
   - Basic project structure from the starter pack


## Post-Creation Steps

After creating your Kiro project:

1. **Update Project Documentation**
   - Modify README.md to reflect your project's purpose
   - Update any template placeholders with actual project information

2. **Configure Development Environment**
   - Install necessary dependencies
   - Set up environment variables if needed
   - Configure any project-specific tools

3. **Start Development**
   - Begin implementing your project features
   - Use Kiro specifications and workflows to guide development
   - Leverage the included Windsurf rules and workflows

## Example Usage

```bash
# Navigate to CascadeProjects directory
cd /home/uratmangun/CascadeProjects

# Create a new task management project
gh repo create my-task-manager --template uratmangun/kiro-starter-pack --public --clone

# Create a new web application
gh repo create awesome-web-app --template uratmangun/kiro-starter-pack --public --clone
```

## Troubleshooting

- **Authentication Issues**: Run `gh auth login` to authenticate with GitHub
- **Template Access**: Ensure the template repository is public and accessible
- **Naming Conflicts**: Choose a unique repository name or check existing repositories
- **Clone Failures**: Verify network connectivity and GitHub permissions