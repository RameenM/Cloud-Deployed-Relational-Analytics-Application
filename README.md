# Mini Project 2: Cloud-Deployed Relational Analytics Application (PostgreSQL + Streamlit)

## 🚀 Live Application (Start Here)

**Streamlit App:**  
👉 https://mini-project2-streamlit.onrender.com

**Access Password:**  
🔑 `runproject2`

> The application is password-protected to demonstrate basic access control and prevent unintended public usage.

---

## Project Overview
This project implements a cloud-deployed relational analytics application that integrates a structured PostgreSQL database with an interactive Streamlit frontend. The objective is to demonstrate an end-to-end analytics pipeline—from cleaned data preparation and database migration to application-layer querying and user interaction—using reproducible and transparent Python-based workflows.

The project emphasizes database structure awareness, controlled SQL execution, and application-level access to relational data rather than predictive modeling or advanced machine learning.

---

## Data Source: Cleaned Customer Orders Dataset
The project uses a final cleaned and denormalized dataset (`cleaned_customer_orders.csv`) that serves as the authoritative data reference.

The dataset combines:
- Customer-level attributes (name, city, country, region)
- Product information
- Order-level transaction details

Each row represents a customer record with associated product order information. The structure supports direct filtering, grouping, and aggregation within Jupyter notebooks and the Streamlit application without requiring additional joins or preprocessing.

All analytical logic and application behavior reference this dataset directly. No separate SQL extraction or transformation scripts are included, as data preparation was completed prior to final analysis and the dataset is provided in its validated form.

---

## Database Exploration and Schema Validation Notebook
The project includes a notebook that documents the exploratory and validation phase of the PostgreSQL database.

### Purpose
The notebook verifies:
- Database connectivity
- Table availability and schema structure
- Referential integrity across tables
- Query accessibility for analytics and application use

### Key Activities
- Establishes a live connection to a PostgreSQL database hosted on Render
- Executes direct SQL queries using `pd.read_sql()`
- Inspects core tables:
  - `region`
  - `country`
  - `customer`
  - `product`
  - `orderdetail`
- Confirms foreign key relationships and identifier alignment
- Performs row count and volume checks (600k+ order detail records)
- Ensures clean data retrieval into Pandas DataFrames

### Why This Notebook Exists
This notebook functions as a **structural validation layer**, not a transformation or modeling pipeline. It ensures that downstream analytics and applications operate on a verified and navigable relational foundation.

No business logic, feature engineering, or data cleaning is performed in this notebook.

---

## SQLite to PostgreSQL Migration Script
The project includes a Python script that migrates a normalized SQLite database into a PostgreSQL database hosted on Render.

### Purpose
The script bridges local development and cloud deployment by:
- Creating the full relational schema
- Enforcing primary and foreign key constraints
- Migrating data in a controlled and reproducible manner

### What the Script Does
- Connects to a local SQLite database
- Connects to a PostgreSQL database on Render
- Drops existing PostgreSQL tables to prevent schema conflicts
- Recreates all tables with explicit constraints
- Migrates data in dependency-safe order:
  - Region
  - Country
  - Customer
  - ProductCategory
  - Product
  - OrderDetail
- Uses batch inserts (`execute_batch`) for performance
- Commits transactions explicitly to preserve data integrity

### Role in the Pipeline
This script serves as the **infrastructure preparation layer**, cleanly separating database setup from analytics and application logic.

---

## Streamlit Application (Python Application Architecture)
The project includes an interactive Streamlit application implemented as a Python web application that integrates database access, application logic, and user interface components.

### Application Architecture Overview
The application follows a layered Python design:

- **Configuration Layer**
  - Streamlit layout and page setup
  - Custom CSS styling
  - Environment variable handling
- **Access Control Layer**
  - Password-based access gating
  - Controlled execution termination when unauthorized
- **Database Integration Layer**
  - PostgreSQL connectivity via `psycopg2`
  - Cached connections for efficiency
  - SQL execution via Pandas `read_sql()`
- **Application Logic Layer**
  - Predefined SQL query templates
  - Dynamic user-driven query execution
  - Schema-aware natural language to SQL translation
- **Presentation Layer**
  - Tabular result rendering
  - Row-level inspection for interpretability
  - Interactive selection widgets and execution controls

This structure reflects standard Python application design principles adapted for an interactive analytics environment.

---

## Execution Flow (Python Perspective)
From a Python execution standpoint, the application follows a deterministic flow:

1. Initialize application configuration and UI styling
2. Authenticate user access via password input
3. Establish and cache PostgreSQL database connection
4. Capture SQL or natural language input
5. Generate or execute validated SQL queries
6. Retrieve results into Pandas DataFrames
7. Display results and handle errors gracefully

Optional AI-assisted SQL generation is implemented with strict schema constraints to prevent invalid or unsafe queries.

---

## Dependencies
The project includes a `requirements.txt` file to ensure reproducibility and support deployment.

Key dependencies:
- `streamlit` — interactive web application framework
- `pandas` — data handling and transformation
- `psycopg2-binary` — PostgreSQL connectivity
- `openai` *(optional)* — natural language to SQL generation


---

## Limitations
- Data is static and pre-cleaned
- No incremental database synchronization is implemented
- The migration script is designed for controlled redeployment, not live updates
- Natural language query generation depends on external API availability
- The project prioritizes structure, transparency, and reproducibility over predictive modeling

---

## Summary
This project demonstrates an end-to-end relational analytics pipeline integrating cleaned data, cloud-hosted databases, Python-based migration scripts, and an interactive Streamlit application. The emphasis is on sound database design, controlled SQL execution, and practical application development rather than exploratory or predictive analytics.

