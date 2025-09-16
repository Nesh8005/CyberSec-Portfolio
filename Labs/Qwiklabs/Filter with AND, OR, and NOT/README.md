# Lab 12: Filter with AND, OR, and NOT
### Overview

In this lab, I learned how to apply AND, OR, and NOT operators in SQL to create more complex filters when querying databases. These operators allowed me to refine results by combining multiple conditions or excluding specific values.

This exercise provided practical experience with MariaDB, focusing on login investigations and employee data retrieval.

### Scenario

As a security analyst, I needed to extract specific login and employee records from the organization’s database to support security investigations and system updates.

The tasks included retrieving failed logins outside business hours, logins from specific dates, attempts outside Mexico, and employee information based on department and office location.

The lab used two tables in the organization database:

log_in_attempts – containing login activity records

employees – containing employee department and office details

## Tasks and Commands

### Task 1: Retrieve After-Hours Failed Login Attempts
Failed logins after 18:00:
```sql
SELECT * 
FROM log_in_attempts
WHERE login_time > '18:00' AND success = 0;
```

#### Failed login attempts after hours: 19

### Task 2: Retrieve Login Attempts on Specific Dates
Logins on 2022-05-08 or 2022-05-09:
```sql
SELECT * 
FROM log_in_attempts
WHERE login_date = '2022-05-08' OR login_date = '2022-05-09';
```

#### Login attempts on those dates: 75

### Task 3: Retrieve Login Attempts Outside of Mexico
Exclude attempts from Mexico (MEX or MEXICO):
```sql
SELECT * 
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

#### Login attempts outside Mexico: 144

### Task 4: Retrieve Employees in Marketing
Employees in Marketing located in the East building:
```sql
SELECT * 
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East-%';

```
#### First Marketing employee in East: elarson

### Task 5: Retrieve Employees in Finance or Sales
Employees in Finance or Sales:
```sql
SELECT * 
FROM employees
WHERE department = 'Finance' OR department = 'Sales';
```

#### First Sales employee returned: sgilmore

### Task 6: Retrieve All Employees Not in IT
Employees not in Information Technology:
```sql
SELECT * 
FROM employees
WHERE NOT department = 'Information Technology';
```

#### Employees not in IT: 170

### Key Learnings

1. Practiced using AND to enforce multiple conditions in a query.

2. Applied OR to capture records that matched at least one condition.

3. Used NOT with patterns and specific values to exclude unwanted data.

4. Retrieved both login activity and employee details based on complex filters.

### Conclusion

This lab demonstrated the power of AND, OR, and NOT operators in refining SQL queries. By combining and negating conditions, I could extract highly specific datasets to support both security monitoring and administrative updates. These techniques are crucial for analysts working with large databases to quickly isolate the exact information needed.
