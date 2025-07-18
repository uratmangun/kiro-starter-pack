# Supabase Migration Rules

## Database Migration Execution

When working with Supabase migrations in this project, always apply migrations directly to the PostgreSQL database using Docker.

### Pre-Migration Checks

Before applying any migration, always verify the current configuration:

```fish
# 1. Check project ID from config.toml
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
echo "Project ID: $PROJECT_ID"

# 2. Get current PostgreSQL container ID
set CONTAINER_ID (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")
echo "PostgreSQL Container ID: $CONTAINER_ID"

# 3. Verify container is running
if test -z "$CONTAINER_ID"
    echo "Error: PostgreSQL container not found for project $PROJECT_ID"
    exit 1
end
```

### Migration Command Pattern

Use this command pattern to apply migration files:

```fish
# Get project configuration
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
set CONTAINER_ID (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")

# Apply migration
cat supabase/migrations/[migration-file].sql | docker exec -i $CONTAINER_ID psql -U postgres -d postgres
```

### Automatic Migration Application

- **Always apply migrations immediately** when creating or modifying migration files
- **Never use** `supabase db push` or other Supabase CLI commands
- **Use the docker exec -i pattern** to pipe SQL content directly to the PostgreSQL container
- **Apply all pending migrations** in chronological order by filename

### Dynamic Container Detection

- **Project ID**: Automatically read from `supabase/config.toml`
- **PostgreSQL Container**: Detected using `docker ps --filter "name=supabase_db_[PROJECT_ID]"`
- **Database**: `postgres`
- **User**: `postgres`

### Complete Migration Example

When a new migration file is created:

```fish
# 1. Get project configuration
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
set CONTAINER_ID (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")

# 2. Verify container exists
if test -z "$CONTAINER_ID"
    echo "Error: PostgreSQL container not found for project $PROJECT_ID"
    exit 1
end

# 3. Apply migration
cat supabase/migrations/new_migration.sql | docker exec -i $CONTAINER_ID psql -U postgres -d postgres

# 4. Verify migration was applied
docker exec -i $CONTAINER_ID psql -U postgres -d postgres -c "\dt"
```

This ensures the database schema is always up-to-date with the latest migrations without requiring separate manual steps.