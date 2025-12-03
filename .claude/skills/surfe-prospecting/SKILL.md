---
name: surfe-prospecting
description: Prospect for leads using Surfe. Use for searching people/companies by ICP criteria, enriching contacts with emails/phone numbers, and building prospect lists. Integrates with Surfe's data platform for B2B prospecting.
allowed-tools:
  - mcp__surfe
  - WebSearch
  - Read
  - Write
  - Grep
  - Glob
---

# Prospecting Skill

This skill provides guidance for B2B prospecting using Surfe's data enrichment platform. Use it to find leads matching your ICP, enrich contacts with email addresses and phone numbers, and research companies.

## Learnings

### 1. Never Enrich Automatically - Costs Credits

**CRITICAL:** Enrichment operations (`surfe_enrich_people`, `surfe_enrich_companies`) consume credits and should ONLY be performed when the user explicitly requests it.

**Allowed:**
- Searching for people/companies (free)
- Checking credits (free)
- Getting filter options (free)

**Requires explicit user request:**
- Enriching contacts for email/phone
- Enriching companies for detailed data

**Example of explicit requests:**
- "Enrich this contact"
- "Get their email address"
- "Find phone numbers for these leads"
- "Enrich these companies"

If the user just asks to "find leads" or "prospect", only SEARCH - do not enrich unless they specifically ask for contact info.

## Available Tools

### People Search & Enrichment

| Tool | Purpose |
|------|---------|
| `surfe_search_people` | Find people by job title, company, location, industry, seniority, etc. |
| `surfe_enrich_people` | Get email addresses, mobile phone numbers, and LinkedIn info for specific people |
| `surfe_get_person_enrichment_results` | Retrieve async enrichment results by request ID |

### Company Search & Enrichment

| Tool | Purpose |
|------|---------|
| `surfe_search_companies` | Find companies by industry, size, location, revenue, keywords |
| `surfe_enrich_companies` | Get detailed company info: address, employee count, revenue, technologies |
| `surfe_get_company_enrichment_results` | Retrieve async company enrichment results by request ID |

### Utility Tools

| Tool | Purpose |
|------|---------|
| `surfe_get_credits` | Check remaining email and mobile credits |
| `surfe_get_filters` | Get valid filter values for industries, seniorities, company sizes, etc. |

## Common Workflows

### 1. Finding People by ICP Criteria

Search for leads matching specific ICP criteria:

```javascript
surfe_search_people({
  filters: {
    jobTitleKeywords: ["CTO", "VP Engineering", "Head of Engineering"],
    seniority: ["vp", "c-level", "director"],
    industry: ["Software Development", "Information Technology"],
    companySize: ["51-200", "201-500"],
    location: { country: "United States" }
  },
  limit: 25
})
```

### 2. Enriching a Specific Person

Get contact info for someone you've identified:

```javascript
// By LinkedIn URL (most accurate)
surfe_enrich_people({
  persons: [
    { linkedinUrl: "https://linkedin.com/in/johndoe" }
  ]
})

// By name + company
surfe_enrich_people({
  persons: [
    { 
      firstName: "John",
      lastName: "Doe",
      companyName: "Acme Inc"
    }
  ]
})
```

### 3. Finding Companies by ICP

Search for target companies:

```javascript
surfe_search_companies({
  filters: {
    industry: ["Software Development"],
    size: ["51-200", "201-500"],
    location: { country: "United States", region: "California" },
    keywords: ["AI", "machine learning"]
  },
  limit: 25
})
```

### 4. Enriching Company Data

Get detailed company information:

```javascript
surfe_enrich_companies({
  companies: [
    { domain: "acme.com" },
    { linkedinUrl: "https://linkedin.com/company/acme" },
    { name: "Acme Inc" }
  ]
})
```

### 5. Building a Prospect List

Full workflow for building a targeted list:

1. **Get valid filters:** `surfe_get_filters` to see available options
2. **Search companies:** Find target companies matching ICP
3. **Search people:** Find decision-makers at those companies
4. **Present results to user** - Show matches found
5. *(Only if user requests)* **Enrich contacts:** Get email/phone for selected prospects

## Search Filter Reference

### People Filters

| Filter | Type | Description |
|--------|------|-------------|
| `firstName` | string | First name |
| `lastName` | string | Last name |
| `jobTitle` | string | Exact job title |
| `jobTitleKeywords` | string[] | Keywords in job title |
| `companyName` | string | Company name |
| `companyDomain` | string | Company website |
| `companyLinkedinUrl` | string | Company LinkedIn URL |
| `companySize` | string[] | e.g., "1-10", "11-50", "51-200" |
| `industry` | string[] | Industry names |
| `seniority` | string[] | "entry", "manager", "director", "vp", "c-level", "owner" |
| `department` | string[] | "engineering", "sales", "marketing", etc. |
| `location` | object | `{city, region, country}` |
| `linkedinUrl` | string | Person's LinkedIn URL |

### Company Filters

| Filter | Type | Description |
|--------|------|-------------|
| `name` | string | Company name |
| `domain` | string | Website domain |
| `linkedinUrl` | string | LinkedIn company URL |
| `industry` | string[] | Industry names |
| `size` | string[] | Employee count ranges |
| `location` | object | `{city, region, country}` |
| `revenue` | object | `{min, max}` in USD |
| `foundedYear` | object | `{min, max}` |
| `keywords` | string[] | Keywords in description |

## Best Practices

1. **Only enrich when explicitly asked** - Enrichment costs credits. Never auto-enrich. Wait for user to request email/phone data.

2. **Use `get_filters` for valid values** - Before searching, check what industries, seniorities, and company sizes are valid.

3. **LinkedIn URLs are most accurate** - When enriching, provide LinkedIn URL if available for best match rate.

4. **Batch enrichment requests** - You can enrich up to 100 people/companies per request.

5. **Use pagination for large searches** - Use `limit` and `offset` parameters to page through results.

6. **Combine with Attio** - After enriching leads, add them to Attio CRM for tracking and outreach.

## Credit Management

- **Email credits** - Consumed when retrieving email addresses
- **Mobile credits** - Consumed when retrieving phone numbers
- Check balance: `surfe_get_credits`
- Plan enrichment batches to optimize credit usage

## Troubleshooting

### No Results Found
- Broaden your search criteria
- Check filter values are valid (use `surfe_get_filters`)
- Try different keyword combinations

### Enrichment Returns No Email/Phone
- Not all profiles have discoverable contact info
- Try alternative identifiers (LinkedIn URL vs name+company)
- Verify the person still works at the company

### Async Enrichment
- For bulk requests, enrichment may be async
- Use `surfe_get_person_enrichment_results` or `surfe_get_company_enrichment_results` with the request ID
- Optionally provide a webhook URL to receive results

## Integration with Other Skills

### → Attio CRM
After finding and enriching prospects, add them to Attio:
1. Create person record with enriched data
2. Add to appropriate outreach list
3. Set initial outreach status

### → Notion GTM
Document prospecting research:
1. Save ICP search criteria that work well
2. Document industry insights discovered
3. Track prospecting experiments and results

