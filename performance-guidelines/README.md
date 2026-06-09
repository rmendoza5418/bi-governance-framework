# Performance Guidelines

Slow dashboards kill adoption. A workbook that takes 30 seconds to load trains users to avoid it. Performance is a governance issue, not just a technical one.

---

## Performance SLAs

| Content Type | Target Load Time | Max Acceptable |
|---|---|---|
| Executive summary dashboard | < 5 seconds | 10 seconds |
| Operational / analyst dashboard | < 10 seconds | 20 seconds |
| Detail / drill-through view | < 15 seconds | 30 seconds |
| Scheduled extract refresh | < 30 minutes | 2 hours |

Workbooks consistently exceeding the "Max Acceptable" threshold must go through a performance review before re-certification.

Measure load time from the Tableau Server admin views (`Admin > Stats for Load Times`) — not from Tableau Desktop, which bypasses server-side caching behavior.

---

## Extract vs. Live Connection Decision Framework

| Scenario | Recommendation | Reason |
|---|---|---|
| Source is a transactional DB under heavy write load | **Extract** | Prevents dashboard queries from impacting production systems |
| Data freshness requirement < 1 hour | **Live** | Extract schedule latency is too high |
| Dataset > 50M rows | **Extract** | Live query at scale will fail SLA |
| Dataset < 500K rows, fast-changing | **Live** | Extract overhead not worth it |
| Dashboard used by 50+ concurrent users | **Extract** | Live queries don't scale with concurrent load |
| Regulatory / audit reporting (point-in-time accuracy) | **Extract with timestamp** | Preserves the exact data state for the reporting period |

**Default:** When in doubt, use an extract. The performance and concurrency benefits outweigh the freshness trade-off for most enterprise BI use cases.

---

## Common Performance Anti-Patterns

### 1. Nested LOD Calculations
```
// BAD — LOD inside an LOD
{ FIXED [Client] : SUM({ FIXED [Client], [Date] : SUM([Revenue]) }) }

// BETTER — compute the inner LOD as a separate calculated field
// Inner: [Client Daily Revenue] = { FIXED [Client], [Date] : SUM([Revenue]) }
// Outer: { FIXED [Client] : SUM([Client Daily Revenue]) }
```
Nested LODs force Tableau to run multiple passes over the data. Split them into separate fields and the query optimizer can handle each independently.

### 2. Cross-Database Joins at Row Level
Joining two large tables from different databases forces Tableau to pull both full tables to the Tableau Server process before joining. Alternatives:
- Use Tableau's Data Blending (aggregate-level join) for large tables
- Pre-join in a published data source or data warehouse view
- Use Virtual Connections if your platform supports them

### 3. Table Calculations on Large Datasets
Table calculations (RUNNING_SUM, WINDOW_AVG, RANK, etc.) run in the Tableau process after the database query returns. On large result sets, this means pulling millions of rows into memory. Use database-side windowing functions via Custom SQL or push the logic to a materialized view.

### 4. Filters That Don't Push Down
Context filters, top-N filters, and fixed LOD calculations can prevent filter pushdown, causing full table scans before filtering. Always check the query issued to the database using Tableau's Performance Recording.

### 5. Too Many Marks
Dashboards with > 5,000 marks render slowly and are usually unreadable anyway. Aggregate to a higher grain or use a detail-on-demand pattern (summary view → drill to detail).

---

## Performance Review Checklist

Before certifying a workbook, the CoE reviewer should verify:

- [ ] Load time measured on server (not Desktop) under concurrent load
- [ ] Extract vs. live decision is documented and appropriate
- [ ] No nested LOD calculations
- [ ] Cross-database joins reviewed and justified
- [ ] Table calculations scoped to aggregated data only
- [ ] Filters verified to push down to the database (check Performance Recording)
- [ ] Mark count < 5,000 on any single view
- [ ] Extract refresh schedule is appropriate for data freshness requirements
- [ ] Extract size documented (> 500MB triggers additional review)

---

## Monitoring

The Tableau Server admin views surface performance data, but they're not user-friendly for CoE monitoring. Recommended approach:

1. Extract the `admin.views` and `admin.workbooks` tables from Tableau's PostgreSQL repository
2. Build a CoE performance dashboard tracking: P50/P95 load times by workbook, slow load trends, and extract refresh SLA compliance
3. Alert the workbook owner when their content exceeds the "Max Acceptable" threshold for 3+ consecutive days
