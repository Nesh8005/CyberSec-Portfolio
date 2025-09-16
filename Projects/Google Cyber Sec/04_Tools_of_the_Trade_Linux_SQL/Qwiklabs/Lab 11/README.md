# Lab 11: Apply More Filters in SQL
### Overview

In this lab, I learned how to apply numeric and date filters in SQL to investigate login attempts in an organization’s database. Using operators such as >, <, >=, <=, and BETWEEN … AND, I practiced retrieving login data by date, time, and event IDs.

This exercise provided hands-on practice with filtering queries in MariaDB, which is compatible with MySQL.

### Scenario

As a security analyst, I needed to investigate login activity related to a recent incident. My task was to retrieve login attempts after certain dates, within specific ranges, during unusual times, and based on event IDs. This information helps identify suspicious behavior and narrow down potential threats.

The lab involved working with the following table in the organization database:

log_in_attempts – containing event IDs, usernames, login dates, and login times

## Tasks and Commands

### Task 1: Retrieve Login Attempts After a Certain Date
Find logins after 2022-05-09:
```sql
SELECT * 
FROM log_in_attempts 
WHERE login_date > '2022-05-09';
```

#### Login attempts after 2022-05-09: 111

#### Include 2022-05-09 in the search:
```sql
SELECT * 
FROM log_in_attempts 
WHERE login_date >= '2022-05-09';
```

#### Login attempts on or after 2022-05-09: 186

### Task 2: Retrieve Logins in a Date Range
Find logins between 2022-05-09 and 2022-05-11:
```sql
SELECT * 
FROM log_in_attempts 
WHERE login_date BETWEEN '2022-05-09' AND '2022-05-11';
```

#### Login attempts in range: 157

### Task 3: Investigate Logins at Certain Times
Logins before 07:00:00:
```sql
SELECT * 
FROM log_in_attempts 
WHERE login_time < '07:00:00';
```

#### Username of 5th record: eraab

Refined to logins between 06:00:00 and 07:00:00:
```sql
SELECT * 
FROM log_in_attempts 
WHERE login_time BETWEEN '06:00:00' AND '07:00:00';
```

#### Earliest login attempt: 06:01:31

### Task 4: Investigate Logins by Event ID
Event IDs greater than or equal to 100:
```sql
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id >= 100;
```

#### Login date of 3rd record: 2022-05-09

Event IDs between 100 and 150:
```sql
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id BETWEEN 100 AND 150;
```

#### Username of 7th record: mabadi

### Key Learnings

1. Applied comparison operators (>, <, >=, <=) to filter by dates and numbers.

2. Used BETWEEN … AND to capture records within a specific range.

3. Practiced filtering by time values to detect logins outside working hours.

4. Retrieved only relevant fields (event ID, username, login date) to narrow down investigation results.

### Conclusion

This lab reinforced the importance of precise filtering when investigating security incidents. By learning how to filter by dates, times, and numeric ranges, I gained practical skills to quickly identify unusual login activity and focus on potential threats. These filtering techniques are essential for security analysts who must sift through large datasets to find critical information.
