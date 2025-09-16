# Lab 13: Complete a SQL Join
### Overview

In this lab, I practiced performing SQL joins to combine information across multiple tables. Using INNER JOIN, LEFT JOIN, and RIGHT JOIN, I connected employee, machine, and login data to investigate a recent security incident.

This exercise provided practical experience in using joins to match related records, include unmatched data, and analyze login attempts across the organization.

### Scenario

As a security analyst, I needed to investigate a security incident that compromised some machines. The information was stored across three tables in the organization database:

1. employees – containing employee details
2. machines – containing device details
3. log_in_attempts – containing login activity

The tasks involved matching employees to their machines, retrieving all machines and employees (including unmatched records), and analyzing login attempts made by employees.

## Tasks and Commands
### Task 1: Match Employees to Their Machines
Select all machines:
```sql
SELECT * 
FROM machines;
```
Perform an INNER JOIN on device_id:
```sql
SELECT * 
FROM machines 
INNER JOIN employees 
ON machines.device_id = employees.device_id;
```
#### > Number of rows returned: 185

### Task 2: Return More Data
LEFT JOIN (all machines included):
```sql
SELECT * 
FROM machines 
LEFT JOIN employees 
ON machines.device_id = employees.device_id;
```
#### > Username in the last record: NULL
RIGHT JOIN (all employees included):
```sql
SELECT * 
FROM machines 
RIGHT JOIN employees 
ON machines.device_id = employees.device_id;
```
#### > Username in the last record: areyes
### Task 3: Retrieve Login Attempt Data

INNER JOIN employees and log_in_attempts on username:
```sql
SELECT * 
FROM employees 
INNER JOIN log_in_attempts 
ON employees.username = log_in_attempts.username;
```
#### > Number of rows returned: 200
### Key Learnings

1. Learned how to use INNER JOIN to match related records in two tables.

2. Applied LEFT JOIN to include all records from one table, even when no match exists.

3. Applied RIGHT JOIN to include all records from the other table, even when no match exists.

4. Practiced analyzing login activity by joining employees with login attempts.

5. Strengthened ability to retrieve precise, connected information across multiple tables.

### Conclusion

This lab improved my SQL skills by demonstrating how to use joins to combine and analyze data across different tables. As a security analyst, joins are essential for linking employee details, device information, and login activity to investigate incidents and uncover potential security risks.
