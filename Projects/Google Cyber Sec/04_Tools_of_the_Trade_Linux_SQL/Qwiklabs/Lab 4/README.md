# Lab 4: Filter with grep

## Overview
In this lab, I used the **`grep`** command and **piping (`|`)** to search for specific strings in log files and filenames. These techniques are essential for quickly filtering and retrieving important information from large datasets in Linux.  

As a security analyst, being able to locate error messages, user data, and department records is critical for incident investigations and audits.

---

## Scenario
In this scenario, I needed to obtain information from **server logs** and **user data files**. The process involved:  

1. Searching for error messages in server logs.  
2. Finding files containing specific string patterns in their names.  
3. Searching within user files to identify added or deleted users.  

---

## Tasks and Commands

###  Task 1: Search for Error Messages in a Log File
```bash
# Navigate to logs directory
cd /home/analyst/logs

# Search for 'error' entries in server_logs.txt
grep "error" server_logs.txt
```
#### Expected findings:

Number of error lines: Six

###  Task 2: Find Files Containing Specific Strings
```bash

# Navigate to users reports directory
cd /home/analyst/reports/users

# List files containing 'Q1' in their names
ls | grep "Q1"

# List files containing 'access' in their names
ls | grep "access"
```
#### Expected findings:

Files containing "Q1": Three

Files containing "access": Three

###  Task 3: Search More File Contents
```bash
# Check for username 'jhill' in deleted users (Q2)
grep "jhill" Q2_deleted_users.txt

# Search for Human Resources users in Q4 added users
grep "Human Resources" Q4_added_users.txt
```
#### Expected findings:

Username jhill found in Q2_deleted_users.txt: Yes

Users added to Human Resources in Q4: Two

### Key Learnings
1. grep is a powerful tool for searching file contents based on specific strings.

2. Piping (|) allows chaining commands together for efficient searching.

3. File analysis with grep helps in identifying important user and log data.

4. Quotation marks (" ") are required when searching for multi-word strings.

### Conclusion
This lab reinforced the importance of filtering and searching techniques in Linux. As a security analyst, I can now:

1. Quickly search for error messages in server logs.

2. Identify files with specific patterns in their names.

3. Extract important user-related information from text files.

These skills are fundamental for effective log analysis and incident response.
