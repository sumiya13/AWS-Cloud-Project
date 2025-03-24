# Project 2: Data Analytics Platform (DAP) Design and Implementation for the City of Vancouver Parks Dataset



# 📌**Objective**
The primary objective of this project is to design and implement a **Data Analytics Platform (DAP)** for the City of Vancouver’s Parks dataset. The platform will enable descriptive analysis of park distribution and average size across neighborhoods, while also calculating the monthly cost of implementing this platform on AWS. The project aims to provide actionable insights for urban planning and resource allocation by analyzing park density and size relative to population distribution.



## 📌 **Dataset Overview**
The dataset used in this project is the **Vancouver Parks Dataset**, retrieved from the **City of Vancouver Open Data Portal**. The dataset includes the following key attributes:

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/main/DAP_design_for_COV/images_ProjPart_1/ProjPart%201Dataset%201.png" />
Parks Dataset from the City of Vancouver

![Image](https://github.com/user-attachments/assets/72931029-478d-478e-ae1f-b57d9b302b10)

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/main/DAP_design_for_COV/images_ProjPart_1/Dataset%20ProjPart%201.png" />
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

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/4c2bb1014a89c85dc864660cce59e33b57e9836e/DAP_design_for_COV/images_ProjPart_1/ProPart%201%20Design%20draw.io.png" />
This image shows the design for this DAP implementation using Draw.io 


### **1. _Data Ingestion Setup_**

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/9c9ce659b7ed5c5ef1aa18b810474851fbf4a488/DAP_design_for_COV/images_ProjPart_1/Data%20Ingestion_proj%20Part%201.png" />
Data Ingestion in S3 Bucket



- **S3 Bucket Creation**: Created an S3 bucket named **`pa-raw-sum`** to store raw park data.
- **Folder Structure**: Organized data into structured folders for efficient storage:
  ```
  /park-data/year=2025/quarter=1/city=vancouver/
  ```
- **Data Upload**: Uploaded the **`park.csv`** file to the S3 bucket using the AWS Management Console.

### **2. _Data Profiling_**

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/9c9ce659b7ed5c5ef1aa18b810474851fbf4a488/DAP_design_for_COV/images_ProjPart_1/Data%20Profiling_SS1.png" />
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


<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/77e97387b38b03e8a195b2e327efa080a2c73e53/DAP_design_for_COV/images_ProjPart_1/CleanData_user_SS.png" />
Cleaned data in User folder 



<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/77e97387b38b03e8a195b2e327efa080a2c73e53/DAP_design_for_COV/images_ProjPart_1/CleanData_System_SS.png" />
Clean and Partitioned data in System folder


- **Outlier Handling**: Detected and handled outliers in the **Hectares** column using the **Interquartile Range (IQR)** method.
  - **Threshold**: Lower bound = 0, Upper bound = 6.75 hectares.
  - **Outliers Replaced**: 8 outliers were replaced with the median value.
- **Column Removal**: Removed irrelevant columns (**EWStreet**, **NSStreet**) to simplify data processing.
- **Data Cleaning Job**: Created a DataBrew job named **`par-cln-sum`** to clean the dataset and store it in both **CSV** (user-friendly) and **Parquet** (system-friendly) formats.

### **4. _Data Cataloging_**

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/77e97387b38b03e8a195b2e327efa080a2c73e53/DAP_design_for_COV/images_ProjPart_1/CleanData_System_SS.png" />
Data Catalog creation for parks dataset using AWS Glue Service


- **AWS Glue Crawler**: Created a crawler named **`parks-crw-sum`** to catalog the cleaned data.
- **Database and Schema**: Created a database **`parks-data-catalog-sum`** and a schema **`par-trf-system`**.
- **Partitioning**: Partitioned data by **NeighborhoodName** for efficient querying.

### **5. _Data Summarization_**

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/77e97387b38b03e8a195b2e327efa080a2c73e53/DAP_design_for_COV/images_ProjPart_1/ProjPart1%20%20ETL%20Pipeline.png" />
Visual ETL Pipeline for Parks data summarization


<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/075da8d0334b73322300e311d38b4e73211e22e0/DAP_design_for_COV/images_ProjPart_1/System%20friendly%20Data%20Summarization_PrjPart1.png" />
System-friendly parks data summarization (report Date-wise )


<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/075da8d0334b73322300e311d38b4e73211e22e0/DAP_design_for_COV/images_ProjPart_1/User%20Friendly%20Summarization_PrjPart%201.png" />
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

<img width="600" alt="Image" src="https://github.com/sumiya13/AWS-Cloud-Project/blob/075da8d0334b73322300e311d38b4e73211e22e0/DAP_design_for_COV/images_ProjPart_1/Cost%20Calculation_Parks%20Data.png" />
Cost Analysis Image 


The estimated monthly cost for implementing the DAP on AWS is **$36.74 per year**, with the following breakdown:
- **S3 Storage**: $0.04/month for 1 GB storage.
- **AWS Glue**: $3.01/month for ETL jobs and interactive sessions.
- **AWS DataBrew**: Included in the overall cost.



## 📌 **Conclusion**
This project successfully designed and implemented a **Data Analytics Platform (DAP)** for the City of Vancouver’s Parks dataset. By leveraging AWS services, we created a scalable and cost-effective solution for analyzing park distribution and size across neighborhoods. The insights generated from this platform will assist urban planners in making data-driven decisions for resource allocation and park development. This project lays the foundation for future enhancements, including automation and advanced analytics.



