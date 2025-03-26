# AWS Cloud Projects Portfolio

<img src="https://github.com/user-attachments/assets/6fcbd034-bbdd-462e-a807-746a6151de9e" alt="AWS Cover photo" >

Welcome to my AWS Cloud Projects portfolio! Below is a list of projects I've worked on:

## Projects
1. **[Project 1: Automated Data Ingestion for UCW Academics Attendance Using AWS](./Auto_Data_Ingestion)**
   - **Objective**: The primary objective of this project is to ingest academic attendance data from the UCW operational environment into AWS Data Analysis Platform (DAP). The dataset includes students, instructors, and department details, and our goal is to establish a structured data lake for efficient storage and analysis.
   - **Tools**:
      - **Cloud Services: AWS S3, AWS EC2**
      - **Scripting: Windows PowerShell**
      - **Design & Planning: Draw.io.**


2. **[Project 2:  Summarization and ETL Pipeline for UCW Academics Attendance Using AWS Services](./Academics_Attendancedata_Summarization)**
   - **Objective**: The goal of this project was to structure, catalog, and summarize UCW’s academic attendance data stored in AWS S3. We transformed raw student, instructor, and department datasets into an organized data catalog using AWS Glue and performed aggregation-based summarization to support UCW’s attendance tracking and reporting system.
   - **Tools**:
      - **Data Cataloging: AWS Glue Crawlers, Glue Data Catalog.**
      - **ETL & Summarization: AWS Glue.**
      - **Storage: Amazon S3 (academics-trf-sum, academics-cur-sum).**
      - **Web Application Launch: AWS Elastic Beanstalk.**
      - **Design & Planning**: Draw.io.**


3. **[Project 3:  Data Security Implementation for UCW Attendance Procedure Datasets Using AWS KMS & S3](./Data_Security_Implementation_attendance)**
   - **Objective**: The objective of this project is to implement data security best practices for academic attendance datasets at UCW using AWS Key Management Service (KMS) and S3 storage configuration. This project ensures data confidentiality, integrity, and availability (CIA) by applying encryption, bucket versioning, and replication strategies.
   - **Tools**:
      - **Cloud Services: AWS S3, AWS KMS, AWS IAM**
      - **Security Features: SSE-KMS, Bucket Versioning, S3 Replication**
      - **Identity Management: IAM Role Labrole**
      - **Monitoring: S3 Management, Encryption Policies**
      - **Design & Planning**: Draw.io.**
    

4. **[Project 4:  Data Analytics Platform (DAP) Design and Implementation for the City of Vancouver Parks Dataset (Part 1)](./DAP_design_for_COV)**
   - **Objective**: The primary objective of this project is to design and implement a **Data Analytics Platform (DAP)** for the City of Vancouver’s Parks dataset. The platform will enable descriptive analysis of park distribution and average size across neighborhoods, while also calculating the monthly cost of implementing this platform on AWS. The project aims to provide actionable insights for urban planning and resource allocation by analyzing park density and size relative to population distribution.
   - **Tools**:
     - **Cloud Services**: AWS S3, AWS DataBrew, AWS Glue.
     - **Data Profiling & Cleaning**: AWS DataBrew.
     - **Data Cataloging**: AWS Glue Crawler.
     - **Data Summarization**: AWS Glue ETL Pipeline.
     - **Cost Estimation**: AWS Pricing Calculator.
     - **Design & Planning**: Draw.io.**


5. **[Project 5:  Data Analytics Platform (DAP) Implementation for the City of Vancouver Parks Dataset (Part 2)](./DAP_Design_COV_Part2)**
   - **Objective**: The second phase of this project focuses on data analysis, security, monitoring, and governance for the City of Vancouver’s Parks dataset. The goal is to enhance the DAP by ensuring data integrity, security, and operational excellence while providing actionable insights into park distribution and size across neighborhoods.
   - **Tools**:
      - **Cloud Services**: AWS S3, AWS KMS, AWS Glue, AWS Athena, AWS CloudWatch, AWS CloudTrail.
      - **Data Analysis**: AWS Athena.
      - **Data Security**: AWS KMS, S3 Encryption, Bucket Versioning.
      - **Data Governance**: AWS Glue DataBrew, Visual ETL Pipeline.
      - **Data Monitoring**: AWS CloudWatch, AWS CloudTrail.
