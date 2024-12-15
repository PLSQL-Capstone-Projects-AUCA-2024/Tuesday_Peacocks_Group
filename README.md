# Peacock Group
## Members:
 1. 25048 NTWARI Deus
 2. 25918 INGABIRE NZARAMBA Ritha
 3. 26155 Ishimwe Mahoro Christianne 
 4. 26046 MABHYALA Wulsy
 5. 25514 HURUMA Innocent
 6. 24849 NAHAYO Arnaud
 7. 25964 Mugisha Godefroid
 8. 26073 UMUGWANEZA Aimée
 9. 26975 NIYOYAVUZE AMIELLE PONTIENNE
 10. 25899 Arnaud NSHUTI
 11. 25444 Uwizeye Ngoga Sandra



# Police Examination Process - README

## Project Overview
The **Police Examination Process** project aims to develop a streamlined, digitalized system to support applicants in obtaining driving licenses, covering everything from registration to examination and result notification. Key processes are automated to minimize manual data handling and ensure data accuracy and enhance protection.

## Project Phases

### Phase 2: Business Process Modeling (BPMN Diagram).
- **Scope:** Design a digitalized driving license application process, from registration to final issuance.
- **Objectives:**
  - Reduce manual errors and enhance processing efficiency.
  - Automate notifications for exam scheduling and results.
- **Expected Outcomes:**
  - Improved data accuracy and faster processing.
  - Centralized database accessible by authorized departments.

- **Key Entities:**
  - **Applicant:** Applies for a license.
  - **Police Officer:** Verifies documents and approves applications.
  - **Examination Center:** Conducts exams and records results.
  - **License:** Issued upon successful completion.

- **Process Flow:** Application Submission → Document Verification → Exam Scheduling → Result Recording → License Issuance or Retest Notification.
- **Decision Points:** Includes checks like "Document Approved?" and "Exam Passed?"

- **Summary:** The process is centralized within a Management Information System (MIS), improving decision-making, efficiency, and reducing errors.

### Phase 3: Logical Model Design
- **Data Model Design:**
  - **Entities & Attributes:**
    - **Applicant:** `applicant_id (PK)`, `fname`, `lname`, `Date_birth`, `gender`, `address`.
    - **Application:** `application_id (PK)`, `applicant_id (FK)`, `application_date`, `status`, `remarks`.
    - **Examination Schedule:** `schedule_id (PK)`, `application_id (FK)`, `exam_date`, `exam_center_id (FK)`, `notification_status`.
    - **Examination Center:** `center_id (PK)`, `center_name`, `location`, `capacity`.
    - **Test:** `test_id (PK)`, `schedule_id (FK)`, `examiner_id (FK)`, `test_type`, `result`, `comments`.
    - **Examiner:** `examiner_id (PK)`, `fname`, `lname`, `qualification`, `assigned_center`.
    - **License:** `license_id (PK)`, `applicant_id (FK)`, `issue_date`, `expiration_date`, `license_type`.
    - **Notifications:** `notification_id (PK)`, `schedule_id (FK)`, `sent_date`, `status`, `message_type`.

- **Relationships:**
  - **One-to-Many:** An applicant can have multiple exam attempts.
  - **One-to-One:** One result per exam.

- **Data Scenarios:**
  - **Failed Exam:** Track failed attempts and flag retest eligibility.
  - **License Issuance:** Issue a license upon passing and archive records.
  - **Notifications:** Automate exam schedule and result notifications. (Trigger notifications for exam dates and results)

    # Phase 4, 5 & 6: Police Examination System  

## Overview  

This project is part of a comprehensive database system designed to streamline the **Police Examination Process**. The system tracks applicants, applications, examination schedules, test results, licenses, and notifications. This README outlines the purpose, design, and operations performed in Phases 4, 5, and 6, focusing on enhancing the system's functionality and ensuring data integrity.  

---

## Key Features  

1. **Applicant Management**:  
   - Records applicant details such as name, date of birth, address, and gender.  
   - Links applicants to their applications, test schedules, and licenses.  

2. **Application Processing**:  
   - Tracks application statuses (e.g., pending, complete) with remarks.  

3. **Examination Scheduling and Notifications**:  
   - Assigns applicants to specific examination centers.  
   - Sends notifications to applicants about scheduled exams and results.  

4. **Test Management**:  
   - Records test types, results, and examiner comments.  

