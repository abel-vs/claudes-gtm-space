---
name: notion-gtm
description: Manage GTM (Go-To-Market) content in Notion. Use when working with GTM documentation, playbooks, templates, meeting notes, or any content in the GTM workspace. Only operates within the GTM page hierarchy.
allowed-tools:
  - mcp__notion
  - Read
  - Write
  - Grep
  - Glob
---

# Notion GTM Skill

This skill provides guidance for working with GTM (Go-To-Market) content in Notion. It is scoped exclusively to the GTM page and its subpages.

## Scope Restriction

**IMPORTANT: This skill ONLY operates within the GTM page hierarchy in Notion.**

Before performing any operation:
1. Verify the target page is within the GTM workspace
2. Never create, modify, or delete pages outside the GTM hierarchy
3. When searching, focus results on GTM-related content

If asked to work with content outside GTM, politely decline and explain this skill is scoped to GTM only.

## GTM Notion Structure

The Notion GTM page serves as the **document database** for strategy, processes, and research. NOT for transactional CRM data (that lives in Attio).

### Current Structure (as of Dec 2025)

```
🤑 GTM
├── 📕 Sales Handbook ─ Master sales process & methodology
│   ├── Funnel ─ How our funnel works
│   └── Prospecting ─ How we prospect (process, not data)
├── 🌝 ICP ─ Ideal Customer Profile (current + archive)
├── 🏭 Industries [database] ─ Industries we can serve
├── 🚁 Use Cases [database] ─ Workflows (existing & potential)
├── ⚙️ Automations ─ GTM automation ideas/todos
├── 🧪 Research ─ Deep dives on industries/topics
├── 💬 Copy & Messaging ─ Sales copy, blurbs, templates
├── 🎫 Conferences & Events [database] ─ Event tracking
├── 💡 Ideas ─ Conceptual ideas & potential actions
│   └── Affiliate Strategy
└── 📦 Archive ─ Deprecated pages (CRM stuff moved to Attio)
```

### Page Purposes

| Page | Purpose |
|------|---------|
| **Sales Handbook** | Formalized approach to GTM - phases, processes, how we do things. The master reference for sales methodology. |
| **ICP** | Who are our ICPs, why we chose them, validated vs unvalidated profiles, and archived/historical ICPs. |
| **Industries** | Different industries we think we could serve. Database of target verticals. |
| **Use Cases** | Workflows we have OR potential workflows discovered through customer conversations. |
| **Automations** | GTM workflow automation ideas as a todo list. Things we want to automate. |
| **Research** | Deep dives on industries or GTM-related topics. Any topic we want to research related to go-to-market. |
| **Copy & Messaging** | All sales copy, blurbs, email templates, messaging frameworks. |
| **Conferences & Events** | Event tracking (may move to Attio later). |
| **Ideas** | Conceptual ideas, potential actions, things that could be useful. Not concrete tasks, but ideas to explore. |
| **Archive** | Deprecated pages that are no longer actively used but kept for reference. |

### Key Page IDs

| Page | ID |
|------|-----|
| GTM (root) | `1f119db581438016b3d2dd132f51526f` |
| Sales Handbook | `1f119db5814380ce9704cc833e8a6103` |
| ICP | `14f19db5814380588671e841c2f85f51` |
| Research | `22819db581438050ba4cdba77f5a1159` |
| Copy & Messaging | `23819db5814380e38cf7e3beadfe6952` |
| Ideas | `2bd19db5814380408064e318ec04f658` |
| Archive | `2bd19db5814380f4927bc62483c0bd43` |

## Available Tools

### Search & Fetch
- `notion-search` - Search across Notion (filter results to GTM content)
- `notion-fetch` - Retrieve content from a Notion page or database by URL

### Page Operations
- `notion-create-pages` - Create new pages (only under GTM hierarchy)
- `notion-update-page` - Modify page properties or content
- `notion-move-pages` - Relocate pages (only within GTM hierarchy)
- `notion-duplicate-page` - Duplicate a page within the workspace

### Database Operations
- `notion-create-database` - Create a new database (only under GTM)
- `notion-update-database` - Update database properties

### Comments
- `notion-create-comment` - Add comments to a page
- `notion-get-comments` - List all comments on a page

### Workspace Info
- `notion-get-teams` - Get teamspaces in the workspace
- `notion-get-users` - List workspace users
- `notion-get-user` - Get user info by ID
- `notion-get-self` - Get bot user info

## Rate Limits

- Standard API: 180 requests per minute per user
- Search: 30 requests per minute

Space out requests when doing bulk operations.

## Common Workflows

### Finding GTM Content

1. Use `notion-search` with GTM-related keywords
2. Filter results to pages within the GTM hierarchy
3. Use `notion-fetch` to get full page content

### Creating New GTM Documentation

1. Identify the appropriate parent page within GTM
2. Use `notion-create-pages` with the parent page ID
3. Structure content with proper headings and blocks

### Updating GTM Playbooks

1. Fetch the current page content with `notion-fetch`
2. Identify what needs to be updated
3. Use `notion-update-page` to apply changes

### Adding Meeting Notes

1. Find or create a meeting notes database under GTM
2. Create a new page entry with meeting details
3. Add attendees, date, and notes content

## Best Practices

1. **Always verify scope** - Confirm operations target GTM pages only
2. **Use descriptive titles** - Make pages easy to find and understand
3. **Maintain hierarchy** - Keep related content grouped together
4. **Add context** - Include relevant metadata and links
5. **Check before creating** - Search first to avoid duplicates

## Troubleshooting

### Page Not Found
- Verify the page URL or ID is correct
- Check if you have access to the page
- Ensure the page is within the GTM hierarchy

### Rate Limited
- Wait and retry after a minute
- Reduce request frequency for bulk operations

### Permission Denied
- The page may be outside your access scope
- Contact workspace admin if GTM access is needed
