<p align="center">
  <img src="assets/logo.png" alt="ClerkChat" width="96" height="96">
</p>

<h1 align="center">ClerkChat MCP server</h1>

<p align="center">
  Run your ClerkChat AI support agents from Claude, ChatGPT, Cursor or any MCP client.<br>
  <a href="https://clerkchat.co">clerkchat.co</a> · <a href="https://clerkchat.co/docs">Docs</a> · <a href="https://clerkchat.co/contact">Support</a>
</p>

---

[ClerkChat](https://clerkchat.co) is an AI agent that answers a business's customers on WhatsApp, Instagram, Messenger, Telegram, a website widget and a hosted help page, trained on the business's own website, files, Google Docs and Sheets, Notion pages and YouTube videos.

This MCP server lets your AI assistant work in your ClerkChat workspace for you: create and train agents, connect channels, read and reply to customer conversations, manage automations and leads, and pull analytics.

This repository holds documentation only. The server is hosted by ClerkChat; there is nothing to install or run.

## Endpoint

```
https://mcp.clerkchat.co/mcp
```

| | |
|---|---|
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1 with dynamic client registration (PKCE) |
| Scopes | `mcp:read`, `mcp:write`, `offline_access` |
| Account | A ClerkChat account ([free plan available](https://clerkchat.co/pricing)) |

When you connect, ClerkChat asks you to sign in and choose which workspaces the assistant may access. You can change workspace access or revoke a client at any time from **MCP** in the ClerkChat dashboard.

## Connect

### Claude (claude.ai and Claude Desktop)

1. Open **Settings → Connectors → Add custom connector**.
2. Name it `ClerkChat` and enter `https://mcp.clerkchat.co/mcp`.
3. Connect, sign in to ClerkChat, choose your workspaces and approve.

### Claude Code

```bash
claude mcp add --transport http clerkchat https://mcp.clerkchat.co/mcp
```

Then run `/mcp` in Claude Code to sign in.

### ChatGPT

In ChatGPT, add a custom MCP connector (developer mode) with the URL `https://mcp.clerkchat.co/mcp` and OAuth authentication, then sign in and approve your workspaces.

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "clerkchat": {
      "url": "https://mcp.clerkchat.co/mcp"
    }
  }
}
```

Cursor opens the ClerkChat sign-in the first time a tool is used.

### Other MCP clients

Any client that supports remote Streamable HTTP servers with OAuth can connect to `https://mcp.clerkchat.co/mcp`. The server publishes discovery metadata at `/.well-known/oauth-protected-resource/mcp`.

## Try it

- "List the agents in my ClerkChat workspace."
- "Create a support agent called Store support and train it on https://example.com."
- "Add this PDF to Store support." (attach the file)
- "Show me unread WhatsApp conversations from today and draft replies."
- "Take over the conversation with Sarah and reply that her order ships tomorrow."
- "Export this week's leads from the Collect Leads automation."
- "How many conversations did each agent handle in the last 30 days?"

## Tools

<details>
<summary><b>Workspaces and agents</b></summary>

`list_workspaces` · `list_agents` · `get_agent` · `create_agent` · `update_agent` · `duplicate_agent` · `archive_agent` · `transfer_agent` · `share_agent_template` · `get_public_agent_template` · `upload_agent_avatar` · `remove_agent_avatar`
</details>

<details>
<summary><b>Knowledge sources</b></summary>

`list_sources` · `get_source` · `get_source_status` · `add_website_source` · `add_text_source` · `add_knowledge_source` · `add_document_source` · `update_source` · `process_source` · `archive_source`

Documents (PDF, TXT, MD, CSV, TSV, JSON, XLS, XLSX, up to 8 MiB) are sent through MCP. No browser upload is needed.
</details>

<details>
<summary><b>Channels and integrations</b></summary>

`get_channel_status` · `start_channel_connection` · `connect_telegram` · `connect_whatsapp_cloud_api` · `start_whatsapp_embedded_signup` · `complete_whatsapp_embedded_signup` · `register_whatsapp_phone` · `get_integration` · `start_integration_oauth` · `disconnect_integration` · `connect_stripe_restricted_key` · `update_stripe_integration` · `list_slack_channels` · `update_slack_integration` · `test_slack_integration` · `list_helpdesk_ticket_types` · `set_helpdesk_ticket_type`

Supported providers: WhatsApp, Instagram, Messenger, Telegram, Slack, Notion, Shopify, Stripe, Intercom and Zendesk. Provider sign-in (OAuth) completes in your browser. Credentials you send are write-only and never returned.
</details>

<details>
<summary><b>Conversations</b></summary>

`list_conversations` · `get_conversation` · `get_conversation_messages` · `reply_to_conversation` · `draft_conversation_reply` · `translate_conversation_message` · `takeover_conversation` · `release_conversation` · `assign_conversation` · `unassign_conversation` · `set_conversation_status` · `set_conversation_priority` · `set_conversation_category` · `mark_conversation_read` · `mark_conversation_unread` · `get_conversation_unread_summary` · `get_workspace_conversation_unread_summary` · `get_conversation_assignment_settings` · `update_conversation_assignment_settings` · `get_conversation_notification_settings` · `update_conversation_notification_settings`
</details>

<details>
<summary><b>Automations and leads</b></summary>

`list_automations` · `get_automation` · `create_automation` · `update_automation` · `delete_automation` · `enable_automation` · `disable_automation` · `list_automation_runs` · `get_automation_run` · `list_automation_leads` · `export_automation_leads` · `mark_automation_leads_read` · `get_workspace_lead_notifications`
</details>

<details>
<summary><b>Deployment and analytics</b></summary>

`get_deployment_settings` · `update_deployment_settings` · `get_widget_embed` · `get_analytics_summary` · `get_agent_analytics` · `get_workspace_analytics`
</details>

## Permissions and safety

- The assistant can only reach the workspaces you approve, with the role and plan you already have in each.
- Write tools take idempotency keys, so a retried request is not applied twice.
- Secrets such as API keys and bot tokens are accepted but never returned in tool output.
- Revoke a client or remove a workspace from **MCP** in the ClerkChat dashboard. Access stops on the next tool call.

## Links

- Website: https://clerkchat.co
- Setup guide: https://clerkchat.co/docs
- Privacy: https://clerkchat.co/privacy
- Terms: https://clerkchat.co/terms
- Support: https://clerkchat.co/contact
