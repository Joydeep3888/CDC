# Change Data Capture (CDC) Pipeline in AWS using Glue, Lambda, and RDS

## Overview
This project implements a robust, end-to-end Change Data Capture (CDC) pipeline using AWS services such as AWS Glue, AWS Lambda, Amazon RDS (MySQL), and AWS Database Migration Service (DMS). The pipeline ensures seamless replication of changes (INSERT, UPDATE, DELETE) from a MySQL database to an Amazon S3 data lake.

## Architecture Workflow

1. **Extracting Data from MySQL**  
   - The pipeline reads data from a MySQL database hosted on Amazon RDS.
   - To facilitate the extraction, we configure AWS DMS (Database Migration Service) with appropriate source and target endpoints.
   - IAM roles with `AmazonS3FullAccess` permissions are assigned to ensure smooth data transfer.

2. **Loading Data into Temporary S3 Bucket**  
   - AWS DMS continuously migrates the data from MySQL to a temporary Amazon S3 bucket.
   - This data serves as an intermediate staging area before final transformation.

3. **Triggering AWS Lambda and Glue Jobs**  
   - Whenever new data lands in the temporary S3 bucket, an event notification triggers an AWS Lambda function.
   - The Lambda function inspects the changes and invokes an AWS Glue job for processing.

4. **Processing Data in AWS Glue**  
   - The AWS Glue job detects INSERT, UPDATE, and DELETE operations in the incoming data.
   - It processes the changes and applies them to the original dataset stored in the final Amazon S3 bucket.
   - The updated dataset maintains data integrity and ensures an accurate, up-to-date data lake.

5. **Final Data Storage in S3**  
   - After processing, the transformed data is stored in a structured format (e.g., Parquet) in the final Amazon S3 bucket.
   - This final dataset is ready for downstream analytics, reporting, or ML workloads.

## Implementation Details
### AWS Services Used
- **Amazon RDS (MySQL):** Source database where transactional data is stored.
- **AWS DMS (Database Migration Service):** Facilitates incremental data migration from MySQL to Amazon S3.
- **Amazon S3:** Two buckets used:
  - **Temporary bucket:** Stores raw CDC event data.
  - **Final bucket:** Stores transformed, up-to-date data.
- **AWS Lambda:** Monitors the temporary S3 bucket and triggers AWS Glue jobs.
- **AWS Glue:** Processes CDC records and updates the final dataset accordingly.
- **IAM Roles:** Ensures appropriate permissions for accessing S3, DMS, and Glue.

## Data Flow Diagram
```plaintext
MySQL (RDS) → AWS DMS → Temporary S3 Bucket → AWS Lambda → AWS Glue → Final S3 Bucket
```
![The CDC pipeline architecture](https://github.com/Joydeep3888/CDC/blob/main/Architecture.jpg)

## Key Benefits
✅ **Automated Data Synchronization:** Real-time updates from MySQL to S3.  
✅ **Serverless and Scalable:** Uses AWS Glue and Lambda for efficient processing.  
✅ **Cost-Effective:** No need for a continuously running ETL process; serverless functions reduce cost.  
✅ **Highly Available:** Utilizes AWS-managed services with built-in fault tolerance.  

## Next Steps
- Implement AWS Athena for querying the final dataset in S3.
- Integrate Amazon Redshift for high-performance analytics.
- Optimize Glue transformations for better efficiency.

---
### 🚀 Ready to Deploy
Clone the repository and modify configurations as per your AWS environment to get started!




