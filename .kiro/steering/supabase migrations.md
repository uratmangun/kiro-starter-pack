---
inclusion: fileMatch
fileMatchPattern: ['supabase/migrations/**/*.sql']
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

## Database Reset with Backup/Restore

**MANDATORY**: When performing `supabase db reset`, always backup the database first and restore it after reset completion.

### Complete Reset Procedure

```fish
# 1. Read project configuration
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
set CONTAINER_ID (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")

# 2. Create backup before reset
set BACKUP_FILE "backup_$(date +%Y%m%d_%H%M%S).sql"
echo "Creating database backup: $BACKUP_FILE"
docker exec $CONTAINER_ID pg_dump -U postgres -d postgres > $BACKUP_FILE

# 3. Verify backup was created successfully
if test -f $BACKUP_FILE; and test -s $BACKUP_FILE
    echo "Backup created successfully: $BACKUP_FILE"
else
    echo "ERROR: Backup failed or is empty. Aborting reset."
    exit 1
end

# 4. Perform database reset
echo "Performing database reset..."
supabase db reset

# 5. Wait for reset to complete and containers to be ready
echo "Waiting for containers to be ready..."
sleep 5

# 6. Get new container ID after reset
set CONTAINER_ID (docker ps --filter "name=supabase_db_$PROJECT_ID" --format "{{.ID}}")

# 7. Restore database from backup
echo "Restoring database from backup: $BACKUP_FILE"
cat $BACKUP_FILE | docker exec -i $CONTAINER_ID psql -U postgres -d postgres

# 8. Verify restore completed successfully
if test $status -eq 0
    echo "Database restored successfully from $BACKUP_FILE"
    echo "Backup file preserved at: $BACKUP_FILE"
else
    echo "ERROR: Database restore failed. Backup preserved at: $BACKUP_FILE"
    exit 1
end
```

### Backup Management

- **Backup Location**: Store backups in project root with timestamp
- **Backup Naming**: `backup_YYYYMMDD_HHMMSS.sql`
- **Backup Verification**: Always verify backup file exists and is not empty
- **Backup Preservation**: Keep backup files after successful restore
- **Error Handling**: Abort reset if backup creation fails

### Migration Rules

- **Immediate Application**: Apply migrations immediately when creating/modifying migration files
- **Chronological Order**: Apply pending migrations in filename order
- **Container Detection**: Use `supabase_db_[PROJECT_ID]` naming pattern
- **Database Connection**: Always use `postgres` database and `postgres` user
- **Error Handling**: Verify container exists before attempting migration
- **Reset Safety**: Always backup before reset operations

### Container Configuration

- **Project ID Source**: `supabase/config.toml` (never hardcode)
- **Container Pattern**: `supabase_db_[PROJECT_ID]`
- **Database**: `postgres`
