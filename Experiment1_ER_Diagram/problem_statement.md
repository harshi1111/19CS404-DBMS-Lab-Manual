# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

---

# ER Diagram Submission - HARSHITHA V

## Scenario Chosen:
Hospital 

## ER Diagram:

![image](https://github.com/user-attachments/assets/b0359b5a-796f-472c-a822-538a72d30a98)

---

## Entities and Attributes:

- PATIENT:
Attributes - PATIENT ID, FULL NAME, DATE OF BIRTH, GENDER, ADDRESS, EMAIL, PHONE NUMBER, INSURANCE DETAILS

- APPOINTMENT:
Attributes - APPOINTMENT ID, DATE, TIME, REASON, NOTES

- DOCTOR:
Attributes - DOCTOR ID, NAME, SPECIALIZATION, PHONE NUMBER, EMAIL, WORK SCHEDULE

- DEPARTMENT:
Attributes - DEPARTMENT ID, DEPARTMENT NAME, DEPARTMENT HEAD

- MEDICAL REPORT:
Attributes - MEDICAL DIAGNOSIS ID, DIAGNOSIS, TREATMENT, PRESCRIBED MEDICATION, TEST RESULTS

- BILLING:
Attributes - BILLING ID, AMOUNT, PAYMENT METHOD, PAYMENT STATUS

---

## Relationships and Constraints:

- Books (1:N, PATIENT to APPOINTMENT — Partial Participation of PATIENT, Total Participation of APPOINTMENT)

- Handles (1:N, DOCTOR to APPOINTMENT — Partial Participation of DOCTOR, Total Participation of APPOINTMENT)

- Belongs To (N:1, DOCTOR to DEPARTMENT — Partial Participation from both DOCTOR and DEPARTMENT)

- Produces (1:1, APPOINTMENT to MEDICAL REPORT — Partial Participation of APPOINTMENT, Total Participation of MEDICAL REPORT)

- Generates (1:1, APPOINTMENT to BILLING — Partial Participation of APPOINTMENT, Total Participation of BILLING)

---

## Extension (Prerequisite / Billing):

- Billing is modeled as a separate entity with a 1:1 relationship to Appointment using the Generates relationship. This ensures that every appointment produces exactly one billing record, which simplifies financial tracking, enables integration with insurance systems, and allows for easy auditing of patient transactions.
- Attributes like Amount, Payment Method, and Payment Status help maintain clear payment trails. This model supports future expansion such as:

  - Linking billing to insurance claims

  - Generating automated payment reminders

  - Adding multi-mode payment histories (cash, online, etc.)

---

## Design Choices:

- Entity Selection: Entities like PATIENT, DOCTOR, APPOINTMENT, BILLING, and MEDICAL REPORT were chosen based on essential components of a clinical/hospital management system.
- Normalization: Information is divided into logical, minimal redundancy tables — for example, separating BILLING and MEDICAL REPORT ensures both can grow independently.
  - Relationship Modeling:

- Books and Handles reflect real-world workflows: patients book appointments; doctors handle them.
- Generates and Produces maintain 1:1 integrity — one appointment equals one bill and one report.
  
  - Participation Constraints:
- Total participation from APPOINTMENT to BILLING and MEDICAL REPORT ensures data completeness.
- Scalability: The DEPARTMENT entity allows the hospital to scale across units like Cardiology, Neurology, etc., and organizes doctors efficiently.

  - Assumptions:
- A doctor belongs to only one department.
- A patient can have multiple appointments but one appointment belongs to one patient.

- Each appointment will always result in billing and a medical report.

---

## RESULT
Thhus, successfully understood and applied the concepts of ER modeling by creating an ER diagram for a real-world application.
