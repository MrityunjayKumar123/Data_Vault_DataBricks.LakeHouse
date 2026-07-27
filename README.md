# Data_Vault_DataBricks.LakeHouse

A practical reference for implementing **Data Vault** on the **Databricks Lakehouse** for EDW migration, auditability, and scalable enterprise data integration.

---

## Why Data Vault for an EDW Migration

Data Vault is the right choice when the migration has one or more of the following characteristics:

- Multiple source systems feed the same business concept.
  - Example: `Customer` exists in a legacy EDW, a CRM, and an acquired company’s system.
- Regulatory or audit requirements demand full history, no data loss, and complete traceability back to source.
- Source volatility is high.
  - Source systems may be replaced, renamed, or structurally changed during migration.
- Parallel-run reconciliation is required.
  - You must prove the new platform matches legacy numbers exactly.
  - Insert-only, non-destructive historization makes this easier.

If none of these apply and the domain is small, stable, and well understood, a direct Kimball build is usually faster.

---

## Why It Fits Databricks Lakehouse

Data Vault fits well on Databricks because the Lakehouse supports scalable ingestion, incremental processing, and historized storage patterns. Databricks guidance explicitly maps Data Vault implementations to the Bronze/Silver/Gold architecture and recommends Delta Live Tables and Delta Lake for scalable warehousing patterns [web:1][web:2].

In practice:

- Bronze stores raw source data.
- Silver hosts the Raw Vault and integration logic.
- Gold serves consumption-ready dimensional marts and reporting layers.

---

## Recommended Folder Structure

```text
Data_Vault_DataBricks.LakeHouse/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── migration-strategy.md
│   ├── modeling-principles.md
│   └── reconciliation-guide.md
├── notebooks/
│   ├── 01_ingest_bronze/
│   ├── 02_raw_vault/
│   ├── 03_business_vault/
│   ├── 04_gold_marts/
│   └── 05_reconciliation/
├── src/
│   ├── ingestion/
│   ├── dv/
│   │   ├── hubs/
│   │   ├── links/
│   │   ├── satellites/
│   │   └── pit_helpers/
│   ├── transforms/
│   └── utils/
├── sql/
│   ├── ddl/
│   ├── views/
│   └── checks/
├── tests/
│   ├── unit/
│   └── data_quality/
├── config/
│   ├── dev.yml
│   ├── test.yml
│   └── prod.yml
└── infra/
    ├── databricks/
    └── terraform/
```

---

## What Each Folder Is For

- `docs/` contains architecture notes, modeling rules, and migration decisions.
- `notebooks/` holds exploratory and pipeline notebooks organized by layer.
- `src/` contains reusable Python code for ingestion, Data Vault objects, and transforms.
- `sql/` stores DDL, view logic, and validation queries.
- `tests/` keeps reconciliation checks and data quality tests.
- `config/` stores environment-specific settings.
- `infra/` contains Databricks deployment and IaC assets.

---

## Core Design Principles

- Preserve source history without overwriting.
- Separate business keys, relationships, and descriptive attributes.
- Make source changes cheap to absorb.
- Keep raw ingestion and business modeling distinct.
- Design for auditability and deterministic reconciliation.

---

## Typical Layer Mapping

| Layer | Purpose | Data Vault Role |
|---|---|---|
| Bronze | Raw ingestion | Source capture and landing zone |
| Silver | Cleaned and integrated data | Raw Vault / Business Vault |
| Gold | Business-ready outputs | Star schemas, marts, reporting tables |

---

## When To Prefer Kimball

Use Kimball when:

- The domain is small.
- The source systems are stable.
- Historical traceability is not a major concern.
- Delivery speed matters more than long-term model flexibility.

In that case, building facts and dimensions directly is often simpler and faster.

---

## Suggested Repo Goals

This repository can be used to:

- Demonstrate an EDW migration pattern on Databricks.
- Compare Data Vault and Kimball approaches.
- Build repeatable reconciliation pipelines.
- Show how a Lakehouse can support enterprise historization and auditability.

---

## License

Add your preferred license here.
