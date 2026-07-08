# Axon Customer Success Command Center

A live, Gainsight-lite Customer Success dashboard built on Axon Salesforce data — an internal replacement for Gainsight.

## What it does

Single self-contained HTML app (`index.html`) that reads live Salesforce data and provides:

- **Command Center** — renewal ARR in scope, ARR at risk, ARR-weighted health, lifetime value, and open escalations, with ARR-by-team and book-health charts.
- **Org Drill-down** — exec → team → CSM → account hierarchy built from the Salesforce manager chain, with roll-ups at every level.
- **Renewals triage** — every account with an open renewal, sortable by revenue exposure, lifetime value, sentiment, and health.
- **Escalations tracker** — auto-seeded from live risk signals; status changes persist locally.
- **My Worklist** — prioritized actions ranked by urgency and revenue.
- **Health Model** — CS-Ops-owned, tunable health-score weights; the whole book re-scores instantly.

### Account 360

Click any account for a full profile:

- **Health breakdown** — transparent, penalty-by-penalty scoring.
- **Purchase history & lifetime value** — total closed-won value, deal count, first/most-recent purchase, and recent won deals.
- **Products purchased** — spend by product family and top individual items, from closed-won line items.
- **Customer sentiment & satisfaction** — a 0–100 index derived from lifetime support-case signals (high/urgent share, escalation rate, ticket volume, open high-priority cases), with full breakdown. *(This org has no native CSAT/NPS field; swap in survey data here when available.)*
- **Communications** — recent logged emails, calls, and meetings.

## Data source

All data is read live through the **Axon Salesforce** connector via `run_soql_query`. Objects used: `Opportunity`, `OpportunityLineItem`, `Case`, `Task`, `Event`, `User`.

## Deployment / usage notes

This runs as a Cowork artifact. The Salesforce connector is authorized per-user, so **each viewer must connect the Axon Salesforce connector in their own Cowork** and sign in with their Axon credentials. Users only see the accounts their Salesforce permissions allow.

Health-model weights and escalation status persist in the browser (`localStorage`); a production deployment would back these with a shared table.
