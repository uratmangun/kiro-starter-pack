# Best Practices - Kiro Specs Documentation

## How do I import existing requirements?

If your requirements or designs already exist in another system (such as JIRA, Confluence, or Word documents), you have two options:

1. **Using MCP integration**: If your requirements tool has an MCP server that supports STDIO, you can connect directly to import requirements into your spec session.

2. **Manual import**: Simply copy your existing requirements (e.g. `foo-prfaq.md`) into a new file in your repo and open a spec chat session and say `#foo-prfaq.md Generate a spec from it`. Kiro will read your requirements, and generate requirement and design specs.

## How do I iterate on my specs?

Kiro's specifications are designed for continuous refinement, allowing you to update and enhance them as your project evolves. This iterative approach ensures that specifications remain synchronized with changing requirements and technical designs, providing a reliable foundation for development.

1. **Update Requirements**: Either modify the `requirements.md` file directly or initiate a spec session and instruct Kiro to add new requirements or design elements.

2. **Update Design**: Navigate to the `design.md` file for your spec and select **Refine**. This action will update both the design documentation and the implementation tasks to reflect your changes.

3. **Update Tasks**: As you complete tasks or identify new ones, you can update the `tasks.md` file directly or use the spec session to add, modify, or remove tasks as needed.

## How do I share specs with my team?

Kiro specifications are stored as markdown files in your repository, making them easily shareable and version-controlled alongside your code. Team members can:

- **View specs directly**: Open the markdown files in any text editor or markdown viewer
- **Collaborate on specs**: Use your existing version control workflow to review and merge spec changes
- **Start spec sessions**: Any team member can initiate a spec session to continue working on the specification
- **Track progress**: Monitor task completion and implementation status through the `tasks.md` file

## Can I share specs across multiple teams?

Yes, Kiro specs can be shared across multiple teams and repositories. You can:

- **Reference external specs**: Link to specifications in other repositories or documentation systems
- **Copy spec templates**: Use successful spec structures as templates for new projects
- **Maintain shared libraries**: Create common design patterns and requirements that can be referenced across projects
- **Cross-team collaboration**: Multiple teams can contribute to the same specification through standard version control practices

## Can I start a spec session from a vibe session?

Yes, you can seamlessly transition from a vibe session to a spec session. When you're in a vibe session and ready to formalize your ideas into structured specifications, simply:

1. Use the command to start a spec session
2. Reference the vibe session context or specific messages
3. Kiro will help transform your exploratory conversation into structured requirements, design, and tasks

This workflow allows you to move fluidly between brainstorming and formal specification development.

## Can I execute all the tasks in my spec in a single shot?

While Kiro provides task tracking and can assist with implementation, executing all tasks in a single operation depends on:

- **Task complexity**: Simple, well-defined tasks may be automatable
- **Dependencies**: Tasks with external dependencies or manual steps require human intervention
- **Code review requirements**: Most development workflows require review processes
- **Testing needs**: Implementation typically requires testing and validation steps

Kiro can help automate portions of the implementation, but complex features usually benefit from iterative development and review.

## What if some tasks are already implemented?

Kiro's task tracking system allows you to mark tasks as completed, providing flexibility for projects where implementation has already begun:

- **Mark completed tasks**: Update the status of implemented tasks in your `tasks.md` file
- **Sync with reality**: Ensure your spec reflects the current state of implementation
- **Focus on remaining work**: Use the spec to track and plan remaining tasks
- **Maintain documentation**: Keep the spec updated as a record of what was built and why

## How many specs can I have in a single repo?

There's no hard limit on the number of specs per repository. The recommended approach is to organize specs by feature or functional area:

```
.kiro/specs/
├── user-authentication/     # Login, registration, password reset
├── payment-processing/      # Billing, subscriptions, invoicing
├── notification-system/     # Email, push, in-app notifications
└── admin-dashboard/         # Product management, user analytics
```

This approach allows you to:

- Work on features independently without conflicts
- Maintain focused, manageable spec documents
- Iterate on specific functionality without affecting other areas
- Collaborate with team members on different features simultaneously

---

*Source: [Kiro Documentation - Specs Best Practices](https://kiro.dev/docs/specs/best-practices/)*
*Page updated: July 14, 2025*
