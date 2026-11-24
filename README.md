<p align="center"><img src="logo.png" width="96" alt="1Job logo"></p>

# 1Job MCP server

Ask your AI about your job applications.

[1Job](https://1job.app) keeps every job you apply to: the posting as it was when you applied, the
answers you submitted, the resume you sent, status history, notes and reminders (captured by the 1Job
browser extension). This MCP server lets Claude, ChatGPT, Cursor, Gemini CLI, Cline, VS Code and
other MCP clients work with that history.

- "Which applications have had no answer for two weeks?"
- "Brief me on the Acme role before my interview."
- "Mark the Globex one as rejected."

It is a hosted (remote) server. There is nothing to install or run:

```
https://api.1job.app/mcp
```

Transport: Streamable HTTP. Sign-in: OAuth (your 1Job email plus a 6-digit code). Free for every
1Job account.

## Before you start

1. A free 1Job account and the [1Job browser extension](https://1job.app).
2. Cloud sync turned on in the extension (Settings), so your applications are in your account.

## Connect

**Claude**: Settings, Connectors, add 1Job (or Add custom connector with
`https://api.1job.app/mcp`).

**Claude Code**

```sh
claude mcp add --transport http 1job https://api.1job.app/mcp
```

Then run `/mcp`, pick `1job` and Authenticate.

**Cursor**: add to `~/.cursor/mcp.json`, then click Needs login next to 1job in MCP settings:

```json
{ "mcpServers": { "1job": { "url": "https://api.1job.app/mcp" } } }
```

**Gemini CLI**

```sh
gemini extensions install https://github.com/c-office/1job-mcp
```

Or add to `~/.gemini/settings.json`:

```json
{ "mcpServers": { "1job": { "httpUrl": "https://api.1job.app/mcp" } } }
```

**VS Code / Cline / Windsurf / Codex / others**: add a remote (HTTP) MCP server with the address
`https://api.1job.app/mcp`. Clients that support MCP sign-in need only the address. Clients without
sign-in can send a personal access token from the extension (Settings, Connected apps) as
`Authorization: Bearer <token>`. Treat a token like a password.

## Tools

| Tool                      | Kind  | What it does                                                         |
| ------------------------- | ----- | -------------------------------------------------------------------- |
| List applications         | Read  | Newest first, filter by status, date or company                      |
| Get application           | Read  | The posting as it was, your answers, resume names, history and notes |
| Search applications       | Read  | Search company, title, description and notes                         |
| Pipeline stats            | Read  | Counts by status, response rate, time to first answer                |
| Follow-ups due            | Read  | Applications with no change for a number of days                     |
| Get resume download links | Read  | A link to the exact PDF you sent, valid for 10 minutes               |
| List reminders            | Read  | Your reminders, soonest first                                        |
| Job detail corrections    | Read  | Every correction to an application's job details                     |
| List resumes              | Read  | Names and ids of your resume and cover-letter PDFs, never the files  |
| Update application status | Write | New status, added to the history with who made the change            |
| Record application        | Write | Record an application an agent submitted for you                     |
| Add note                  | Write | Adds a dated note                                                    |
| Correct job details       | Write | Fixes title, company, location or description; originals are kept    |
| Set / complete reminder   | Write | Create a reminder or mark it done                                    |

Writes never delete anything and never change or upload files. Choose read-only on the consent page
if that is enough. Prompts: role brief, company brief, interview prep and weekly review.

## Privacy

The server sees the copy of your applications that cloud sync keeps. It never receives anything that
is only on your computer, and gets a resume file only when you ask, through a link that works for 10
minutes. Disconnect an app or revoke a token any time in the extension (Settings, Connected apps).
See the [privacy policy](https://1job.app/privacy/) and [full guide](https://1job.app/mcp/).

Questions: support@1job.app
