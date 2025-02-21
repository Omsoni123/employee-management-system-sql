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






