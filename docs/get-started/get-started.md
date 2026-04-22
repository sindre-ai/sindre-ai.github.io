# Get started with Maskin

> **Placeholder content.** The full hosted-MCP onboarding guide is authored in a separate task. This file exists so the page shell has something to render.

Maskin is an open-source workspace where your whole team — humans and AI agents — works together with shared memory, context, and process.

## What you'll do

1. Sign in at [maskin.sindre.ai](https://maskin.sindre.ai) and create a workspace.
2. Paste your Anthropic API key in settings.
3. Grab your Maskin API key and workspace ID.
4. Connect Claude to the hosted Maskin MCP.
5. Make your first MCP tool call.

## Connect Claude

Once you have your Maskin API key and workspace ID, run:

```sh
claude mcp add maskin \
  --transport http \
  --url https://maskin.sindre.ai/mcp \
  --header "Authorization: Bearer <YOUR_MASKIN_API_KEY>" \
  --header "X-Workspace-Id: <YOUR_WORKSPACE_ID>"
```

Then ask Claude:

> Use the maskin MCP to call `get_started`.

---

This page is rendered from [`get-started.md`](https://github.com/sindre-ai/sindre-ai.github.io/blob/main/docs/get-started/get-started.md). Edits to the markdown show up here on reload.
