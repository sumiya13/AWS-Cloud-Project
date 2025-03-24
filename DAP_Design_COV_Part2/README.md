
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

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/1c71a89e-4ee6-4793-8028-f746c05c68e3" />

S3 Bucket Encryption and Versioning



### **3. Data Governance**
- **AWS Glue DataBrew**: Used for data quality checks and validation.
  - Created a **Quality Check** folder in the S3 transform bucket (`parks-trf-sum`) with subfolders for **Passed** and **Failed** data.
  - Set rules for data completeness, uniqueness, and value consistency.
- **Visual ETL Pipeline**: Automated data quality checks using AWS Glue.

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/834f083c-de44-4969-b391-c6e800cfe0aa" />

AWS Glue Data Quality Check Pipeline

---

### **4. Data Monitoring**
- **AWS CloudWatch**: Created a dashboard (`parks-MCR-sum`) to monitor:
  - **Bucket Size**: Tracked storage changes in S3 buckets over time.
  - **AWS Glue Resource Usage**: Monitored resource consumption for ETL jobs.
  - **Number of Objects**: Tracked the average number of objects in each S3 bucket.
- **AWS CloudTrail**: Created a trail (`parks-trail-sum`) to monitor user activities and API usage.

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/1615e734-44bb-461b-b396-aa168c831112" />

CloudWatch Monitoring Dashboard



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


