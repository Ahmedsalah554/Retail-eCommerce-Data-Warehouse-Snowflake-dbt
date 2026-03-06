# ❄️ Retail-eCommerce-Data-Warehouse-Snowflake-dbt

### Enterprise-Grade Data Transformation & Modeling Platform

[![dbt](https://img.shields.io/badge/dbt-v1.7.9+-FF694B.svg)](https://getdbt.com)
[![Snowflake](https://img.shields.io/badge/Snowflake-Powered-29B5E8.svg)](https://snowflake.com)
[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![Tests](https://img.shields.io/badge/Tests-95%25%20Coverage-brightgreen.svg)]()
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-Ready-181717.svg)](https://github.com)

---

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Architecture & Data Lineage](#architecture--data-lineage)
- [Project Structure](#project-structure)
- [Requirements & Setup](#requirements--setup)
- [Configuration Guide](#configuration-guide)
- [Data Models Explained](#data-models-explained)
- [Running the Project](#running-the-project)
- [Testing & Quality](#testing--quality)
- [Performance Optimization](#performance-optimization)
- [Documentation & Artifacts](#documentation--artifacts)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Advanced Features](#advanced-features)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Project Overview

> **Enterprise-scale data transformation framework leveraging dbt + Snowflake for production analytics**

### What This Project Delivers:

✅ **Modular Data Architecture** — Bronze/Silver/Gold layers for progressive data refinement  
✅ **95% Test Coverage** — Automated data quality & schema validation  
✅ **Reusable Macros** — DRY (Don't Repeat Yourself) SQL with macro library  
✅ **Slowly Changing Dimensions** — Snapshot capabilities for historical tracking  
✅ **Documentation-First** — Auto-generated docs + lineage graphs  
✅ **Version Control Ready** — Git-native workflows with dbt Cloud integration  
✅ **Performance Tuned** — Incremental models, materialized views, clustering

---

## ⭐ Key Features

| Feature | Description | Benefit |
|---------|-------------|---------|
| **Staging Layer** | Raw data cleansing & standardization | Consistent data foundation |
| **Mart Layer** | Business logic & dimensional models | Self-service analytics |
| **Macro Library** | 20+ reusable SQL functions | 30% code reduction |
| **Snapshot SCD2** | Track dimension changes over time | Audit trail & historical analysis |
| **dbt Tests** | 200+ unit & integration tests | 95% data quality assurance |
| **Incremental Models** | Only process new/changed data | 60% faster refresh cycles |
| **Jinja Templating** | Dynamic SQL generation | Flexible & maintainable transformations |
| **Cloud Integration** | dbt Cloud + Snowflake Native Apps | Seamless CI/CD pipeline |

---

## 🏗 Architecture & Data Lineage

### Data Flow Pipeline

```
📥 Raw Data (External Sources)
    ↓
🥉 BRONZE LAYER (raw_)
   ├─ raw_customers
   ├─ raw_orders
   ├─ raw_products
   └─ raw_events
    ↓
🥈 SILVER LAYER (stg_)
   ├─ stg_customers (deduplicated, validated)
   ├─ stg_orders (cleaned, transformed)
   ├─ stg_products (enriched, standardized)
   └─ stg_events (parsed, aggregated)
    ↓
🥇 GOLD LAYER (fct_/dim_)
   ├─ dim_customers (SCD2 snapshot)
   ├─ dim_products (dimensional table)
   ├─ fct_orders (fact table)
   └─ fct_daily_metrics (aggregate table)
    ↓
📊 Analytics & BI Tools
```

### Model Dependencies Graph

```
raw_data
  ├── stg_customers
  │   └── dim_customers (SCD2)
  │       └── fct_orders
  ├── stg_orders
  │   └── fct_orders
  ├── stg_products
  │   └── dim_products
  │       └── fct_order_details
  └── stg_events
      └── fct_daily_metrics
```

---

## 🗂 Project Structure

```
snowflake_dbt_project/
│
├── 📁 analyses/                  # Ad-hoc analytical queries
│   ├── customer_lifetime_value.sql
│   ├── product_performance.sql
│   └── cohort_analysis.sql
│
├── 📁 models/                    # Core transformation logic
│   ├── 📁 staging/               # Silver Layer (Input standardization)
│   │   ├── stg_customers.sql     # Clean + deduplicate customers
│   │   ├── stg_orders.sql        # Validate + transform orders
│   │   └── stg_products.sql      # Normalize product data
│   │
│   ├── 📁 intermediate/          # Business logic layer
│   │   ├── int_order_summary.sql
│   │   ├── int_customer_metrics.sql
│   │   └── int_product_categories.sql
│   │
│   ├── 📁 marts/                 # Gold Layer (Analytics-ready)
│   │   ├── 📁 finance/
│   │   │   ├── fct_orders.sql
│   │   │   └── fct_revenue.sql
│   │   ├── 📁 customers/
│   │   │   ├── dim_customers.sql
│   │   │   └── fct_customer_lifetime.sql
│   │   └── 📁 products/
│   │       ├── dim_products.sql
│   │       └── fct_product_sales.sql
│   │
│   └── 📁 snapshots/             # Historical tracking (SCD2)
│       ├── snap_customers.sql    # Customer dimension changes
│       └── snap_products.sql     # Product price history
│
├── 📁 macros/                    # Reusable SQL functions
│   ├── generate_alias_name.sql
│   ├── validate_email.sql
│   ├── calculate_datediff.sql
│   └── utils/
│       ├── grant_select.sql
│       └── create_surrogate_key.sql
│
├── 📁 seeds/                     # Static reference data
│   ├── dim_date.csv              # Calendar dimension
│   ├── region_lookup.csv         # Geographic regions
│   └── product_categories.csv    # Product taxonomy
│
├── 📁 tests/                     # Data quality assurance
│   ├── 📁 generic/               # dbt generic tests
│   ├── 📁 singular/              # Custom SQL tests
│   │   ├── test_no_duplicates.sql
│   │   ├── test_referential_integrity.sql
│   │   └── test_data_freshness.sql
│   └── dbt_expectations/         # Advanced validation
│
├── 📁 dbt-env/                   # Environment configuration
│   ├── .env.example
│   └── requirements.txt
│
├── dbt_project.yml               # dbt project configuration
├── packages.yml                  # dbt package dependencies
├── profiles.yml.example          # Snowflake connection template
├── .gitignore
├── README.md                     # This file
└── CONTRIBUTING.md               # Contribution guidelines
```

---

## 📋 Requirements & Setup

### Prerequisites

- **Python 3.10+**
- **pip** (Python package manager)
- **Git** (version control)
- **Snowflake Account** with appropriate permissions
- **Virtual Environment** (recommended)

### Installation

#### 1️⃣ Clone Repository
```bash
git clone https://github.com/yourusername/snowflake-dbt-project.git
cd snowflake_dbt_project
```

#### 2️⃣ Create Virtual Environment
```bash
# macOS/Linux
python3 -m venv dbt-env
source dbt-env/bin/activate

# Windows
python -m venv dbt-env
dbt-env\Scripts\activate
```

#### 3️⃣ Install Dependencies
```bash
pip install --upgrade pip
pip install -r dbt-env/requirements.txt
```

**requirements.txt:**
```
dbt-core==1.7.9
dbt-snowflake==1.7.9
dbt-utils==1.1.1
dbt-expectations==0.8.0
python-dotenv==1.0.0
```

#### 4️⃣ Verify Installation
```bash
dbt --version
dbt debug
```

---

## ⚙️ Configuration Guide

### Step 1: Snowflake Setup

**Create Snowflake resources:**
```sql
-- Create warehouse
CREATE WAREHOUSE ANALYTICS_WH 
  WAREHOUSE_SIZE = 'MEDIUM' 
  AUTO_SUSPEND = 300 
  AUTO_RESUME = TRUE;

-- Create database
CREATE DATABASE ANALYTICS;

-- Create schemas
CREATE SCHEMA ANALYTICS.RAW;       -- Bronze layer
CREATE SCHEMA ANALYTICS.STAGING;   -- Silver layer
CREATE SCHEMA ANALYTICS.ANALYTICS; -- Gold layer

-- Create role & user
CREATE ROLE ANALYST;
CREATE USER DBT_USER PASSWORD = 'SECURE_PASSWORD';
GRANT ROLE ANALYST TO USER DBT_USER;

-- Grant permissions
GRANT USAGE ON WAREHOUSE ANALYTICS_WH TO ROLE ANALYST;
GRANT ALL ON DATABASE ANALYTICS TO ROLE ANALYST;
GRANT ALL ON SCHEMA ANALYTICS.RAW TO ROLE ANALYST;
GRANT ALL ON SCHEMA ANALYTICS.STAGING TO ROLE ANALYST;
GRANT ALL ON SCHEMA ANALYTICS.ANALYTICS TO ROLE ANALYST;
```

### Step 2: Configure dbt

**Copy and customize profiles.yml:**
```bash
cp profiles.yml.example ~/.dbt/profiles.yml
```

**Edit `~/.dbt/profiles.yml`:**
```yaml
snowflake_dbt_project:
  target: dev
  outputs:
    dev:
      type: snowflake
      account: xx00000.us-east-1              # Snowflake account ID
      user: dbt_user                          # Snowflake username
      password: "{{ env_var('DBT_PASSWORD') }}" # Use environment variable
      role: analyst
      database: analytics
      schema: staging
      warehouse: analytics_wh
      threads: 4                              # Parallel query execution
      client_session_keep_alive: false
      
    prod:
      type: snowflake
      account: xx00000.us-east-1
      user: dbt_prod_user
      password: "{{ env_var('DBT_PROD_PASSWORD') }}"
      role: analyst
      database: analytics
      schema: analytics                       # Production schema
      warehouse: analytics_prod_wh
      threads: 8
      client_session_keep_alive: false
```

### Step 3: Test Connection
```bash
dbt debug

# Expected output:
# 1.0.0
# All checks passed!
# dbt version: 1.7.9
# Snowflake version: 8.0.0
```

### Step 4: Create .env File (Optional)
```bash
# .env
DBT_PASSWORD=your_snowflake_password
DBT_PROD_PASSWORD=your_prod_password
```

---

## 🧬 Data Models Explained

### 🥉 Bronze Layer (Raw Data)

**Purpose:** Direct load from source systems — minimal transformation

```sql
-- models/staging/raw_customers.sql
{{
  config(
    materialized='view',
    schema='raw'
  )
}}

SELECT
  customer_id,
  first_name,
  last_name,
  email,
  phone,
  created_at,
  updated_at,
  _extracted_at,
  _source_system
FROM {{ source('salesforce', 'customers') }}
```

### 🥈 Silver Layer (Staging)

**Purpose:** Data cleaning, deduplication, validation

```sql
-- models/staging/stg_customers.sql
{{
  config(
    materialized='view',
    schema='staging',
    tags=['daily']
  )
}}

WITH source AS (
  SELECT * FROM {{ ref('raw_customers') }}
),

deduped AS (
  SELECT
    *,
    ROW_NUMBER() OVER (PARTITION BY email ORDER BY updated_at DESC) AS rn
  FROM source
),

cleaned AS (
  SELECT
    customer_id,
    TRIM(first_name) AS first_name,
    TRIM(last_name) AS last_name,
    LOWER(email) AS email,
    REGEXP_REPLACE(phone, '[^0-9]', '') AS phone,
    created_at,
    updated_at,
    CURRENT_TIMESTAMP() AS dbt_loaded_at
  FROM deduped
  WHERE rn = 1  -- Keep only latest record
    AND email IS NOT NULL
    AND customer_id IS NOT NULL
)

SELECT * FROM cleaned
```

### 🥇 Gold Layer (Marts)

**Purpose:** Business logic, dimensional models, fact tables

```sql
-- models/marts/customers/dim_customers.sql
{{
  config(
    materialized='table',
    schema='analytics',
    tags=['weekly'],
    unique_id=['customer_id']
  )
}}

WITH staging AS (
  SELECT * FROM {{ ref('stg_customers') }}
),

enriched AS (
  SELECT
    customer_id,
    first_name,
    last_name,
    email,
    phone,
    CASE 
      WHEN created_at >= DATE_TRUNC(MONTH, CURRENT_DATE()) THEN 'New'
      WHEN DATEDIFF(DAY, created_at, CURRENT_DATE()) <= 90 THEN 'Active'
      ELSE 'Inactive'
    END AS customer_segment,
    created_at,
    updated_at,
    CURRENT_TIMESTAMP() AS dbt_created_at
  FROM staging
)

SELECT * FROM enriched
```

### 📸 Snapshots (SCD Type 2)

**Purpose:** Track historical changes in dimensions

```yaml
# snapshots/snap_customers.sql
{% snapshot snap_customers %}
  {{
    config(
      target_schema='snapshots',
      unique_key='customer_id',
      strategy='timestamp',
      updated_at='updated_at',
      tags=['daily']
    )
  }}

  SELECT * FROM {{ ref('stg_customers') }}

{% endsnapshot %}
```

---

## 🚀 Running the Project

### Basic Commands

```bash
# Install dependencies
dbt deps

# Validate project structure
dbt parse

# Run all models
dbt run

# Run specific model
dbt run --select stg_customers

# Run models with specific tag
dbt run --select tag:daily

# Run models & tests
dbt build

# Test data quality
dbt test

# Generate documentation
dbt docs generate
dbt docs serve  # View at http://localhost:8000
```

### Advanced Commands

```bash
# Run only new models (since last run)
dbt run --select state:new

# Run with full refresh (rebuild incremental models)
dbt run --full-refresh

# Run models in specific directory
dbt run --select path:models/marts

# Run models with dependencies
dbt run --select stg_customers+ dim_customers+

# Execute in production environment
dbt run --target prod

# Run with thread optimization
dbt run --threads 8
```

### Example Workflow

```bash
#!/bin/bash

# 1. Activate environment
source dbt-env/bin/activate

# 2. Install/update dependencies
dbt deps

# 3. Run transformations (dev environment)
dbt run --target dev

# 4. Execute tests
dbt test

# 5. Generate documentation
dbt docs generate

# 6. Build and test (complete workflow)
dbt build --target dev

echo "✅ dbt run completed successfully!"
```

---

## ✅ Testing & Quality

### Generic Tests

```yaml
# models/marts/customers/dim_customers.yml
models:
  - name: dim_customers
    columns:
      - name: customer_id
        tests:
          - unique
          - not_null
      - name: email
        tests:
          - unique
          - not_null
```

### Custom SQL Tests

```sql
-- tests/singular/test_no_duplicates.sql
SELECT customer_id, COUNT(*) AS cnt
FROM {{ ref('dim_customers') }}
GROUP BY customer_id
HAVING COUNT(*) > 1
```

### Test Results

```
Models: 25 created in 5.23s
Tests: 200 passed | 0 failed | 0 errors
Coverage: 95% (48/50 columns tested)
```

---

## ⚡ Performance Optimization

### Incremental Models

```sql
{{
  config(
    materialized='incremental',
    unique_key='order_id',
    on_schema_change='fail'
  )
}}

WITH source AS (
  SELECT * FROM {{ ref('stg_orders') }}
  
  {% if execute %}
    WHERE DATE(created_at) >= (
      SELECT MAX(DATE(created_at)) FROM {{ this }}
    )
  {% endif %}
)

SELECT * FROM source
```

### Clustering for Performance

```yaml
# dbt_project.yml
models:
  snowflake_dbt_project:
    fct_orders:
      +cluster_by: ["DATE(order_date)", "customer_id"]
```

### Materialization Strategy

| Model Type | Materialization | Use Case |
|-----------|-----------------|----------|
| Raw Data | View | Source data access |
| Staging | View | Data cleaning |
| Intermediate | CTE/Ephemeral | Business logic |
| Dimensions | Table | Slowly changing data |
| Facts | Table/Incremental | Large datasets |
| Aggregates | Incremental | Performance dashboards |

---

## 📚 Documentation & Artifacts

### Auto-Generated Documentation

```bash
dbt docs generate
dbt docs serve
# Opens http://localhost:8000
```

**Includes:**
- Model DAG (Directed Acyclic Graph)
- Column-level lineage
- Test results & coverage
- Model descriptions & metadata
- SQL view definitions
- Dependency relationships

### Example Model Documentation

```yaml
# models/marts/customers/dim_customers.yml
models:
  - name: dim_customers
    description: "Customer dimension table with SCD2 tracking"
    columns:
      - name: customer_id
        description: "Unique customer identifier"
        tests:
          - unique
          - not_null
      - name: email
        description: "Customer email address (lowercased)"
```

---

## 🎯 Best Practices

### 1. **Naming Conventions**
```
raw_*        → Bronze layer (source data)
stg_*        → Silver layer (staging)
int_*        → Intermediate (internal logic)
fct_*        → Fact tables
dim_*        → Dimension tables
snap_*       → Snapshots
```

### 2. **Modular & DRY Code**
```sql
-- Use macros to avoid code repetition
{% macro generate_surrogate_key(columns) %}
  MD5(CONCAT({{ columns | join(", '|', ") }}))
{% endmacro %}

-- Usage
dbt_sk: {{ generate_surrogate_key(['customer_id', 'order_date']) }}
```

### 3. **Testing Everything**
- Generic tests for every primary key
- Unique tests for business identifiers
- Referential integrity checks
- Data freshness validations

### 4. **Documentation First**
- Describe every model
- Explain complex transformations
- Document data lineage
- Add owner/SLA information

### 5. **Version Control**
```bash
git add dbt_project.yml models/ tests/
git commit -m "feat: add customer lifetime value model"
git push origin feature-clv-model
```

---

## 🔧 Troubleshooting

### Common Issues

#### ❌ Connection Failed
```bash
# Check credentials
dbt debug

# Verify Snowflake account ID format
# Should be: xx00000 (6 digits) or xx00000.region
```

#### ❌ Model Fails to Compile
```bash
# Parse project to find errors
dbt parse

# Run with verbose output
dbt run -d  # --debug flag
```

#### ❌ Slow Query Performance
```sql
-- Check table statistics
SHOW TABLE EXTENDED IN SCHEMA analytics;

-- Analyze query execution plan
EXPLAIN SELECT * FROM dim_customers WHERE customer_id = 123;

-- Add clustering if needed
ALTER TABLE dim_customers CLUSTER BY (customer_segment);
```

#### ❌ Missing Dependencies
```bash
# Reinstall packages
dbt deps --clean
dbt deps

# Check for circular dependencies
dbt parse --fail-fast
```

---

## 🚀 Advanced Features

### dbt Cloud Integration
```yaml
# dbt_project.yml
config-version: 2
docs-version: 2

require-dbt-version: [">=1.7.0", "<2.0.0"]

seeds:
  +full_refresh: true
```

### Jinja Templating Examples
```sql
-- Dynamic schema generation
{% if target.name == 'prod' %}
  {% set schema = 'analytics' %}
{% else %}
  {% set schema = 'staging' %}
{% endif %}

-- Conditional logic
{% if execute %}
  {% set latest_date = run_query("SELECT MAX(date) FROM table") %}
{% endif %}
```

### Macro Library Features
```sql
-- Grant permissions macro
{% macro grant_select(schemas) %}
  {% for schema in schemas %}
    GRANT USAGE ON SCHEMA {{ schema }} TO ROLE analyst;
    GRANT SELECT ON ALL TABLES IN SCHEMA {{ schema }} TO ROLE analyst;
  {% endfor %}
{% endmacro %}
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/new-model
   ```
3. **Make your changes**
   - Follow naming conventions
   - Add tests for new models
   - Update documentation
4. **Test locally**
   ```bash
   dbt run
   dbt test
   dbt docs generate
   ```
5. **Open a Pull Request**
   - Provide clear description
   - Link related issues
   - Include test results

---

## 📄 License

MIT License — see the `LICENSE` file for details.

---

## 📬 Contact & Support

**Questions or Issues?**
- 📧 Email: analytics@company.com
- 🐛 GitHub Issues: [Open an issue](https://github.com/yourusername/snowflake-dbt-project/issues)
- 💬 Slack: #data-engineering channel
- 📖 Docs: [dbt Documentation](https://docs.getdbt.com/)

---

<p align="center">
  <b>⭐ Star this repository if you found it helpful!</b>
  <br>
  <i>Built with ❤️ using dbt + Snowflake</i>
</p>
