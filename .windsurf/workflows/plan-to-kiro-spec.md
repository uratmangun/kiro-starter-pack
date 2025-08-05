---
description: Convert a Windsurf plan into a comprehensive Kiro specification following the three-file format
---

You are a Kiro specification generator that converts Windsurf plans into structured Kiro specs following the established standards in `.kiro/steering/spec-generation-standards.md`.

## Conversion Process

1. **Analyze the Windsurf Plan**
   - Read the current plan from `.windsurf/brain/*/plan.md` or user-provided plan
   - Identify the main feature/project being described
   - Extract key requirements, technical details, and tasks
   - Determine appropriate feature name for the spec directory

2. **Create Spec Directory Structure**
   - Generate feature name using kebab-case (e.g., "homepage-redesign", "user-authentication")
   - Create directory: `.kiro/specs/[feature-name]/`
   - Prepare to create the three mandatory files

3. **Generate requirements.md**
   Convert plan goals into structured requirements:
   
   ```markdown
   # [Feature Name] Requirements
   
   ## Introduction
   [Brief description of the feature/project]
   
   ## Requirements
   
   ### Requirement 1: [Requirement Title]
   **User Story:** As a [user type], I want [goal], so that [benefit].
   
   #### Acceptance Criteria
   1. WHEN [condition] THEN the system SHALL [behavior]
   2. WHEN [condition] THEN the system SHALL [behavior]
   3. WHEN [condition] THEN the system SHALL [behavior]
   
   ### Requirement 2: [Next Requirement]
   [Continue pattern for all requirements...]
   ```

4. **Generate design.md**
   Convert technical aspects of the plan into design documentation:
   
   ```markdown
   # [Feature Name] Design
   
   ## Architecture Overview
   [High-level system design and component interactions]
   
   ## Technical Approach
   [Implementation strategy and patterns]
   
   ## Component Design
   ### [Component Name]
   - **Purpose**: [What this component does]
   - **Dependencies**: [What it depends on]
   - **Interface**: [How it interacts with other components]
   
   ## Data Flow
   [Sequence of operations and data transformations]
   
   ## Technical Considerations
   [Performance, security, scalability considerations]
   ```

5. **Generate tasks.md**
   Convert plan action items into trackable implementation tasks:
   
   ```markdown
   # Implementation Plan
   
   - [ ] 1. [Task Description]
     - [Specific implementation details]
     - [Technical requirements]
     - _Requirements: [Reference to requirements, e.g., 1.1, 2.1]_
   
   - [ ] 2. [Next Task Description]
     - [Implementation details]
     - [Dependencies on previous tasks]
     - _Requirements: [Reference to requirements]_
   
   [Continue for all implementation tasks...]
   ```

6. **Apply Quality Standards**
   - Ensure user stories follow "As a [user], I want [goal], so that [benefit]" format
   - Use EARS notation for acceptance criteria: "WHEN [condition] THEN the system SHALL [behavior]"
   - Make tasks discrete and trackable with clear success criteria
   - Include requirement references in task descriptions
   - Follow the three-file structure consistently

7. **Create the Specification Files**
   - Save requirements.md in `.kiro/specs/[feature-name]/requirements.md`
   - Save design.md in `.kiro/specs/[feature-name]/design.md`
   - Save tasks.md in `.kiro/specs/[feature-name]/tasks.md`

8. **Validation Checklist**
   - [ ] Directory created in `.kiro/specs/[feature-name]/`
   - [ ] All three files present (requirements.md, design.md, tasks.md)
   - [ ] Requirements use proper user story format
   - [ ] Acceptance criteria follow EARS notation
   - [ ] Design includes technical architecture and approach
   - [ ] Tasks are discrete and trackable
   - [ ] Requirements are properly referenced in tasks
   - [ ] Quality standards from spec-generation-standards.md are followed

## Example Usage
When you have a Windsurf plan for a homepage redesign, this workflow will:
1. Extract the plan's objectives (clean layout, responsive design)
2. Convert to user stories with acceptance criteria
3. Document technical approach and component design
4. Break down into implementable tasks with requirement references
5. Create the complete three-file Kiro specification

## Notes
- This workflow follows the standards in `.kiro/steering/spec-generation-standards.md`
- Generated specs are living documents that should evolve with the project
- All implementation work should reference the created specification
- Update specs before making major changes to requirements or design