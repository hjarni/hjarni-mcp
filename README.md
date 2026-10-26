<p align="center">
  <img src="docs/icon.png" alt="Hjarni" width="80" />
</p>

<h1 align="center">Hjarni</h1>

<p align="center">
  <strong>Markdown notes for you, ChatGPT, and Claude.</strong><br>
  An official, hosted MCP server for the same notes you read and edit.
</p>

<p align="center">
  <a href="https://hjarni.com">Website</a> &middot;
  <a href="https://hjarni.com/docs">Docs</a> &middot;
  <a href="https://hjarni.com/blog">Blog</a>
</p>

---

## What it does

Hjarni is a Markdown note-taking app with an official, hosted MCP server at `https://hjarni.com/mcp`. Write and edit notes in the browser or Hjarni's iPhone, iPad, Apple Silicon Mac, and Android apps. Connect ChatGPT, Claude, or another compatible MCP client to search, read, create, update, and organize those same saved notes.

Use folders, tags, wiki-links, and instructions to keep a project brief, research notebook, or second brain current across assistants. You can review saved changes in [note history](https://hjarni.com/docs/note-history), restore an earlier body, and [export active notes as Markdown with attachments](https://hjarni.com/docs/export-and-ownership).

Hjarni hosts the server; connecting does not require running a local bridge or Docker container. This repository documents that hosted service. See [client compatibility](https://hjarni.com/compatibility) for setup routes and client-specific limits.

<p align="center">
  <img src="docs/claude-memory-demo.gif" alt="Claude searching and creating notes in Hjarni" width="600" />
</p>

## Keep client context between ChatGPT and Claude

Keep each client's preferences, agreed scope, dated decisions, current status, and next action in one project brief. ChatGPT and Claude can read and update that same Markdown note through Hjarni's official, hosted MCP server.

1. Connect both assistants to the same Hjarni account using the [setup guides below](#connect). Start with the [Client Project Context template](https://hjarni.com/templates/client-project-context): it creates a project index and a blank brief to fill with facts you confirm. Keep a separate brief for each client and project.
2. Before drafting, ask the assistant to find the correct client and project, read the full current brief, and return its source link. If several notes match, have it clarify which one to use.
3. Draft proposed updates in chat first. After you confirm them, ask the assistant to save only those changes to the same brief, preserving other facts and the dates and reasons behind decisions. Open the note to check the result.
4. In a fresh chat with the other assistant, explicitly ask it to retrieve that updated brief before continuing the work. Check that it reports the new status and next action alongside the unchanged scope and preferences.

Connecting makes saved notes available; it does not guarantee retrieval or copy every conversation or the assistants' native memories. The [recorded client-context walkthrough](https://hjarni.com/blog/freelancer-client-context-chatgpt-claude) shows both assistants using the same fictional brief, with prompts to repeat the checks.

## Review, recover, and export

[Note history and Trash](https://hjarni.com/docs/note-history) let you inspect saved edits and their recorded author or AI client, compare a previous note body with the current text, and restore an earlier body as a new version. Restoring replaces the whole body, including any later edits; the current title, folder, and other fields stay unchanged. Rapid edits by the same author can be grouped into one revision. Deleted notes and folders remain recoverable in Trash for 30 days, subject to account limits. History reviews saved changes; approval before a write depends on the assistant's connection and settings.

[Export and data ownership](https://hjarni.com/docs/export-and-ownership) explains how to download active notes as a Markdown ZIP with folders and attachments, and includes a sample ZIP to inspect without an account. Export is an action in Hjarni, not an MCP tool. The standard Markdown ZIP excludes archived and trashed notes, revision history, and folder instructions; wiki links and attachment URLs may need updating in another app. Personal notes, individual folders, and teams can be exported separately.

## Connect

The endpoint is `https://hjarni.com/mcp`. Use OAuth sign-in for ChatGPT and Claude; no manually copied API token is needed. For a client that accepts an Authorization header, Hjarni also supports full-access API tokens and restricted [agent tokens](#access-and-agent-tokens).

### Claude.ai / Claude Desktop / Claude mobile

Hjarni is in the Claude Connectors Directory: [open the listing](https://claude.ai/directory/connectors/hjarni-notes), click **Connect**, and sign in.

Or add it by URL:

1. Open **Customize > Connectors** and add a custom web connector.
2. Enter the URL `https://hjarni.com/mcp`.
3. Choose OAuth sign-in, finish adding the connector, and sign in to Hjarni.

See the [Hjarni Claude guide](https://hjarni.com/docs/claude) and [Claude's current connector instructions](https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities) for account and workspace requirements. Custom connectors are available on Claude Free, with a limit of one; Team and Enterprise owners manage workspace availability.

### Claude Code

```sh
claude mcp add --transport http hjarni https://hjarni.com/mcp
```

Add `--scope user` to make it available in every project. Then run `/mcp` inside Claude Code to complete the OAuth sign-in.

### ChatGPT

Install Hjarni from its [ChatGPT directory page](https://chatgpt.com/plugins/plugin_asdk_app_69c3058914bc81919b807c176a7c106c) and sign in. See the [ChatGPT setup guide](https://hjarni.com/docs/chatgpt) for availability and usage.

If your account permits custom MCP servers, you can also add it by URL:

1. Open **Plugins**, select **+**, then **Add custom MCP server**.
2. Enter a name, the server URL `https://hjarni.com/mcp`, and **OAuth** authentication.
3. Review the connection details, create and install the plugin, and sign in to Hjarni.
4. In a new chat, select Hjarni from the `@` menu and ask it to find a saved note.

Custom-server availability and workspace controls are separate from installing the directory entry. Follow [OpenAI's current custom MCP instructions](https://developers.openai.com/api/docs/guides/custom-mcp-server) if the labels in your account differ.

### Other MCP clients

Clients need Streamable HTTP and a supported authentication method: OAuth 2.0 with PKCE or `Authorization: Bearer YOUR_API_TOKEN`. OAuth discovery is at `https://hjarni.com/.well-known/oauth-authorization-server`; protected resource metadata is at `https://hjarni.com/.well-known/oauth-protected-resource`. Features such as prompts, panels, and events depend on the client.

Setup guides: [Cursor](https://hjarni.com/docs/connect-cursor-mcp) &middot; [Copilot](https://hjarni.com/docs/connect-copilot-mcp) &middot; [Copilot Studio](https://hjarni.com/docs/connect-copilot-studio-mcp) &middot; [Perplexity](https://hjarni.com/docs/connect-perplexity-mcp) &middot; [Raycast](https://hjarni.com/docs/connect-raycast-mcp)

## Access and agent tokens

OAuth sign-in connections use the access of the connected Hjarni account, including its authorized team and shared notes. Naming one folder in a prompt or adding folder instructions does not restrict that connection's access.

For compatible clients such as Claude Code or Cursor, create an [agent token](https://hjarni.com/docs/agent-tokens) in **Settings > Connections** and grant **no access**, **read**, or **write** at a space or folder. Grants inherit down the tree and can be overridden below it; an agent cannot exceed your own access. Each token can have its own instructions and identity in history. Use the token as a Bearer credential instead of the regular OAuth connection.

Restricted tokens see a narrower tool list and cannot use account-wide management tools or the note panel. They still expose a few account-wide details, including your profile, and brain instructions unless disabled for that token; the [agent-token reference](https://hjarni.com/docs/agent-tokens) lists the exact boundaries. [Privacy and permissions](https://hjarni.com/docs/privacy-and-permissions) explains account, team, and connection access.

## Available tools

The table describes assistant-facing tools. Actual availability depends on the connection's permissions and the client's cached tool list; reconnect or refresh the server in the client after a server update.

| Tool | Description |
|------|-------------|
| `me` | Connected profile, teams, note quota, and onboarding state; restricted tokens return their grants instead of account-wide quota and onboarding |
| `dashboard-get` | Overview of the account: counts, recent notes, and recent changes across all spaces |
| `search` | Full-text search across notes, containers, and tags |
| `notes-list` | List notes with filtering by container, tags, and sorting |
| `notes-get` | Read a single note: full body, tags, links, backlinks, files, and inherited AI instructions |
| `notes-create` | Create a new note with title, body, summary, tags, and container placement |
| `notes-update` | Edit or append content, replace or append a Markdown section, move notes, change tags, archive, favorite, or mark verified |
| `notes-open` | Open an editable note panel on supported hosts, or return note data on other clients; omit the ID to open a picker |
| `notes-delete` | Move a note to Trash (recoverable for 30 days) |
| `notes-restore` | Restore a note from Trash |
| `notes-history` | Read a note's revision history: who wrote each version, when, and what changed |
| `notes-revert` | Revert a note's body to an earlier revision (appends a new revision, so it can be undone) |
| `containers-list` | List folders for organizing notes |
| `containers-get` | Get a single container with its description and AI instructions |
| `containers-create` | Create new folders |
| `containers-update` | Update a container (rename, move, change description, archive) |
| `containers-permissions` | Set or clear a team member's role on a team container |
| `containers-delete` | Move a folder, its sub-folders, and their notes to Trash (recoverable for 30 days) |
| `containers-restore` | Restore a deleted folder and everything deleted with it |
| `tags-list` | List all tags |
| `tags-create` | Create new tags |
| `tags-manage` | Rename, merge, or delete a tag |
| `links-manage` | Create or remove bidirectional links between notes |
| `instructions-get` | Read AI instructions at brain, personal root, container, or team level |
| `instructions-update` | Replace or append brain, personal-root, personal-folder, or team instructions, subject to access and owner permissions |
| `files-attach` | Attach a base64 file to a personal note |
| `files-attach_from_url` | Attach a public URL or native ChatGPT file reference to a personal note |
| `files-create_upload_url` | Generate a one-time browser upload link for an authorized personal, team, or shared note |
| `files-check_upload` | Check the status of an upload link |
| `files-get_download_url` | Get a temporary, login-free download URL; treat it as a credential while valid |
| `files-remove` | Permanently remove an attachment from a personal note |
| `email-addresses-list` | List email capture addresses |
| `email-addresses-create` | Create an email capture address: mail sent to it becomes a note, subject to account eligibility |
| `teams-list` | List all teams the user is a member of |
| `teams-get` | Get team details including recent notes |
| `teams-create` | Create a new team |
| `teams-invite` | Invite a teammate by email or get a shareable join link |
| `feedback-submit` | Send feedback about Hjarni to the maintainers |
| `nudges-dismiss` | Dismiss a product suggestion the user declined |

For edits, read the current note first and prefer targeted edits over replacing the full body. Pass its `lock_version` as `expected_lock_version` for stale-write checks. This is not a strict lock: a pure `append_body` call skips that check, and a mismatched version is accepted if the note's latest edit is attributed to the connected user and is older than 30 minutes. Check tool results before reporting success: access and limit refusals can return `ok: false` with a `status`, or `error: true` with an error message. See the [tool and permissions reference](https://hjarni.com/docs/mcp#permissions).

### Built-in prompts

The server also exposes MCP prompts for clients that support prompt discovery:

| Prompt | Description |
|--------|-------------|
| `summarize_note` | Summarize a note and suggest tags and related links |
| `weekly_review` | Review recent activity and suggest organization improvements |
| `research_topic` | Synthesize everything in the knowledge base related to a topic |

### MCP Apps

On hosts that support MCP Apps (the `io.modelcontextprotocol/ui` extension), `files-create_upload_url` can render an inline drop-zone so files upload straight into a note from the chat. Other clients get the plain upload link.

`notes-open` can show a note picker and an editor beside the conversation. In ChatGPT hosts that support Hjarni's panel extensions, the panel also supports note mentions and attaching selected text as context. Availability depends on the host and the published connection's current tool metadata. `notes-panel` and `notes-search_mentions` are app-only tools used by that interface; assistants should read with `notes-get` and edit with `notes-update`.

Clients can also read a saved note as a resource with `resources/read` and a URI such as `hjarni://notes/42`, subject to the same note-access checks. These are saved-note resources, not automatic conversation synchronization.

### Change events

Clients that support the events extension can subscribe to `note.created`, `note.updated`, and `note.deleted` (moved to Trash). Hjarni delivers notifications to a verified webhook callback, with access checked before delivery. Notifications identify the changed note; the client retrieves its content with `notes-get`.

`events/list`, `events/subscribe`, and `events/unsubscribe` are protocol methods, not tools. Delivery is webhook-only; polling and stream delivery are not supported. Events do not by themselves make every connected assistant run in the background. See the [events reference](https://hjarni.com/docs/mcp#events) and [event-triggered workflows](https://hjarni.com/docs/event-triggered-workflows).

## Usage examples

### Research assistant

> "What decisions have I made about the tech stack?"

Claude searches your notes, follows wiki-links between related notes, and synthesizes a summary from multiple sources.

### Quick capture

> "Save this as a note in my Projects folder and tag it"

Claude finds the right container, creates the note with Markdown formatting, adds tags, and links it to related notes.

### Weekly review

> "Help me triage my inbox"

Ask Claude to list unfiled notes, suggest where each belongs based on your folder structure, and wait for your approval before moving them.

### Writing with context

> "Draft a project update using my recent meeting notes"

Claude pulls relevant notes and uses them as source material.

## Features

- **Markdown notes** with full formatting support
- **Wiki-links** (`[[id:Note Title]]`) for cross-referencing
- **Folders** with custom AI instructions per folder
- **Full-text search** across all content
- **Bidirectional linking** between notes
- **Tags** for cross-cutting categorization
- **AI instructions** at brain, personal root, folder, team, and individual agent-token level
- **Note history** with per-revision attribution (you or which AI client) and revert
- **Trash** with 30-day restore for notes and folders
- **File attachments** on every plan (unlimited on Pro and Teams)
- **Email capture**: give a folder its own email address (Pro)
- **Public sharing**: view-only links for notes and folders on every plan; guest editing requires paid access
- **Agent tokens** with enforced per-space and per-folder read/write grants
- **Team collaboration** with shared knowledge bases and per-folder roles
- **iPhone, iPad, Mac & Android apps**
- **REST API** for custom integrations
- **Export** your data as Markdown at any time

## MCP server details

| | |
|---|---|
| **Endpoint** | `https://hjarni.com/mcp` |
| **Transport** | Streamable HTTP with JSON-RPC 2.0 |
| **Protocol versions** | `2025-11-25`, `2025-06-18`, `2025-03-26`, and `2024-11-05` through `initialize`; `2026-07-28` through `server/discover` (see the reference for supported methods) |
| **Authentication** | OAuth 2.0 (PKCE), full-access API token, or restricted agent token as a Bearer credential |
| **Capabilities** | Tools, prompts, note and UI resources (MCP Apps), and webhook events |

For the full protocol reference, see the [MCP server docs](https://hjarni.com/docs/mcp).

## Pricing

| Plan | Price | What you get |
|------|-------|--------------|
| **Free** | $0 | 25 personal notes, folders, tags, search, MCP & API access, view-only public links, 20 MB across 5 file attachments |
| **Pro** | $12/mo or $120/yr | Unlimited notes and file attachments, email capture, public sharing, share with 2 collaborators |
| **Teams** | $20/seat/mo or $200/seat/yr | Shared knowledge base, team MCP & API, member management, per-folder roles |

MCP and API access are included on every plan; account limits, feature eligibility, and permissions still apply. ChatGPT or Claude subscriptions are separate. Prices are also available in EUR and GBP; [see current pricing and limits](https://hjarni.com/pricing).

## Links

- [Website](https://hjarni.com)
- [Docs](https://hjarni.com/docs)
- [Getting started](https://hjarni.com/docs/getting-started)
- [MCP server reference](https://hjarni.com/docs/mcp)
- [REST API reference](https://hjarni.com/docs/api)
- [Claude setup guide](https://hjarni.com/docs/claude)
- [ChatGPT setup guide](https://hjarni.com/docs/chatgpt)
- [Blog](https://hjarni.com/blog)
- [Privacy](https://hjarni.com/privacy)
- [Terms](https://hjarni.com/terms)

## Support

Email [evert@hjarni.com](mailto:evert@hjarni.com).

---

[![MCP Badge](https://lobehub.com/badge/mcp/hjarni-hjarni-mcp)](https://lobehub.com/mcp/hjarni-hjarni-mcp)
[![hjarni MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/com.hjarni/hjarni/badges/score.svg)](https://glama.ai/mcp/connectors/com.hjarni/hjarni)
