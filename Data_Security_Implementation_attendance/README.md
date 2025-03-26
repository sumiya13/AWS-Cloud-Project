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

---

## 🔐 Methodology

### 1. **Confidentiality and Integrity via Encryption (AWS KMS + SSE-KMS)**
- Created a **Customer Managed Key** in **AWS Key Management Service (KMS)**:
  - **Key Name**: `aca-attn-key-sum`
  - **Key Type**: Symmetric
  - **Key Usage**: Encryption and Decryption
  - **Permissions**: Attached to IAM Role `Labrole`
- Applied the KMS key to three primary buckets:
  - `aca-raw-sum`
  - `aca-trf-sum`
  - `aca-cur-sum`
- Updated **Default Encryption Settings** in each bucket:
  - From: `SSE-S3` (Amazon-managed key)
  - To: `SSE-KMS` (Customer-managed key `aca-attn-key-sum`)

🔐 This ensures all data **uploaded is encrypted automatically**, and **decrypted upon access**, maintaining both confidentiality and integrity.

---

### 2. **Version Control for Enhanced Security (Bucket Versioning)**
- Enabled **Bucket Versioning** for all primary buckets:
  - `aca-raw-sum`
  - `aca-trf-sum`
  - `aca-cur-sum`

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


