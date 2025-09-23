# Lab 3: Find Files with Linux Commands

## Overview
In this lab, I practiced **navigating directories, locating files, and reading file contents** in the Linux Bash shell using commands such as `pwd`, `ls`, `cd`, `cat`, and `head`.  

These are essential skills for a security analyst when investigating logs, reading reports, or analyzing user data without a graphical interface.

---

## Scenario
As a **security analyst**, I needed to locate and analyze files stored under `/home/analyst`.  

The tasks involved:  
1. Checking the current directory and listing its contents.  
2. Navigating to a reports directory and identifying subdirectories.  
3. Reading a user report file to extract employee details.  
4. Navigating to a logs directory and reviewing server logs.  

---

## Tasks and Commands

### Task 1: Get the Current Directory Information
```bash
# Display current working directory
pwd

# List files and directories in the current location
ls
```
#### Expected output:

#### Current directory: /home/analyst

#### Number of directories: Four

### Task 2: Change Directory and List Subdirectories
```bash
# Navigate to reports directory
cd /home/analyst/reports

# List contents
ls
```
#### Expected output:

#### Subdirectory in /home/analyst/reports: users

#### Task 3: Locate and Read the Contents of a File
```bash
# Navigate to users subdirectory
cd /home/analyst/reports/users

# List files
ls

# Display file contents
cat Q1_added_users.txt
```
#### Expected findings:

#### Employee aezra works in: Finance

#### Employee ID of mreed (Information Technology department): 1177


### Task 4: Navigate to a Directory and Locate a File
```bash
# Navigate to logs directory
cd /home/analyst/logs

# Display file name
ls

# Display first 10 lines of the log file
head server_logs.txt
```

#### Expected result:

#### File: server_logs.txt

#### Number of warning messages in first 10 lines: Three

### Key Learnings

1. Used pwd to confirm the current working directory.

2. Applied ls to list files and directories.

3. Navigated directories with cd.

4. Displayed full file contents using cat.

5. Previewed the first 10 lines of a log file with head.

6. Practiced analyzing reports and logs to extract useful details.

### Conclusion

This lab provided practical experience in file navigation and content analysis using Linux commands.

#### As a security analyst, these skills are fundamental for:

1. Investigating unauthorized access.

2. Reviewing user activity reports.

3. Analyzing server logs for warnings or anomalies.
