# StealthGPT MCP

![StealthGPT](assets/icon.png)

Connect Gemini CLI, Cursor, Grok Build, and other MCP clients to StealthGPT's hosted writing tools.

**Server URL:** `https://www.stealthgpt.ai/api/mcp/mcp`  
**Transport:** Streamable HTTP  
**Authentication:** Sign in to your StealthGPT account with OAuth.

## Account and billing

You need a StealthGPT account with available subscription usage or API credits. API accounts must complete their API onboarding. Runs use the account's applicable StealthGPT subscription or API balance and billing settings.

When your MCP client requests authorization, open the browser sign-in flow, sign in to StealthGPT, and approve access. Supported clients discover the OAuth endpoints and register their client automatically. Each user authorizes their own account.

API pay-as-you-go requires the user to complete StealthGPT's billing setup. Review any payment or usage terms before enabling it.

[Account](https://www.stealthgpt.ai/signin) · [API plans](https://www.stealthgpt.ai/stealthapi) · [MCP documentation](https://docs.stealthgpt.ai/api-reference/integrations/mcp)

## Tools

| Tool | Purpose |
| --- | --- |
| `humanize_text` | Start a rewrite of existing text, with model, quality, and plain-text or Markdown output options. |
| `generate_content` | Start an academic, SEO, or social content draft. Social drafts support LinkedIn and Medium. Fact-checking and image generation are optional. |
| `get_run_status` | Retrieve progress and the completed result for a run owned by the signed-in account. |
| `enable_pay_as_you_go` | Retrieve billing status and, when needed, a setup link that the user completes in their browser. |

`humanize_text` and `generate_content` return a `runId`. Use `get_run_status` with that returned ID until the run is `completed`, `failed`, or `cancelled`. Display the finished result or the reported error. Content generation produces drafts; publishing to external services is outside these tools' capabilities.

## Gemini CLI

Install the extension:

```sh
gemini extensions install https://github.com/StealthGPT/stealthgpt-mcp
```

Start Gemini CLI. If authorization is required, run:

```text
/mcp auth stealthgpt
```

Complete the StealthGPT browser sign-in flow. The root `gemini-extension.json` configures the hosted server directly.

[Gemini CLI extension documentation](https://geminicli.com/docs/extensions/) · [MCP and OAuth setup](https://geminicli.com/docs/tools/mcp-server/)

## Cursor

The Cursor plugin manifest is `.cursor-plugin/plugin.json`. It explicitly loads the shared `.mcp.json` server configuration.

For a manual connection, add this server to your project's `.cursor/mcp.json` or your user-level `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "stealthgpt": {
      "url": "https://www.stealthgpt.ai/api/mcp/mcp"
    }
  }
}
```

Open Cursor's MCP settings, connect StealthGPT, and complete the browser authorization flow when prompted.

[Cursor MCP documentation](https://cursor.com/docs/mcp) · [Cursor plugin reference](https://cursor.com/docs/reference/plugins)

## Grok Build

The Grok Build plugin manifest is `.grok-plugin/plugin.json`, with its server configuration in `.mcp.json`.

For a manual connection:

```sh
grok mcp add --transport http stealthgpt https://www.stealthgpt.ai/api/mcp/mcp
```

Grok Build opens the OAuth browser flow when authorization is required. Use `grok mcp list` or `grok mcp doctor stealthgpt` to inspect the connection.

[Grok Build MCP documentation](https://docs.x.ai/build/features/mcp-servers) · [Plugins and marketplaces](https://docs.x.ai/build/features/skills-plugins-marketplaces)

## Other MCP clients

Add the server URL using Streamable HTTP and complete your client's OAuth connection flow. The hosted server supports OAuth discovery and dynamic client registration. Account eligibility, available tools, and usage limits are enforced by StealthGPT.

Example requests:

- Humanize this paragraph using the standard model and return plain text.
- Draft an SEO article about neighborhood tool libraries, with fact-checking and image generation disabled.
- Draft a LinkedIn post announcing a community repair workshop, then retrieve the completed draft.

## Help and service terms

[API support](https://docs.stealthgpt.ai/api-reference/introduction#need-help) · [Privacy Policy](https://www.stealthgpt.ai/privacy) · [Terms of Service](https://www.stealthgpt.ai/tos)
