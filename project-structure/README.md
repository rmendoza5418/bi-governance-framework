# Project Structure

How you organize Tableau Server projects shapes how users discover content, who can publish where, and how governance scales. Get this wrong early and it's painful to fix at scale.

---

## Recommended Top-Level Structure

```
Tableau Server Site
├── 📁 [Certified]                    ← Gold-certified content only; CoE-managed
│   ├── Executive Reporting
│   ├── Wealth Management
│   ├── Risk & Compliance
│   ├── Operations
│   └── Finance
│
├── 📁 [Reviewed]                     ← Silver-reviewed content; domain-managed
│   ├── Wealth Management
│   ├── Risk & Compliance
│   ├── Operations
│   ├── Finance
│   └── Technology
│
├── 📁 [Sandbox]                      ← In-development; no governance guarantees
│   ├── WIP - Wealth Management
│   ├── WIP - Risk
│   └── WIP - [Your Name]             ← Named personal workspaces allowed here only
│
├── 📁 [Archive]                      ← Decertified or deprecated content; read-only
│
└── 📁 [Admin]                        ← CoE infrastructure; admin access only
    ├── CoE Monitoring
    └── Data Source Library
```

---

## Permission Model

| Project | Publisher | Viewer | Notes |
|---|---|---|---|
| `[Certified]` | CoE Lead only | All authenticated users | No self-publishing; CoE promotes content |
| `[Reviewed]` | BI Champions + CoE | All authenticated users | Domain champions can publish |
| `[Sandbox]` | All Creators | Authenticated users in same team | Visible but clearly labeled as unofficial |
| `[Archive]` | CoE only | All authenticated users | Read-only; no refreshes |
| `[Admin]` | CoE only | CoE only | Hidden from general users |

**Key principle:** Users should never be confused about whether content is official. The project name makes status unambiguous — if it's in `[Certified]`, it's been reviewed. If it's in `[Sandbox]`, it hasn't.

---

## Content Promotion Path

```
Author creates in [Sandbox]
        │
        ▼ (submits certification request)
BI Champion reviews → moves to [Reviewed] (Silver)
        │
        ▼ (nominates for Gold)
CoE Lead reviews → moves to [Certified] (Gold)
        │
        ▼ (deprecated or decertified)
CoE moves to [Archive]
```

Authors do **not** move their own content between projects. Promotion is a CoE action, which maintains the integrity of the certification signal.

---

## What Not To Do

**Don't** create a project per team or per person at the top level. A flat list of 40 team folders is hard to navigate, makes permissions complex, and gives no signal about content quality.

**Don't** nest more than 3 levels deep. Tableau's project nesting becomes confusing beyond that, and permissions inheritance gets hard to reason about.

**Don't** put "Default" project into production use. Rename it, restrict permissions, or disable publishing to it. The Default project is a dumping ground by default.

**Don't** use dates in project names (e.g., "Q1 2024 Reports"). Projects should represent domains, not time periods. Time-specific content belongs in the workbook name or in a data filter.

---

## Data Source Library

The `[Admin] > Data Source Library` project contains the CoE-managed published data sources that workbooks should connect to. This is how you enforce a single version of truth at the data layer.

Published data sources in the library should:
- Follow the data source naming convention
- Be owned by the CoE team account, not individual users
- Have documented refresh schedules and SLAs
- Be certified before any workbook in `[Certified]` connects to them

When an author in Sandbox wants to use a new data source, they request it be added to the library. The CoE reviews and publishes it centrally. This prevents 40 workbooks each creating their own slightly-different connection to the same database.
