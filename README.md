# Dintak MCP Gateway

Public remote **MCP (Model Context Protocol)** server that connects Claude
(Claude Desktop, claude.ai, and Claude-API agents), ChatGPT, and other
MCP-compatible clients to [Dintak](https://www.dintak.com)'s job platform —
semantic job search, job posting, and applying to jobs, with resume-to-job
match scoring.

> **This repository is a public documentation mirror.** It intentionally
> contains only the README and the MCP server manifest (`server.json`) —
> no source code, infrastructure/deploy configuration, or credentials.
> It exists so MCP directories that require a public GitHub repository
> (glama.ai, mcpfind.org, etc.) can discover and verify this listing.

## Connect

- **MCP endpoint:** `https://mcp.dintak.com/mcp` (streamable-http transport)
- **Full docs & setup instructions** (Claude Desktop, claude.ai, ChatGPT,
  Python client): https://www.dintak.com/mcp-docs

A generic remote-MCP client config looks like:

```json
{
  "mcpServers": {
    "dintak": {
      "url": "https://mcp.dintak.com/mcp"
    }
  }
}
```

See the docs page above for the exact, up-to-date snippets for your client.

## Tools exposed

| Tool | Description |
| --- | --- |
| `search_jobs` | Guest-allowed. Semantic (vector-embedding) job search, ranked by resume-fit match score when a resume is on file. Optional filters: location, job type, workplace (remote/hybrid/on-site), career level, salary range. |
| `create_job` | Requires a connected Dintak account. Creates a job posting on behalf of the authenticated user's company. |
| `update_job` | Requires a connected Dintak account. Updates a job posting the caller owns. |
| `apply_to_job` | Requires a connected Dintak account. Submits an application to a Dintak-hosted job, or forwards to an external job when the posting's application method is external and a source URL is provided. |

## Authentication

OAuth 2.1, authenticating through Dintak's own authorization server
(magic-link login today; Google and Apple sign-in planned). No API key
or credential is embedded anywhere in this repository — clients
authenticate interactively in a browser, and Dintak issues short-lived
tokens scoped to the connecting agent.

## Learn more

- Docs: https://www.dintak.com/mcp-docs
- Website: https://www.dintak.com
- Contact: team@dintak.com

See [`server.json`](./server.json) for the machine-readable MCP server
manifest, and [`docs/CONNECTING.md`](./docs/CONNECTING.md) for a quick
connection walkthrough.
