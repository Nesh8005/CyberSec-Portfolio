# Lab 7: Add and Manage Users with Linux Commands
### Overview

In this lab, I practiced Linux user management using commands such as useradd, usermod, chown, userdel, and groupdel. These commands allowed me to create users, assign them to groups, grant file ownership, and remove users when they leave the organization.

This exercise strengthened my understanding of authentication and access management in Linux, ensuring that only authorized users can access specific resources.

### Scenario

A new employee, researcher9, joined the organization and needed access to project files and groups. My role was to:

1. Add researcher9 as a system user and assign them to the research_team group.

2. Transfer ownership of a project file to researcher9.

3. Add researcher9 to an additional group when their role expanded.

4. Delete researcher9 from the system when they left the company.

## Tasks and Commands

### Task 1: Add a New User

#### Added the user researcher9:
```bash
sudo useradd researcher9
```

#### Assigned them to the research_team group as their primary group:
```bash
sudo usermod -g research_team researcher9
```

### Task 2: Assign File Ownership

#### Transferred ownership of project_r.txt to researcher9:
```bash
sudo chown researcher9 /home/researcher2/projects/project_r.txt
```

### Task 3: Add the User to a Secondary Group

#### Expanded researcher9’s role by adding them to the sales_team group (while keeping their primary group as research_team):
```bash
sudo usermod -a -G sales_team researcher9
```

### Task 4: Delete a User

#### When researcher9 left the organization, removed them from the system:
```bash
sudo userdel researcher9
```

#### Cleaned up the automatically created group with the same name:
```bash
sudo groupdel researcher9
```
### Key Learnings

1. Gained hands-on experience creating and deleting Linux users.

2. Learned how to assign primary and secondary groups using usermod.

3. Practiced transferring file ownership with chown.

4. Reinforced good practice of removing unused groups when deleting users.

5. Understood how authentication and user lifecycle management contribute to secure system administration.

### Conclusion

This lab demonstrated how to effectively add, manage, and remove Linux users while controlling their access through groups and file ownership. As a security analyst, these skills are vital for maintaining proper authentication and ensuring users only have access to the resources they require during their time in the organization.
