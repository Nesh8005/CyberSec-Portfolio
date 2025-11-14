# Bandit Level 0 → Level 1

**Date:** `2025-11-09`

**Start point:** `bandit0@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in a file called `readme` located in the home directory. Use this password to log into `bandit1` using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

**Tip:** Create a file for notes and passwords on your local machine. Passwords are not saved automatically, and sometimes change, so taking notes is essential for reference.

---

## Thought process / Plan

* We need to find a file called `readme` in the home directory.
* Once found, the file contains the password for the next level (`bandit1`).
* Plan of attack:

  1. Check the home directory using `ls` to see files.
  2. Confirm the `readme` file exists.
  3. Use `cat` to read its contents.
  4. Copy the password and SSH into the next level using the same host and port.

---

## Commands tried (with short notes)

```bash
# List all files in home directory
ts
ls -la

# Check contents of readme
cat readme

# Log in to next level using password from readme
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

* `ls -la` shows all files, including hidden ones, with permissions and sizes.
* `cat readme` prints the password to the terminal.
* SSH command connects to the next level using the password retrieved.

---

## Key outputs / Evidence

```
$ ls -la
-rw-r--r-- 1 bandit0 bandit0 33 Nov  9 12:00 readme

$ cat readme
[password-for-bandit1]

$ ssh bandit1@bandit.labs.overthewire.org -p 2220
Password:
Welcome to OverTheWire: Bandit
bandit1@bandit:~$
```

---

## Final solution (private note)

* **Path to file:** `~/readme`
* **Command used to read it:** `cat ~/readme`
* **Password / flag:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
* **Next step:** Logged in as `bandit1`, ready for Level 1 instructions.

---

## What I learned

* How to inspect files in the home directory using `ls`.
* How to read files safely using `cat`.
* Using retrieved passwords to log into the next level via SSH.
* Importance of keeping local notes for passwords.

---

## Mistakes to avoid next time

* Forgetting to check file permissions (`ls -la`) if `readme` doesn’t show up.
* Copying passwords incorrectly (watch for trailing spaces or newlines).
* Not noting the password locally; it may change later.

---

## References / Further reading

* [OverTheWire Bandit Level 1 Instructions](https://overthewire.org/wargames/bandit/bandit1.html)
* `man ls` for listing files and permissions
* `man cat` for viewing file contents

---

## Git workflow notes

```
git add level01-02.md
git commit -m "docs: Bandit level01-02 find readme and SSH login notes"
```
