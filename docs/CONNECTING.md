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
`update_job`, `create_post`, `request_resume_upload_link`, `upload_resume`,
`list_resumes`, `list_cover_letters`, `save_cover_letter`,
`get_cover_letter`, `apply_to_job`). `search_jobs` works for guests
without logging in.

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
| `search_jobs` | No | Semantic search, ranked by resume-match score if a resume is supplied. |
| `create_job` | Yes | Creates a posting for your company from a natural-language request. |
| `update_job` | Yes | You must own the job. Only the fields you provide are changed. |
| `create_post` | Yes | Publishes a text post to your Dintak feed. Goes through moderation before becoming visible to others. |
| `request_resume_upload_link` | Yes | Returns a one-time link to upload a resume file in your own browser (preferred over pasting resume text in chat). |
| `upload_resume` | Yes | Uploads a resume file provided in-chat (base64) to your Dintak account. |
| `list_resumes` | Yes | Lists your uploaded resumes so you can reuse one instead of re-uploading. |
| `list_cover_letters` | Yes | Lists your saved cover letters. |
| `save_cover_letter` | Yes | Saves a cover letter for reuse across applications. |
| `get_cover_letter` | Yes | Fetches the full text of a saved cover letter by id. |
| `apply_to_job` | Yes | Applies to a Dintak job (optionally with a resume/cover letter), or forwards to an external application URL when the posting is external. |

## Full documentation

For a complete walkthrough with screenshots and example prompts, see
https://www.dintak.com/mcp-docs.

## Questions

team@dintak.com
