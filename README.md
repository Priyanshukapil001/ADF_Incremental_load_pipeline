# 🚀 Enterprise Incremental Data Load Framework using Azure Data Factory

![Azure](https://img.shields.io/badge/Azure-Data%20Factory-0078D4?logo=microsoftazure)
![Azure SQL](https://img.shields.io/badge/Azure%20SQL-Database-red?logo=microsoftsqlserver)
![GitHub](https://img.shields.io/badge/Git-Version%20Control-black?logo=github)
![Status](https://img.shields.io/badge/Status-Completed-success)

An enterprise-grade **Incremental Data Loading Framework** built using **Azure Data Factory (ADF)** and **Azure SQL Database**. The solution loads only new or modified records based on the **last_updated** timestamp, maintains execution history in a **last_updated_log** table, and automatically sends **Success** and **Failure Email Notifications** for every pipeline execution.

---

# 📖 Project Overview

In modern data engineering, loading complete datasets on every execution is inefficient and expensive. Organizations require scalable ETL solutions that process only newly inserted or updated records while providing reliable monitoring and alerting.

This project demonstrates a reusable **Incremental ETL Framework** that:

- Reads only incremental records using the **last_updated** column.
- Tracks every successful execution in a **last_updated_log** table.
- Sends automatic **Success** and **Failure Email Notifications**.
- Uses parameterized and metadata-driven pipeline components.
- Reduces execution time and database workload compared to full data loads.

---

# 🎯 Business Problem

Traditional ETL pipelines reload entire tables during every execution, resulting in:

- ❌ Longer execution time
- ❌ Increased infrastructure cost
- ❌ High database workload
- ❌ Unnecessary data movement
- ❌ Lack of execution monitoring
- ❌ Manual verification of pipeline failures

---

# 💡 Solution

The pipeline follows an enterprise incremental loading approach by:

- ✔ Reading the last processed timestamp from **last_updated_log**
- ✔ Fetching only changed records using the **last_updated** column
- ✔ Copying incremental records into the target table
- ✔ Recording the latest processed timestamp
- ✔ Sending automated success or failure notifications

---

# 🏗 Solution Architecture

```text
                 Azure SQL Source
                        │
                        ▼
     Lookup Last Processed Timestamp
           (last_updated_log)
                        │
                        ▼
      Read Incremental Records
(last_updated > Last Processed Timestamp)
                        │
                        ▼
             Records Available?
                │             │
             Yes              No
              │               │
              ▼               ▼
        Copy Activity     Success Email
              │
              ▼
     Get MAX(last_updated)
              │
              ▼
 Insert into last_updated_log
              │
              ▼
     Success Email Notification

If any activity fails
              │
              ▼
     Failure Email Notification
```

---

# 🔄 Pipeline Workflow

1. Retrieve the latest processed timestamp from the **last_updated_log** table.
2. Read only records where **last_updated** is greater than the latest processed timestamp.
3. Validate whether incremental records are available.
4. Copy incremental records into the target table.
5. Retrieve the latest **MAX(last_updated)** value from the source.
6. Insert a new execution record into **last_updated_log**.
7. Send an automatic **Success Email Notification** after successful execution.
8. Send an automatic **Failure Email Notification** if any activity fails.

---

# ⚙ Technologies Used

- Azure Data Factory
- Azure SQL Database
- SQL Server
- SMTP Email Notifications
- Dynamic SQL
- Dynamic Content Expressions
- Parameterized Pipelines
- GitHub

---

# ✨ Features

- ✅ Incremental Data Loading
- ✅ last_updated Based Change Detection
- ✅ last_updated_log Execution Tracking
- ✅ Parameterized Pipeline
- ✅ Dynamic SQL Query Generation
- ✅ Metadata-driven Design
- ✅ Lookup Activity
- ✅ Copy Activity
- ✅ Script Activity
- ✅ If Condition Activity
- ✅ Automatic Success Email Notification
- ✅ Automatic Failure Email Notification
- ✅ Enterprise Error Handling
- ✅ GitHub Version Control

---

# 📂 Repository Structure

```
ADF_Incremental_Load_Pipeline
│
├── pipeline/
├── dataset/
├── linkedService/
├── integrationRuntime/
├── trigger/
├── images/
│     ├── architecture.png
│     ├── pipeline.png
│     ├── pipeline_run.png
│     ├── success_mail.png
│     ├── failure_mail.png
│     ├── source_table.png
│     ├── target_table.png
│     └── last_updated_log.png
│
└── README.md
```

---

# 📸 Architecture Diagram

![Architecture](images/architecture.png)

---

# 📸 ADF Pipeline

![ADF Pipeline](images/pipeline.png)

---

# 📸 Pipeline Execution

![Pipeline Execution](images/pipeline_run.png)

---

# 📸 Source Table

![Source Table](images/source_table.png)

---

# 📸 Target Table

![Target Table](images/target_table.png)

---

# 📸 last_updated_log Table

![last_updated_log](images/last_updated_log.png)

---

# 📧 Email Notifications

## ✅ Success Email

![Success Email](images/success_mail.png)

---

## ❌ Failure Email

![Failure Email](images/failure_mail.png)

---

# 📊 last_updated_log Table

The framework stores every successful execution inside the **last_updated_log** table, allowing the pipeline to identify the latest processed timestamp for future incremental loads.

| Column | Description |
|---------|-------------|
| SchemaName | Source schema |
| TableName | Source table |
| LastUpdatedTimestamp | Latest processed `last_updated` value |
| PipelineRunTime | Pipeline execution timestamp |

---

# 🚀 How It Works

1. Pipeline starts.
2. Reads the latest processed timestamp from **last_updated_log**.
3. Fetches only records where **last_updated > LastUpdatedTimestamp**.
4. Checks whether incremental records exist.
5. Copies records into the target table.
6. Retrieves the latest processed timestamp.
7. Inserts a new record into **last_updated_log**.
8. Sends a Success Email.
9. If any activity fails, a Failure Email is automatically sent.

---

# 🚀 Getting Started

## Prerequisites

- Azure Subscription
- Azure Data Factory
- Azure SQL Database
- SQL Server Management Studio (SSMS)
- GitHub Repository

## Steps

1. Clone this repository.
2. Import the ADF pipeline.
3. Configure Azure SQL linked services.
4. Create Source, Target and **last_updated_log** tables.
5. Update pipeline parameters.
6. Trigger the pipeline.
7. Verify:
   - Target table
   - last_updated_log table
   - Email notifications
   - Pipeline Monitor

---

# 📈 Future Enhancements

- Azure Key Vault Integration
- Change Data Capture (CDC)
- Metadata Configuration Table
- Parallel Table Processing
- Azure Monitor Integration
- Microsoft Teams Notifications
- Logging Dashboard
- CI/CD using GitHub Actions

---

# 📚 Skills Demonstrated

This project demonstrates practical implementation of:

- Azure Data Factory
- Azure SQL Database
- Enterprise ETL Design
- Incremental Data Loading
- Dynamic SQL
- Parameterized Pipelines
- Metadata-driven Framework
- Dynamic Content Expressions
- Pipeline Error Handling
- Automated Email Notifications(Logic APP)
- GitHub Version Control

---

# ⭐ Support

If you found this project useful, consider giving it a ⭐ on GitHub.

---

# 👨‍💻 Author

**Priyanshu Kapil**

**Data Engineer | Azure | SQL | Azure Data Factory | Power BI**

Passionate about building scalable, enterprise-grade data engineering solutions and automating modern ETL workflows.
