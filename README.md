
# 🧪 Research Projects Database - NIAT

This project presents a **Relational Database Design** for managing research projects, employees, and funding agencies using **SQL**.

## 📌 Overview

The system keeps track of:
- **Research Projects**: Each has a name, duration, budget, and is funded by one funding agency.
- **Employees**: Each has an SSN, name, and salary. Employees can work on multiple projects and can also be project managers.
- **Funding Agencies**: Each agency has a unique name and address, and funds one or more projects.

## 🧩 Entity-Relationship (ER) Design Highlights

- **Each project** is funded by **a single funding agency**.
- **Employees** can be assigned to **multiple projects** (many-to-many relationship).
- A **project manager** is an employee who is responsible for one or more projects.
- **Project names** are unique within a given agency (assumption for uniqueness scope).
- **Employee-Project** relation captures which employee works on which project, along with the associated project manager.

## 🛠️ Tables Created

1. `Employee` – Stores employee details.
2. `FundingAgency` – Stores information about the agency funding the research.
3. `Project` – Stores project metadata (linked to agency).
4. `Project_Manager` – Maps a project to its manager (manager is an employee).
5. `Employee_Project` – Tracks which employees are working on which projects and under which manager.

<img width="626" alt="Screenshot 2025-06-13 at 3 06 42 PM" src="https://github.com/user-attachments/assets/c340d1d1-907b-46d7-92c2-985ece4c0981" />
![WhatsApp Image 2025-06-13 at 14 39 09](https://github.com/user-attachments/assets/458556b7-e5fd-427b-910b-f0540832eb0f)





## 🧾 Sample SQL Table Creation

```sql
CREATE TABLE Employee (
    SSN INT PRIMARY KEY,
    Emp_Name VARCHAR(50),
    Salary DECIMAL
);

CREATE TABLE FundingAgency (
    Agency_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Address VARCHAR(255)
);

CREATE TABLE Project (
    Project_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Duration INT,      -- e.g. months
    Budget DECIMAL(12,2)
);

CREATE TABLE Project_Manager (
    Project_ID INT PRIMARY KEY,
    Manager_SSN INT,
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
    FOREIGN KEY (Manager_SSN) REFERENCES Employee(SSN)
);

CREATE TABLE Employee_Project (
    SSN INT,
    Project_ID INT,
    Manager_SSN INT,
    PRIMARY KEY (SSN, Project_ID),
    FOREIGN KEY (SSN) REFERENCES Employee(SSN),
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
    FOREIGN KEY (Manager_SSN) REFERENCES Employee(SSN)
);