5. **License Issuance**:  
   - Issues licenses to successful applicants, tracking issue and expiration dates.  

6. **Data Relationships**:  
   - Enforces relational constraints to maintain data consistency across the database.  

---

## Database Design  

### Tables and Relationships  

- **Applicant Table**: Stores applicant details.  
- **Application Table**: Links applicants to their application statuses.  
- **Examination Scheduling Table**: Associates applications with exam centers and notifications.  
- **Examination Center Table**: Contains details of examination centers.  
- **Examiner Table**: Tracks examiners and their qualifications.  
- **Test Table**: Records test details, results, and comments.  
- **License Table**: Manages license issuance details.  
- **Notifications Table**: Tracks notifications sent to applicants.  

Each table is interconnected using **primary keys** and **foreign key constraints** to ensure relational integrity.

---

## Transactions Performed  

### 1. **Insert Operations**  
- Inserted data into all core tables, including `Applicant`, `Application`, `Examination_Scheduling`, `Test`, `License`, and `Notifications`.  
- Example: Adding a new applicant, their application, and scheduling their exam.  

### 2. **Data Retrieval**  
- Queried data to retrieve detailed reports such as:  
  - Applicant details along with application status and exam schedule.  
  - Examination results for an applicant.  
  - Overall pass/fail rates for different test types.  

### 3. **Join Operations**  
- Used various joins to link tables for reports and insights:  
  - **INNER JOIN**: Fetch applicant details with application and exam statuses.  
  - **LEFT OUTER JOIN**: Retrieve all applicants, whether scheduled for exams or not.  
  - **RIGHT OUTER JOIN**: List all schedules, even if no applicant is assigned.  
  - **FULL OUTER JOIN**: Combine all applicants and schedules, regardless of matching records.  

### 4. **Update Operations**  
- Example: Updating the status of a notification.  

### 5. **Delete Operations**  
- Example: Deleting test records for failed results.  

---

## Results and Reports  

### Sample Queries  

1. **Retrieve Applicant Details**  
   ```sql  
   SELECT a.FirstName, a.LastName, ap.Status AS ApplicationStatus, es.NotificationStatus AS ExamStatus  
   FROM Applicant a  
   JOIN Application ap ON a.ApplicantID = ap.ApplicantID  
   JOIN Examination_Scheduling es ON ap.ApplicationID = es.ApplicationID  
   WHERE a.ApplicantID = 1;  
   ```

2. **Generate Pass/Fail Rates**  
   ```sql  
   SELECT t.TestType, t.Result, COUNT(*) AS ResultCount  
   FROM Test t  
   GROUP BY t.TestType, t.Result;  
   ```

3. **Retrieve All Licenses Issued**  
   ```sql  
   SELECT a.FirstName, a.LastName, l.LicenseType, l.IssueDate, l.ExpirationDate  
   FROM License l  
   JOIN Applicant a ON l.ApplicantID = a.ApplicantID;  
   ```

---


## Usage  

### Prerequisites  

1. Oracle Database or a compatible RDBMS.  
2. A database tool (e.g., SQL Developer) for running SQL scripts.  

### How to Run  

1. Execute the table creation scripts.  
2. Apply the foreign key constraints.  
3. Insert sample data into each table.  
4. Run the provided queries to verify relationships and retrieve data.  

---

## Future Enhancements  

1. Add more detailed notifications (e.g., SMS or email integration).  
2. Implement stored procedures for common tasks such as scheduling exams or issuing licenses.  
3. Introduce role-based access control for examiners and administrators.  

---



## Conclusion
The **Police Examination Process** project establishes an efficient, digitalized workflow for driving license applications, with enhanced speed, accuracy, and centralized data management through BPMN modeling and structured data relationships.

## **Phase 7**

  

---

# **Police Examination Process - Driving License Management System**  

## **Project Overview**  
The **Driving License Management System** is a database-driven solution designed to streamline and enhance the process of managing police examinations for driving license issuance. This system ensures accuracy, data integrity, automation, and efficient workflow management for applicants, examiners, and the police department.

---

## **Problem Statement**  
The current paper-based system for managing driving license examinations is inefficient, error-prone, and lacks transparency. Advanced database programming techniques such as triggers, cursors, functions, packages, and auditing were implemented to address these challenges and optimize the system's performance.  

