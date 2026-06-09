# Dashboard Review Checklist

Use this checklist when reviewing a workbook for Silver or Gold certification.
Complete all sections. A single FAIL blocks certification until resolved.

---

**Workbook:** _______________________________________________
**Review type:** ☐ Silver (Champion review)  ☐ Gold (CoE review)
**Reviewer:** _______________________________________________
**Date:** _______________________________________________
**Author / Data Steward:** _______________________________________________

---

## 1. Naming & Metadata

| Check | Pass | Fail | N/A | Notes |
|---|---|---|---|---|
| Workbook name follows `[Domain] - [Subject] - [Audience]` pattern | | | | |
| Description is present and ≥ 20 characters | | | | |
| Description explains what the workbook measures and who it's for | | | | |
| Published to correct project (not Default, not personal space) | | | | |
| Owner is a named, active employee (not a shared/service account) | | | | |
| Appropriate tags applied | | | | |
| No "Copy of", "Test", "FINAL", or date in workbook name | | | | |

---

## 2. Data Accuracy

| Check | Pass | Fail | N/A | Notes |
|---|---|---|---|---|
| Author has documented the data source(s) and their refresh cadence | | | | |
| At least one key metric has been spot-checked against the source system | | | | |
| Known data quality issues are disclosed (in description or tooltip) | | | | |
| Date ranges and filters are correct and clearly labeled | | | | |
| Aggregation logic (SUM vs. AVG vs. COUNT DISTINCT) is appropriate | | | | |
| NULL handling is correct and documented | | | | |

---

## 3. Performance

| Check | Pass | Fail | N/A | Notes |
|---|---|---|---|---|
| Load time < 10s measured on Tableau Server (not Desktop) | | | | |
| No nested LOD calculations | | | | |
| No cross-database joins on large tables without justification | | | | |
| Mark count < 5,000 on any single view | | | | |
| Filters verified to push down (Performance Recording reviewed) | | | | |
| Extract vs. live decision is appropriate and documented | | | | |
| Extract refresh schedule matches data freshness requirements | | | | |

---

## 4. Design & Usability

| Check | Pass | Fail | N/A | Notes |
|---|---|---|---|---|
| Chart type is appropriate for the data being displayed | | | | |
| Axes are labeled with units (%, $, count, etc.) | | | | |
| Color is used intentionally (not just decoratively) | | | | |
| Color choices are accessible (not red/green only for status) | | | | |
| Tooltips add information beyond what's visible in the mark | | | | |
| Filters are clearly labeled and have sensible defaults | | | | |
| Mobile layout provided (if dashboard is used on mobile) | | | | |
| Dashboard fits 1920×1080 without horizontal scrolling | | | | |

---

## 5. Governance

| Check | Pass | Fail | N/A | Notes |
|---|---|---|---|---|
| Data steward named and confirmed willing to maintain | | | | |
| Data source is from the approved Data Source Library (or approved exception) | | | | |
| No hardcoded dates or values that will become stale | | | | |
| No PII or sensitive data exposed to unauthorized audiences | | | | |
| Row-level security configured if required by data classification | | | | |

---

## Decision

☐ **Approved** — proceed to certification  
☐ **Approved with conditions** — address items noted before final certification  
☐ **Rejected** — fails on: _______________________________________________

**Reviewer signature:** _______________________________________________  
**Date:** _______________________________________________

---

*This checklist is maintained by the BI CoE. For questions, contact the CoE Lead.*
