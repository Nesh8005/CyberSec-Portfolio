# Lab 6: Manage Authorization
### Overview

In this lab, I worked with Linux file and directory permissions to configure proper authorization. Using the ls -l and chmod commands, I examined existing permissions, identified misconfigurations, and corrected them to prevent unauthorized access.

This exercise provided hands-on experience in controlling access rights for files and directories, which is critical for protecting sensitive data and maintaining system security.

### Scenario

As a security analyst, I was tasked with managing permissions for the /home/researcher2/projects directory.

The researcher2 user belongs to the research_team group. My responsibility was to:

1. Check permissions for files (including hidden ones).

2. Remove unnecessary write and read permissions.

3. Restrict access to sensitive files and directories.

## Tasks and Commands

### Task 1: Check file and directory details
```bash
cd /home/researcher2/projects
ls -la
```

#### Observed permissions:
```diff
drwx--x--- drafts
-rw-rw-rw- project_k.txt
-rw-r----- project_m.txt
-rw-rw-r-- project_r.txt
-rw-rw-r-- project_t.txt
.project_x.txt
```

#### Group ownership: research_team

#### Hidden file found: .project_x.txt

### Task 2: Change file permissions

##### Identified that project_k.txt incorrectly allowed others to write.
```bash
chmod o-w project_k.txt
```

##### Verified that project_m.txt should only be accessible by the user.
```bash
chmod g-rw project_m.txt
chmod o-rw project_m.txt
```

### Task 3: Change permissions on a hidden file

#### .project_x.txt had incorrect write permissions for user and group.

#### Adjusted so both user and group can read-only:
```bash
chmod ug-w .project_x.txt
```

### Task 4: Change directory permissions

#### Checked drafts directory:
```bash
ls -ld drafts
```

#### Found group had execute access. Removed it so only researcher2 can access:
```bash
chmod g-x drafts
```
### Key Learnings

1. Learned to interpret file and directory permissions with ls -l.

2. Practiced adjusting user (u), group (g), and others (o) permissions using chmod.

3. Reinforced importance of restricting hidden files and sensitive directories.

4. Understood how improper permissions can expose systems to unauthorized access.

### Conclusion

This lab demonstrated how to manage Linux authorization through file and directory permissions. As a security analyst, these skills are essential for ensuring that only authorized users and groups can access sensitive files, thereby reducing security risks.
