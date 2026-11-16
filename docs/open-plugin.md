# easyrender plugin

Turn a product photo into a textured GLB model with easyrender. The skill guides
the agent through a free preview and an approved paid build using account credits.

## Package layout

[Open Plugins](https://open-plugins.com) now redirects to the
[Agent Plugins specification](https://agent-plugins.org/specification).
This package targets version 1.0.0:

- `plugin.json` identifies the plugin as `easyrender`.
- `mcp.json` declares the remote Streamable HTTP server in the portable format.
- `.mcp.json` supplies the same endpoint for clients and directory scanners that
  use that filename and URL-based remote configuration.
- `skills/easyrender-image-to-3d/SKILL.md` contains the existing workflow, with its
  own `references/` and `agents/openai.yaml` so it can be installed independently.

[Cursor Directory](https://cursor.directory/plugins/new) can discover the MCP
configuration and the skill at these paths. Directory submission and approval
are separate from adding these files to the repository.

## Authentication

Both bundled configurations point to `https://easyrender.ai/api/mcp` and leave
credentials to the client. Use its OAuth sign-in flow; setup instructions are at
[easyrender MCP](https://easyrender.ai/mcp#connect). Installing the package does
not sign in, generate an asset or authorize spending.

For an API key instead, obtain an `er_` key from
[account connectors](https://easyrender.ai/connectors) and make it available to
the client as the `EASYRENDER_API_KEY` environment variable. Keep the value out
of this repository and chat.

In Cursor's **local** `.cursor/mcp.json` or `~/.cursor/mcp.json`, merge this entry
into `mcpServers`, replacing an existing `easyrender` entry if present:

```json
{
  "mcpServers": {
    "easyrender": {
      "url": "https://easyrender.ai/api/mcp",
      "headers": {
        "Authorization": "Bearer ${env:EASYRENDER_API_KEY}"
      }
    }
  }
}
```

This is [Cursor-specific environment interpolation](https://cursor.com/docs/context/mcp#config-interpolation).
Ensure the variable is available to the Cursor process. Other clients may use
different credential settings. The portable Agent Plugins v1 `mcp.json` does not
expand environment variables in headers, so keep this override in the client's
configuration. Use one connection for this endpoint to avoid duplicate tools.

## Existing skill installs

The root `SKILL.md`, `references/`, `agents/openai.yaml` and
`gemini-extension.json` retain their existing paths and contents. The root
package remains available to skills.sh and ClawHub installers. The plugin skill
reuses that workflow with generic wording for unsupported outputs; its linked
references and agent metadata are copied without changes.

When maintaining the workflow, update both skill entrypoints and copy supporting
resource changes into `skills/easyrender-image-to-3d/`. Keep the plugin skill's
relative links within its own directory so clients that copy only that skill
still receive the full instructions.
