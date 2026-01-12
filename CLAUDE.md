# Claude Code Instructions

## Response Formatting (Slack/Email)

When responding via Slack or Email, your **final message** is what gets sent to me. Structure it as a clean, conversational response:

- **Don't repeat your thinking process** - I only see the final message, not your tool calls or reasoning
- **Be direct** - Start with the answer/result, not "I'll do X" or "Let me check Y"
- **Summarize outcomes** - If you created something (Linear issue, calendar event, etc.), give me the key details
- **Keep it conversational** - Write like you're chatting with me, not documenting your process

**Good example:**
> ✅ Created Linear issue GTM-66: "Set up Snitcher n8n workflow" - it's in your backlog ready to go!

**Bad example:**
> I'll create a Linear issue. Let me get the team ID first... [tool output] ... Now creating the issue... [more output] ... Done! I created GTM-66.

## On Session Start

Always first check MEMORY.md at the start of each session to review past errors, learnings, and workarounds to prevent repeating mistakes.

## Project Context

This is a GTM (Go-To-Market) workspace for managing sales outreach, contact research, and CRM operations using Attio and Linear integrations.

## Updating Memory

Whenever you encounter an issue that should be remembered for future sessions, add it to MEMORY.md. This includes:

- **API errors and workarounds** - e.g., Attio MCP tools that fail and alternative approaches
- **Field mappings** - correct slugs, field names, or data structures
- **Tool limitations** - things that don't work as expected
- **Successful patterns** - approaches that work well and should be reused

Always document:
1. What the issue was
2. Why it happened (if known)
3. The workaround or solution

This ensures the next Claude Code session doesn't repeat the same mistakes.
