---
description: Run Cursor Agent in non-interactive mode with a custom prompt using --print and optional JSON/text output for integration in scripts and CI.
---

You are using Cursor Agent from the CLI in non-interactive mode to generate responses for scripts, CI pipelines, or quick one-off runs. This workflow shows how to pass a custom prompt, choose output formats, and keep execution safe.

1. Verify Cursor Agent is installed and view help
// turbo
- Run:
```fish
cursor-agent -h
```
- You should see flags including `--print` and `--output-format`.

2. Authenticate (one-time or via CI env var)
- Option A (preferred in CI): set the API key via environment variable
```fish
# Replace with your real key
set -x CURSOR_API_KEY "<your-cursor-api-key>"
```
- Option B (local dev): login once
```fish
cursor-agent login
```

3. Set your prompt dynamically (you can change this anytime)
```fish
# Example; change to whatever you ask
set PROMPT "<your prompt here>"
```

4. Choose output format
- `text`: plain text, easy to read
- `json`: structured JSON, easy to parse in scripts
- `stream-json`: streaming JSON (default when using --print)

5. Run Cursor Agent in non-interactive mode (no file writes or shell by default). Uses model -m gpt-5-fast.
- Plain text output:
```fish
echo $PROMPT | cursor-agent --print --output-format text -m gpt-5-fast
```
- JSON output:
```fish
echo $PROMPT | cursor-agent --print --output-format json -m gpt-5-fast
```
 - The examples in this workflow enforce the model via `-m gpt-5-fast` for consistency.
6. Capture output to a file (useful in CI)
```fish
# For JSON output saved to a file
echo $PROMPT | cursor-agent --print --output-format json -m gpt-5-fast | tee agent-output.json
```

7. Safety and best practices
- Avoid `-f/--force` unless you understand the risks; it can allow command execution.
- In non-interactive mode, prefer prompts that explicitly say not to run shell or write files, for example:
```fish
set PROMPT "Do NOT run shell or write files. Respond in JSON with keys 'summary' and 'steps': <your task>"
```
- Keep prompts concise and specific for predictable outputs.

8. Troubleshooting
- Not authenticated: ensure `CURSOR_API_KEY` is set or run `cursor-agent login`.
- CI usage: set `CURSOR_API_KEY` as a secret and export it in the job environment.
- Large outputs: prefer `--output-format json` for reliable parsing.

When to use this workflow
- You need a non-interactive run for automation.
- You want to quickly get a response with a custom prompt in your terminal.
- You need structured output for downstream tooling.
