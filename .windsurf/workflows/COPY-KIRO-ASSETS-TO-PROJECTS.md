---
description: Copies Windsurf workflows, rules, Kiro hooks, and steering rules to kiro-starter-pack and react-kiro-starter projects
---

You are a project asset synchronization specialist that copies essential Kiro and Windsurf configurations to target projects.

## Your Task
Copy the following directories from the current citrea-boilerplate project to two target projects:
- `/home/uratmangun/CascadeProjects/kiro-starter-pack`
- `/home/uratmangun/CascadeProjects/react-kiro-starter`

## Directories to Copy
1. `.windsurf/workflows/` - All Windsurf workflow files
2. `.windsurf/rules/` - All Windsurf rule files
3. `.kiro/hooks/` - All Kiro hook files  
4. `.kiro/steering/` - All Kiro steering rule files

## Copy Process

### Step 1: Verify Target Projects Exist
Check that both target projects exist:

```fish
# Check if target directories exist
if test -d /home/uratmangun/CascadeProjects/kiro-starter-pack
    echo "✓ kiro-starter-pack exists"
else
    echo "✗ kiro-starter-pack not found"
end

if test -d /home/uratmangun/CascadeProjects/react-kiro-starter
    echo "✓ react-kiro-starter exists"
else
    echo "✗ react-kiro-starter not found"
end
```

### Step 2: Copy to kiro-starter-pack
// turbo
```fish
# Create target directories if they don't exist
mkdir -p /home/uratmangun/CascadeProjects/kiro-starter-pack/.windsurf
mkdir -p /home/uratmangun/CascadeProjects/kiro-starter-pack/.kiro

# Copy workflows directory
cp -r .windsurf/workflows /home/uratmangun/CascadeProjects/kiro-starter-pack/.windsurf/

# Copy rules directory
cp -r .windsurf/rules /home/uratmangun/CascadeProjects/kiro-starter-pack/.windsurf/

# Copy hooks directory
cp -r .kiro/hooks /home/uratmangun/CascadeProjects/kiro-starter-pack/.kiro/

# Copy steering directory
cp -r .kiro/steering /home/uratmangun/CascadeProjects/kiro-starter-pack/.kiro/

echo "✓ Copied all assets to kiro-starter-pack"
```

### Step 3: Copy to react-kiro-starter
// turbo
```fish
# Create target directories if they don't exist
mkdir -p /home/uratmangun/CascadeProjects/react-kiro-starter/.windsurf
mkdir -p /home/uratmangun/CascadeProjects/react-kiro-starter/.kiro

# Copy workflows directory
cp -r .windsurf/workflows /home/uratmangun/CascadeProjects/react-kiro-starter/.windsurf/

# Copy rules directory
cp -r .windsurf/rules /home/uratmangun/CascadeProjects/react-kiro-starter/.windsurf/

# Copy hooks directory
cp -r .kiro/hooks /home/uratmangun/CascadeProjects/react-kiro-starter/.kiro/

# Copy steering directory
cp -r .kiro/steering /home/uratmangun/CascadeProjects/react-kiro-starter/.kiro/

echo "✓ Copied all assets to react-kiro-starter"
```

### Step 4: Verify Copy Success
// turbo
```fish
# Verify kiro-starter-pack
echo "=== kiro-starter-pack verification ==="
echo "Workflows:"; and ls -la /home/uratmangun/CascadeProjects/kiro-starter-pack/.windsurf/workflows/ | wc -l
echo "Rules:"; and ls -la /home/uratmangun/CascadeProjects/kiro-starter-pack/.windsurf/rules/ | wc -l
echo "Hooks:"; and ls -la /home/uratmangun/CascadeProjects/kiro-starter-pack/.kiro/hooks/ | wc -l
echo "Steering:"; and ls -la /home/uratmangun/CascadeProjects/kiro-starter-pack/.kiro/steering/ | wc -l

# Verify react-kiro-starter
echo "=== react-kiro-starter verification ==="
echo "Workflows:"; and ls -la /home/uratmangun/CascadeProjects/react-kiro-starter/.windsurf/workflows/ | wc -l
echo "Rules:"; and ls -la /home/uratmangun/CascadeProjects/react-kiro-starter/.windsurf/rules/ | wc -l
echo "Hooks:"; and ls -la /home/uratmangun/CascadeProjects/react-kiro-starter/.kiro/hooks/ | wc -l
echo "Steering:"; and ls -la /home/uratmangun/CascadeProjects/react-kiro-starter/.kiro/steering/ | wc -l
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

This workflow ensures both target projects have the same Kiro and Windsurf configurations as the source citrea-boilerplate project.
