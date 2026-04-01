# Hjarni

**Give your AI long-term memory.** Note-taking app with a built-in MCP server.

[hjarni.com](https://hjarni.com)

---

## What it does

Hjarni is an AI-native note-taking app. Write notes in Markdown, organize them in folders with custom AI instructions per folder, and let Claude or ChatGPT search, read, create, and organize your notes via MCP. Your notes serve two readers: you and your AI.

## Connect

Hjarni is a hosted remote MCP server with OAuth authentication. No API keys, no Docker, no local setup.

### Claude.ai

Settings → Connectors → Add custom connector → name "Hjarni", URL: `https://hjarni.com/mcp`

### Claude Desktop / Claude Code

```json
{
  "mcpServers": {
    "hjarni": {
      "url": "https://hjarni.com/mcp",
      "type": "streamable-http"
    }
  }
}
```

### ChatGPT

Available in the ChatGPT MCP app directory (pending approval).

## Available Tools

| Tool | Description |
|------|-------------|
| `notes-create` | Create a new note with title, body, tags, and container placement |
| `notes-get` | Read a single note including full content, tags, and linked notes |
| `notes-list` | List notes with filtering by container, tags, and sorting |
| `notes-update` | Update content, move notes, change tags, archive/unarchive |
| `notes-delete` | Permanently delete a note |
| `search` | Full-text search across notes, containers, and tags |
| `containers-list` | List folders for organizing notes |
| `containers-create` | Create new folders |
| `containers-get` | Get a single container with its AI instructions |
| `containers-update` | Update a container (rename, move, change description) |
| `tags-list` | List all tags |
| `tags-create` | Create new tags |
| `links-manage` | Create or remove bidirectional links between notes |
| `instructions-get` | Read AI instructions set on a folder |
| `instructions-update` | Update folder-level AI instructions |
| `files-attach` | Attach a file to a note |
| `files-attach_from_url` | Fetch a file from a URL and attach it to a note |
| `files-get_download_url` | Get a temporary download URL for a file |
| `files-remove` | Remove a file attachment |
| `dashboard-get` | Overview of the account: note count, containers, tags, inbox |
| `teams-list` | List all teams the user is a member of |
| `teams-get` | Get team details including recent notes |

## Example prompts

- "What notes do I have about [topic]?"
- "Save this as a note in my Projects folder"
- "Summarize my meeting notes from this week"
- "Link the project brief to the roadmap"
- "What's tagged 'launch'?"

## Features

- Markdown notes
- Wiki-links (`[[id:Note Title]]`)
- Folders with custom AI instructions
- Full-text search
- Bidirectional linking
- Team collaboration
- File attachments
- Free tier — 25 notes with full MCP access

## Pricing

| Plan | Price |
|------|-------|
| Free | 25 notes, full MCP access |
| Pro | €9 / £8 / $10 per month |
| Team | €12 / £10 / $13 per seat/month |

## Links

- [Website](https://hjarni.com)
- [Docs](https://hjarni.com/docs)
- [Blog](https://hjarni.com/blog)
- [Privacy](https://hjarni.com/privacy)
- [Terms](https://hjarni.com/terms)
