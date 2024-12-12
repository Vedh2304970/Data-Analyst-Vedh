## Data-Analyst-Vedh

## <div align="center">   Project Phase 1  </div>

## <div align="center"> Descriptive Analysis </div>

### Project Description
**Descriptive Analysis of Business Licenses in the City of Vancouver**

### Project Title
**Analyzing Employment Distribution Across Business Types in Downtown Vancouver**

### Objective
The primary objective of this project is to analyze the employment distribution across different business types in the downtown area of Vancouver. By applying descriptive analytics, we aim to summarize the number of employees in various business categories, providing insights that can inform urban planning, business investments, and workforce strategies.

### Dataset
The dataset is sourced from the City of Vancouver’s Open Data Portal. Key attributes include:
- **FOLDERYEAR**: Year of license folder creation.
- **LicenceRSN**: Unique identifier for the license.
- **LicenceNumber**: Business license number.
- **LicenceRevisionNumber**: Revision number of the license.
- **BusinessName**: Official name of the business.
- **BusinessTradeName**: Trade name used by the business.
- **Status**: License status (e.g., Issued).
- **IssuedDate**: Date the license was issued.
- **ExpiredDate**: Expiry date of the license.
- **BusinessType**: Type of business (e.g., Retail, Technology).
- **BusinessSubType**: Further classification of the business type.
- **Unit, UnitType, House, Street, City, Province, Country, PostalCode**: Address details.
- **LocalArea**: Specific area within Vancouver (e.g., Downtown).
- **NumberofEmployees**: Total employees in the business.
- **FeePaid**: Licensing fee paid.

## Methodology
1. **Data Collection and Preparation**:
   - Load the Business License dataset using AWS services.
   - Apply filters to narrow down the data:
     - FOLDERYEAR: 24
     - LicenceRevisionNumber: 11
     - Status: Issued
     - LocalArea: Downtown
   - Perform initial data cleaning using AWS Glue DataBrew.

2. **Data Ingestion**:
   - Store raw data in S3 bucket `businesslicences-raw-vedh`.
   - Organize data in folders by ingestion year (2024).

3. **Data Profiling**:
   - Use AWS Glue DataBrew to analyze and summarize the dataset.
   - Generate a summary report including row and column counts, missing cells, and duplicate values.

4. **Data Cleaning**:
   - Create a project `prj-businesslicence-dataset-vedh` in AWS Glue DataBrew.
   - Remove white spaces and additional timestamps.
   - Convert number columns from string to integer format.
   - Remove null values.
   - Save the cleaning steps as a "recipe" for future use.

5. **Data Pipeline**:
   - Design an ETL pipeline using AWS Glue.
   - Load cleaned data from the transform bucket.
   - Aggregate data based on BusinessType and NumberofEmployees.
   - Calculate the total sum and count of employees for each business type.
   - Store the transformed data in the S3 bucket `businesslicences-trf-vedh`.

6. **Data Visualization**:
   - Create a column chart showing the total sum of employees for each business type.
   - Generate a comparison chart displaying both the average and sum of employees across business types.

## Tools and Technologies
- **AWS S3**: Data storage.
- **AWS Glue DataBrew**: Data profiling and cleaning.
- **AWS Glue**: ETL pipeline design and execution.
- **AWS CloudWatch**: Monitoring and logging.

## Deliverables
1. Cleaned and processed dataset stored in AWS S3.
2. ETL pipeline documentation.
3. Summary report of data profiling results.
4. Visualizations of employee distribution across business types.
5. Analysis report detailing insights and findings from the descriptive analysis.
6. Recommendations for further analysis or potential business implications based on the findings.


## <div align="center"> Exploratory Analysis </div>

## Project Description
**Exploratory Data Analysis (EDA) for Business Licenses Dataset**

## Project Title
**Analyzing Employee Distribution Across Business Types in Vancouver**

## Objective
The primary goal of this project is to perform an exploratory data analysis (EDA) on the Business Licenses dataset from the City of Vancouver. The analysis aims to uncover patterns, trends, and insights related to employee distribution across various business types. This includes comparing the total sum and average number of employees within each business type to understand employment patterns.

## Dataset
The Business Licenses dataset includes the following columns:
- **FOLDERYEAR**: Year of the license folder.
- **LicenceRSN**: Unique identifier for the license.
- **LicenceNumber**: Number assigned to the license.
- **LicenceRevisionNumber**: Revision number of the license.
- **BusinessName**: Name of the business.
- **BusinessTradeName**: Trade name of the business.
- **Status**: License status (e.g., Issued).
- **IssuedDate**: Date when the license was issued.
- **ExpiredDate**: License expiration date.
- **BusinessType**: Category of the business.
- **BusinessSubType**: Subcategory of the business (if applicable).

## Methodology

### 1. Data Ingestion
- Store raw data in S3 bucket `businesslicences-raw-vedh` in the US East (N. Virginia) region.
- Organize data in folders by ingestion year (2024).
- Upload the "Business Type" dataset in Excel format.

### 2. Data Profiling
- Use **AWS Glue DataBrew** to analyze and summarize the dataset.
- Connect to the dataset `businesslicences-dataset-vedh`.
- Generate a summary report including row and column counts, missing cells, and duplicate values.
- Save profiling results in JSON format in the transform bucket under "Data Profiling."

