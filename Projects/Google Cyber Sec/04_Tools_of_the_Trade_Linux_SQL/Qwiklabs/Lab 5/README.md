# Lab 5: Manage Files with Linux Commands
### Overview

In this lab, I used core Linux Bash commands to create, remove, move, and edit directories and files. I also practiced using the nano text editor to add documentation to a file.

This exercise provided hands-on practice with file and directory management in a Linux environment, which is an essential skill for keeping systems organized and ensuring data is maintained properly.

### Scenario

As a security analyst, I was tasked with restructuring the /home/analyst directory to make it better organized. This involved:

1. Creating a new subdirectory for logs.

2. Removing outdated files and directories.

3. Moving reports into their correct location.

4. Creating and editing a task log to document changes.

## Tasks and Commands

###  Task 1: Create a new directory
```bash
cd /home/analyst
mkdir logs
ls
```

#### Expected output:
logs notes reports temp

### Task 2: Remove a directory
```bash
rmdir temp
ls
```

#### Expected output:
logs notes reports

### Task 3: Move a file
```bash
cd /home/analyst/notes
mv Q3patches.txt ../reports/
ls ../reports
```

#### Expected output:
Q1patches.txt Q2patches.txt Q3patches.txt

### Task 4: Remove a file
```bash
rm tempnotes.txt
ls
```

#### Expected output:
No files should remain in the notes directory.

### Task 5: Create a new file
```bash 
touch tasks.txt
ls
```

#### Expected output:
tasks.txt

### Task 6: Edit a file
```bash
nano tasks.txt
```

#### Inside nano, entered:
```arduino
Completed tasks
1. Managed file structure in /home/analyst
```

#### Then saved with CTRL+X → Y → ENTER.

To verify:
```bash
cat tasks.txt
```

#### Expected output:
```arduino
Completed tasks
1. Managed file structure in /home/analyst
```

### Key Learnings

1. Practiced creating and removing directories with mkdir and rmdir.

2. Moved and deleted files using mv and rm.

3. Learned to create new files with touch.

4. Used the nano text editor to document completed tasks.

5. Reinforced the importance of maintaining organized directories for system management and auditing.

### Conclusion

This lab demonstrated how to manage files and directories effectively in Linux. As a security analyst, these skills are critical for maintaining well-structured file systems, documenting changes, and ensuring data is easy to locate and review during security operations.
