# 🔐 Descriptive Analysis  
## **Project Title:**
**Data Security Implementation for UCW Attendance Procedure Datasets Using AWS KMS & S3**

---

## 🧩 **Objective**
The objective of this project is to **implement data security best practices** for academic attendance datasets at UCW using **AWS Key Management Service (KMS)** and **S3 storage configuration**. This project ensures **data confidentiality, integrity, and availability (CIA)** by applying encryption, bucket versioning, and replication strategies.

---

## 📁 **Dataset Overview**
This project utilizes three datasets:

### 🎓 Student List
- **Student_ID**: Unique identifier for each student  
- **Name**: Full name of the student  
- **Age**: Age of the student  
- **Gender**: Student’s gender  
- **Grade**: Academic level (Freshman, Sophomore, Junior, Senior)  
- **Major**: Student’s major field of study  
- **GPA**: Grade Point Average  
- **Attendance (%)**: Attendance percentage of the student  
- **Scholarship**: Yes/No indicator for scholarship status  

### 👨‍🏫 Instructor List
- **Instructor_ID**: Unique identifier for each instructor  
- **Name**: Instructor's full name  
- **Age**: Instructor’s age  
- **Subject**: Subject taught by the instructor  
- **Experience_Years**: Number of years of teaching experience  
- **Salary**: Instructor’s salary  
- **Location**: Campus location of the instructor  

### 🏢 Department List
- **Department_ID**: Unique identifier for each department  
- **Department_Name**: Name of the department  
- **Head_of_Department**: Name of the department head  
- **Number_of_Faculty**: Total faculty members in the department  
- **Building_Name**: The location of the department


### 🔐 Secured Datasets in AWS S3

#### 1. Student Attendance Data  
**PII requiring encryption**  
`Student_ID` | `Name` | `GPA` | `Attendance (%)` | `Scholarship Status`  

#### 2. Instructor Records  
**Sensitive employment data**  
`Instructor_ID` | `Salary` | `Experience_Years`  

#### 3. Department Information  
**Organizational structure**  
`Department_ID` | `Head_of_Department` | `Faculty_Count`  


**Security Classification**:
- 🔒 **Tier 1 (High Sensitivity)**: Student PII
- 🔐 **Tier 2 (Medium Sensitivity)**: Instructor salary data
- 🔓 **Tier 3 (Low Sensitivity)**: Department metadata


---

## 🔐 Methodology

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/2528848f-7157-4628-9183-91e817830df6" />

Design Part: Draw.io design for data security implementation

### 1. **Confidentiality and Integrity via Encryption (AWS KMS + SSE-KMS)**
- Created a **Customer Managed Key** in **AWS Key Management Service (KMS)**:
  - **Key Name**: `aca-attn-key-sum`
  - **Key Type**: Symmetric
  - **Key Usage**: Encryption and Decryption
  - **Permissions**: Attached to IAM Role `Labrole`
 

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/646e8b45-72c3-4557-8a98-396e7dbcfd86" />

Key creation using AWS key Management Service (KMS)

- Applied the KMS key to three primary buckets:
  - `aca-raw-sum`
  - `aca-trf-sum`
  - `aca-cur-sum`
- Updated **Default Encryption Settings** in each bucket:
  - From: `SSE-S3` (Amazon-managed key)
  - To: `SSE-KMS` (Customer-managed key `aca-attn-key-sum`)


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/5a0a7694-77ec-418c-bf50-9fb1d426b959" />

Changing the 'Default encryption' in 'academics-raw-sum' bucket to use the new key 'aca-attn-key-sum'



<img width="600" alt="Image" src="https://github.com/user-attachments/assets/eebc6234-9cc6-469d-a64a-80976243572f" />

Changing the 'Default encryption' in 'academics-trf-sum' bucket to use the new key 'aca-attn-key-sum'


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/a066423b-3a57-48bf-bd97-f1547a41e793" />

Changing the 'Default encryption' in 'academics-cur-sum' bucket to use the new key 'aca-attn-key-sum'


🔐 This ensures all data **uploaded is encrypted automatically**, and **decrypted upon access**, maintaining both confidentiality and integrity.

---

### 2. **Version Control for Enhanced Security (Bucket Versioning)**
- Enabled **Bucket Versioning** for all primary buckets:
  - `aca-raw-sum`
  - `aca-trf-sum`
  - `aca-cur-sum`

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/0e5f6ef1-7398-4a74-b6a3-c6d7b9c529a6" />

Enabling the 'Bucket Versioning' for 'academics-raw-sum' bucket 


<img width="600" alt="Image" src="https://github.com/user-attachments/assets/33dc59e6-0135-4ef0-baf7-46f65d6a506d" />

Enabling the 'Bucket Versioning' for 'academics-trf-sum' bucket 

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/e90ca737-bc8a-4945-b8eb-b64e5300ab75" />

Enabling the 'Bucket Versioning' for 'academics-cur-sum' bucket 


📌 This ensures **every version of every object** is retained. If a file is overwritten or deleted, previous versions remain accessible.

💡 While this increases storage costs, it guarantees stronger **audit trails and rollback options**, improving data integrity and recovery.

---

### 3. **Availability via Replication and Backup Buckets**
- Created **backup buckets** for each primary bucket:
  - `academics-raw-bac-sum`
  - `academics-trf-bac-sum`
  - `academics-cur-bac-sum`

- Configured **Replication Rules**:
  - Rule Name: `aca-attn-rep-rule-sum`
  - Configured in **Management tab** of each primary bucket
  - Selected **destination buckets** as their respective backups
  - Enabled **Bucket Versioning** in all backup buckets as a prerequisite

💾 This ensures **automated, real-time replication** of all data into backup buckets — a crucial step in maintaining **availability**.

---

## 🔍 Insights and Findings
- ✅ Encryption via AWS KMS guarantees **data confidentiality**.
- ✅ Bucket versioning ensures **historical integrity and recovery**.
- ✅ Replication provides **high availability and fault tolerance**.
- ✅ S3 + KMS integration enables **seamless security management**.

---

## 🧠 Recommendations
- 🔐 Use **customer-managed KMS keys** instead of default AWS keys for greater control.
- 📦 Regularly review bucket policies and access controls for potential vulnerabilities.
- 🔄 Set up **event-based triggers or CloudWatch alerts** for replication failures.
- 📊 Monitor **cost implications** of versioning and replication in production-scale environments.

---

## 🛠 Tools and Technologies
- **Cloud Services**: AWS S3, AWS KMS, AWS IAM  
- **Security Features**: SSE-KMS, Bucket Versioning, S3 Replication  
- **Identity Management**: IAM Role `Labrole`  
- **Monitoring**: S3 Management, Encryption Policies  

---

## 📦 Deliverables
- ✅ Configured **customer-managed encryption key** (`aca-attn-key-sum`)  
- ✅ Updated encryption policy in 3 primary buckets  
- ✅ Bucket versioning enabled on both primary and backup buckets  
- ✅ Real-time replication rules applied  
- ✅ Security-first data lake structure for UCW Attendance datasets

---

## 🔐 Summary
This project focuses on securing UCW Attendance datasets by implementing core principles of the **CIA triad (Confidentiality, Integrity, Availability)** using AWS services. It includes full encryption with AWS KMS, version control with bucket versioning, and high availability via bucket replication — ensuring the attendance data is safe, accessible, and trustworthy in any circumstance.


