# Supabase Function Deployment Rules

## Local Function Deployment Process

When working with Supabase Edge Functions in this project, always deploy functions directly to the running Edge Functions container.

### Pre-Deployment Checks

Before deploying any function, always verify the current configuration:

```fish
# 1. Check project ID from config.toml
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
echo "Project ID: $PROJECT_ID"

# 2. Get current Edge Functions container ID
set CONTAINER_ID (docker ps --filter "name=supabase_edge_runtime_$PROJECT_ID" --format "{{.ID}}")
echo "Edge Functions Container ID: $CONTAINER_ID"

# 3. Verify container is running
if test -z "$CONTAINER_ID"
    echo "Error: Edge Functions container not found for project $PROJECT_ID"
    exit 1
end
```

### Deployment Command Pattern

Use this command pattern to deploy function changes:

```fish
# Get project configuration
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
set CONTAINER_ID (docker ps --filter "name=supabase_edge_runtime_$PROJECT_ID" --format "{{.ID}}")

# Copy function to Edge Functions container
docker cp supabase/functions/[function-name] $CONTAINER_ID:/functions/

# Restart the Edge Functions container to pick up changes
docker restart $CONTAINER_ID
```

### Dynamic Container Detection

- **Project ID**: Automatically read from `supabase/config.toml`
- **Edge Functions Container**: Detected using `docker ps --filter "name=supabase_edge_runtime_[PROJECT_ID]"`
- **Functions Path**: `/functions/`
- **Access URL**: `http://127.0.0.1:54321/functions/v1/[function-name]`

### Project Configuration

- **Project ID**: Automatically detected from `supabase/config.toml`
- **Config file**: `supabase/config.toml` contains the authoritative project ID
- **Container naming**: All containers use the suffix `_[PROJECT_ID]`

### Automatic Deployment Workflow

- **Always deploy immediately** when creating or modifying Edge Functions
- **Never use** `supabase functions deploy` for local development
- **Use the docker cp + restart pattern** to deploy functions to the local container
- **Verify deployment** by checking container logs or testing the endpoint

### Authorization Requirements

All function calls require the Supabase anon key:
- **Header**: `Authorization: Bearer [VITE_SUPABASE_ANON_KEY]`
- **Key Location**: `.env.local` file


### Complete Deployment Example

When a new function is created or modified:

```fish
# 1. Get project configuration
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
set CONTAINER_ID (docker ps --filter "name=supabase_edge_runtime_$PROJECT_ID" --format "{{.ID}}")

# 2. Verify container exists
if test -z "$CONTAINER_ID"
    echo "Error: Edge Functions container not found for project $PROJECT_ID"
    exit 1
end

# 3. Deploy function
docker cp supabase/functions/my-function $CONTAINER_ID:/functions/
docker restart $CONTAINER_ID

# 4. Verify deployment
docker logs $CONTAINER_ID --tail 10

# 5. For new functions only: Restart Supabase stack if needed
# Only use this step when deploying a brand new function that has never existed before
# Skip this step when updating existing functions
bunx supabase stop
bunx supabase start
```
3. **Test**: `curl -X POST http://127.0.0.1:54321/functions/v1/my-function -H "Authorization: Bearer [anon-key]" -H "Content-Type: application/json" -d '{"test": "data"}'`
4. **Verify**: Check function response and container logs
5. **New Functions Only**: If this is a brand new function (not an update), restart the Supabase stack to ensure proper recognition

### Benefits

- **Immediate Deployment**: Functions are available instantly after restart
- **No CLI Dependencies**: Works without Supabase CLI deployment commands
- **Local Integration**: Functions integrate properly with local Supabase stack
- **Consistent Environment**: Matches production Edge Functions behavior

## Troubleshooting Failed Deployments

### When Functions Don't Load After Deployment

If functions are not being recognized by the Edge Functions container after using the docker cp method, try these solutions:

#### Solution 1: Restart Supabase Stack (For New Functions Only)

**⚠️ Use this method ONLY when deploying a brand new Edge Function that has never existed before.**

For updating existing functions, use the regular deployment method above (docker cp + docker restart). The full stack restart is only necessary when the Edge Functions container needs to recognize a completely new function for the first time.

```fish
# Stop all Supabase services
bunx supabase stop

# Start all Supabase services
bunx supabase start
```

**When to use:**
- Deploying a new function that doesn't exist yet
- First-time function deployment after creating new function files

**When NOT to use:**
- Updating existing functions (use regular docker cp method instead)
- Redeploying functions that are already working

#### Solution 2: Check Container Logs

Verify if functions are loaded by checking container logs:

```fish
# Check current container ID
docker ps | grep edge

# Check logs for function loading
docker logs [container-id] --tail 10
```

Look for lines like:
```
Serving functions on http://127.0.0.1:54321/functions/v1/<function-name>
 - http://127.0.0.1:54321/functions/v1/your-function-name
```

#### Solution 3: Verify Function Structure

Ensure your function has the correct structure:
- `index.ts` - Main function code
- `deno.json` - Deno configuration (required)
- Proper serve() function export

#### Solution 4: Manual Container Inspection

Check if files were copied correctly:

```fish
# List functions in container
docker exec [container-id] ls -la /functions/

# Check specific function files
docker exec [container-id] ls -la /functions/your-function-name/
```

### Common Issues

1. **Function returns 404**: Usually means function wasn't loaded - try Solution 1
2. **Container not starting**: Check for syntax errors in function code
3. **Function not in logs**: Function directory may be missing or improperly structured
4. **Persistent issues**: Remove and recreate the function directory, then redeploy

### When to Use CLI Restart

Use the Supabase CLI restart method when:
- Functions don't appear in container logs after deployment
- Getting 404 errors on function endpoints
- Docker restart doesn't resolve the issue
- Multiple functions are not being recognized

This method ensures a clean restart of the entire Supabase stack and often resolves function loading issues.

This ensures Edge Functions are properly deployed and accessible through the local Supabase API gateway without requiring remote deployment or additional CLI setup.