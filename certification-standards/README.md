# Certification Standards

Certification signals to users that a workbook has been reviewed for accuracy, follows governance standards, and has an accountable owner. It's the BI equivalent of a code review gate.

Uncertified high-usage content is the most common source of "we made a decision on bad data" incidents.

---

## Certification Tiers

| Tier | Label | Who Can Grant | What It Means |
|---|---|---|---|
| **Gold** | ✦ Certified | CoE Lead or Data Steward | Reviewed, accurate, official source of truth |
| **Silver** | ✓ Reviewed | Department BI Champion | Reviewed by domain SME; not yet CoE-validated |
| **Bronze** | ~ Community | Content owner | Author attests to accuracy; no independent review |

In Tableau Server, use the built-in Certification feature for Gold. Use Tags for Silver (`reviewed`) and Bronze (`community`).

---

## When Certification Is Required

Content **must** be certified (Gold minimum) if any of the following apply:

- Used in executive or board reporting
- Referenced in regulatory filings or compliance reporting
- Has more than 50 unique users in a 30-day window
- Linked from an intranet portal, SharePoint, or official documentation
- Used for compensation calculations or client-facing deliverables

Content is **recommended** for Silver certification if:
- It has 10+ unique users in a 30-day window
- It appears in search results for common business terms
- It's been referenced in 3+ meetings or Slack conversations

---

## Certification Workflow

```
Author publishes workbook
        │
        ▼
Author submits certification request
(use template: templates/certification-request.md)
        │
        ▼
BI Champion review (Silver gate)
  ├── Does it follow naming conventions?
  ├── Is there a meaningful description?
  ├── Has the data source been validated against the source system?
  └── Has the author documented assumptions and known limitations?
        │
        ▼ (passes Silver)
CoE Lead review (Gold gate)
  ├── Performance: loads in < 10s on standard hardware?
  ├── Accuracy: spot-checked against source system or prior report?
  ├── Governance: correct project, owner, tags, description?
  ├── Sustainability: is there an active owner who will maintain it?
  └── Documentation: is the certification note complete?
        │
        ▼ (passes Gold)
Certified — CoE publishes to canonical project
CoE logs in asset registry
SLA clock starts for owner
```

---

## Data Steward Responsibilities

Every certified workbook must have an assigned **Data Steward** — a named person accountable for:

| Responsibility | Cadence |
|---|---|
| Verify data accuracy | Monthly spot check |
| Update when source system changes | Within 5 business days of change |
| Review and respond to accuracy complaints | Within 2 business days |
| Re-certify after major changes | Before republishing |
| Notify CoE when stepping down as steward | Immediately |

If a data steward leaves the organization and no successor is named, the workbook reverts to Bronze status automatically after 30 days.

---

## Decertification

Certification is revoked when:
- The workbook fails a data accuracy spot check
- The data source behind it has been decommissioned or migrated
- The steward is unreachable and no successor is named
- The workbook has not been accessed in 180+ days

Decertified workbooks are moved to a `[Archive]` project subfolder rather than deleted. They remain accessible but no longer appear in certification-filtered searches.

---

## SLAs

| Event | SLA |
|---|---|
| Initial certification review (Silver) | 5 business days |
| CoE Gold review | 10 business days |
| Response to accuracy complaint | 2 business days |
| Decertification notice to steward | 24 hours before action |
| Archive after decertification | 30 days grace period |