### 3. Data Cleaning
- Create a project `prj-businesslicence-dataset-vedh` in **AWS Glue DataBrew**.
- Remove white spaces and additional timestamps.
- Convert number columns from string to integer format.
- Remove null values.
- Save cleaning steps as a "recipe" for future use.
- Run the job `businesslicence-job-vedh` to apply the cleaning process.
- Store output in "Data Cleaning" folder in the transform bucket:
  - CSV format in "user" folder.
  - PARQUET format with Snappy compression in "System" folder.

### 4. Data Pipeline
- Design ETL pipeline `businesslicences-adm-exploratory-vedh` using **AWS Glue**.
- Load data from `s3://businesslicences-trf-vedh/Business Licences/Data-cleaning/System/`.
- Drop additional columns and filter for `Number of Employees > 0`.
- Create two aggregate paths:
  - Total Sum of Employees by Business Type.
  - Total Count of Employees by Business Type.
- Apply Inner Join based on `Business Type`.
- Calculate average employees using a derived column.
- Store results in "Business Type - Average Employees" folder in the transform bucket.

## Tools and Technologies
- **AWS S3**: Data storage.
- **AWS Glue DataBrew**: Data profiling and cleaning.
- **AWS Glue**: ETL pipeline design and execution.

## Deliverables
1. Cleaned and processed dataset stored in **AWS S3**.
2. Data profiling summary report.
3. ETL pipeline documentation for exploratory analysis.
4. Visualizations comparing average and total employees across business types.
5. Analysis report detailing insights and findings from the exploratory analysis.
6. Recommendations for further analysis or potential business implications based on the findings.

## <div align="center">  Project Phase 2 </div>
## <div align="center"> Data Quality Control </div>

## Project Description
**Data Quality Control for Business Licenses Dataset: Enriching, Governance, Protection, and Observability**

## Project Title
**Comprehensive Data Management for Business Licenses in Vancouver**

## Objective
The primary goal of this project is to implement robust methodologies for enriching, governing, protecting, and observing the Business Licenses dataset. By leveraging advanced data techniques, the project ensures the data’s accuracy, security, and usability while maintaining compliance with governance standards and enhancing monitoring capabilities.

## Dataset
The Business Licenses dataset includes the following columns:
- **FOLDERYEAR**: Year of the license folder.
- **LicenceRSN**: Unique identifier for the license.
- **LicenceNumber**: Number assigned to the license.
- **LicenceRevisionNumber**: Revision number of the license.
- **BusinessName**: Name of the business.
- **BusinessTradeName**: Trade name of the business.
- **Status**: License status (e.g., Issued).
- **IssuedDate**: Date when the license was issued.
- **ExpiredDate**: License expiration date.
- **BusinessType**: Category of the business.
- **BusinessSubType**: Subcategory of the business (if applicable).

## Methodology

### 1. Data Enriching
- **Create a table**: Use Amazon DynamoDB to create a table `business-license-vedh`.
- **Export data**: Export enriched table data to the raw S3 bucket (`businesslicences-raw-vedh`).
- **Generate metadata**: Use AWS Glue Crawler to generate metadata tables in the Data Catalog from the enriched data.
- **Schema standardization**: Consolidate and standardize schemas using Glue transformations for seamless integration.

### 2. Data Governance
- **Data Quality Evaluation**: Apply AWS Glue Evaluate Data Quality to assess completeness and uniqueness metrics, referencing `LicenceNumber`.
- **ETL Pipelines**: Route "passed" and "failed" data into separate S3 buckets for transparency.
- **Governance Rules**: Implement governance rules ensuring adherence to industry and regulatory standards.

### 3. Data Protection
- **Key Management**: Use AWS Key Management Service (KMS) to create and manage encryption keys.
- **Bucket Protection**: Secure S3 buckets with customer-managed KMS keys.
- **Replication Policies**: Establish cross-region replication rules with encryption for disaster recovery.

### 4. Data Observability
- **Monitoring Setup**:
  - Use Amazon CloudWatch to create dashboards visualizing:
    - Number of objects in S3 buckets.
    - Bucket sizes and estimated total charges.
    - Logs of system activity and errors.
- **Alerts and Notifications**: Configure alarms for deviations in storage usage or ETL pipeline performance.
- **Log Analysis**: Enable detailed tracking of AWS Glue jobs and S3 operations for comprehensive observability.

## Tools and Technologies
- **Data Enriching**: AWS DynamoDB, AWS Glue Crawler
- **Data Governance**: AWS Glue, S3, AWS Glue Data Quality
- **Data Protection**: AWS KMS, S3 Bucket Policies
- **Data Observability**: Amazon CloudWatch, AWS Glue Logs

## Deliverables
1. A consolidated, enriched dataset with enhanced metadata stored in S3.
2. ETL pipeline diagrams illustrating governance workflows.
3. Secure and replicated S3 buckets with encryption policies.
4. CloudWatch dashboards for real-time data monitoring.
5. Comprehensive documentation detailing enrichment, governance, protection, and observability methods.
