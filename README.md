# Enterprise BI Governance Framework

A practical playbook for running a Tableau Center of Excellence (CoE) at scale — covering naming standards, certification workflows, performance guidelines, onboarding, and project governance.

Built from operational experience managing enterprise Tableau environments across financial services organizations with 1,000–10,000+ users.

## Why This Exists

Most BI governance documentation is either too theoretical (nobody follows it) or too vendor-specific (doesn't survive a platform migration). This framework is designed to be:

- **Operationally specific** — concrete standards with examples, not abstract principles
- **Enforceable** — every standard here can be audited programmatically (see [tableau-asset-auditor](https://github.com/rmendoza5418/tableau-asset-auditor))
- **Platform-agnostic at the principle level** — core governance concepts apply equally to Tableau, Power BI, and Looker environments

## Contents

| Section | What's Inside |
|---|---|
| [naming-conventions/](naming-conventions/) | Workbook, view, field, and project naming standards |
| [certification-standards/](certification-standards/) | When and how to certify content; data steward responsibilities |
| [performance-guidelines/](performance-guidelines/) | Workbook performance standards; extract vs. live rules |
| [onboarding/](onboarding/) | New user onboarding, developer tracks, champion program |
| [project-structure/](project-structure/) | How to organize Tableau Server projects and permissions |
| [templates/](templates/) | Dashboard review checklist, certification form, CoE meeting agenda |

## Governance Maturity Model

Before applying these standards, locate your organization on the maturity curve:

| Level | Characteristics | Focus |
|---|---|---|
| **1 — Ad Hoc** | No standards; personal space sprawl; nobody knows what's official | Establish basic naming + project structure |
| **2 — Repeatable** | Some standards exist; inconsistently followed; no enforcement | Implement certification workflow; train champions |
| **3 — Defined** | Standards documented; certification pipeline active; CoE established | Automate auditing; publish usage metrics |
| **4 — Managed** | Adoption measured; SLAs defined; stale content removed proactively | Run experiments to optimize adoption (see [bi-adoption-experiment](https://github.com/rmendoza5418/bi-adoption-experiment)) |
| **5 — Optimizing** | CoE is a strategic function; BI is a product with a roadmap | Capacity planning, deprecation cycles, self-service maturity |

This framework targets Level 2 → 4.

## Contributing

Standards should be living documents. When a standard fails in practice, update it with the failure mode and what replaced it. Governance that isn't updated becomes shelfware.
