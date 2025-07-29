---
description: Copies Windsurf workflows, rules, Kiro hooks, and steering rules to all projects with .kiro and .windsurf folders
---

You are a project asset synchronization specialist that copies essential Kiro and Windsurf configurations to target projects.

## Your Task
Dynamically find all projects in `/home/uratmangun/CascadeProjects` that contain `.kiro` or `.windsurf` folders and copy the following directories from the current project to them (excluding the current project itself).

## Directories to Copy
1. `.windsurf/workflows/` - All Windsurf workflow files
2. `.windsurf/rules/` - All Windsurf rule files
3. `.kiro/hooks/` - All Kiro hook files  
4. `.kiro/steering/` - All Kiro steering rule files

## Copy Process

### Step 1: Find Target Projects
// turbo
```fish
# Initialize empty list and get current project name
set -g TARGET_PROJECTS
set CURRENT_PROJECT (basename (pwd))
echo "Current project: $CURRENT_PROJECT"
echo "Scanning /home/uratmangun/CascadeProjects for target projects..."
```

// turbo
```fish
# Find projects with .kiro or .windsurf folders
for project_path in /home/uratmangun/CascadeProjects/*
    if test -d "$project_path"
        set project_name (basename "$project_path")
        if test "$project_name" != "$CURRENT_PROJECT"
            if test -d "$project_path/.kiro"; or test -d "$project_path/.windsurf"
                set TARGET_PROJECTS $TARGET_PROJECTS "$project_path"
                echo "✓ Found target project: $project_name"
            end
        end
    end
end
```

// turbo
```fish
# Verify we found target projects
if test (count $TARGET_PROJECTS) -eq 0
    echo "✗ No target projects found with .kiro or .windsurf folders"
    exit 1
else
    echo "\nFound" (count $TARGET_PROJECTS) "target projects:"
    for proj in $TARGET_PROJECTS
        echo "  - "(basename $proj)
    end
    echo ""
end
```

### Step 2: Copy Assets to All Target Projects
// turbo
```fish
# Copy to each target project
for target_project in $TARGET_PROJECTS
    set project_name (basename $target_project)
    echo "=== Copying to $project_name ==="
    
    # Create target directories if they don't exist
    mkdir -p "$target_project/.windsurf"
    mkdir -p "$target_project/.kiro"
    
    # Copy workflows directory if it exists in source
    if test -d .windsurf/workflows
        cp -r .windsurf/workflows "$target_project/.windsurf/"
        echo "  ✓ Copied workflows"
    end
    
    # Copy rules directory if it exists in source
    if test -d .windsurf/rules
        cp -r .windsurf/rules "$target_project/.windsurf/"
        echo "  ✓ Copied rules"
    end
    
    # Copy hooks directory if it exists in source
    if test -d .kiro/hooks
        cp -r .kiro/hooks "$target_project/.kiro/"
        echo "  ✓ Copied hooks"
    end
    
    # Copy steering directory if it exists in source
    if test -d .kiro/steering
        cp -r .kiro/steering "$target_project/.kiro/"
        echo "  ✓ Copied steering"
    end
    
    echo "  ✓ Completed copying to $project_name"
end
```

### Step 3: Verify Copy Success
// turbo
```fish
# Verify each target project
for target_project in $TARGET_PROJECTS
    set project_name (basename $target_project)
    echo "=== $project_name verification ==="
    
    if test -d "$target_project/.windsurf/workflows"
        set workflow_count (ls -1 "$target_project/.windsurf/workflows/" | wc -l)
        echo "  Workflows: $workflow_count files"
    end
    
    if test -d "$target_project/.windsurf/rules"
        set rules_count (ls -1 "$target_project/.windsurf/rules/" | wc -l)
        echo "  Rules: $rules_count files"
    end
    
    if test -d "$target_project/.kiro/hooks"
        set hooks_count (ls -1 "$target_project/.kiro/hooks/" | wc -l)
        echo "  Hooks: $hooks_count files"
    end
    
    if test -d "$target_project/.kiro/steering"
        set steering_count (ls -1 "$target_project/.kiro/steering/" | wc -l)
        echo "  Steering: $steering_count files"
    end
end
```

## What Gets Copied

### Windsurf Workflows (.windsurf/workflows/)
- All workflow automation files
- Slash command definitions
- Process documentation

### Windsurf Rules (.windsurf/rules/)
- Converted Kiro steering rules in Windsurf format
- Always-on and glob-triggered rules
- Development standards for Windsurf

### Kiro Hooks (.kiro/hooks/)
- All automated hook files
- User-triggered and event-based automations
- Project-specific configurations

### Kiro Steering (.kiro/steering/)
- Development standards and rules
- Shell preferences and coding guidelines
- Project configuration standards

## Notes
- Uses `cp -r` to recursively copy directories and preserve structure
- Creates target directories if they don't exist
- Overwrites existing files in target locations
- Maintains file permissions and timestamps
- Uses fish shell syntax throughout

This workflow ensures all target projects with existing .kiro or .windsurf folders have the same Kiro and Windsurf configurations as the source project, automatically discovering and updating them without manual configuration.