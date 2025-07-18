# Supabase Project Configuration Rules

## Dynamic Project ID Detection

When working with Supabase locally in this project, always read the project ID from the configuration file to ensure consistency.

### Project ID Verification

Before any Supabase operation, verify the current project configuration:

```fish
# Check current project ID from config.toml
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
echo "Current Project ID: $PROJECT_ID"

# Verify config file exists and is readable
if not test -f supabase/config.toml
    echo "Error: supabase/config.toml not found"
    exit 1
end

if test -z "$PROJECT_ID"
    echo "Error: project_id not found in supabase/config.toml"
    exit 1
end
```

### Project Configuration Standards

- **Project ID**: Automatically read from `supabase/config.toml`
- **Config File**: `supabase/config.toml` contains the authoritative project ID
- **Container Naming**: All Supabase containers use the suffix `_[PROJECT_ID]`
- **Container Detection**: Use `docker ps --filter "name=supabase_*_[PROJECT_ID]"` to find containers

### Configuration Rules

1. **Always read project ID** from `supabase/config.toml` before operations
2. **Never hardcode project IDs** in scripts or documentation
3. **Verify config consistency** by checking the config file exists and contains valid project_id
4. **Use dynamic container detection** based on the project ID from config
5. **Validate project ID format** to ensure it matches expected patterns
### Container Detection Examples

Use these patterns to detect and work with Supabase containers:

```fish
# Get project ID from config
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)

# Find all Supabase containers for this project
docker ps --filter "name=supabase_*_$PROJECT_ID" --format "table {{.Names}}\t{{.ID}}\t{{.Status}}"

# Get specific container IDs
set DB_CONTAINER (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")
set EDGE_CONTAINER (docker ps --filter "name=supabase_edge_runtime_$PROJECT_ID" --format "{{.ID}}")
set API_CONTAINER (docker ps --filter "name=supabase_kong_$PROJECT_ID" --format "{{.ID}}")

# Verify containers are running
if test -z "$DB_CONTAINER"
    echo "Warning: PostgreSQL container not found"
end
if test -z "$EDGE_CONTAINER"
    echo "Warning: Edge Functions container not found"
end
```

### Usage in Scripts

When creating scripts that interact with Supabase:

```fish
#!/usr/bin/env fish

# Always start with project ID detection
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)

if test -z "$PROJECT_ID"
    echo "Error: Could not determine project ID from supabase/config.toml"
    exit 1
end

echo "Working with Supabase project: $PROJECT_ID"

# Use PROJECT_ID in all subsequent operations
set CONTAINER_ID (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")
# ... rest of script
```

### Container Environment

All local Supabase containers follow this naming pattern based on the project ID from `config.toml`:

```fish
# Get project ID from config
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)

# Expected container names:
# - supabase_db_$PROJECT_ID
# - supabase_kong_$PROJECT_ID
# - supabase_auth_$PROJECT_ID
# - supabase_edge_runtime_$PROJECT_ID
# - supabase_studio_$PROJECT_ID
# - And other Supabase services with _$PROJECT_ID suffix
```

### Container Verification

To verify all containers are running with the correct project ID:

```fish
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
echo "Checking containers for project: $PROJECT_ID"
docker ps --filter "name=supabase_*_$PROJECT_ID" --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
```

### Benefits

- **Dynamic Configuration**: Automatically adapts to any project ID changes in config.toml
- **No Hardcoding**: Eliminates the need to update documentation when project ID changes
- **Consistency**: Ensures all Supabase operations work with the current project configuration
- **Flexibility**: Supports different project IDs across different environments
- **Predictable Naming**: Makes container management and debugging easier through standardized patterns

This approach ensures all Supabase local development stays consistent with the project configuration defined in `supabase/config.toml`.