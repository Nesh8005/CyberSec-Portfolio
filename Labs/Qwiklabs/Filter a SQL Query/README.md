# Lab 10: Filter a SQL Query
### Overview

In this lab, I learned how to filter SQL queries to retrieve more specific data from a database. Using the WHERE and LIKE clauses, I practiced narrowing down results to find machines, employees, and departments that matched certain conditions.

This exercise provided hands-on practice with filtering queries in MariaDB, an open-source database compatible with MySQL.

#### Scenario

As a security analyst, I needed to quickly retrieve specific information about employee machines, departments, and office locations. My team required this data to perform updates, post privacy notices in certain departments, and notify employees about machine issues.

The lab involved working with two tables in the organization database:

machines – containing employee device details

employees – containing employee and office information

Tasks and Commands

### Task 1: List All Organization Machines
Retrieve all device IDs and their operating systems:
```sql
SELECT device_id, operating_system
FROM machines;
```

#### Rows returned: 200

### Task 2: Retrieve a List of Machines with OS 2
#### Filter machines that use OS 2:
```sql
SELECT device_id, operating_system
FROM machines
WHERE operating_system = 'OS 2';
```

#### Machines using OS 2: 80

### Task 3: List Employees in Specific Departments

#### Employees in Finance:
```sql
SELECT * 
FROM employees
WHERE department = 'Finance';
```

#### First row employee_id: 1003

### Employees in Sales:
```sql
SELECT * 
FROM employees
WHERE department = 'Sales';
```

#### Employees in Sales: 33

### Task 4: Identify Employee Machines

#### Find employee in office South-109:
```sql
SELECT * 
FROM employees
WHERE office = 'South-109';
```

#### Employee: jlansky

#### Find all employees in the South building:
```sql
SELECT * 
FROM employees
WHERE office LIKE 'South-%';
```

#### First employee’s department: Finance

### Key Learnings

1. Learned to apply filters using the WHERE clause.

2. Used equality checks (=) to return specific values.

3. Practiced pattern matching with the LIKE operator and % wildcard.

4. Retrieved both device and employee information efficiently.

### Conclusion

This lab reinforced the importance of filtering queries to extract only the relevant data from large datasets. As a security analyst, being able to pinpoint specific machines, departments, or employees helps streamline system updates, identify security risks, and send targeted alerts quickly.
