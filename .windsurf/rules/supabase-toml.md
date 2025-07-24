---
trigger: glob
description: "Applies Supabase project configuration rules for supabase.toml files"
globs: "**/supabase.toml"
---

# Supabase Project Configuration

## Core Principles

- **Dynamic Project ID**: Always read from `supabase/config.toml`, never hardcode
- **Container Naming**: All containers use suffix `_[PROJECT_ID]`
- **Config Authority**: `supabase/config.toml` is the single source of truth

## Project ID Detection Pattern

```fish
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
if test -z "$PROJECT_ID"
    echo "Error: project_id not found in supabase/config.toml"
    exit 1
end
```

## Container Operations

### Detection
```fish
# Find all project containers
docker ps --filter "name=supabase_*_$PROJECT_ID"

# Get specific container IDs
set DB_CONTAINER (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")
```

### Standard Container Names
- `supabase_db_$PROJECT_ID` - PostgreSQL database
- `supabase_kong_$PROJECT_ID` - API gateway
- `supabase_auth_$PROJECT_ID` - Authentication service
- `supabase_edge_runtime_$PROJECT_ID` - Edge functions
- `supabase_studio_$PROJECT_ID` - Admin dashboard

## Script Template

```fish
#!/usr/bin/env fish
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
if test -z "$PROJECT_ID"
    echo "Error: Could not determine project ID"
    exit 1
end
# Use $PROJECT_ID in all operations
```

## Validation Rules

1. Verify `supabase/config.toml` exists before operations
2. Check project ID is non-empty after extraction
3. Use dynamic container detection with project ID
4. Never hardcode project IDs in scripts or documentation