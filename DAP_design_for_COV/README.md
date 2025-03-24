# Project 2: Data Analytics Platform (DAP) Design and Implementation for the City of Vancouver Parks Dataset



# 📌**Objective**
The primary objective of this project is to design and implement a **Data Analytics Platform (DAP)** for the City of Vancouver’s Parks dataset. The platform will enable descriptive analysis of park distribution and average size across neighborhoods, while also calculating the monthly cost of implementing this platform on AWS. The project aims to provide actionable insights for urban planning and resource allocation by analyzing park density and size relative to population distribution.



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

#### **Design to Implement**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/3f44c0e0-522c-4ad6-99d9-f3be1b6a6f11" />

This image shows the design for this DAP implementation using Draw.io 


### **1. _Data Ingestion Setup_**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/58f752fc-789b-42ce-a6e8-94536cf20b0f" />

Data Ingestion in S3 Bucket



- **S3 Bucket Creation**: Created an S3 bucket named **`pa-raw-sum`** to store raw park data.
- **Folder Structure**: Organized data into structured folders for efficient storage:
  ```
  /park-data/year=2025/quarter=1/city=vancouver/
  ```
- **Data Upload**: Uploaded the **`park.csv`** file to the S3 bucket using the AWS Management Console.

### **2. _Data Profiling_**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/a0ce134f-5206-43e1-b07a-ba898b7da353" />

Data Profiling 


- **AWS DataBrew**: Used AWS DataBrew for data profiling to identify missing values, data types, and correlations.
  - **Dataset Summary**: The dataset contains **216 rows** and **15 columns**.
  - **Data Quality Issues**: Identified **7 missing values** (<1% of total data).
  - **Duplication**: No duplicate rows were found.
  - **Correlation**: Weak correlation between numerical columns.
- **Column Summary**: 
  - **String Columns**: 11
  - **Double Columns**: 1
  - **Integer Columns**: 3

### **3. _Data Cleaning_**


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/b091a69e-937d-4efc-b2bc-022823d6693f" />

Cleaned data in User folder 



<img width="600" alt="Image" src="https://github.com/user-attachments/assets/f3031b4a-fcc9-433c-b149-5fe3f4d443e2" />

Clean and Partitioned data in System folder


- **Outlier Handling**: Detected and handled outliers in the **Hectares** column using the **Interquartile Range (IQR)** method.
  - **Threshold**: Lower bound = 0, Upper bound = 6.75 hectares.
  - **Outliers Replaced**: 8 outliers were replaced with the median value.
- **Column Removal**: Removed irrelevant columns (**EWStreet**, **NSStreet**) to simplify data processing.
- **Data Cleaning Job**: Created a DataBrew job named **`par-cln-sum`** to clean the dataset and store it in both **CSV** (user-friendly) and **Parquet** (system-friendly) formats.

### **4. _Data Cataloging_**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/834f083c-de44-4969-b391-c6e800cfe0aa" />

Data Catalog creation for parks dataset using AWS Glue Service


- **AWS Glue Crawler**: Created a crawler named **`parks-crw-sum`** to catalog the cleaned data.
- **Database and Schema**: Created a database **`parks-data-catalog-sum`** and a schema **`par-trf-system`**.
- **Partitioning**: Partitioned data by **NeighborhoodName** for efficient querying.

### **5. _Data Summarization_**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/5a6207e8-424b-4629-87b0-2d94e1390db4" />

Visual ETL Pipeline for Parks data summarization


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/abd8e8c1-7d65-4b92-8b8c-d2d6225b6b7b" />

System-friendly parks data summarization (report Date-wise )


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/c7907d24-2994-4fc3-9a32-7aaf8d5bb200" />

User-friendly parks data summarization in CSV format



- **AWS Glue ETL Pipeline**: Used AWS Glue to summarize the dataset based on the descriptive analysis question:
  - **Grouping**: Grouped data by **NeighborhoodName**.
  - **Aggregation**: Calculated the **count of ParkID** and **average size of parks (Hectares)**.
  - **Output**: Stored summarized data in both **system-friendly** (Parquet) and **user-friendly** (CSV) formats.



## 📌 **Results & Findings**

### **Park Distribution Across Neighborhoods:**
- **Downtown**: Highest number of parks (**22 parks**), but smaller in size (**1.44 hectares** on average).
- **Shaughnessy**: Fewer parks (**5 parks**), but largest in size (**5.85 hectares** on average).
- **Hastings-Sunrise & Kitsilano**: Moderate number of parks (**16 parks each**).
- **Grandview-Woodland**: Smaller parks (**0.78 hectares** on average).

### 📌 **Key Observations**
- **Urban Areas (Downtown, Grandview-Woodland)**: High park density but smaller park sizes due to space constraints.
- **Suburban Areas (Shaughnessy, Dunbar-Southlands)**: Fewer parks but larger in size, reflecting lower population density and more available land.



## 📌 **Tools & Technologies Used**
- **Cloud Services**: AWS S3, AWS DataBrew, AWS Glue.
- **Data Profiling & Cleaning**: AWS DataBrew.
- **Data Cataloging**: AWS Glue Crawler.
- **Data Summarization**: AWS Glue ETL Pipeline.
- **Cost Estimation**: AWS Pricing Calculator.
- **Design & Planning**: Draw.io.



## 📌  **Deliverables**
1. **Infrastructure Design Diagram** (Draw.io).
2. **AWS S3 Data Ingestion Process**.
3. **Data Profiling and Cleaning Reports** (AWS DataBrew).
4. **Data Summarization Output** (CSV and Parquet formats).
5. **Cost Analysis Report** for DAP implementation.



## 📌 **Future Enhancements**
1. **Automation**: Use **AWS Lambda** to automate data ingestion and cleaning processes.
2. **Advanced Analytics**: Integrate **AWS Athena** for querying and advanced analysis.
3. **Real-Time Data Processing**: Implement **Amazon Kinesis** for real-time data streaming.
4. **Cost Optimization**: Explore **S3 Intelligent-Tiering** for cost-effective storage.



## 📌 **Cost Analysis**

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/1615e734-44bb-461b-b396-aa168c831112" />

Estimated cost for DAP implementation  


The estimated monthly cost for implementing the DAP on AWS is **$36.74 per year**, with the following breakdown:
- **S3 Storage**: $0.04/month for 1 GB storage.
- **AWS Glue**: $3.01/month for ETL jobs and interactive sessions.
- **AWS DataBrew**: Included in the overall cost.



## 📌 **Conclusion**
This project successfully designed and implemented a **Data Analytics Platform (DAP)** for the City of Vancouver’s Parks dataset. By leveraging AWS services, we created a scalable and cost-effective solution for analyzing park distribution and size across neighborhoods. The insights generated from this platform will assist urban planners in making data-driven decisions for resource allocation and park development. This project lays the foundation for future enhancements, including automation and advanced analytics.



