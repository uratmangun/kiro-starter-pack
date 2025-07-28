---
inclusion: fileMatch
fileMatchPattern: ['supabase/**/*']
---

# Supabase Docker Network and Configuration Management

## Docker Network Requirements

**MANDATORY**: When restarting Supabase database, all containers must be connected to the `my-net` network with restart policies configured.

### Network Configuration

```fish
# Connect all Supabase containers to my-net network
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)

# Connect database container
docker network connect my-net supabase_db_$PROJECT_ID

# Connect other Supabase containers to my-net
docker network connect my-net supabase_auth_$PROJECT_ID
docker network connect my-net supabase_rest_$PROJECT_ID
docker network connect my-net supabase_realtime_$PROJECT_ID
docker network connect my-net supabase_storage_$PROJECT_ID
docker network connect my-net supabase_imgproxy_$PROJECT_ID
docker network connect my-net supabase_edge_$PROJECT_ID
```

### Restart Policy Configuration

**MANDATORY**: Set restart policy to `always` for all Supabase containers.

```fish
# Set restart policy for all Supabase containers
docker update --restart=always supabase_db_$PROJECT_ID
docker update --restart=always supabase_auth_$PROJECT_ID
docker update --restart=always supabase_rest_$PROJECT_ID
docker update --restart=always supabase_realtime_$PROJECT_ID
docker update --restart=always supabase_storage_$PROJECT_ID
docker update --restart=always supabase_imgproxy_$PROJECT_ID
docker update --restart=always supabase_edge_$PROJECT_ID
```

## JWT Secret Configuration

**MANDATORY**: Use global environment variable `JWT_SECRET` instead of .env file variables in `supabase/config.toml`.

### Required Configuration

In `supabase/config.toml` at line 126:

```toml
# Correct configuration - uses global environment variable
jwt_secret = "env(JWT_SECRET)"
```

### Environment Variable Setup

```fish
# Set global JWT_SECRET environment variable
set -x JWT_SECRET "your-jwt-secret-here"

# Verify the variable is set
echo $JWT_SECRET
```

### Verification Commands

```fish
# Verify network connections
docker network inspect my-net

# Verify restart policies
docker inspect supabase_db_$PROJECT_ID --format='{{.HostConfig.RestartPolicy.Name}}'

# Verify JWT secret configuration
grep "jwt_secret" supabase/config.toml
```

## Complete Restart Procedure

When restarting the Supabase database, follow this sequence:

```fish
# 1. Read project configuration
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)

# 2. Stop Supabase
supabase stop

# 3. Start Supabase
supabase start

# 4. Connect all containers to my-net network
for container in db auth rest realtime storage imgproxy edge
    docker network connect my-net supabase_{$container}_$PROJECT_ID
end

# 5. Set restart policies
for container in db auth rest realtime storage imgproxy edge
    docker update --restart=always supabase_{$container}_$PROJECT_ID
end

# 6. Verify configuration
docker network inspect my-net
echo "All containers connected to my-net with restart=always policy"
```

This ensures consistent network connectivity and automatic container restart behavior for the Supabase infrastructure.
