---
description: Generate a concise Railway hosting overview for the current repository, including 1-click deploy link, setup, dependencies, and reasons to use Railway.
---

You are creating a short "Railway Template Overview" document for the current repository. Copy the Final Output below into `PITCH/RAILWAY-TEMPLATE.md` (or your README) as needed.

Gather project metadata first (prefer automation; do not invent details):

- Project name: from `package.json:name`; else the repository folder name
- Description: concise ~50 words from `README.md` intro or `package.json:description`
- Runtime: from `package.json:engines.node`; default to Node.js 20+ if absent
- Scripts: determine build/start from `package.json:scripts`
  - Prefer: `build`, `start`; else infer common patterns per framework
- Package manager: prefer pnpm, fallback to yarn (never npm)
- Framework hints (optional): detect via dependencies
  - Remix (`@remix-run/*`), Next.js (`next`), Express (`express`), NestJS (`@nestjs/*`), Astro (`astro`), SvelteKit (`@sveltejs/kit`), Nuxt (`nuxt`)

Compute a Railway 1‑click deploy URL for this repo (fish shell):

```fish
# Get remote and normalize to https URL
set ORIGIN (git config --get remote.origin.url)
if test -z "$ORIGIN"
  echo "No git remote.origin.url found"; end
set HTTPS_URL (string replace -r '^git@([^:]+):(.+?)(\.git)?$' 'https://$1/$2' -- $ORIGIN)
set HTTPS_URL (string replace -r '^(https?://.+?)(\.git)$' '$1' -- $HTTPS_URL)

# URL-encode for Railway template param
set TEMPLATE_ENC (python3 -c "import sys,urllib.parse as u; print(u.quote(sys.argv[1], safe=''))" $HTTPS_URL)
set RAILWAY_1CLICK https://railway.app/new?template=$TEMPLATE_ENC
echo $RAILWAY_1CLICK
```

Compute framework docs links (fish shell):

```fish
# Build a comma-separated list of framework docs links based on dependencies
set PJSON (cat package.json)
set LINKS
if string match -rq '\"@remix-run/' -- $PJSON
    set LINKS $LINKS '[Remix docs](https://remix.run/docs)'
end
if string match -rq '\"next\"' -- $PJSON
    set LINKS $LINKS '[Next.js docs](https://nextjs.org/docs)'
end
if string match -rq '\"express\"' -- $PJSON
    set LINKS $LINKS '[Express docs](https://expressjs.com/)'
end
if string match -rq '\"@nestjs/' -- $PJSON
    set LINKS $LINKS '[NestJS docs](https://docs.nestjs.com/)'
end
if string match -rq '\"astro\"' -- $PJSON
    set LINKS $LINKS '[Astro docs](https://docs.astro.build/)'
end
if string match -rq '\"@sveltejs/kit\"' -- $PJSON
    set LINKS $LINKS '[SvelteKit docs](https://kit.svelte.dev/docs)'
end
if string match -rq '\"nuxt\"' -- $PJSON
    set LINKS $LINKS '[Nuxt docs](https://nuxt.com/docs)'
end
if test (count $LINKS) -gt 0
    set FRAMEWORK_DOCS (string join ', ' $LINKS)
else
    set FRAMEWORK_DOCS 'N/A'
end
echo $FRAMEWORK_DOCS
```

Build/Start guidance (use detected scripts; examples):

- Build: `pnpm run build`; fallback `yarn build`
- Start: `pnpm start`; fallback `yarn start`
- Ensure the server binds to `$PORT` provided by Railway

Notes:

- Keep instructions framework‑agnostic; add specific notes only when confidently detected
- Ensure the Final Output does not contain placeholders. Replace any angle-bracket tokens (e.g., <repo name>) with concrete values detected from this repository.

Final Output:

```markdown
# Deploy and Host {{ project_name }} on Railway

{{ project_description }}

## One click deploy url

{{ railway_1click_url }}

## About Hosting {{ project_name }}

{{ hosting_description }}

## Common Use Cases

- <use case 1 based on app type>
- <use case 2>

## Dependencies for {{ project_name }} Hosting

{{ project_dependencies }}

### Deployment Dependencies

{{ deployment_dependencies }}

## Using .kiro Automation (optional)

{{ kiro_automation_section }}

## Why Deploy {{ project_name }} on Railway?

{{ railway_benefits }}

```