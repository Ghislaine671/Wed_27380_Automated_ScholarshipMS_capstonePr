# 🎓 Automated Scholarship Management System

This project implements a PL/SQL-based Oracle database solution for an automated scholarship management system, designed to streamline application processing, enhance accuracy, and provide real-time updates for students and administrators at the Adventist University of Central Africa (AUCA). The system leverages Oracle PL/SQL for database creation, table management, data insertion, advanced programming, and auditing.

## 📋 Project Overview

- **Objective**: Develop a database-driven system to automate scholarship applications, reviews, and disbursements, reducing errors and improving efficiency.
- **Database**: Oracle Pluggable Database (`wed_27380_Mushirarungu_AutomatedScholarshipMS_db`).
- **Features**:
  - Automated scholarship application processing. 📝
  - Real-time status updates for stakeholders. 🕒
  - Secure data management with auditing. 🔒
  - Fair and efficient candidate selection. ✅
  - Restriction rules for data manipulation. 🚫

## 🛠️ Phases and Implementation

### 📦 Phase I: Problem Statement and Presentation
- **Objective**: Identify a real-world problem requiring a PL/SQL-based solution for scholarship management.
- **Problem Statement**: Manual scholarship systems cause errors, delays, and inefficiencies. The system automates application processing, enhances accuracy, and ensures secure, transparent updates.
- **Entities**:
  - **Students**: `Student_ID`, `Name`, `GPA`.
  - **Scholarships**: `Scholarship_ID`, `Name`, `Criteria`.
  - **Reviewers**: `Reviewer_ID`, `Name`, `Role`.
- **Deliverable**: PowerPoint presentation (`wed_27380_Mushirarungu_AutomatedScholarshipMS_db.pptx`) with up to three slides, submitted by March 25, 2025.
- **Sample Code**: Not applicable, as this phase focuses on documentation. A sample SQL query to preview the entity structure:
  ```sql
  -- Preview of entity structure (conceptual)
  SELECT 'Student_ID, Name, GPA' AS Students,
         'Scholarship_ID, Name, Criteria' AS Scholarships,
         'Reviewer_ID, Name, Role' AS Reviewers
  FROM DUAL;
  ```

### 📑 Phase II: Business Process Modeling
- **Objective**: Model the scholarship application and review process using BPMN/UML notations.
- **Tasks**:
  - Define the scope: Application submission, review, and award disbursement.
  - Identify entities: Students, reviewers, administrators, and the database.
  - Create a swimlane diagram using Lucidchart/draw.io to visualize interactions.
  - Write a one-page explanation aligning with MIS principles (e.g., streamlined decision-making).
