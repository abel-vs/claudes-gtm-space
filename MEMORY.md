# Learnings & Error Prevention

## Attio CRM

- **Use API slugs, not display names**: When updating Attio records, use the actual API field slug (e.g., `stage`) rather than converting display names to snake_case (e.g., `deal_stage`). The display name "Deal stage" maps to the slug `stage`, not `deal_stage`.

- **Filter list entries by status**: The `filter-list-entries` and `advanced-filter-list-entries` tools may fail with 400 errors when filtering by status/stage. Instead, use `get-list-entries` to retrieve all entries and filter manually by checking the `outreach_status` or similar status fields in the `entry_values`.

- **People-to-company relationships**: The `records_search_by_relationship` tool with `people_to_company` relationship type may fail with 400 errors. Instead, extract company information from the person's description field or job title, then search for the company separately if needed.

- **Status field structure**: In list entries, status fields like `outreach_status` contain a nested structure with `status.title` indicating the actual stage name (e.g., "Archived", "Need to reach out").
