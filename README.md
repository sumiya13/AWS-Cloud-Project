# Project 1: Automated Data Ingestion for UCW Academics Attendance Using AWS
# Objective 
The primary objective of this project is to ingest academic attendance data from the UCW operational environment into AWS Data Analysis Platform (DAP). The dataset includes students, instructors, and department details, and our goal is to establish a structured data lake for efficient storage and analysis.

# Dataset Overview
This project utilizes three datasets:

Student List
- Student_ID: Unique identifier for each student
- Name: Full name of the student
- Age: Age of the student
- Gender: Student’s gender
- Grade: Academic level (Freshman, Sophomore, Junior, Senior)
- Major: Student’s major field of study
- GPA: Grade Point Average
- Attendance (%): Attendance percentage of the student
- Scholarship: Yes/No indicator for scholarship status

Instructor List
- Instructor_ID: Unique identifier for each instructor
- Name: Instructor's full name
- Age: Instructor’s age
- Subject: Subject taught by the instructor
- Experience_Years: Number of years of teaching experience
- Salary: Instructor’s salary
- Location: Campus location of the instructor

Department List
- Department_ID: Unique identifier for each department
- Department_Name: Name of the department
- Head_of_Department: Name of the department head
- Number_of_Faculty: Total faculty members in the department
- Building_Name: The location of the department

# Methodology:
1. Data Ingestion Setup
- Designed the Data Analysis Platform (DAP) using Draw.io to map out the ingestion process.
- Created a Virtual Server (Academic General Virtual Server - AGVS-Sum) in AWS using EC2.
- Configured Amazon S3 as the Data Lake to store all raw academic attendance data.

 ![Image](https://github.com/user-attachments/assets/c0e38251-b310-4b2a-b7af-567fdee46aef)

2. Data Storage in AWS S3
- Created S3 bucket named academics-raw-sum to store raw data.
- Created Sub Folders inside the raw file to provide struture to our data
- Defined 'data Ingestion rate' for each of our dataset like this:
  /attendance/instructor-list/year=2025/quarter=1/month=1/server=AGVS-Sum
  /attendance/student-list/year=2025/quarter=1/server=AGVS-Sum
  /attendance/department-list/year=2025/server=AGVS-Sum

3. Virtual Server Configuration (EC2)
- Created EC2 Instance named AGVS-Sum
- Chose Windows AMI and t3.micro instance type (2 CPU, 1 GiB Memory)
- Used Vockey Key Pair for encryption
- Configured RDP access for remote connection
- Generated username, password and public DNS to connect to the sample virtual server created for UCW Academics Opeartion team
- Used 'Windows App' to connect to the remote virtual server using the pre generated credentials

4. Data Ingestion Process
- Generated datasets in CSV format in the virtual server:
  - Student-List.csv
  - Instructor-List.csv
  - Department-List.csv
- To complete 'Data Ingestion' used 'PowerShell'
  - Ran three different command to ingest three datset in AWS S3 bucket
- Verified successful ingestion in AWS S3 (Raw Data Storage)

Add PowerSheel Image Here

#  Results & Findings:
- Successfully created a remote virtual server to simulate UCW Academics operations.
- Designed an organized S3 data lake structure for long-term data storage.
- Implemented automated ingestion using Windows PowerShell & AWS EC2.
- Verified ingestion rate assumptions:
  - Instructor Data: Quarterly Ingestion
  - Student Data: Quarterly Ingestion
  - Department Data: Quarterly Ingestion

Add S3 SS for all 3 datasets

# Tools & Technologies Used:
- Cloud Services: AWS S3, AWS EC2
- Scripting: Windows PowerShell
- Design & Planning: Draw.io
- Version Control: GitHub

# Deliverables:
- Infrastructure Design Diagram (Draw.io)
- AWS S3 Data Ingestion Process
- PowerShell Commands for Data Upload
- Final Verification of Data in AWS S3

This project successfully established a data ingestion pipeline for UCW academic attendance data. By leveraging AWS Cloud Services, we ensured scalable, secure, and structured storage of academic records, forming the first step toward a comprehensive data analysis platform (DAP) for UCW Academics.
