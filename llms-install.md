# Installing the 1Job MCP server

1Job is a hosted remote MCP server. Do not clone, build or run anything.

Add this server to the MCP settings:

```json
{
  "mcpServers": {
    "1job": {
      "type": "streamableHttp",
      "url": "https://api.1job.app/mcp"
    }
  }
}
```

The server uses OAuth. On first use the client opens a 1Job sign-in page; the user enters their 1Job
email address and the 6-digit code emailed to them, then approves access.

If the client does not support MCP OAuth, ask the user for a personal access token from the 1Job
extension (Settings, Connected apps) and add it as a header:

```json
{
  "mcpServers": {
    "1job": {
      "type": "streamableHttp",
      "url": "https://api.1job.app/mcp",
      "headers": { "Authorization": "Bearer <token>" }
    }
  }
}
```

Prerequisites for the user: a free 1Job account (https://1job.app) with cloud sync turned on in the
extension. Questions: support@1job.app
