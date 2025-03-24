
# Project 3: Data Analytics Platform (DAP) Implementation for the City of Vancouver Parks Dataset (Part 2)

## 📌 **Objective**
The second phase of this project focuses on **data analysis, security, monitoring, and governance** for the City of Vancouver’s Parks dataset. The goal is to enhance the DAP by ensuring data integrity, security, and operational excellence while providing actionable insights into park distribution and size across neighborhoods.



## 📌 **Dataset Overview**
The dataset used in this project is the **Vancouver Parks Dataset**, retrieved from the **City of Vancouver Open Data Portal**. The dataset includes the following key attributes:

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/72931029-478d-478e-ae1f-b57d9b302b10" />

Parks Dataset from the City of Vancouver

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/66c89ab1-cdbb-43a6-b083-33120a6dbcd5" />

Parks Dataset from the City of Vancouver with selected metrics for data analysis

- **ParkID**: Unique identifier for each park.
- **Name**: Name of the park.
- **Official**: Binary indicator (0 or 1) for official park status.
- **Advisories**: Information about park advisories.
- **Special Features**: Unique features of the park.
- **Facilities**: Available facilities in the park.
- **Washrooms**: Availability of washrooms.
- **StreetNumber**: Street number of the park location.
- **StreetName**: Street name of the park location.
- **NeighborhoodName**: Neighborhood where the park is located.
- **NeighborhoodURL**: URL for neighborhood information.
- **GoogleMapDest**: Google Maps destination link.
- **EWStreet**: East-West street location.
- **NSStreet**: North-South street location.
- **Hectares**: Size of the park in hectares.



## 📌 **Methodology**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/d3e50f44-6d30-4ece-82eb-e2edfeb0d13d" />

This is the DAP Implementation design part that we implemented for 'parks' dataset


### **1. Data Analysis**
- **AWS Athena**: Used to analyze the dataset and answer key questions about park distribution and size across neighborhoods.
  - **Business Problem 1**: Total number of parks per neighborhood.
  - **Business Problem 2**: Average park size per neighborhood.
  - **Business Problem 3**: Top 5 largest parks in Vancouver.
  - **Business Problem 4**: Comparison of neighborhoods with similar park counts but different park sizes.

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/1c71a89e-4ee6-4793-8028-f746c05c68e3" />

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/657583b3-9b71-4b8b-9ead-185ae5f0b941" />


Query and the output for finding the insights for Business Problem 1


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/6ee3ddbf-ab6e-465c-9ddc-5b566978bda1" />
<img width="600" alt="Image" src="https://github.com/user-attachments/assets/a569bdf4-6590-43bb-b474-27642e4a8e92" />


Query and the output for finding the insights for Business Problem 2


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/9e0165ae-6889-46ee-8047-8aa2f8a389b5" />
<img width="600" alt="Image" src="https://github.com/user-attachments/assets/134dc375-6663-42bb-8ab0-bd22dc2427c1" />


Query and the output for finding the insights for Business Problem 3


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/8e8ac1a7-c573-4863-9e98-0da13b6c5423" />
<img width="600" alt="Image" src="https://github.com/user-attachments/assets/3d9fb0e0-4608-442b-8941-f63812b5bf4f" />


Query and the output for finding the insights for Business Problem 4

### **2. Data Security**
- **AWS Key Management System (KMS)**: Created a custom key (`parks-key-sum`) for encryption and decryption.
- **S3 Bucket Encryption**: Enabled default encryption for all S3 buckets (`parks-raw-sum`, `parks-trf-sum`, `parks-cur-sum`) using the custom key.
- **Bucket Versioning**: Enabled versioning to track changes and ensure data integrity.
- **Replication Rules**: Created replication rules to ensure data availability across multiple locations.


**Bucket: S3 raw bucket**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/9ea57c15-0252-4780-8721-be5004ef7fbe" />

Assigning keys to S3 raw bucket by changing ‘Default Encryption’


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/842b6f94-9b07-4c4f-8e0b-a8e49b646c5b" />

Enables ‘Bucket Versioning’ in S3 raw bucket


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/e005a2e2-b3f7-44ba-8217-c11da4cde9d3" />

Replication rule in S3 raw bucket


**Bucket: parks-trf-sum**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/1a106cfe-cdee-4c0e-b638-ac8126e61eb9" />

Assigning keys to the S3 trf bucket by changing ‘Default Encryption’


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/726f3bfb-e188-4465-9d05-f66f7fad31b2" />

Enables ‘Bucket Versioning’ in S3 trf bucket


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/72d9a43a-04e2-4e5d-ae54-6051fda3b1c6" />

Replication rule in S3 trf bucket


**Bucket: parks-cur-sum**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/1e919fc8-cdac-4bf7-9626-bacc7a3cdd5a" />

