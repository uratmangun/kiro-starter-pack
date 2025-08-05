---
description: Creates a comprehensive Kiro specification with requirements, design, and tasks following Kiro best practices
---

# Create Kiro Specification Workflow

This workflow guides you through creating a complete Kiro specification following the three-file structure: requirements.md, design.md, and tasks.md.

## Step 1: Analyze Project Context

First, understand the current project structure and existing specifications:

1. List existing specs in `.kiro/specs/` directory
2. Review any existing requirements documents or PRFAQs
3. Identify the feature or component that needs specification
4. Determine the scope and boundaries of the specification

## Step 2: Create Spec Directory Structure

Create the specification directory structure:

```fish
# Create the spec directory (replace 'feature-name' with your actual feature)
mkdir -p .kiro/specs/[FEATURE-NAME]
```

## Step 3: Generate Requirements Document

Create `requirements.md` using structured EARS notation:

1. **Introduction Section**: Provide context and overview of the feature
2. **User Stories**: Write requirements in the format:
   - "As a [user type], I want [goal], so that [benefit]"
3. **Acceptance Criteria**: Use EARS format:
   - "WHEN [condition] THEN the system SHALL [expected behavior]"
4. **Non-functional Requirements**: Include performance, security, and usability requirements

Template structure:
```markdown
# Requirements Document

## Introduction
[Brief overview of the feature and its purpose]

## Requirements

### Requirement 1
**User Story:** As a [user], I want [goal], so that [benefit].

#### Acceptance Criteria
1. WHEN [condition] THEN the system SHALL [behavior]
2. WHEN [condition] THEN the system SHALL [behavior]

### Requirement 2
[Continue with additional requirements...]

## Non-functional Requirements
- Performance: [specific performance criteria]
- Security: [security requirements]
- Usability: [usability standards]
```

## Step 4: Create Design Document

Create `design.md` with technical architecture and implementation approach:

1. **System Architecture**: High-level component overview
2. **Component Interactions**: How different parts work together
3. **Sequence Diagrams**: Process flows and interactions
4. **Technical Considerations**: Constraints, dependencies, and trade-offs
5. **Implementation Strategy**: Approach and patterns to be used

Template structure:
```markdown
# Design Document

## System Architecture
[High-level architecture overview]

## Component Design
### Component 1
[Detailed component description]

### Component 2
[Detailed component description]

## Sequence Diagrams
[Process flows and interactions]

## Technical Considerations
- Dependencies: [list of dependencies]
- Constraints: [technical constraints]
- Trade-offs: [design decisions and rationale]

## Implementation Strategy
[Approach and patterns]
```

## Step 5: Create Implementation Plan

Create `tasks.md` with ONLY the implementation plan - no extra text, headers, or explanations:

**Important Guidelines:**
- Start directly with `# Implementation Plan` heading
- Include only the task list with checkboxes
- No introductory text, task overview, success criteria, or quality standards
- Keep it clean and focused on actionable tasks only
- Use requirement references at the end of each task

Template structure:
```markdown
# Implementation Plan

- [ ] 1. [Task Name]
  - [Brief description of what needs to be done]
  - [Additional sub-task or detail]
  - [Another implementation detail]
  - [Any technical considerations]
  - _Requirements: [X.X, Y.Y]_

- [ ] 2. [Second Task Name]
  - [Brief description of second task]
  - [Sub-task or implementation detail]
  - [Technical specification or constraint]
  - [Expected outcome or deliverable]
  - _Requirements: [X.X, Z.Z]_

- [ ] 3. [Third Task Name]
  - [Description of third task]
  - [Implementation approach]
  - [Dependencies or prerequisites]
  - [Validation criteria]
  - _Requirements: [Y.Y, Z.Z]_
```

## Step 6: Validate Specification

Review the complete specification:

1. **Requirements Validation**: Ensure all requirements are testable and clear
2. **Design Consistency**: Verify design addresses all requirements
3. **Task Completeness**: Confirm tasks cover all design elements
4. **Dependencies**: Check for missing dependencies or circular references

## Step 7: Initialize Spec Session (Optional)

If using Kiro directly, you can start a spec session to refine the specification:

1. Open Kiro and navigate to your project
2. Start a spec session for your feature
3. Reference existing documents to generate or refine specs
4. Use commands like "Generate a spec from [existing-doc]" if importing requirements

## Best Practices

### Requirements Best Practices
- Use structured EARS notation for acceptance criteria
- Focus on "what" and "why", not "how"
- Make requirements testable and measurable
- Include both functional and non-functional requirements

### Design Best Practices
- Document the big picture first, then dive into details
- Include sequence diagrams for complex interactions
- Address technical constraints and trade-offs
- Consider scalability and maintainability

### Tasks Best Practices
- Keep tasks small and focused (ideally 1-3 days of work)
- Make tasks independent when possible
- Include clear success criteria
- Order tasks by dependencies and priority

### Iteration Best Practices
- Treat specs as living documents
- Update specs as requirements change
- Sync specs with actual implementation
- Use version control to track spec evolution

## Example Usage

```fish
# Create a new authentication spec
mkdir -p .kiro/specs/user-authentication

# Create the three core files
touch .kiro/specs/user-authentication/requirements.md
touch .kiro/specs/user-authentication/design.md
touch .kiro/specs/user-authentication/tasks.md

# Edit each file following the templates above
```

This workflow ensures your Kiro specifications follow best practices and provide a solid foundation for development work.
