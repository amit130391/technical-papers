# Data Warehousing

**Technical Paper**\
**Date:** 2nd November 2026

## 1. Introduction
Modern organizations rely on data to understand customers, manage
operations, evaluate performance, forecast demand, and make strategic
decisions. Relevant information, however, is rarely stored in one place.
Sales transactions may reside in an operational database, customer
information in a customer relationship management system, inventory
records in an enterprise resource planning application, and website
activity in analytics platforms.

## 2. Need for Data Warehousing
* **Handling Large Data Volumes:** Traditional databases store limited data (MBs to GBs), while data warehouses are built to handle huge datasets (up to TBs), making it easier to store and analyze long-term historical data.
* **Enhanced Analytics:** Databases handle transactions; data warehouses are optimized for complex analysis and historical insights.
* **Centralized Data Storage:** A data warehouse combines data from multiple sources, giving a single, unified view for better decision-making.
* **Trend Analysis:** By storing historical data, a data warehouse allows businesses to analyze trends over time, enabling them to make strategic decisions based on past performance and predict future outcomes.
* **Business Intelligence Support:** Data warehouses work with BI tools to give quick access to insights, helping in data-driven decisions and improving efficiency.

## 3. Core Characteristics

A **data warehouse** is a centralized analytical data repository that
stores integrated data from multiple sources, often over extended
periods, to support querying, reporting, analysis, and decision-making.

A data warehouse has four characteristics:

### 3.1 Subject-oriented

Data is organized around important business subjects, such as customers,
products, sales, suppliers, and finance. This differs from many
operational applications, which are organized around individual
processes or transactions.

### 3.2 Integrated

Data from different systems is standardized and reconciled. For example,
one source may represent a country as `IN`, another as `India`, and a
third as `IND`. Integration establishes consistent representations so
that the records can be analysed together.

### 3.3 Time-variant

A warehouse commonly retains historical snapshots or events. This
enables users to analyse how a business measure changes over time,
rather than seeing only the current state.

### 3.4 Non-volatile

Warehouse data is generally loaded and then queried, rather than
frequently changed by individual business transactions. Corrections,
reloads, and controlled updates still occur, but the environment is not
typically used as the primary system for processing everyday
transactions.

## 4. Data Warehouse Architecture

A data warehouse architecture describes how data moves from source
systems through ingestion, transformation, storage, and analytical
access.

A common logical architecture contains the following layers:

1.  **Source layer:** Operational databases, business applications,
    files, APIs, logs, and external datasets.
2.  **Ingestion layer:** Batch pipelines, change data capture (CDC),
    streaming systems, or file transfers that move source data into the
    analytical environment.
3.  **Staging layer:** A temporary or persistent area where incoming
    data is stored before it is cleaned and transformed.
4.  **Transformation and integration layer:** Processes that validate,
    standardize, combine, enrich, and apply business rules to data.
5.  **Warehouse storage layer:** Integrated data organized for
    enterprise-wide analysis.
6.  **Data mart or semantic layer:** Business-oriented datasets,
    metrics, and definitions tailored to departments or analytical use
    cases.
7.  **Consumption layer:** Dashboards, reports, ad hoc SQL, notebooks,
    machine-learning workflows, and other analytical tools.

## 5. Data Integration: ETL and ELT

Data integration is the process of collecting information from source
systems and preparing it for analytical use. Two widely used patterns
are ETL and ELT.

### 5.1 ETL: Extract, Transform, Load

ETL performs transformations before loading the final data into the
warehouse.

-   **Extract:** Read data from source systems such as databases, APIs,
    and files.
-   **Transform:** Clean, validate, standardize, combine, and apply
    business rules.
-   **Load:** Store the transformed result in warehouse tables.

ETL is useful when data must be carefully processed before entering the
target environment, or when the target platform has limited
transformation capabilities.

### 5.2 ELT: Extract, Load, Transform

ELT loads source data into the target platform first and performs
transformations within that platform.

-   **Extract:** Collect data from source systems.
-   **Load:** Store raw or lightly processed data in the target
    environment.
-   **Transform:** Use the warehouse or lakehouse compute engine to
    create curated analytical datasets.

ELT is common in modern cloud environments because scalable storage and
compute can support transformations close to the data.

## 6. Data Warehouse Components and Related Concepts

### 6.1 Enterprise data warehouse

An enterprise data warehouse (EDW) provides an integrated analytical
foundation across multiple business functions. It aims to establish
consistent definitions and shared data structures across the
organization.

### 6.2 Data mart

A data mart is a subject-specific or department-oriented analytical
dataset. Examples include sales, finance, marketing, and inventory data
marts.

A data mart may be created from an enterprise warehouse, or it may be
built directly from source systems. The latter approach can create
inconsistent definitions if separate teams independently implement the
same business concepts.

### 6.3 Metadata

Metadata is information that describes data. It can include table
definitions, column meanings, data types, lineage, ownership, refresh
schedules, quality rules, and sensitivity classifications.

Metadata helps users discover datasets, interpret fields correctly, and
understand where information originated.

### 6.4 OLAP

Online Analytical Processing (OLAP) supports multidimensional analysis.
Common analytical operations include:

-   **Roll-up:** Aggregate data to a higher level, such as daily sales
    to monthly sales.
-   **Drill-down:** Move from a summary to more detailed information,
    such as year to quarter to month.
-   **Slice:** Select one value from a dimension, such as sales for a
    particular year.
-   **Dice:** Select a sub-cube using multiple dimension filters.
-   **Pivot:** Rotate dimensions to view data from a different
    perspective.

## 7. Issues Occur While Building the Data Warehouse

### 7.1 When and How to Gather Data?

- **Source-driven:** Data sources push updates to the warehouse periodically or continuously.
- **Destination-driven:** The warehouse pulls data on a fixed schedule.
- **Synchronization:** Perfect synchronization is costly, so data may be slightly outdated. This is acceptable for analytical purposes.

### 7.2 What Schema to Use?

- Source systems have varied formats.
- The warehouse stores a cleaned and unified version of the data.
- It is not a direct copy of the source data, but a consistent snapshot for analysis.

### 7.3 Data Transformation and Cleansing

- Fixes errors such as typos or invalid codes using reference data.
- **Fuzzy lookup:** Helps match similar but not identical values.

### 7.3 How to Propagate Updates?

- If the warehouse schema is the same as the source schema, synchronization is easy.
- If the schemas differ, it becomes a **view maintenance challenge**.

### 7.4 What Data to Summarize?

- Raw data is large, so summaries are stored (e.g., total sales by category).
- Aggregates support efficient querying without requiring access to all detailed data.
