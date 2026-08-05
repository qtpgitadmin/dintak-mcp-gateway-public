# Connecting to the Dintak MCP Gateway

The Dintak MCP Gateway is a hosted remote MCP server — there is nothing to
install or run yourself. Point any MCP-compatible client at the endpoint
below and complete the OAuth login prompt when it appears.

- **Endpoint:** `https://mcp.dintak.com/mcp`
- **Transport:** streamable-http
- **Auth:** OAuth 2.1 (interactive browser login via Dintak's magic-link flow)

## Claude Desktop / claude.ai

Add a remote connector pointing at the endpoint above, or add it to your
MCP client config:

```json
{
  "mcpServers": {
    "dintak": {
      "url": "https://mcp.dintak.com/mcp"
    }
  }
}
```

You'll be redirected to Dintak to log in (or create an account) the first
time you use a tool that requires authentication (`create_job`,
`update_job`, `apply_to_job`). `search_jobs` works for guests without
logging in.

## ChatGPT / other MCP clients

Use the official "Add a connector" (or equivalent) flow in your client and
supply the same endpoint URL. Any client that speaks the MCP
streamable-http transport and OAuth 2.1 will work.

## Programmatic / Python clients

Any standard MCP Python client (e.g. the official `mcp` SDK) can connect
using the same URL and will be walked through the same OAuth login the
first time a gated tool is called.

## Tools

| Tool | Auth required | Notes |
| --- | --- | --- |
| `search_jobs` | No | Semantic search, ranked by resume-match score if you have a resume on file. |
| `create_job` | Yes | Creates a posting for your company. |
| `update_job` | Yes | You must own the job. |
| `apply_to_job` | Yes | Applies to a Dintak job, or forwards to an external application URL when the posting is external. |

## Full documentation

For a complete walkthrough with screenshots and example prompts, see
https://www.dintak.com/mcp-docs.

## Questions

team@dintak.com
