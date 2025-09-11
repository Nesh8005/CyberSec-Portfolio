# Lab 9: Perform a SQL Query
### Overview

In this lab, I practiced writing basic SQL queries to retrieve and sort information from a database. Using the SELECT, FROM, and ORDER BY keywords, I queried tables to investigate employee device data and login activity.

This exercise provided hands-on experience with database queries, focusing on column selection, retrieving all records, and organizing results through sorting.

### Scenario

As a security analyst, I needed to determine which employee devices required updates and investigate login attempts for signs of unusual activity. The information was stored in two tables within the organization database:

#### 1. machines – containing employee device details

#### 2. log_in_attempts – containing login records

The tasks involved retrieving device details, analyzing login activity by location and time, and ordering login attempts by date and time.

## Tasks and Commands

### Task 1: Retrieve Employee Device Data

#### Select all devices:
```sql
SELECT * 
FROM machines;
```

#### Select only device_id and email_client:
```sql
SELECT device_id, email_client 
FROM machines;
```

#### > Third row result: Email Client 2

#### Select device_id, operating_system, and OS_patch_date:
```sql
SELECT device_id, operating_system, OS_patch_date
FROM machines;
```

#### > First entry patch date: 2021-09-01

### Task 2: Investigate Login Activity

#### Check login countries:
```sql
SELECT event_id, country
FROM log_in_attempts;
```

#### > Login attempts from Australia: Yes

#### Check login times:
```sql
SELECT username, login_date, login_time
FROM log_in_attempts;
```

#### > Fifth row username: jrafael

#### Select all login attempt details:
```sql
SELECT * 
FROM log_in_attempts;
```

### Task 3: Order Login Attempts Data

#### Sort by date:
```sql
SELECT * 
FROM log_in_attempts
ORDER BY login_date;
```

#### > First record: ivelasco on 2022-05-08

#### Sort by date and time:
```sql
SELECT * 
FROM log_in_attempts
ORDER BY login_date, login_time;
```

####  > First record: wjaffrey at 00:15:55

### Key Learnings

1. Learned how to query specific columns with SELECT.

2. Used * to retrieve all columns from a table.

3. Applied ORDER BY to sort data by date and time.

4. Gained practical experience investigating database records for anomalies.

### Conclusion

This lab strengthened my SQL skills by showing how to query and organize data efficiently. As a security analyst, the ability to retrieve device details and analyze login activity helps identify outdated systems and detect unusual login behavior—both essential for maintaining strong security practices.
