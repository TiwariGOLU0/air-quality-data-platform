# Air Quality Data Platform

An enterprise-grade, cloud-native data lakehouse built with AWS, PySpark, Apache Airflow, and Power BI to ingest, validate, transform, and analyze multi-year environmental metrics.

## 📁 Project Directory Structure

```text
air-quality-data-platform/
│
├── resources/
│   ├── dev/                  # Development configs, database URIs, S3 paths, environment variables
│   ├── qa/                   # QA environment properties and validation configs
│   ├── prod/                 # Production configuration templates
│   └── sql_scripts/          # Athena / Spark SQL DDLs, views, and analytical query scripts
│
├── infrastructure/           # Infrastructure as Code (Terraform / CloudFormation)
│   ├── s3_buckets.tf         # S3 Landing, Bronze, Silver, and Gold bucket definitions
│   ├── iam_roles.tf          # IAM policies and roles for Glue, Lambda, and Airflow
│   ├── glue_catalog.tf       # AWS Glue Databases, Crawlers, and Data Catalog setup
│   └── sns_alerts.tf         # Amazon SNS topics and subscriptions for data quality failures
│
├── airflow/                  # Orchestration pipelines (DAGs)
│   └── dags/
│       └── air_quality_etl_pipeline.py  # Orchestrates Ingest -> Bronze -> Silver -> Quality Gate -> Gold
│
├── src/
│   └── main/
│       ├── delete/           # S3 temporary cleanup & file management utilities
│       ├── download/         # Kaggle API integration scripts to fetch raw air quality data
│       ├── move/             # S3 bucket-to-bucket file movement scripts (Landing -> Bronze)
│       ├── read/             # PySpark / Pandas readers for CSV, JSON, and Parquet formats
│       ├── transformations/  # Core cleaning & processing logic matching architecture diagram
│       │   └── jobs/         # PySpark scripts for Silver cleansing & Gold aggregation ETLs
│       ├── upload/           # Uploader handlers pushing raw files into S3 Landing zone
│       ├── utility/
│       │   ├── encrypt_decrypt.py  # Credential and token management utilities
│       │   └── logging_config.py   # Centralized Amazon CloudWatch logging setup
│       └── write/            # Writers persisting Parquet data to Silver/Gold S3 & Glue Catalog
│
├── tests/                    # Unit & integration tests for data pipelines and quality checks
│   ├── test_transformations.py
│   └── test_data_quality.py
│
├── powerbi/                  # Analytics & Consumption tier assets
│   ├── air_quality_dashboard.pbix  # Power BI report connected via Amazon Athena / S3 Gold
│   └── dax_measures.md       # Documented DAX queries for YoY, seasonal, and city trends
│
├── docs/                     # Architecture diagrams, data lineage, and documentation
│   └── architecture_diagram.png
│
├── .github/
│   └── workflows/
│       └── ci_cd_pipeline.yml  # Automated linting, testing, and deployment to AWS
│
├── .gitignore
├── requirements.txt          # Python dependencies (boto3, pyspark, kagglehub, pandas)
└── README.md                 # Professional project portfolio overview
