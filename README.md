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

## code
```sql
SELECT * FROM employees_3;

![image](https://github.com/user-attachments/assets/ce5f2981-4d90-4844-a86c-34163648e4f9)


2. Find Employees with Salary Above 5000:
sql
SELECT emp_name, salary
FROM employees_3
WHERE salary > 5000;



![image](https://github.com/user-attachments/assets/4812ff41-a54e-4fd8-bcb6-caba3bab6815)


3. List All Employees with Department Names:
select e.id,e.name,d.dept_name
from employees as e
join departments as d
on e.department_id = d.dept_id;


![image](https://github.com/user-attachments/assets/d0723bce-73be-49da-a611-245d78112ab0)


4.Find the Average Salary in Each Department:
SELECT d.dept_name, AVG(e.salary) AS average
FROM employees_3 AS e
JOIN departments AS d
ON e.department_id = d.dept_id
GROUP BY d.dept_name;



![image](https://github.com/user-attachments/assets/652b9d6c-c673-49bb-8f47-0911d0c0d23f)


5. Top 3 Highest Paid Employees in Each Department:
 select * from employees_3;
 
 with level as (select emp_name,department,salary,
       rank() over ( partition by department order by salary) as 'ranks'
from employees_3
)
select * 
from level
where ranks = 1;


![image](https://github.com/user-attachments/assets/c45394bc-c654-4eaa-abd4-d5bbc17885b6)



6. Update Salary and Audit the Changes:
Update Salary:
# need to unable the safe mode

SET SQL_SAFE_UPDATES = 0;

# update salary 
select * from salary_audit;
update salary_audit
set new_salary = new_salary * 1.1
where emp_id = 101;

Track the Change in Audit Table:
insert into salary_audit(emp_id,old_salary,new_salary,audit_date)
values
(106,8000,9000,'2023-11-23');

6. Find the Second Highest Salary:
 select * from employees_3;
 
 with level as (select emp_name,department,salary,
       rank() over ( partition by department order by salary) as 'ranks'
from employees_3
)
select * 
from level
where ranks = 2;


![image](https://github.com/user-attachments/assets/e1ae6f9e-0a98-478f-87c9-a8324790df32)