- **Triggers** automate workflows and enforce business rules.  
- **Cursors** process row-by-row operations effectively.  
- **Functions** ensure reusable and modular programming.  
- **Packages** organize related database objects for better maintenance.  
- **Auditing techniques** ensure accountability and track unauthorized access or changes.  

---

## **System Features**  
- **Applicant Management:** Stores personal details and tracks application progress.  
- **Examination Scheduling:** Automates the scheduling of examinations.  
- **Test Results Storage:** Manages test results and pass/fail status.  
- **License Issuance:** Issues licenses for successful candidates.  
- **Notifications:** Tracks and automates notifications for applicants.  

---

## **Contributors and Roles**  

| **ID**      | **Name**                     | **Role**                                                                                   |  
|-------------|------------------------------|-------------------------------------------------------------------------------------------|  
| **25964**   | Mugisha Godefroid            | Database Architect & Developer – Designed the database schema and implemented advanced techniques.  |  
| **25048**   | NTWARI Deus                  | Lead System Designer & Project Coordinator – Led the project design and team coordination efforts. |  
| **25918**   | INGABIRE NZARAMBA Ritha      | Application Tester – Ensured the database and system functionality met requirements.      |  
| **26155**   | Ishimwe Mahoro Christianne   | UI/UX Designer – Designed the front-end interfaces for the management system.             |  
| **26046**   | MABHYALA Wulsy               | System Administrator – Managed database deployment and configurations.                    |  
| **25514**   | HURUMA Innocent              | Security Specialist – Implemented data encryption and auditing mechanisms.               |  
| **24849**   | NAHAYO Arnaud                | Backend Developer – Worked on integrating database operations with application logic.     |  
| **26073**   | UMUGWANEZA Aimée             | Quality Assurance Analyst – Verified workflow processes and handled error management.     |  
| **26975**   | NIYOYAVUZE AMIELLE PONTIENNE | Data Analyst – Generated statistical reports on examination results.                      |  
| **25899**   | Arnaud NSHUTI                | Scheduler & Tester – Optimized examination schedules and tested their functionality.      |  
| **25444**   | Uwizeye Ngoga Sandra         | Documentation Specialist – Created system documentation and user manuals.                |  

---

## **Setup Instructions**  

### **Database Setup**  
1. Import the provided database schema into your Oracle SQL environment.  
2. Run the scripts for triggers, functions, and packages provided in the `DatabaseScripts` folder.  
3. Ensure the database user has appropriate privileges to execute advanced programming constructs.  

### **Application Setup**  
1. Clone the repository to your local machine.  
2. Set up the front-end interface for connecting to the database.  
3. Configure the database connection in the configuration file (`db_config.xml`).  

---

## **How to Run**  
1. Launch the application interface.  
2. Use administrator credentials to log in and access management features.  
3. Schedule examinations, track applicant progress, and manage test results through the interface.  

---

## **Key Features Implemented**  
### **1. Triggers**  
- **Example:** BEFORE INSERT trigger to validate test scores.  
- Automates processes such as sending notifications or updating application status.  

### **2. Cursors**  
- Used for processing multiple test results row-by-row during report generation.  

### **3. Functions**  
- Modularized complex operations such as calculating pass percentages or determining eligibility.  

### **4. Packages**  
- Encapsulated related procedures and functions, such as applicant management and result processing, into reusable packages.  

### **5. Auditing**  
- Logs unauthorized access attempts and tracks all modifications to sensitive data.  

---

## **Sample SQL Queries**  
1. **Generate Pass/Fail Statistics:**  
```sql  
SELECT test_type, COUNT(*) AS total,  
    SUM(CASE WHEN result = 'Pass' THEN 1 ELSE 0 END) AS passed,  
    SUM(CASE WHEN result = 'Fail' THEN 1 ELSE 0 END) AS failed  
FROM test_results  
GROUP BY test_type;  
```  

2. **Schedule Examination:**  
```sql  
INSERT INTO examination_schedule (applicant_id, test_date, center_id)  
VALUES (101, TO_DATE('2024-12-15', 'YYYY-MM-DD'), 5);  
```  

3. **Audit Query:**  
```sql  
SELECT * FROM audit_log WHERE user_id = 'admin' AND action = 'UPDATE';  
```  

---

## **Acknowledgments**  
Special thanks to the contributors for their dedicated efforts to ensure the success of this project from the beginning till the end, May God bless you all.

--- 