Assigning keys to the S3 cur bucket by changing ‘Default Encryption’


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/1c3e27a8-c512-4882-b451-dfe3f5a327eb" />

Enables ‘Bucket Versioning’ in S3 cur bucket


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/58bf6be6-2f88-4adc-8994-60c9f50ab77e" />

Replication rule in S3 cur bucket


### **3. Data Governance**
- **AWS Glue DataBrew**: Used for data quality checks and validation.
  - Created a **Quality Check** folder in the S3 transform bucket (`parks-trf-sum`) with subfolders for **Passed** and **Failed** data.
  - Set rules for data completeness, uniqueness, and value consistency.
- **Visual ETL Pipeline**: Automated data quality checks using AWS Glue.

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/b4eabb4b-2f39-4cbb-8134-9584f2a935bd" />

AWS Glue Data Quality Check Pipeline



<img width="600" alt="Image" src="https://github.com/user-attachments/assets/a1f06c03-e037-4904-86c6-f0cf44cb084b" />

Quality check rules


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/9351567b-2418-4d39-9da8-c6fb04e5557d" />

Data preview for quality check rulesets


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/e8991b07-6564-48fc-b2f7-5204a2d0c343" />

Quality Checked passed dataset in S3 trf bucket


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/34f9bb89-21bd-4e34-96b2-5e56993dc097" />

Quality checked failed dataset in S3 trf bucket


### **4. Data Monitoring**
- **AWS CloudWatch**: Created a dashboard (`parks-MCR-sum`) to monitor:
  - **Bucket Size**: Tracked storage changes in S3 buckets over time.
  - **AWS Glue Resource Usage**: Monitored resource consumption for ETL jobs.
  - **Number of Objects**: Tracked the average number of objects in each S3 bucket.
- **AWS CloudTrail**: Created a trail (`parks-trail-sum`) to monitor user activities and API usage.

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/efc93d0d-4e9b-4f6b-836d-f0ab21fc10e8" />

Data monitoring dashboard in AWS CloudWatch


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/d1d05907-e40e-424c-bbf3-78fa67beb0c6" />

CloudTrail user activities log


## 📌 **Results & Findings**

### **Data Analysis Insights**
- **Park Distribution**: Downtown has the highest number of parks (22), while Shaughnessy has the largest average park size (5.85 hectares).
- **Top 5 Largest Parks**: John Hendry (Trout Lake) Park is the largest at 27.31 hectares.
- **Neighborhood Comparison**: Dunbar-Southlands has fewer but larger parks compared to Kensington-Cedar Cottage.

### **Data Security**
- Successfully implemented encryption, versioning, and replication for all S3 buckets.
- Ensured data confidentiality, integrity, and availability using AWS KMS and S3 features.

### **Data Governance**
- Automated data quality checks using AWS Glue.
- Segregated data into **Passed** (63%) and **Failed** (37%) categories based on quality metrics.

### **Data Monitoring**
- Established real-time monitoring using AWS CloudWatch and CloudTrail.
- Tracked system performance, resource usage, and user activities.



## 📌 **Tools & Technologies Used**
- **Cloud Services**: AWS S3, AWS KMS, AWS Glue, AWS Athena, AWS CloudWatch, AWS CloudTrail.
- **Data Analysis**: AWS Athena.
- **Data Security**: AWS KMS, S3 Encryption, Bucket Versioning.
- **Data Governance**: AWS Glue DataBrew, Visual ETL Pipeline.
- **Data Monitoring**: AWS CloudWatch, AWS CloudTrail.



## 📌 **Deliverables**
1. **Data Analysis Reports**: Insights from AWS Athena queries.
2. **Data Security Implementation**: Encryption, versioning, and replication for S3 buckets.
3. **Data Governance Pipeline**: Automated quality checks and data segregation.
4. **Monitoring Dashboard**: CloudWatch dashboard for real-time monitoring.
5. **User Activity Logs**: CloudTrail logs for tracking user activities.



## 📌 **Future Enhancements**
1. **Automation**: Use AWS Lambda to automate data ingestion and quality checks.
2. **Advanced Analytics**: Integrate AWS QuickSight for advanced visualization and reporting.
3. **Cost Optimization**: Explore S3 Intelligent-Tiering for cost-effective storage.
4. **Operational Excellence**: Implement Infrastructure as Code (IaC) using AWS CloudFormation.



## 📌 **Conclusion**
This project successfully implemented the second phase of the **Data Analytics Platform (DAP)** for the City of Vancouver’s Parks dataset. By leveraging AWS services, we ensured data security, governance, and monitoring while providing actionable insights into park distribution and size. This phase lays the foundation for future enhancements, including automation and advanced analytics.


