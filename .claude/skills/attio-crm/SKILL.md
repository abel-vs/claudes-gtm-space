---
name: attio-crm
description: Manage Attio CRM operations including contacts, companies, deals, lists, and pipeline management. Use when working with Attio contacts, people records, deal stages, outreach status, company information, or CRM data operations.
allowed-tools:
  - mcp__attio-mcp
  - WebFetch
  - WebSearch
  - Read
  - Write
  - Grep
  - Glob
---

# Attio CRM Skill

This skill provides guidance for working with Attio CRM operations, including creating and updating records, managing lists, and handling common API patterns.

## Learnings

### 1. Always Use API Slugs, Not Display Names

When updating Attio records, use the actual API field slug rather than converting display names to snake_case.

**Example:**
- Display name: "Deal stage" → Use slug: `stage` (NOT `deal_stage`)
- Display name: "Outreach status" → Use slug: `outreach_status`

**Best Practice:** Always call `records_discover_attributes` or `get-list-details` first to confirm the correct field slugs before updating records.

### 2. Filter List Entries Workaround

The `filter-list-entries` and `advanced-filter-list-entries` tools may fail with 400 errors when filtering by status/stage fields.

**Workaround:** Use `get-list-entries` to retrieve all entries, then filter manually by checking status fields in the `entry_values`.

**Example:**
```javascript
// Instead of filtering by status directly, do this:
const entries = await get_list_entries(listId);
const filtered = entries.filter(e =>
  e.entry_values?.outreach_status?.status?.title === "Need to reach out"
);
```

### 3. Status Field Structure

In list entries, status fields contain a nested structure:

```javascript
{
  entry_values: {
    outreach_status: {
      status: {
        title: "Archived"  // or "Need to reach out", etc.
      }
    }
  }
}
```

Always access the status via `entry_values.<field_slug>.status.title`.

### 4. People-to-Company Relationships

The `records_search_by_relationship` tool with `people_to_company` relationship type may fail with 400 errors.

**Workaround:**
- Extract company information from the person's description field or job title
- Search for the company separately using `records_search`
- Use the company record's direct fields instead of relationship traversal

## Common Workflows

### Creating a New Contact

1. Search to check if contact exists: `records_search`
2. If not found, create: `create-record` with resource_type="people"
3. Required fields typically: name, email_addresses
4. Add to list if needed: `add-record-to-list`

### Updating Deal Stages

1. Get list details to see available stages: `get-list-details`
2. Find the entry in the list: `get-list-entries` or `filter-list-entries-by-parent-id`
3. Update the entry: `update-list-entry` with attributes like `{stage: "Demo Scheduling"}`

### Managing Outreach Status

1. Retrieve list entries: `get-list-entries`
2. Filter locally by checking `entry_values.outreach_status.status.title`
3. Update status: `update-list-entry` with the correct slug and value

### Researching Companies

1. Search for company: `records_search` with resource_type="companies"
2. If enrichment needed, use `WebSearch` or `WebFetch` to gather additional data
3. Update company record: `update-record` with discovered information

## Field Discovery Pattern

Before any update operation:

1. Call `records_discover_attributes` for the resource type
2. Note the exact `slug` values from the response
3. Use those slugs in your update payloads

Example:
```
# First discover
records_discover_attributes(resource_type="people")

# Then use the exact slugs returned
update-record(
  resource_type="people",
  record_id="...",
  record_data={"email_addresses": [...], "job_title": "..."}
)
```

## Tools Reference

### Primary Tools
- `records_search` - Search for records across all types
- `records_get_details` - Get full record details
- `create-record` - Create new records
- `update-record` - Update existing records
- `records_discover_attributes` - Find valid field slugs

### List Management
- `get-lists` - List all available lists
- `get-list-details` - Get list schema and stages
- `get-list-entries` - Get all entries in a list
- `add-record-to-list` - Add a record to a list
- `update-list-entry` - Update list-specific fields like stage
- `filter-list-entries-by-parent-id` - Find list entries for a specific record

### Notes
- `create-note` - Add notes to records
- `list-notes` - Retrieve notes for a record

## Troubleshooting

### 400 Errors on Filter Operations
→ Use `get-list-entries` and filter manually

### Unknown Field Slug
→ Call `records_discover_attributes` or `get-list-details`

### Relationship Traversal Fails
→ Extract data from description/title fields and search separately

### Status Update Not Working
→ Verify you're using `update-list-entry` (not `update-record`) for list-specific fields like stage
