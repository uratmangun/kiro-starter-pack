---
description: Creates a simple blog post about the project by analyzing its structure, features, and purpose
---

This workflow analyzes your project and generates a simple blog post highlighting its key features, tech stack, and purpose.

// turbo-all

1. **Analyze project structure**: Examine the project files to understand the tech stack and architecture
```fish
find . -type f -name "package.json" -o -name "*.md" -o -name "*.py" -o -name "*.js" -o -name "*.ts" -o -name "*.jsx" -o -name "*.tsx" -o -name "*.html" -o -name "*.css" -o -name "*.go" -o -name "*.rs" -o -name "*.java" | head -20
```

2. **Read project README**: Extract project information from README if it exists
```fish
if test -f README.md
    echo "Found README.md - extracting project info"
    head -50 README.md
else
    echo "No README.md found - will generate blog post from project analysis"
end
```

3. **Check package.json for dependencies**: Identify the tech stack from package.json
```fish
if test -f package.json
    echo "=== Tech Stack Analysis ==="
    cat package.json | grep -E '"(react|vue|angular|svelte|next|nuxt|vite|webpack|tailwind|typescript|supabase|firebase|mongodb|postgres)"'
end
```

4. **Analyze project type**: Determine if it's a web app, API, CLI tool, etc.
```fish
echo "=== Project Type Analysis ==="
if test -f package.json
    echo "Frontend/Fullstack Project (Node.js based)"
else if test -f requirements.txt; or test -f pyproject.toml
    echo "Python Project"
else if test -f go.mod
    echo "Go Project"
else if test -f Cargo.toml
    echo "Rust Project"
else if test -f pom.xml; or test -f build.gradle
    echo "Java Project"
else
    echo "General Project"
end
```

5. **Create blog post**: Generate a simple blog post based on the analysis
```fish
set project_name (basename (pwd))
set current_date (date '+%Y-%m-%d')

echo "# Building $project_name: A Journey Through Code

*Published on $current_date*

## Introduction

Recently, I've been working on an exciting project called **$project_name**. In this blog post, I'll share what this project is about, the tech stack I chose, and some interesting challenges I encountered along the way.

## What is $project_name?

[Brief description based on README or project analysis - describe the project's purpose and main functionality]

## Tech Stack & Architecture

Based on my analysis of the project, here's the technology stack I'm using:

### Frontend/UI
- [List frontend technologies found]

### Backend/Database
- [List backend technologies found]

### Development Tools
- [List development and build tools]

## Key Features

The main features of $project_name include:

1. **Feature 1**: [Describe a key feature]
2. **Feature 2**: [Describe another feature]
3. **Feature 3**: [Describe additional functionality]

## Development Challenges & Solutions

During development, I encountered several interesting challenges:

### Challenge 1: [Technical Challenge]
**Problem**: [Describe the problem]
**Solution**: [Describe how you solved it]

### Challenge 2: [Architecture Decision]
**Problem**: [Describe the decision point]
**Solution**: [Explain your approach]

## What I Learned

Working on $project_name taught me several valuable lessons:

- **Technical Learning**: [What new technologies or concepts you learned]
- **Best Practices**: [Development practices you adopted]
- **Problem Solving**: [How you approached complex problems]

## Future Plans

Looking ahead, I'm planning to:

- [ ] Add new features like [feature ideas]
- [ ] Improve performance in [specific areas]
- [ ] Expand the project with [additional functionality]

## Getting Started

If you're interested in trying out $project_name, here's how to get started:

\`\`\`bash
# Clone the repository
git clone [repository-url]

# Install dependencies
[installation commands based on project type]

# Run the project
[run commands]
\`\`\`

## Conclusion

Building $project_name has been an incredible learning experience. The combination of [mention key technologies] proved to be powerful for [mention project goals].

I'm excited to continue developing this project and would love to hear your thoughts and feedback. Feel free to check out the code and let me know what you think!

---

*Have questions or suggestions? Feel free to reach out or contribute to the project!*

## Project Links

- 🔗 **Repository**: [Add your repository URL]
- 🚀 **Live Demo**: [Add demo URL if available]
- 📧 **Contact**: [Add your contact information]

---

*This blog post was generated using an automated workflow. The content has been customized based on the actual project structure and features.*" > BLOG_POST.md
```

6. **Add project-specific sections**: Enhance the blog post with actual project details
```fish
echo "

## Technical Deep Dive

### Project Structure
\`\`\`
$(find . -type f -name "*.js" -o -name "*.ts" -o -name "*.jsx" -o -name "*.tsx" -o -name "*.py" -o -name "*.go" -o -name "*.rs" | head -10 | sed 's|^\./||')
\`\`\`

### Key Dependencies
$(if test -f package.json; cat package.json | grep -A 10 '"dependencies"' | head -15; end)

### Development Workflow
The development process for this project involves:
1. Planning and design
2. Implementation with [tech stack]
3. Testing and debugging
4. Deployment and maintenance

" >> BLOG_POST.md
```

7. **Customize content placeholders**: Provide guidance for manual customization
```fish
echo "
---

## Customization Notes

This blog post template has been generated based on your project structure. 
To complete the blog post, please:

1. **Replace placeholders** in square brackets [like this] with actual content
2. **Add repository URL** and demo links
3. **Include screenshots** or code examples if desired
4. **Review and personalize** the technical sections
5. **Add specific examples** of challenges you faced
6. **Update the conclusion** with your personal thoughts

The blog post is saved as BLOG_POST.md in your project root.

## Publishing Options

Consider publishing this blog post on:
- Dev.to
- Medium
- Your personal blog
- LinkedIn articles
- GitHub Pages
- Hashnode

Remember to add relevant tags like your technology stack, project type, and development topics!
" >> BLOG_POST.md
```

8. **Final formatting**: Clean up the blog post formatting
```fish
echo "✅ Blog post generated successfully as BLOG_POST.md"
echo "📝 Please review and customize the content before publishing"
echo "🚀 Don't forget to add your repository URL and demo links"
```

## Usage Tips

1. **Run in your project directory**: This workflow analyzes your current project
2. **Customize the output**: Replace placeholder text with your specific details
3. **Add visuals**: Consider adding screenshots, diagrams, or code snippets
4. **Review before publishing**: Always review and personalize the generated content
5. **Add SEO**: Include relevant keywords and tags when publishing

The workflow creates a comprehensive blog post template that you can customize and publish on any blogging platform!
