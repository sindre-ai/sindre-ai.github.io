# Get started with *Maskin*

Maskin is an open-source workspace where your whole team — humans and AI agents — works together with shared memory, context, and process. This guide connects Claude to the hosted Maskin MCP so you can drive a workspace from inside Claude Code or Claude Desktop. Expect to spend about five minutes.

## Prerequisites

- **[Claude Code](https://docs.claude.com/en/docs/claude-code/overview)** or **[Claude Desktop](https://claude.ai/download)** installed.
- An **[Anthropic API key](https://console.anthropic.com/settings/keys)**. Maskin runs Claude Code in sandboxes on your behalf and uses this key to authenticate those runs.

You don't need to clone anything, install dependencies, or run a local server. Maskin is hosted at [`maskin.sindre.ai`](https://maskin.sindre.ai).

## Automated setup (Claude runs it)

Click **Open in Claude** at the top of this page. A pre-filled prompt opens in Claude Code (or Claude Desktop) that tells Claude to drive the setup end-to-end — no copy-pasting commands.

You still do the browser-auth steps below (Steps 1–3) because they require signing in and pasting your Anthropic API key into the Maskin UI. Then Claude takes over and runs Steps 4–5 for you.

1. **You:** do Steps 1–3 in the Maskin UI. Have your Maskin API key (`ank_…`) and workspace ID (UUID) ready.
2. **Claude:** asks you for those two values, then runs `claude mcp add maskin …` with the right headers. In Claude Code it runs `/reload-plugins`; in Claude Desktop it tells you to restart the app. Then it calls the `get_started` MCP tool.
3. **You:** pick a template (development / growth / custom). Claude applies it, seeds the workspace, and kicks off the pipeline.

Prefer to wire it by hand? Follow the numbered steps below — they produce the same result.

## Step 1 — Sign in and create a workspace

1. Go to [**maskin.sindre.ai**](https://maskin.sindre.ai) and sign in.
2. Create your first workspace from the prompt. A workspace is an isolated environment with its own objects, actors, and settings — you can create more later.

Once you're in, you'll see the unified pipeline view: **Insights → Bets → Tasks**. All work — yours and your agents' — lives as objects in this pipeline.

## Step 2 — Paste your Anthropic API key

Maskin needs your Anthropic API key to run agent sessions in its sandboxes. Keys are stored encrypted and scoped to the workspace.

1. Open **Settings → Integrations** (or **Settings → LLM keys**) from the workspace sidebar.
2. Paste your Anthropic API key and **Save**. Maskin validates the key with a cheap call to Anthropic before storing it.
3. You can update or remove the key from the same screen at any time. After save, only the last four characters are shown.

## Step 3 — Get your Maskin API key and workspace ID

To let Claude talk to your workspace, you need two values from the UI:

1. Open **Settings → API keys** and click **Create key**. Copy the `ank_…` value that appears — this is your **Maskin API key**. You'll only see it once.
2. Open **Settings → Workspace** and copy the **Workspace ID** (UUID). This tells the MCP which workspace to act on.

Keep both values handy for the next step.

## Step 4 — Connect Claude to the hosted Maskin MCP

### Claude Code

From a terminal, run:

```sh
claude mcp add maskin \
  --transport http \
  --url https://maskin.sindre.ai/mcp \
  --header "Authorization: Bearer <YOUR_MASKIN_API_KEY>" \
  --header "X-Workspace-Id: <YOUR_WORKSPACE_ID>"
```

Replace `<YOUR_MASKIN_API_KEY>` with the `ank_…` key from Step 3 and `<YOUR_WORKSPACE_ID>` with the workspace UUID.

If Claude Code is already running, reload plugins so the new tools show up in the current session:

```sh
/reload-plugins
```

### Claude Desktop

Open your Claude Desktop MCP config (`Settings → Developer → Edit config`) and add the `maskin` entry:

```json
{
  "mcpServers": {
    "maskin": {
      "type": "http",
      "url": "https://maskin.sindre.ai/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_MASKIN_API_KEY>",
        "X-Workspace-Id": "<YOUR_WORKSPACE_ID>"
      }
    }
  }
}
```

Save the file and restart Claude Desktop.

## Step 5 — Make your first MCP call

Back in Claude Code or Claude Desktop, ask:

> Use the maskin MCP to call `get_started`.

`get_started` is the entry-point tool. It previews and applies a workspace template — either **development** (for shipping a product), **growth** (for running a launch or outreach pipeline), or **custom** (a short questionnaire that tailors the workspace to whatever you're working on). Once you pick one, Claude seeds the workspace with object types, statuses, custom fields, and a first set of objects, and kicks off the pipeline.

If the tool returns a response without errors, you're connected. From here Claude can create and update insights, bets, and tasks, run triggers, and stream events directly against your hosted workspace.

## What's next

- **Invite teammates.** Workspaces support multiple members — add humans and agents from **Settings → Members**.
- **Wire up integrations.** Connect Slack, GitHub, Google Calendar, and more from **Settings → Integrations** to let agents react to real-world events.
- **Explore the 39 MCP tools.** `get_started` is just the start — list objects, create bets, fire triggers, and manage agent sessions all from Claude. Run `list_tools` to see the full set.

---

Stuck? Open an issue in [`sindre-ai/maskin`](https://github.com/sindre-ai/maskin/issues) or read the [README](https://github.com/sindre-ai/maskin#readme) for deeper background on the data model, agent sessions, and the event stream.
