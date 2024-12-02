# Employee Management System

## Overview
This project demonstrates SQL techniques using an **Employee Management System**. It includes:
- Employee and department management.
- Salary updates and audit tracking.
- Complex queries like ranking and salary calculations.

---

## Features

1. **Table Design**:
   - `employees_3`: Employee details including `emp_name`, `department`, and `salary`.
   - `departments`: Department details.
   - `salary_audit`: Tracks salary changes with `old_salary` and `new_salary`.

2. **Key Queries**:
   - Retrieve all employees.
   - List employees with salary above a threshold.
   - Join tables to display employee and department names.
   - Advanced queries (ranking, averages, second-highest salary).

3. **Audit Log**:
   - Automatically logs salary changes for tracking updates.

---

## Table Schema

### `employees_3`
| Column    | Type       |
|-----------|------------|
| emp_id    | INT        |
| emp_name  | VARCHAR    |
| department| VARCHAR    |
| salary    | DECIMAL(10, 2) |

### `departments`
| Column    | Type       |
|-----------|------------|
| dept_id   | INT        |
| dept_name | VARCHAR    |

### `salary_audit`
| Column      | Type       |
|-------------|------------|
| emp_id      | INT        |
| old_salary  | DECIMAL(10, 2) |
| new_salary  | DECIMAL(10, 2) |
| audit_date  | DATE       |

---

### 1. Retrieve All Employees:
```sql
SELECT * FROM employees_3;

2. Find Employees with Salary Above 5000:
sql
SELECT emp_name, salary
FROM employees_3
WHERE salary > 5000;

3. List All Employees with Department Names:
SELECT e.emp_id, e.emp_name, d.dept_name
FROM employees_3 AS e
JOIN departments AS d
ON e.department_id = d.dept_id;

4.Find the Average Salary in Each Department:
SELECT d.dept_name, AVG(e.salary) AS average
FROM employees_3 AS e
JOIN departments AS d
ON e.department_id = d.dept_id
GROUP BY d.dept_name;

5. Top 3 Highest Paid Employees in Each Department:
WITH level AS (
    SELECT emp_name, department, salary,
           RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
    FROM employees_3
)
SELECT * 
FROM level
WHERE rank <= 3;

6. Update Salary and Audit the Changes:
Update Salary:
UPDATE salary_audit
SET new_salary = new_salary * 1.1
WHERE emp_id = 101;

Track the Change in Audit Table:
INSERT INTO salary_audit (emp_id, old_salary, new_salary, audit_date)
VALUES (106, 8000, 9000, '2023-11-23');





