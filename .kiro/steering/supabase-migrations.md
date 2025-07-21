---
inclusion: fileMatch
fileMatchPattern: ['supabase/migrations/**/*.sql', 'supabase/config.toml']
---

# Supabase Migration Standards

## Migration Execution Pattern

Apply migrations directly to PostgreSQL container using Docker exec. Never use `supabase db push` or CLI migration commands.

### Required Pre-Migration Steps

1. Read project ID from `supabase/config.toml`
2. Detect PostgreSQL container using dynamic naming
3. Verify container is running before applying migration

### Standard Migration Command

```fish
# Dynamic project detection and migration application
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
set CONTAINER_ID (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")

# Apply migration file
cat supabase/migrations/[filename].sql | docker exec -i $CONTAINER_ID psql -U postgres -d postgres
```

### Migration Rules

- **Immediate Application**: Apply migrations immediately when creating/modifying migration files
- **Chronological Order**: Apply pending migrations in filename order
- **Container Detection**: Use `supabase_db_[PROJECT_ID]` naming pattern
- **Database Connection**: Always use `postgres` database and `postgres` user
- **Error Handling**: Verify container exists before attempting migration

### Container Configuration

- **Project ID Source**: `supabase/config.toml` (never hardcode)
- **Container Pattern**: `supabase_db_[PROJECT_ID]`
- **Database**: `postgres`
- **User**: `postgres`

This pattern ensures migrations are applied consistently using the current project configuration.