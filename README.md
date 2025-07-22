# 🚀 Kiro & Windsurf Starter Pack

A comprehensive starter template that combines the power of **Kiro** (AI-powered development workflows) and **Windsurf** (advanced AI coding assistant) to supercharge your development experience.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![AI-Powered](https://img.shields.io/badge/AI-Powered-blue.svg)](https://github.com/topics/artificial-intelligence)
[![Automation](https://img.shields.io/badge/Automation-Ready-green.svg)](https://github.com/topics/automation)

## 🚀 Quick Start

### Clone as Template with GitHub CLI

Create a new project using this template with a custom name:

```fish
# Clone this repository as a template with your project name
gh repo create your-project-name --template uratmangun/kiro-starter-pack --public --clone

# Navigate to your new project
cd your-project-name
```

Or for a private repository:

```fish
gh repo create your-project-name --template uratmangun/kiro-starter-pack --private --clone
cd your-project-name
```

## 🎯 What This Template Provides

This starter pack sets up your project with pre-configured automation, workflows, and development standards that work seamlessly with both Kiro and Windsurf.

### 🤖 Kiro Integration
**Kiro** is an AI-powered development companion that automates repetitive tasks and maintains project standards through intelligent hooks and steering configurations.

### 🌊 Windsurf Integration  
**Windsurf** is Codeium's revolutionary agentic AI coding assistant that operates on the AI Flow paradigm, enabling both independent work and collaborative pair programming.

## 📦 What's Included

### 🔗 Kiro Hooks (`.kiro/hooks/`)
Automated workflows that trigger based on project changes:

- **📝 Auto README Generator** - Automatically updates README.md based on project structure
- **🎯 AKINDO Pitch Generator** - Creates comprehensive project pitch documents
- **📊 DevPost Pitch Creator** - Generates DevPost submission content
- **📚 Kiro Usage Documentation** - Documents how Kiro was used in the project
- **⚖️ OSI License Creator** - Automatically creates OSI-compliant licenses
- **🔄 Auto Git Commit** - Automated conventional commits with proper formatting
- **🔍 Project Analysis Tools** - Various hooks for analyzing project structure and workflows

### 🛠️ Windsurf Workflows (`.windsurf/workflows/`)
Pre-built workflows accessible via slash commands:

- `/AUTO-README-GENERATOR` - Automatically generates or updates README.md files by analyzing project structure
- `/CREATE-AKINDO-PITCH` - Monitors project files and automatically generates comprehensive AKINDO pitch documents
- `/CREATE-DEVPOST-PITCH` - Monitors changes and generates DEVPOST.md with inspiration, tech stack, and project details
- `/CREATE-KIRO-USAGE-AUTO` - Automatically creates or updates HOW_KIRO_WAS_USED.md documentation when .kiro files are modified
- `/CREATE-OSI-LICENSE-AUTO` - Automatically creates or updates OSI-compliant license files when project config changes
- `/CREATE-PROJECT-FROM-KIRO-STARTER-PACK` - Automatically creates new projects using the kiro-starter-pack GitHub template
- `/GIT-PUSH-AUTO` - Automatically stages changes, generates conventional commit messages with emojis, and pushes to remote
- `/KIRO-TO-WINDSURF-CONVERTER` - Converts .kiro/hooks files to .windsurf/workflows markdown files with proper formatting
- `/QUESTION-KIRO-HOOKS` - Analyzes all files in .kiro/hooks directory and creates workflow summaries
- `/QUESTION-KIRO-SPECS` - Analyzes spec structure in .kiro/specs and updates PITCH/SPECS.txt with insights
- `/QUESTION-KIRO-VIBE` - Creates responses about project conversation patterns and code generation examples
- `/WINDSURF-TO-KIRO-CONVERTER` - Converts Windsurf workflow markdown files to Kiro hooks JSON format

### 📋 AI Schema Documentation (`ai-schema/`)
Schema definitions and specifications for automation systems:

- **`kiro-hooks-schema.txt`** - Complete schema specification for Kiro hooks JSON configuration files, including structure, triggers, and automation patterns
- **`windsurf-workflow-schema.txt`** - Schema specification for Windsurf workflow markdown files, covering YAML frontmatter and instruction formatting

These schema files serve as reference documentation for creating and converting between Kiro hooks and Windsurf workflows, ensuring consistent automation patterns across projects.

### ⚙️ Development Standards (`.kiro/steering/`)
Predefined configurations for consistent development:

- **🐚 Shell Preferences** - Fish shell configuration and standards
- **💬 Commit Message Standards** - Conventional commit formats with emojis
- **📋 Spec Context Rules** - Spec-driven development guidelines
- **🗄️ Supabase Configurations** - Database and function deployment standards

## 🚀 Getting Started

### 1. Use This Template
Click the **"Use this template"** button on GitHub to create a new repository with all configurations pre-installed.

### 2. Clone Your New Repository
```bash
git clone https://github.com/yourusername/your-new-project.git
cd your-new-project
```

### 3. Start Development
- **With Kiro**: The hooks will automatically trigger based on your development activities
- **With Windsurf**: Use the `/` slash commands to access pre-built workflows
- **Combined**: Enjoy seamless automation and AI-assisted development

## ✨ Key Features

- **🔄 Automated Documentation** - README, licenses, and project documentation stay up-to-date
- **📝 Conventional Commits** - Standardized commit messages with emojis
- **🎯 Project Pitching** - Automated creation of pitch documents for competitions and showcases
- **🐚 Fish Shell Optimized** - All configurations use Fish shell for better development experience
- **🗄️ Supabase Ready** - Pre-configured for Supabase development workflows
- **📊 Spec-Driven Development** - Built-in support for specification-based development

## 🛠️ Development Standards

This template enforces several development best practices:

### Shell & Terminal
- **Fish Shell Required** - All commands use Fish shell syntax
- **PNPM for Node.js** - Uses pnpm instead of npm for package management
- **Conventional Commits** - Standardized commit format with appropriate emojis

### Project Structure
- **Spec-First Development** - Always read specs before implementation
- **Automated Quality Checks** - Hooks ensure consistency and quality
- **Template Reusability** - Designed to be cloned and reused across projects

## 🤝 Contributing

This template is designed to evolve with the community:

1. Fork the repository
2. Make your improvements
3. Submit a pull request
4. Help others by sharing your enhancements

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Kiro Team** - For creating powerful AI development automation
- **Windsurf/Codeium Team** - For revolutionizing AI-assisted coding
- **Community Contributors** - For continuously improving this template

---

**Ready to supercharge your development workflow?** Start building with the combined power of Kiro and Windsurf! 🚀
