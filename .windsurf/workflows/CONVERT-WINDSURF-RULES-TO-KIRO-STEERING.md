---
description: Converts Windsurf rules to Kiro steering files by transforming frontmatter and filename format
---

You are a Windsurf-to-Kiro conversion tool that transforms Windsurf rule files into Kiro steering files.

## Conversion Process

1. **Identify Source Windsurf Rule**
   - Locate the Windsurf rule file in `.windsurf/rules/[rule-name].md`
   - Read the current frontmatter and content
   - Note the original filename for conversion

2. **Transform Frontmatter**
   Convert the Windsurf frontmatter structure:
   
   **FROM (Windsurf format):**
   ```yaml
   ---
   trigger: always_on|manual|model_decision|glob
   description: "Description of what the rule does"
   globs: "**/pattern" # Only for glob trigger
   ---
   ```
   
   **TO (Kiro format):**
   
   **For non-glob triggers:**
   ```yaml
   ---
   inclusion: always
   ---
   ```
   
   **For glob triggers:**
   ```yaml
   ---
   inclusion: fileMatch
   fileMatchPattern: ['pattern1', 'pattern2']
   ---
   ```
   
   **Conversion Rules:**
   - `always_on`, `manual`, `model_decision` → `inclusion: always`
   - `glob` → `inclusion: fileMatch` + `fileMatchPattern: ['glob_pattern']`
   - Remove `description` field entirely
   - Convert `globs` field to `fileMatchPattern` array (only for glob triggers)
   - Transform glob pattern from string to array format

3. **Transform Filename**
   Convert the filename format:
   - **FROM**: `kebab-case-filename.md` (hyphens)
   - **TO**: `space separated filename.md` (spaces)
   
   **Examples:**
   - `use-bun-or-pnpm-for-nodejs-dependency-manager.md` → `use bun or pnpm for nodejs dependency manager.md`
   - `enforce-typescript-usage.md` → `enforce typescript usage.md`
   - `require-jsx-file-extension.md` → `require jsx file extension.md`

4. **Preserve Content**
   - Keep all markdown content exactly the same
   - Maintain all headers, code blocks, formatting, and structure
   - No changes to the rule logic or documentation

5. **Create Kiro Steering File**
   - Save to `.kiro/steering/[space separated filename].md`
   - Ensure the `.kiro/steering/` directory exists
   - Verify the file uses the correct frontmatter format

6. **Verification Steps**
   - Confirm frontmatter only contains `inclusion: always`
   - Verify filename uses spaces instead of hyphens
   - Check that content is identical to source
   - Ensure file is saved in correct `.kiro/steering/` location

## Batch Conversion Command Example

To convert multiple rules at once:

```bash
# Create the steering directory if it doesn't exist
mkdir -p .kiro/steering

# Convert each rule file
for file in .windsurf/rules/*.md; do
  # Extract filename without path and extension
  basename=$(basename "$file" .md)
  
  # Convert kebab-case to space-separated
  kiro_name=$(echo "$basename" | sed 's/-/ /g')
  
  # Check if original file has glob trigger
  if grep -q "trigger: glob" "$file"; then
    # Extract glob pattern from original file
    glob_pattern=$(grep "globs:" "$file" | sed 's/globs: *"\(.*\)"/\1/')
    
    # Create file with fileMatch frontmatter
    echo "---" > ".kiro/steering/$kiro_name.md"
    echo "inclusion: fileMatch" >> ".kiro/steering/$kiro_name.md"
    echo "fileMatchPattern: ['$glob_pattern']" >> ".kiro/steering/$kiro_name.md"
    echo "---" >> ".kiro/steering/$kiro_name.md"
  else
    # Create file with always inclusion frontmatter
    echo "---" > ".kiro/steering/$kiro_name.md"
    echo "inclusion: always" >> ".kiro/steering/$kiro_name.md"
    echo "---" >> ".kiro/steering/$kiro_name.md"
  fi
  
  echo "" >> ".kiro/steering/$kiro_name.md"
  
  # Append content after frontmatter (skip original frontmatter)
  tail -n +5 "$file" >> ".kiro/steering/$kiro_name.md"
done
```

## Manual Conversion Steps

1. Open the Windsurf rule file
2. Check the trigger type in the frontmatter
3. Copy all content after the frontmatter (line 5 onwards)
4. Create new Kiro steering file with space-separated filename
5. Add appropriate Kiro frontmatter:
   
   **For non-glob triggers:**
   ```yaml
   ---
   inclusion: always
   ---
   ```
   
   **For glob triggers:**
   ```yaml
   ---
   inclusion: fileMatch
   fileMatchPattern: ['pattern1', 'pattern2']
   ---
   ```
   (Convert the `globs` field value to the `fileMatchPattern` array)
6. Paste the copied content
7. Save to `.kiro/steering/` directory

## Important Notes

- **Frontmatter Simplification**: Kiro steering uses much simpler frontmatter than Windsurf rules
- **Always Inclusion**: All converted rules use `inclusion: always` regardless of original trigger type
- **Filename Convention**: Kiro uses spaces while Windsurf uses hyphens
- **Content Preservation**: The actual rule content remains unchanged
- **Directory Structure**: Maintain separate `.windsurf/rules/` and `.kiro/steering/` directories

This conversion allows you to maintain the same coding standards across both Windsurf and Kiro systems.
