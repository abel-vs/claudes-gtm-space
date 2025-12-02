# Learnings & Error Prevention

## Attio CRM

- **Use API slugs, not display names**: When updating Attio records, use the actual API field slug (e.g., `stage`) rather than converting display names to snake_case (e.g., `deal_stage`). The display name "Deal stage" maps to the slug `stage`, not `deal_stage`.
