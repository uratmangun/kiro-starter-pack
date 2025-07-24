---
trigger: glob
description: "Applies Supabase deployment rules for all files in supabase directories"
globs: "**/supabase/**/*"
---

# Supabase Edge Functions Deployment

## Core Deployment Pattern

Deploy Edge Functions directly to the local container using Docker operations:

```fish
# Get project configuration
set PROJECT_ID (grep '^project_id' supabase/config.toml | cut -d'"' -f2)
set CONTAINER_ID (docker ps --filter "name=supabase_edge_runtime_$PROJECT_ID" --format "{{.ID}}")

# Deploy function
docker cp supabase/functions/[function-name] $CONTAINER_ID:/functions/
docker restart $CONTAINER_ID
```

## Deployment Rules

- **Always deploy immediately** when creating or modifying Edge Functions
- **Never use** `supabase functions deploy` for local development
- **Use docker cp + restart pattern** for existing functions
- **Use full stack restart** only for brand new functions

## Function Structure Requirements

Each function must have:
- `index.ts` - Main function code with proper `serve()` export
- `deno.json` - Deno configuration file (required)

## Authorization

All function calls require:
- **Header**: `Authorization: Bearer [VITE_SUPABASE_ANON_KEY]`
- **Key source**: `.env.local` file

## New vs Existing Functions

### Existing Functions (Updates)
```fish
docker cp supabase/functions/my-function $CONTAINER_ID:/functions/
docker restart $CONTAINER_ID
```

### New Functions (First Deploy)
```fish
# Deploy function files
docker cp supabase/functions/my-function $CONTAINER_ID:/functions/
docker restart $CONTAINER_ID

# If function not recognized, restart full stack
bunx supabase stop
bunx supabase start
```

## Testing

Test deployed functions:
```fish
curl -X POST http://127.0.0.1:54321/functions/v1/my-function \
  -H "Authorization: Bearer [anon-key]" \
  -H "Content-Type: application/json" \
  -d '{"test": "data"}'
```

## Troubleshooting

- **404 errors**: Function not loaded - restart full stack for new functions
- **Container issues**: Check `docker logs $CONTAINER_ID --tail 10`
- **File verification**: `docker exec $CONTAINER_ID ls -la /functions/`