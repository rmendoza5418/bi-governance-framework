# Naming Conventions

Consistent naming is the single highest-leverage governance intervention. It costs almost nothing to implement and makes every other audit, search, and governance task dramatically easier.

---

## Workbook Names

**Pattern:** `[Domain] - [Subject] - [Audience] v[N]`

| Component | Description | Examples |
|---|---|---|
| Domain | Business domain or function | `Wealth Mgmt`, `Risk`, `Operations`, `Finance` |
| Subject | What the workbook measures | `AUM Summary`, `Portfolio Performance`, `Advisor Pipeline` |
| Audience | Intended consumer | `Executive`, `Advisor`, `Analyst`, `Operations` |
| Version | Optional; only for versioned releases | `v2`, `v3` |

**Good examples:**
- `Wealth Mgmt - AUM Summary - Executive`
- `Risk - Credit Exposure Dashboard - Analyst`
- `Operations - Daily Settlement Report - Operations`

**Bad examples:**
- `New Dashboard` ← no domain, no subject, no audience
- `John's AUM tracker` ← personal artifact in shared space
- `Copy of Portfolio Perf FINAL (2)` ← version chaos

**Rules:**
- Title case for all components
- No dates in the name (use the Last Modified timestamp on the server)
- Max 80 characters total
- No special characters except hyphens and parentheses

---

## View (Sheet/Dashboard) Names

Views inside a workbook should follow the same hierarchy as the workbook itself:

- **Summary dashboards** → `[Subject] Overview` (e.g., `AUM Overview`)
- **Detail views** → `[Subject] Detail` (e.g., `Portfolio Detail`)
- **Drill-through views** → `[Dimension] Breakdown` (e.g., `Advisor Breakdown`)
- **Reference / support sheets** → prefix with `_` to push to bottom of list (e.g., `_Calc Validation`)

Do not publish sheets that are only calculation-validation scaffolding. Hide them or use the `_` prefix to signal non-public status.

---

## Calculated Field Names

| Type | Naming Pattern | Example |
|---|---|---|
| Dimension | `[Context] [Name]` | `Client Risk Category`, `Advisor Tenure Band` |
| Measure | `[Aggregation] [Metric]` | `Total AUM`, `Avg Portfolio Return`, `Count Active Clients` |
| LOD Calculation | `LOD [Description]` | `LOD Client AUM at Date`, `LOD Fixed Region Total` |
| Parameter-driven | `PARAM [Description]` | `PARAM Date Range Label`, `PARAM Metric Selector` |
| Boolean flag | `IS [Condition]` or `HAS [Property]` | `IS High Value Client`, `HAS Active Position` |
| Date field | `[Field] [Granularity]` | `Transaction Month`, `Reporting Quarter` |

**Rules:**
- No abbreviations unless universally known in your domain (AUM, YTD, NAV are fine; `Rtn` for Return is not)
- Don't embed the data source name in a field name — it creates maintenance debt when sources change
- LOD calculations must always have a comment block explaining the business logic

---

## Data Source Names

**Pattern:** `[Source System] - [Entity] - [Grain] [(Extract)]`

| Component | Description | Example |
|---|---|---|
| Source System | Where the data comes from | `Salesforce`, `Data Warehouse`, `Bloomberg` |
| Entity | Primary entity in the source | `Accounts`, `Transactions`, `Holdings` |
| Grain | Row-level grain if non-obvious | `Daily`, `Monthly Snapshot`, `Position-Level` |
| Extract flag | Append `(Extract)` if using an extract | `(Extract)` |

**Good examples:**
- `Data Warehouse - Client Holdings - Daily (Extract)`
- `Salesforce - Advisor Pipeline - Opportunity-Level`
- `Bloomberg - Market Data - Daily Prices (Extract)`

---

## Project (Folder) Structure

See [project-structure/](../project-structure/) for the full folder hierarchy. Name projects using:
- Title case
- Business domain as the top-level folder
- Audience or maturity level as the second-level folder

**Do not** use dates, team member names, or temporary labels in project names.

---

## Enforcement

These conventions are auditable with [tableau-asset-auditor](https://github.com/rmendoza5418/tableau-asset-auditor). The auditor flags:
- Workbooks with names shorter than 10 characters
- Workbooks containing "Copy of", "New", "Test", "Temp", or "FINAL"
- Calculated fields with names shorter than 5 characters
- Data sources not following the `Source - Entity` pattern

Run the audit monthly and report violations in the CoE dashboard.
