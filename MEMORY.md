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
