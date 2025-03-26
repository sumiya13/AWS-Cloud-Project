# **Summarization and ETL Pipeline for UCW Academics Attendance Using AWS Services** 

## **📌 Objective**  
The goal of this project was to **structure, catalog, and summarize** UCW’s academic attendance data stored in AWS S3. We transformed raw student, instructor, and department datasets into an **organized data catalog** using **AWS Glue** and performed **aggregation-based summarization** to support UCW’s attendance tracking and reporting system.  



## **📌 Dataset Overview**  
We worked with **three cleaned datasets** stored in the `academics-trf-sum` S3 bucket:  

### **1. Student Attendance Data**  
- `Student_ID`, `Name`, `Age`, `Gender`  
- `Grade`, `Major`, `GPA`, `Attendance (%)`, `Scholarship`  

### **2. Instructor Data**  
- `Instructor_ID`, `Name`, `Age`, `Subject`  
- `Experience_Years`, `Salary`, `Location`  

### **3. Department Data**  
- `Department_ID`, `Department_Name`, `Head_of_Department`  
- `Number_of_Faculty`, `Building_Name`  


## **📌 Methodology**  

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/dde82dc0-e653-45bd-8ad8-e0b3131dbac5" />

Design for Academics (Attendace) data cataloging and summarization. 



### **1. Data Cataloging with AWS Glue**  
✅ **Created a Glue Database**: `academics-data-catalog-sum`  
✅ **Set Up Crawlers**:  
   - `academics-crw-sum` (automatically detects schema from S3)  
   - Ran crawlers to generate **3 structured tables** (student, instructor, department)  
✅ **Stored Metadata**: Table definitions stored in **AWS Glue Data Catalog**  

🔹 **Why?**  
- Converted **semi-structured** CSV data into **query-ready tables**  
- Enabled **SQL-based analysis** via AWS Athena  



### **2. Data Summarization with AWS Glue ETL**  
We built **three summarization pipelines** to extract key metrics:  

#### **📊 Student Attendance Summary**  
- **Filter**: Students with `Attendance (%) > 85`  
- **Group By**: `Major`  
- **Aggregations**:  
  - Average `GPA` per major  
  - Average `Age` per major  
- **Output**: Stored in `academics-cur-sum` (CSV for users, Parquet for systems)  

#### **📊 Instructor Experience Summary**  
- **Filter**: Instructors with `Experience_Years > 5`  
- **Group By**: `Subject`  
- **Aggregations**:  
  - Average `Experience_Years` per subject  
  - Average `Age` per subject  
- **Output**: Stored in `academics-cur-sum` (CSV for users, Parquet for systems)

#### **📊 Department Faculty Summary**  
- **Filter**: Departments with `Number_of_Faculty > 18`  
- **Group By**: `Department_Name`  
- **Aggregation**: Average `Number_of_Faculty`  
- **Output**: Stored in `academics-cur-sum` (CSV for users, Parquet for systems)

🔹 **Why Summarize?**  
- Reduced data volume for faster reporting  
- Provided **pre-computed metrics** for UCW’s academic dashboard  


### 4. Beanstalk Implementation for Web App & Log Ingestion
- Created an **Elastic Beanstalk app** named `AWA-sum`.
- Platform: **Python**, Region: `us-east-1a`
- Deployed sample web application, configured with auto-managed EC2 instance.
- Enabled monitoring and log file analysis.


## **📌 Results & Insights**  

### **🔍 Key Findings**  
✔ **Identified experienced instructors by subject area.**  
✔ **Recognized student majors with highest GPA and attendance.**  
✔ **Highlighted departments with strong faculty strength.**
✔ **Enabled centralized log management for academic applications**  





## **📌 Tools & Technologies**  
- **Data Cataloging**: AWS Glue Crawlers, Glue Data Catalog  
- **ETL & Summarization**: AWS Glue (PySpark)  
- **Storage**: Amazon S3 (`academics-trf-sum`, `academics-cur-sum`)  
- **Visualization**: AWS QuickSight (for future dashboards)  



## **📌 Deliverables**  
1. **AWS Glue Data Catalog** with 3 structured tables  
2. **Summarized datasets** in CSV & Parquet formats  
3. **ETL Job Scripts** for automated refreshes  
4. **Documentation** on schema & aggregation logic  



## **📌 Future Improvements**  
🔸 **Automate refreshes** with Glue Triggers  
🔸 **Build a dashboard** in QuickSight for UCW admins  
🔸 **Add ML-based predictions** for at-risk students  



## **📌 Conclusion**  
This project successfully **structured and summarized** UCW’s academic attendance data, enabling **faster reporting** and **data-driven decisions**. By leveraging **AWS Glue**, we transformed raw data into an **organized catalog** and extracted **key attendance trends** for UCW’s academic team.  

