# Bandit Level 3 → Level 4

**Date:** `2025-11-09`

**Start point:** `bandit3@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in a hidden file in the `inhere` directory.

---

## Thought process / Plan

* The hint says the password is in a **hidden file** (starts with a dot) inside the `inhere` directory. Hidden files are not shown by `ls` unless you use `-a` or `-la`.
* Plan:

  1. List files with `ls -la` to reveal hidden files.
  2. `cd` into `inhere` and list files there with `ls -la`.
  3. Identify the hidden file (it will start with a dot) and read it with `cat`, taking care to reference the exact filename.

---

## Commands tried (with short notes)

```bash
# Confirm location and list hidden files
pwd
ls -la

# Enter the specified directory and list hidden files there
cd inhere
ls -la

# Read the hidden file safely
cat ./...Hiding-From-You
```

Notes:

* `ls -la` was used to reveal files that begin with a dot (hidden files).
* The filename in this level begins with a dot and contains multiple leading dots; referencing it with `./` avoids option parsing or ambiguity.

---

## Key outputs / Evidence

```
$ ls -la
total 24
drwxr-xr-x   3 root root 4096 Oct 14 09:26 .
drwxr-xr-x 150 root root 4096 Oct 14 09:29 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Oct 14 09:19 .bashrc
drwxr-xr-x   2 root root 4096 Oct 14 09:26 inhere
-rw-r--r--   1 root root  807 Mar 31  2024 .profile

$ cd inhere
$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 14 09:26 ...Hiding-From-You

$ cat ./...Hiding-From-You
[REDACTED_PASSWORD_FOR_PUBLIC]
```


---

## Final solution (private note)

* **Path to file:** `inhere/...Hiding-From-You` (hidden file in the `inhere` directory)
* **Command used to read it:** `cat ./...Hiding-From-You`
* **Password / flag:** `REDACTED_FOR_PUBLIC` (store the real password locally)
* **Next step:** SSH into `bandit4` using the found password

---

## What I learned

* Hidden files start with a dot and require `ls -a` or `ls -la` to see.
* Filenames can have multiple leading dots; referencing them with `./` is safe and unambiguous.
* Always keep passwords private and don’t commit them to public repositories.

---

## Mistakes to avoid next time

* Forgetting to use `-a` with `ls` and missing hidden files.
* Publishing real passwords by accident. Keep them in a private vault or local note file.

---

## References / Further reading

* `man ls` for listing hidden files
* Bandit Level documentation

---

## Git workflow notes

```
git add level03-04.md
git commit -m "docs: Bandit level03-04 hidden file in inhere; notes and safe handling"
```