- **Deliverable**: BPMN diagram and description submitted via GitHub.
  
  ![Image](https://github.com/user-attachments/assets/10ec60d8-d162-403f-85a9-19a11fc58180)

- **Sample Code**: Not directly applicable, but a query to simulate process flow analysis:
  ```sql
  -- Simulate process flow data retrieval
  SELECT 'Student submits application' AS Step1,
         'Reviewer evaluates application' AS Step2,
         'Admin approves disbursement' AS Step3
  FROM DUAL;
  ```

### 📊 Phase III: Logical Model Design
- **Objective**: Design a logical data model for the scholarship system.
- **Tasks**:
  - Create an ER model with entities (`Students`, `Scholarships`, `Reviewers`, `Applications`).
  - Define attributes, primary keys (PKs), foreign keys (FKs), and constraints (e.g., NOT NULL, CHECK for GPA between 0-4).
  - Normalize to 3rd Normal Form (3NF) to eliminate redundancy.
- **Deliverable**: ![Image](https://github.com/user-attachments/assets/e33639af-4830-486b-a5d0-e72030b84ab2)
- **Sample Code**: SQL for a conceptual table structure:
  ```sql
  -- Conceptual table structure for Students
  CREATE TABLE Students (
      Student_ID NUMBER PRIMARY KEY,
      Name VARCHAR2(100) NOT NULL,
      GPA NUMBER CHECK (GPA >= 0 AND GPA <= 4)
  );
  ```

### 📦 Phase IV: Database (Pluggable Database) Creation and Naming
- **Database Creation** 🗄️: A pluggable database named `wed_27380_Mushirarungu_AutomatedScholarshipMS_db` was created with the admin user `admin` and password `Mushirarungu`. The database is configured with super admin privileges.
- **Oracle Enterprise Manager (OEM)** 📊: OEM is set up to monitor the database. Screenshots of the OEM dashboard (showing the project name) are available in the GitHub repository for progress tracking.
- **Sample Code**: Database creation script:
  ```sql
  CREATE PLUGGABLE DATABASE wed_27380_Mushirarungu_AutomatedScholarshipMS_db
      ADMIN USER admin IDENTIFIED BY Mushirarungu
      ROLES = (DBA)
      FILE_NAME_CONVERT = ('/u01/app/oracle/oradata/CDB1/pdbseed/', '/u01/app/oracle/oradata/CDB1/wed_27380_Mushirarungu_AutomatedScholarshipMS_db/');
  ALTER PLUGGABLE DATABASE wed_27380_Mushirarungu_AutomatedScholarshipMS_db OPEN;
  ALTER SESSION SET CONTAINER = wed_27380_Mushirarungu_AutomatedScholarshipMS_db;
  ```

### 📑 Phase V: Table Implementation and Data Insertion
- **Table Creation** 📋: Tables (`Students`, `Scholarships`, `Reviewers`, `Applications`, `Holidays`, `Audit_Log`) are implemented with appropriate columns, data types, primary/foreign keys, and constraints (e.g., NOT NULL, CHECK, UNIQUE).
- **Data Insertion** 📥: Realistic data is inserted into each table, including:
  - 10 students with names and GPAs. 🎓
  - 5 scholarships with criteria (e.g., GPA ≥ 3.0). 🏆
  - 3 reviewers with roles (e.g., Faculty, Admin). 👥
  - 10 application records linking students to scholarships. 📋
  - Holiday dates for June 2025 (e.g., June 1, June 15). 📅
  - Audit log entries for tracking. 📜
- **Data Integrity** ✅: Constraints ensure data consistency, and queries validate the structure.
- **Sample Code**: Table creation and sample data insertion:
  ```sql
  -- Create Students table
  CREATE TABLE Students (
      Student_ID NUMBER PRIMARY KEY,
      Name VARCHAR2(100) NOT NULL,
      GPA NUMBER CHECK (GPA >= 0 AND GPA <= 4)
  );

  -- Insert sample data
  INSERT INTO Students (Student_ID, Name, GPA) VALUES (1, 'John Doe', 3.8);
  INSERT INTO Students (Student_ID, Name, GPA) VALUES (2, 'Jane Smith', 3.5);
  ```

### 💻 Phase VI: Database Interaction and Transactions
- **Database Operations** 🛠️: DDL (e.g., `ALTER TABLE`) and DML (e.g., `INSERT`, `UPDATE`, `DELETE`) operations are supported.
- **Procedures and Functions** 🧩:
  - `get_eligible_students(p_scholarship_id IN NUMBER)`: Retrieves students meeting scholarship criteria using a cursor.
  - `get_application_status(p_student_id IN NUMBER)`: Returns the status of a student’s application using window functions.
- **Packages** 📦: The `scholarship_pkg` package encapsulates procedures and functions for modular data retrieval and analysis.
- **Testing** ✔️: Procedures and functions are tested to ensure correct output (e.g., `EXEC scholarship_pkg.get_eligible_students(1);`).
- **Sample Code**: Procedure for retrieving eligible students:
  ```sql
  CREATE OR REPLACE PACKAGE scholarship_pkg AS
      PROCEDURE get_eligible_students(p_scholarship_id IN NUMBER);
  END scholarship_pkg;
  /

  CREATE OR REPLACE PACKAGE BODY scholarship_pkg AS
      PROCEDURE get_eligible_students(p_scholarship_id IN NUMBER) IS
          CURSOR eligible_cur IS
              SELECT s.Student_ID, s.Name, s.GPA
              FROM Students s
              JOIN Applications a ON s.Student_ID = a.Student_ID
              WHERE a.Scholarship_ID = p_scholarship_id
              AND s.GPA >= (SELECT Criteria FROM Scholarships WHERE Scholarship_ID = p_scholarship_id);
      BEGIN
          FOR rec IN eligible_cur LOOP
              DBMS_OUTPUT.PUT_LINE('Student: ' || rec.Name || ', GPA: ' || rec.GPA);
          END LOOP;
      EXCEPTION
          WHEN OTHERS THEN
              DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
      END get_eligible_students;
  END scholarship_pkg;
  /
  ```

### 🔍 Phase VII: Advanced Database Programming and Auditing
- **Problem Statement** ❓: Prevent unauthorized table manipulations (INSERT, UPDATE, DELETE) by employees on weekdays and holidays in June 2025 to maintain data reliability.
- **Trigger Implementation** ⚙️: A compound trigger (`trg_restrict_manipulation`) blocks manipulations on weekdays (Monday-Friday) and holidays (e.g., June 1, June 15) using a `Holidays` table.
- **Auditing** 📜: An `Audit_Log` table tracks user actions (UserID, ActionDate, Operation, Status) with a trigger (`trg_audit_scholarship`) to log allowed/denied operations, enhancing security and accountability.
- **Sample Code**: Compound trigger and audit table:
  ```sql
  -- Create Holidays table
  CREATE TABLE Holidays (
      Holiday_Date DATE PRIMARY KEY
  );

  -- Insert sample holiday data
  INSERT INTO Holidays (Holiday_Date) VALUES (TO_DATE('2025-06-01', 'YYYY-MM-DD'));
  INSERT INTO Holidays (Holiday_Date) VALUES (TO_DATE('2025-06-15', 'YYYY-MM-DD'));

  -- Create Audit_Log table
  CREATE TABLE Audit_Log (
      Log_ID NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
      User_ID VARCHAR2(50),
      Action_Date DATE,
      Operation VARCHAR2(50),
      Status VARCHAR2(20)
  );

  -- Compound trigger to restrict manipulations
  CREATE OR REPLACE TRIGGER trg_restrict_manipulation
  FOR INSERT OR UPDATE OR DELETE ON Students
  COMPOUND TRIGGER
      v_day VARCHAR2(10);
      v_holiday NUMBER;
  BEFORE STATEMENT IS
  BEGIN
      SELECT TO_CHAR(SYSDATE, 'DY') INTO v_day FROM DUAL;
      SELECT COUNT(*) INTO v_holiday
      FROM Holidays
      WHERE Holiday_Date = TRUNC(SYSDATE)
      AND EXTRACT(MONTH FROM Holiday_Date) = 6
      AND EXTRACT(YEAR FROM Holiday_Date) = 2025;
      IF v_day IN ('MON', 'TUE', 'WED', 'THU', 'FRI') OR v_holiday > 0 THEN
          RAISE_APPLICATION_ERROR(-20001, 'Manipulations restricted on weekdays and holidays.');
      END IF;
  END BEFORE STATEMENT;
  AFTER STATEMENT IS
  BEGIN
      INSERT INTO Audit_Log (User_ID, Action_Date, Operation, Status)
      VALUES (USER, SYSDATE, 'DML Attempt', 'Allowed');
  EXCEPTION
      WHEN OTHERS THEN
          INSERT INTO Audit_Log (User_ID, Action_Date, Operation, Status)
          VALUES (USER, SYSDATE, 'DML Attempt', 'Denied: ' || SQLERRM);
  END AFTER STATEMENT;
  END trg_restrict_manipulation;
  /
  ```

### 📝 Phase VIII: Documentation and Demonstration
- **GitHub Report** 📸: Includes:
  - Introduction: Student name (Mushirarungu), ID (27380), and problem statement.
  - Screenshots: OEM dashboard, ER diagram, BPMN diagram, and query results.
  - SQL Queries: DDL, DML, triggers, procedures, and packages.
- **PowerPoint Presentation** 📽️:
  - Maximum 10 slides covering introduction, problem definition, methodology, results, and conclusion.
  - Includes visual aids (e.g., ER diagram, BPMN diagram, OEM screenshots).
  - Submitted via email and Google Drive by the exam deadline.
- **Sample Code**: Sample query for reporting:
  ```sql
  -- Sample query for audit log report
  SELECT User_ID, Action_Date, Operation, Status
  FROM Audit_Log
  WHERE Action_Date >= TRUNC(SYSDATE) - 7;
  ```

## 🛠️ Setup Instructions

1. **Prerequisites** 📋:
   - Oracle Database 21c or later with PL/SQL support.
   - Access to Oracle Enterprise Manager (OEM).
   - GitHub account for progress reporting.
   - Lucidchart or draw.io for diagram creation.

2. **Database Setup** 🗄️:
   - Create the pluggable database using the provided SQL script (adjust file paths as needed):
     ```sql
     CREATE PLUGGABLE DATABASE wed_27380_Mushirarungu_AutomatedScholarshipMS_db
       ADMIN USER admin IDENTIFIED BY Mushirarungu
       ROLES = (DBA)
       FILE_NAME_CONVERT = ('/u01/app/oracle/oradata/CDB1/pdbseed/', '/u01/app/oracle/oradata/CDB1/wed_27380_Mushirarungu_AutomatedScholarshipMS_db/');
     ALTER PLUGGABLE DATABASE wed_27380_Mushirarungu_AutomatedScholarshipMS_db OPEN;
     ALTER SESSION SET CONTAINER = wed_27380_Mushirarungu_AutomatedScholarshipMS_db;
     ```
   - Set up OEM and configure monitoring.

3. **Table and Data Setup** 📥:
   - Run the table creation and data insertion scripts provided in Phase V.

4. **Package and Trigger Setup** ⚙️:
   - Execute the `scholarship_pkg` package and trigger scripts from Phases VI and VII.

## 🚀 Usage

- **Query Eligible Students** 🎓: Use `scholarship_pkg.get_eligible_students(1)` to view students eligible for a specific scholarship.
- **Check Application Status** 📋: Use `SELECT scholarship_pkg.get_application_status(1) FROM DUAL` to check a student’s application status.
- **Monitor Restrictions** 🔒: Attempt table manipulations on a weekday (e.g., May 26, 2025) or holiday to test the trigger; check `Audit_Log` for results.

## 🤝 Contributing

1. **Progress Reporting** 📸: Upload screenshots of OEM and SQL scripts to the GitHub repository, ensuring the project name is visible to avoid plagiarism.
2. **Collaboration** 🌐: Fork the repository, create a branch, and submit pull requests with changes.
3. **Issues** 🐞: Report bugs or suggest enhancements via GitHub Issues.

## 🔮 Future Work
- Integrate a web-based front-end for user interaction.
- Enhance auditing with real-time notifications for unauthorized access.
- Expand to support additional scholarship types and criteria.

## 📚 References
- Oracle PL/SQL Documentation
- AUCA Capstone Project Guidelines (2024-2025)
- BPMN and UML standards for process modeling

---

**Author**: Mushirarungu (Student ID: 27380)  
**Course**: Database Development with PL/SQL (INSY 8311)  
**Institution**: Adventist University of Central Africa  
**Date**: April 20, 2025
