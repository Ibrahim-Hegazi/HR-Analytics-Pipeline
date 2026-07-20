# HR Data Quality Framework & Analytics Pipeline

## 🔎 Project Overview
This project implements an end-to-end data quality framework and analytics pipeline for employee data ingested from multiple source formats (TXT, Excel) into Microsoft Fabric. The pipeline standardizes, validates, cleans, and models the data into a star schema for reporting and analytics.

## 🚀 Project Goals
- Ingest employee data from heterogeneous source files into a centralized lakehouse
- Apply comprehensive data quality checks across 9 dimensions (completeness, validity, consistency, uniqueness, format standardization)
- Cleanse and standardize categorical, numeric, and date values
- Model cleansed data into a Kimball-style star schema (fact and dimension tables)
- Enable self-service analytics and reporting via Power BI

## 💡 Proposed Solutions
- **Data Ingestion**: PySpark notebooks to load raw files into the ODS layer
- **Data Quality Framework**: Systematic checks executed in optimal order (Format → Validity → Completeness → Uniqueness → Consistency)
- **Data Cleansing**: Pandas-based standardization with stakeholder review for critical missing data
- **Data Modeling**: Dataflow Gen2 to build DimEmployee, DimDepartment, DimCountry, DimJobTitle, DimEmployeeStatus, DimDate, and FactEmployee
- **Storage**: Medallion architecture (ODS → STG → DWH) in Microsoft Fabric Lakehouse and Warehouse

## 📈 System Architecture























## 🔧 Features
- detection of data quality issues (missing values, duplicates, outliers, inconsistencies)
- Categorical standardization with mapping dictionaries
- Date format harmonization (YYYY-MM-DD)
- Numeric cleanup (currency symbols, commas, negative values)
- Cross-column validation (FullName = FirstName + LastName)
- Gender correction using real-world name-gender reference lists
- Sequential EmployeeId gap filling
- Stakeholder-ready missing data reports
- Star schema modeling for analytical queries

## 🧪 Pipeline Phases

| Phase | Description | Status |
|---|---|---|
| 1. Lakehouse Creation | Create HR_Analytics_Lakehouse in Fabric workspace | ✅ Complete |
| 2. Schema Creation | Create ODS and STG schemas inside the lakehouse tables section | ✅ Complete |
| 3. Raw Data Upload | Manually upload Excel and TXT source files to the files section of the lakehouse | ✅ Complete |
| 4. Raw Data Ingestion | PySpark code to load files from files section into ODS schema tables | ✅ Complete |
| 5. Schema Validation | Detect and resolve schema mismatches (extra/missing columns) across file formats | ✅ Complete |
| 6. Data Quality & Cleansing | Comprehensive EDA and 5-stage data quality framework | ✅ Complete |
| ├── 6.1 Format Standardization | Column renaming, categorical mapping, date/numeric cleanup, text normalization | ✅ Complete |
| ├── 6.2 Validity Checks | Data types, invalid categories, pattern mismatches, range violations, format consistency | ✅ Complete |
| ├── 6.3 Completeness Checks | Missing per column/row, missing patterns (MCAR/MAR/MNAR), missing value correlation | ✅ Complete |
| ├── 6.4 Uniqueness Checks | Duplicate rows, duplicate IDs, unique value distribution | ✅ Complete |
| └── 6.5 Consistency Checks | Cross-column validation, logical contradictions, dependency violations, value range logic, category mapping | ✅ Complete |
| 7. Data Combination | Combine cleaned Excel and TXT data, remove exact duplicates, update timestamps and source location | ✅ Complete |
| 8. Warehouse Creation | Create HR_Analytics_Warehouse in Fabric workspace | ✅ Complete |
| 9. DWH Schema Creation | Create DWH schema inside the warehouse | ✅ Complete |
| 10. Data Modeling | Dataflow Gen2 to build star schema (FactEmployee + 6 dimension tables) and load into DWH schema | ✅ Complete |
| 11. Semantic Model | Create semantic model for aggregations, derived columns, and relationships | ✅ Complete |
| 12. Visualization | Power BI dashboards and reports for analytics | ✅ Complete |

## 🧬 Data Flow Diagram


















## 📦 Tech Stack
| Component | Technology |
|---|---|
| Cloud Platform | Microsoft Fabric |
| Lakehouse | Fabric Lakehouse |
| Warehouse | Fabric Warehouse |
| Ingestion/Transformation | PySpark, Pandas |
| Data Quality | Python (pandas, numpy) |
| Data Modeling | Dataflow Gen2 (Power Query M) |
| Visualization | Power BI |
| Version Control | GitHub / Fabric Git Integration |

## 🛠️ Setup & Installation
1. Create a Fabric workspace
2. Create a Lakehouse (`HR_Analytics_Lakehouse`)
3. Create a Warehouse (`HR_Analytics_Warehouse`)
4. Upload source files to `Files/` directory
5. Import notebooks and configure Lakehouse connection
6. Run notebooks in order: Ingestion → Data Quality → Combine
7. Configure Dataflow Gen2 with source pointing to `STG.employee_combined_cleaned_data`
8. Publish and refresh Dataflow
9. Build semantic model and reports in Power BI

## 📊 Datawarehouse Schema















## 🗓 Roadmap
- [x] Phase 1-5: Data quality checks (Format, Validity, Completeness, Uniqueness, Consistency)
- [ ] Phase 6-9: Remaining checks (Accuracy, Domain, Referential, Timeliness)
- [x] Data modeling (Star schema via Dataflow Gen2)
- [x] Power BI semantic model
- [ ] Incremental refresh configuration
- [ ] Monitoring and alerting for data quality metrics


## 👨‍💻 Author
Ibrahim Hegazi
Data & Analytics Engineer
ihegaziwork@gmail.com

## 📬 Future Improvements
- Automate data quality checks with Fabric Data Pipelines
- Implement SCD Type 2 for slowly changing dimensions
- Add data quality scorecards and dashboards
- Integrate with Microsoft Purview for data governance
- Build real-time alerts for data quality failures
- Expand to additional HR data sources (payroll, performance, recruitment)
