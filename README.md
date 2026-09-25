# Student Analytics Platform: End-to-End Microsoft Fabric Orchestration & Governance

An enterprise end-to-end data analytics and engineering project implemented within **Microsoft Fabric**. The solution ingests academic and behavioral student metrics, enriches the pipeline using external cloud endpoints, automates multi-stage workflows, enforces least-privilege security/governance policies, and tracks comprehensive data lineage for Power BI reporting.

---

## Architecture Overview
External REST API / Raw Datasets ]
│
▼
[ Fabric Lakehouse (Student_LH) ]
│
▼ (PySpark Transformation Logic)
[ Notebook 1 ]
│
▼ (Automated Pipeline Orchestration)
[ pl_student_analytics_automation ]
│
▼ (Scheduled Execution & Refresh)
[ Semantic Model (sm_student_analytics) ]
│
▼ (Row-Level Security & Lineage)
[ sm anayltics Report ]


---

## Core Project Components

### 1. Data Ingestion & Lakehouse Storage
- **Workspace:** `Fabric_Student_Project`
- **Lakehouse:** `Student_LH`
- Implemented Delta Lake architecture to persist curated student academic records alongside historical reference dimensions (`dim_student`, `dim_habits`, `fact_performance`).

### 2. External Cloud Connectivity
- Integrated an external public Cloud REST API via **PySpark** (`requests` and JSON deserialization).
- Ingested real-time external user reference data directly into the Lakehouse as a Delta table (`dbo.external_cloud_users`) without requiring pre-configured credentials or external gateways.

### 3. Pipeline Orchestration & Scheduling
- **Pipeline:** `pl_student_analytics_automation`
- Constructed a sequential execution dependency:
  1. Triggering data engineering transformations (`Notebook 1`).
  2. Orchestrating semantic layer synchronization (`Semantic model refresh`).
- Enabled automated **Daily Scheduled Execution** with proactive run-status alerting.

### 4. Enterprise Security & Access Control
- **Workspace RBAC:** Enforced the principle of least privilege by maintaining pipeline governance under Admin roles while provisioning secure read-only access (`Viewer`) to analytical consumers.
- **Row-Level Security (RLS):** Implemented DAX security predicates on the `sm_student_analytics` semantic model:
  ```dax
  [school_type] = "Public"
Restricted data visibility strictly to authorized user roles while serving reports from a single consolidated data model.

5. Monitoring & Operational Observability
Verified pipeline health, runtime logs, execution IDs, and component latencies via the centralized Microsoft Fabric Monitoring Hub.

Ensured 100% operational success status (Succeeded) across all automated workloads.

6. Data Lineage & Governance
Traced end-to-end visual data provenance from raw lakehouse tables through PySpark transformations to the presentation semantic model and final executive report (sm anayltics).

Repository Structure
├── Notebook 1.ipynb                     # PySpark transformation & API integration script
├── Fabric_Project_Documentation.pdf     # Full technical report with verification screenshots
└── README.md                            # Architecture & project overview
