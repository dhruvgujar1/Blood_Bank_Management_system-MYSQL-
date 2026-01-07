# Blood_Bank_Management_system-MYSQL-
🩸 Blood Bank Management System – SQL Data Analysis Project
📌 Project Overview

This project focuses on analyzing a Blood Bank Management System using SQL to gain insights into blood availability, hospital demand, donor behavior, and inventory status. The objective is to identify shortages, operational risks, and inefficiencies in blood bank operations and provide data-driven recommendations to improve decision-making.

🎯 Objectives

Analyze blood availability across different blood groups

Identify high-demand blood groups and hospitals

Detect shortages, especially for rare blood groups

Evaluate inventory status including expired and contaminated blood

Assess donor contribution and donation patterns

Support operational improvements using SQL-based insights

🗂️ Dataset Description

The project uses a relational database consisting of the following tables:

donors – Donor details including blood group and medical conditions

donations – Records of blood donations and quality test status

inventory – Current status of blood units (Available, Issued, Expired, Quarantined)

hospitals – Hospital details requesting blood

recipients – Patient/recipient information linked to hospitals

requests – Blood requests raised by hospitals

🧩 Database Design

The database follows a relational design with proper foreign key relationships to maintain data integrity.
An ER Diagram was created using MySQL Workbench to visualize table relationships and dependencies.

🔍 Key Business Questions Addressed

Is sufficient blood available for each blood group?

Which blood groups are most frequently requested by hospitals?

Are rare blood groups donated less frequently than common groups?

Which hospitals face the highest demand and shortages?

Are hospitals requesting blood that is currently unavailable?

What percentage of blood units expire or fail quality tests?

What are the major risks to blood availability in the system?

🛠️ SQL Techniques Used

INNER JOIN and LEFT JOIN

GROUP BY and HAVING clauses

Aggregate functions (COUNT, SUM, AVG)

CASE statements for classification

Subqueries

Date and time functions

📊 Key Insights

Rare blood groups such as A2, A2B, and hh are donated significantly less frequently.

Some hospitals consistently experience unmet demand due to limited inventory.

A portion of blood inventory is lost due to expiry and quality test failures.

Blood donation and demand show seasonal variations, leading to supply-demand imbalance.

⚠️ Risks Identified

Shortage of rare blood groups

Blood wastage due to expiry

Dependence on a limited number of frequent donors

Unfulfilled hospital requests

Quality-related rejection of donated blood

✅ Recommendations

Conduct targeted donor drives for rare blood groups

Improve inventory rotation using FEFO (First Expiry First Out)

Monitor demand vs availability in real time

Expand the donor base to reduce dependency on frequent donors

Plan donation drives based on seasonal demand patterns

🧠 Conclusion

This project demonstrates the practical use of SQL in healthcare data analysis. By transforming raw blood bank data into actionable insights, the analysis supports improved blood availability, reduced wastage, and more efficient blood bank operations.

🧑‍💻 Tools & Technologies

MySQL

MySQL Workbench

SQL

📌 Author

Dhruv Gujar
Aspiring Data Analyst
🔗 LinkedIn: https://www.linkedin.com/in/dhruv-gujar-data-analyst/
