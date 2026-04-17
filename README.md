# 🏥 Smart Hospital Management System

A relational database project designed to manage hospital operations efficiently — including patients, doctors, appointments, billing, prescriptions, and departments.

---

## 📖 Project Overview

The **Smart Hospital Management System** is a structured relational database system built to eliminate manual record-keeping in hospitals. It provides a well-normalized database schema to handle:

- Patient registration and medical records
- Doctor and staff management
- Appointment scheduling
- Prescription and medicine tracking
- Billing and insurance management
- Room and department management

---

## 🗃️ Database Design

The database is designed using the **Entity-Relationship (ER) model** and implemented in SQL. It follows a fully normalized schema up to **5NF**.

### Entities & Tables

| Table | Primary Key | Description |
|-------|-------------|-------------|
| Patient | Patient_ID | Stores patient personal and medical details |
| Doctor | Doctor_ID | Stores doctor qualifications and specialization |
| Employee | Emp_ID | Stores hospital staff details |
| Department | Dept_ID | Stores department name and head |
| Prescription | Prescription_ID | Links patient, doctor and medicine |
| Medicine | Medicine_ID | Stores medicine name, cost and quantity |
| Bill | Bill_ID | Stores billing and payment details |
| Room | Room_ID | Stores room type and cost |
| Appointment | Appointment_ID | Stores appointment date, time and doctor |
| Insurance | Insurance_ID | Stores policy, provider and coverage details |

---

## 🔗 Functional Dependencies

```
Patient_ID     → Name, Phone, Blood_Type, Email, Gender, Condition
Doctor_ID      → Qualification, Specialization, Emp_ID, Dept_ID
Emp_ID         → Name, Email, Address, Dept_ID
Dept_ID        → Dept_Name, Dept_Head
Prescription_ID→ Patient_ID, Medicine_ID, Doctor_ID, Date, Dosage
Medicine_ID    → Medicine_Name, Cost, Quantity
Bill_ID        → Patient_ID, Total, Remaining_Balance
Room_ID        → Room_Type, Patient_ID, Room_Cost
Appointment_ID → Date, Time, Doctor_ID, Patient_ID
Insurance_ID   → Policy_Number, Provider, Coverage
```

---

## 📐 Normalization

The database is fully normalized from **1NF to 5NF** to ensure data integrity, eliminate redundancy, and prevent anomalies.

### ✅ First Normal Form (1NF)
- All attributes contain **atomic (single) values**
- No repeating groups
- Each table has a primary key
- Example: One phone number per patient, one medicine per prescription row

### ✅ Second Normal Form (2NF)
- Satisfies 1NF
- **No partial dependency** — all attributes depend on the full primary key
- Most tables use single primary keys (Patient_ID, Doctor_ID, Bill_ID), making partial dependency impossible

### ✅ Third Normal Form (3NF)
- Satisfies 2NF
- **No transitive dependency** — non-key attributes do not depend on other non-key attributes
- Example: Department details are stored in a separate Department table (Dept_ID → Dept_Name), not inside the Patient or Doctor table

### ✅ BCNF (Boyce-Codd Normal Form)
- Satisfies 3NF
- Every determinant is a **candidate key / superkey**
- All functional dependencies are determined by primary keys only (Patient_ID, Doctor_ID, Appointment_ID)

### ✅ Fourth Normal Form (4NF)
- Satisfies BCNF
- **No multi-valued dependencies**
- Example: Each prescription stores one medicine per row; each appointment links to one doctor per visit

### ✅ Fifth Normal Form (5NF)
- Satisfies 4NF
- Tables **cannot be decomposed further** without losing information
- All relationships are simple and direct: Patient↔Appointment, Doctor↔Prescription, Staff↔Department

---

## ⚙️ SQL Implementation

The project includes:

- `CREATE TABLE` statements with primary keys, foreign keys and constraints
- `DEFAULT` values for balance fields
- `NOT NULL` constraints for critical fields
- **JOIN queries** — to fetch combined patient-doctor-appointment data
- **Nested queries** — to filter billing and prescription records
- **Aggregate queries** — for total billing, medicine cost summaries

---

## 🌟 Features

- ✅ Patient registration and record management
- ✅ Doctor and staff profile management
- ✅ Appointment scheduling system
- ✅ Prescription and medicine tracking
- ✅ Automated billing with remaining balance
- ✅ Room allocation management
- ✅ Insurance policy tracking
- ✅ Department-wise organization
- ✅ Fully normalized schema (1NF → 5NF)
- ✅ Referential integrity enforced via foreign keys

---

## 🛠️ Tech Stack

| Tool | Usage |
|------|-------|
| MySQL / SQL | Database implementation |
| ER Diagram Tool | Database design |
| GitHub | Version control and collaboration |

---

## 📊 Sample Queries

```sql
-- Get all appointments with patient and doctor details
SELECT p.Name, d.Specialization, a.Date, a.Time
FROM Patient p
JOIN Appointment a ON p.Patient_ID = a.Patient_ID
JOIN Doctor d ON a.Doctor_ID = d.Doctor_ID;

-- Get total bill for each patient
SELECT p.Name, b.Total, b.Remaining_Balance
FROM Patient p
JOIN Bill b ON p.Patient_ID = b.Patient_ID;

-- Get all prescriptions with medicine details
SELECT pr.Prescription_ID, m.Medicine_Name, m.Cost, pr.Dosage
FROM Prescription pr
JOIN Medicine m ON pr.Medicine_ID = m.Medicine_ID;
```

---

## 📁 Project Structure

```
SmartHospitalManagementSystem/
│
├── README.md
├── ER_Diagram.png
├── create_tables.sql
├── insert_data.sql
├── queries.sql
└── normalization_report.pdf
```

<img width="1136" height="390" alt="image" src="https://github.com/user-attachments/assets/cc7bef55-8160-4f7f-956d-e361d3a99383" />


## 📝 Conclusion

The Smart Hospital Management System demonstrates how a well-designed, fully normalized relational database can streamline hospital operations. By applying normalization from 1NF to 5NF, the system ensures **zero redundancy**, **data consistency**, and **efficient query performance**.

---

> 📌 *This project was developed as part of a Database Management System course.*
