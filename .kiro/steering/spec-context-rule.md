# Spec Context Rule

## Always Read Spec Files Before Starting Work

When working on any feature or task that has an associated spec in `.kiro/specs/`, always read the complete spec documentation first to understand the current state and context.

### Required Reading Order

1. **Requirements Document** (`requirements.md`) - Understand what needs to be built
2. **Design Document** (`design.md`) - Understand the technical approach and architecture
3. **Tasks Document** (`tasks.md`) - Understand what has been completed and what remains

### When to Apply This Rule

- **Before implementing any task** from a spec
- **Before making changes** to existing functionality covered by a spec
- **Before answering questions** about features that have specs
- **Before creating new functionality** that might relate to existing specs

### Benefits

- **Full Context**: Understand the complete feature scope and requirements
- **Avoid Duplication**: Know what's already been implemented
- **Maintain Consistency**: Ensure new work aligns with existing design decisions
- **Reference Requirements**: Validate implementations against acceptance criteria
- **Track Progress**: Understand what tasks are complete vs. remaining

### Implementation

Always start work sessions by reading the relevant spec files:

```fish
# Read all spec files for a feature
cat .kiro/specs/[feature-name]/requirements.md
cat .kiro/specs/[feature-name]/design.md  
cat .kiro/specs/[feature-name]/tasks.md
```

### Exception

Only skip reading specs if:
- The work is completely unrelated to any existing specs
- You are creating a brand new spec from scratch
- The user explicitly asks you to work without spec context

This rule ensures comprehensive understanding before any implementation work begins.