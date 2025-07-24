---
name: "Kiro Specification Generation Requirements"
trigger: always_on
description: "Mandates creation of comprehensive Kiro specifications for all development plans following the three-file format"
---

# Spec Generation Standards

## Overview
This document establishes the mandatory practice of creating comprehensive Kiro specifications whenever development plans are created. Every plan must be accompanied by a properly structured specification following the three-file Kiro format to ensure consistent documentation and clear implementation guidance.

## Core Principles
- Every plan requires a corresponding specification
- Specifications must precede implementation work
- Follow the standardized three-file Kiro format (requirements.md, design.md, tasks.md)
- Specifications are living documents that evolve with the project
- All team members must follow the spec creation workflow

## Standards and Guidelines

### When to Create Specs
Create a specification for any development work that involves:

```markdown
// Triggers for spec creation:
- New feature development
- Significant refactoring or redesign
- Architecture changes
- API modifications
- Database schema updates
- Complex bug fixes affecting multiple components
- Performance optimization initiatives
```

### Specification Structure
Every spec must follow the three-file format:

```
.kiro/specs/[feature-name]/
├── requirements.md  # User stories and acceptance criteria
├── design.md       # Technical architecture and implementation approach
└── tasks.md        # Discrete, trackable implementation tasks
```

### Spec Creation Process
Follow the established workflow in `.windsurf/workflows/CREATE-KIRO-SPEC.md`:

1. **Analyze Project Context**
   - Review existing specs and project structure
   - Identify feature scope and boundaries
   - Understand dependencies and constraints

2. **Create Directory Structure**
   ```fish
   mkdir -p .kiro/specs/[feature-name]
   ```

3. **Generate Requirements Document**
   - Write user stories in "As a [user], I want [goal], so that [benefit]" format
   - Use EARS notation for acceptance criteria: "WHEN [condition] THEN the system SHALL [behavior]"
   - Include non-functional requirements (performance, security, usability)

4. **Create Design Document**
   - Document system architecture and component interactions
   - Include sequence diagrams for complex flows
   - Address technical considerations and trade-offs
   - Define implementation strategy and patterns

5. **Create Implementation Plan**
   - Break work into discrete, trackable tasks
   - Define clear success criteria for each task
   - Identify dependencies and proper task ordering
   - Include status tracking (Not Started, In Progress, Completed)

### Quality Standards for Specs

#### Requirements Quality
```markdown
// Good requirement example:
**User Story:** As a developer using the Citrea boilerplate, I want a clean homepage layout, so that I can quickly understand the project's purpose.

**Acceptance Criteria:**
1. WHEN a user visits the homepage THEN they SHALL see a prominent "Citrea Boilerplate" title
2. WHEN a user reads the description THEN they SHALL understand how to use the boilerplate
3. WHEN a user views the page on mobile THEN the layout SHALL remain responsive and readable
```

#### Design Quality
```markdown
// Good design documentation:
## Component Design
### HomePage Component
- **Purpose**: Display clean, centered boilerplate introduction
- **Props**: None required
- **Styling**: Uses Tailwind utility classes for responsive design
- **Dependencies**: Layout component for consistent theming
```

#### Task Quality

**Critical Guidelines for tasks.md:**
- Start directly with `# Implementation Plan` heading
- Include ONLY the task list with checkboxes
- NO introductory text, task overview, success criteria, or quality standards
- Keep clean and focused on actionable tasks only
- Use requirement references at the end of each task

```markdown
// Good task definition (Implementation Plan format):
# Implementation Plan

- [x] 1. Remove complex HomePage content and imports
  - Remove Button, CopyButton, ExternalLink, Github icons from imports
  - Remove React and Vite logo imports and assets
  - Remove GitHub CLI command and template integration logic
  - Clean up all interactive elements and complex state management
  - _Requirements: 1.1, 3.1_

- [ ] 2. Implement clean centered layout structure
  - Create Flexbox container with vertical and horizontal centering
  - Set minimum height to 70vh for proper vertical positioning
  - Add responsive container with max-width constraints
  - Implement proper spacing utilities for content organization
  - _Requirements: 1.1, 2.1_
```

## Implementation Examples

### Example Spec Creation for Homepage Redesign
```fish
# 1. Create spec directory
mkdir -p .kiro/specs/homepage-redesign

# 2. Create the three core files
cat > .kiro/specs/homepage-redesign/requirements.md << 'EOF'
# Homepage Redesign Requirements

## Introduction
Redesign the homepage to focus solely on the Citrea Boilerplate introduction.

## Requirements

### Requirement 1: Single Section Layout
**User Story:** As a developer, I want a clean homepage, so that I understand the project purpose immediately.

#### Acceptance Criteria
1. WHEN a user visits the homepage THEN they SHALL see only the "Citrea Boilerplate" section
2. WHEN a user reads the content THEN they SHALL see the description "Use this boilerplate to easily create your citrea project"
EOF

# 3. Continue with design.md and tasks.md following the templates
```

## Common Pitfalls
- Creating plans without accompanying specifications
- Writing specs that are too vague or high-level
- Forgetting to update specs when requirements change
- Not following the three-file structure consistently
- Skipping acceptance criteria or success metrics

## Tools and Resources
- **Workflow Reference**: `.windsurf/workflows/CREATE-KIRO-SPEC.md`
- **EARS Notation**: For structured acceptance criteria
- **User Story Format**: "As a [user], I want [goal], so that [benefit]"
- **Task Tracking**: Use clear status indicators and dependencies

## Enforcement Guidelines
- All pull requests must reference corresponding specifications
- Code reviews should verify implementation matches spec requirements
- Specifications must be updated before major changes are implemented
- Team leads should validate spec quality before development begins

## Exception Handling
Minor changes that don't require specs:
- Typo fixes
- Simple styling adjustments
- Documentation updates
- Dependency version bumps

For any ambiguous cases, default to creating a specification to maintain consistency and documentation quality.
