# insureflow-azure-data-engineering
End-to-end Azure Data Engineering project for Insurance domain using ADF, Databricks, PySpark, Delta Lake - Medallion Architecture
# 🏦 InsureFlow — Azure Insurance Data Engineering Project

![Azure](https://img.shields.io/badge/Azure-Data%20Engineering-0078D4?style=for-the-badge&logo=microsoft-azure)
![Databricks](https://img.shields.io/badge/Databricks-PySpark-FF3621?style=for-the-badge&logo=databricks)
![ADF](https://img.shields.io/badge/Azure%20Data%20Factory-Pipeline-00B4D8?style=for-the-badge)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-Medallion-00ADD8?style=for-the-badge)

## 📌 Project Overview

End-to-end **Azure Data Engineering** project simulating a real-world **Insurance Analytics Platform**. Built using **Medallion Architecture (Bronze → Silver → Gold)** with full pipeline orchestration via **Azure Data Factory**.

---

## 🏗️ Architecture

```
Raw CSV Files (160,000 rows)
        ↓
   [Azure Data Factory]
        ↓
  Bronze Layer (ADLS Gen2)     ← Raw ingested data
        ↓
  [Azure Databricks + PySpark]
        ↓
  Silver Layer (Delta Format)  ← Cleaned & standardized
        ↓
  [Azure Databricks + PySpark]
        ↓
  Gold Layer (Delta Format)    ← Business aggregations
        ↓
  [Azure SQL Database]         ← Segment Data Warehouse
        ↓
  Power BI Dashboard           ← Reporting & Analytics
```

---

## 🛠️ Tech Stack

| Service | Purpose |
|---------|---------|
| Azure Data Factory | Pipeline orchestration & scheduling |
| Azure Databricks | PySpark transformations |
| Azure Data Lake Storage Gen2 | Medallion storage (Bronze/Silver/Gold) |
| Delta Lake | ACID transactions & versioning |
| Azure SQL Database | Gold layer serving (Segment DW) |
| Azure Key Vault | Secrets management |
| Power BI | Business dashboards |
| GitHub | Version control & CI/CD |

---

## 📊 Dataset

| Table | Records | Description |
|-------|---------|-------------|
| customers.csv | 10,000 | Customer personal & contact data |
| policies.csv | 25,000 | Insurance policy details |
| claims.csv | 50,000 | Claims filed against policies |
| payments.csv | 75,000 | Premium payment transactions |
| **Total** | **160,000** | **Rows processed** |

---

## 🔄 Pipeline Flow

```
tr_insureflow_10min (Schedule Trigger)
        ↓
nb_silver_customers    → Bronze → Silver (10,000 records)
        ↓
nb_silver_policies     → Bronze → Silver (25,000 records)
        ↓
nb_silver_claims       → Bronze → Silver (50,000 records)
        ↓
nb_silver_payments     → Bronze → Silver (75,000 records)
        ↓
nb_gold_summary        → Silver → Gold (62,000 records)
        ↓
nb_gold_to_sql         → Gold → Azure SQL DB
        ↓
nb_audit_log           → Pipeline audit logging
```

---

## 📁 Project Structure

```
insureflow-azure-data-engineering/
├── adf/                          ← ADF pipeline JSON files
│   ├── pipeline/
│   │   └── pl_master_insureflow.json
│   ├── linkedService/
│   │   ├── ls_databricks_insureflow.json
│   │   └── ls_adls_insureflow.json
│   └── trigger/
│       └── tr_insureflow_10min.json
├── InsureFlow_notebooks.dbc      ← Databricks notebooks
└── README.md
```

---

## 🏅 Key Achievements

- ✅ Designed **Medallion Architecture** (Bronze → Silver → Gold) on ADLS Gen2
- ✅ Built **parameterized ADF pipelines** with schedule triggers
- ✅ Implemented **PySpark transformations** with Delta Lake format
- ✅ Created **business aggregations**: Claims Summary, Customer Risk Profile, Policy Performance
- ✅ Loaded Gold layer to **Azure SQL Database** (Segment DW)
- ✅ Secured all credentials using **Azure Key Vault** + Service Principal
- ✅ Implemented **audit logging** for every pipeline run
- ✅ Version controlled with **GitHub CI/CD**

---

## 🔐 Security

- All secrets stored in **Azure Key Vault**
- Authentication via **Service Principal** (OAuth 2.0)
- ADLS Gen2 access via **RBAC** (Storage Blob Data Contributor)
- SQL Database access via **JDBC with encrypted connection**

---

## 📈 Gold Layer Tables (Azure SQL DB)

| Table | Rows | Description |
|-------|------|-------------|
| dbo.claims_summary | 27,078 | Claims by policy type, month, state |
| dbo.customer_risk_profile | 9,923 | Customer risk categorization (HIGH/MEDIUM/LOW) |
| dbo.policy_performance | 25,000 | Policy loss ratio & performance metrics |

---

## 👨‍💻 Author

**Madhu Kondaveti**  
Azure Data Engineer | TCS  
📧 kondavetimadhu@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/kondavetimadhu)

---

## 📜 Certifications

- DP-700 Fabric Data Engineer Associate
- Databricks Certified Data Engineer Associate
- Databricks Certified Data Analyst Associate
