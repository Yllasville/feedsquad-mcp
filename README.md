> **Archived (2026-10-22).** This repository is no longer maintained. The FeedSquad plugin for Claude and ChatGPT lives at [Feedsquad/feedsquad-plugin](https://github.com/Feedsquad/feedsquad-plugin). Connector docs: [feedsquad.com/docs/mcp](https://feedsquad.com/docs/mcp). The MCP server runs at `https://feedsquad.com/api/mcp`.

# FeedSquad MCP Server

**A content calendar your AI can drive.** Connect FeedSquad from Claude, ChatGPT, Cursor, or any MCP client and your assistant can draft posts, build multi-week campaigns, find publishing slots that respect per-platform cadence rules, and publish to **LinkedIn, X, and Threads** through official APIs.

> This is the documentation repo for the hosted server. The server itself runs at `https://feedsquad.com/api/mcp` — there is nothing to install or self-host.

## Install

**Claude Code**

```bash
claude mcp add feedsquad https://feedsquad.com/api/mcp
```

**Claude.ai / Claude Desktop** — Settings → Connectors → Add custom connector → `https://feedsquad.com/api/mcp`

**Cursor / other MCP clients** — streamable HTTP:

```json
{
  "mcpServers": {
    "feedsquad": {
      "url": "https://feedsquad.com/api/mcp"
    }
  }
}
```

Auth is **OAuth 2.1 + PKCE with dynamic client registration** — your client opens a sign-in window on first use. No API keys, no developer apps.

## Why it's different

- **Approval-first** — every post your agent drafts requires an explicit confirm before it goes live. Drafts are the default state.
- **Anti-slop gate** — drafts are checked against a published banned-pattern registry ([the rules](https://feedsquad.com/anti-slop)) before they can be scheduled.
- **Cadence guardrails** — per-platform daily caps and enforced spacing, server-side. Your agent cannot flood a feed.
- **Campaigns as a unit** — multi-week arcs generated, reviewed, and confirmed together.

## Tools

| Tool | What it does |
|---|---|
| `create_post` | FeedSquad's primary publishing tool |
| `create_posts` | FeedSquad's batch publishing primitive |
| `create_campaign` | Create a content campaign with multiple posts |
| `confirm_post` | Approve a draft post (go live, ship it, schedule for publishing) or cancel to delete the draft |
| `confirm_campaign` | Approve all or cancel all posts in a campaign. |
| `publish_post` | Publish a post immediately |
| `delete_post` | Delete a draft or scheduled post |
| `get_calendar` | View your scheduled content |
| `get_usage` | Account-management read: current-month posting usage, plan tier, and rate-limit status for the authenticate... |
| `get_help` | Task-oriented prose help |
| `get_plans` | Account-management read: FeedSquad subscription pricing tiers and upgrade URLs |
| `connect_platform` | Connect a social media platform (LinkedIn, X/Twitter, or Threads) to your FeedSquad account |
| `update_post` | Edit a draft or scheduled post in place |
| `reschedule_post` | Move a post to a new scheduled time |
| `search_posts` | Find posts by keyword across content + title, with optional filters (platforms, statuses, date range, campa... |
| `get_post` | Fetch a single post by id with optional expansions |
| `adapt_for_platform` | Take one draft and return platform-tuned versions for each requested platform (LinkedIn / X / Threads) |
| `get_calendar_health` | Return derived signals over your content calendar: clusters (3+ posts in 4h), gaps (>72h between scheduled)... |
| `get_performance_insights` | What's working, best posts, top-performing content, engagement winners |
| `set_post_image` | Attach an image to a draft or scheduled post by URL |
| `list_accounts` | List the posting accounts the authenticated user can publish to: their personal LinkedIn / X / Threads (eac... |
| `capabilities` | What is FeedSquad / what can this do / show me the tool set |
| `find_next_slot` | When can I post next? When's my next available slot? Find me 3 slots Tuesday afternoon for LinkedIn |

Machine-readable metadata: [`/.well-known/mcp/server-card.json`](https://feedsquad.com/.well-known/mcp/server-card.json) · [registry entry `com.feedsquad/feedsquad`](https://registry.modelcontextprotocol.io)

## Links

- Product page: https://feedsquad.com/mcp
- Docs: https://feedsquad.com/docs/mcp
- LLM-readable summary: https://feedsquad.com/mcp.md
- How it compares (Buffer MCP, Typefully, Postiz): https://feedsquad.com/compare/buffer-mcp
- Pricing: https://feedsquad.com/pricing (free tier — 10 posts/mo)
- Support: support@feedsquad.com
