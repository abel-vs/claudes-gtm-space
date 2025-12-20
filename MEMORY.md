# Learnings & Error Prevention

This file contains general learnings and workarounds. For Attio CRM-specific guidance, see `.claude/skills/attio-crm/SKILL.md`. For GTM Notion structure, see `.claude/skills/notion-gtm/SKILL.md`.

## System Architecture

### Tool Responsibilities

| Domain | Primary Tool | Notes |
|--------|-------------|-------|
| **CRM (Contacts, Companies, Deals, Pipeline)** | Attio | All contact/company/deal management lives here |
| **Product Tasks & Feature Requests** | Linear | Customer feature requests go to Linear |
| **GTM Documentation & Strategy** | Notion | Sales handbook, ICP, research, copy/messaging |
| **Conferences & Events** | Notion (for now) | May move to Attio later |

### Integrations
- **Attio ↔ Linear**: There is an existing integration between Attio and Linear. Customer feature requests should be created in Linear and linked back to the Attio company/contact.

### What NOT to Use Notion For
The following have been archived from Notion (managed in Attio instead):
- Sales CRM
- Customers database
- Companies database
- Customer Individuals
- Sales Pipeline
- Sales Meetings
- Prospecting (as a database)

## MCP Tool Access Limitations

### MCP Tools Not Directly Callable in Main Agent Context

**Issue:** MCP tools (mcp__attio-mcp, mcp__notion, mcp__surfe) are listed in settings.json permissions but are not directly accessible as function calls in the main agent conversation context.

**Attempted:**
- Calling mcp__attio-mcp, mcp__surfe directly as tools
- Using Bash to invoke MCP commands

**Workaround:**
- MCP tools may only be accessible within skill contexts (which require prompts and separate execution)
- For research tasks requiring MCP integration, use web search to gather data, then provide structured output for manual import
- Alternative: Skills may need to be invoked if they support MCP access

**Date:** 2025-12-16
