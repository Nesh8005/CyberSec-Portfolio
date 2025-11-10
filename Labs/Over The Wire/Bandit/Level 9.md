# Bandit Level 8 → Level 9

**Date:** `2025-11-09`

**Start point:** `bandit8@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in the file `data.txt` and is the only line of text that occurs only once.

---

## Thought process / Plan

* We need to find the unique line in a large file — the single line that appears exactly once while all other lines appear multiple times.
* `uniq -u` prints lines that occur only once, but it works correctly only on adjacent identical lines. Therefore we **sort** the file first so identical lines become adjacent, then use `uniq -u` to find the unique line.

**Plan:**

1. Use `sort` to group identical lines.
2. Pipe into `uniq -u` to print lines that occur only once.
3. The output is the password. Save it privately and use it to SSH into the next level.

---

## Commands tried (with short notes)

```bash
# Sort the file then print lines that occur only once
sort data.txt | uniq -u

# If you prefer to save the result first
sort data.txt | uniq -u > unique_line.txt
cat unique_line.txt

# Use the password to login to next level
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

**Notes:**

* `uniq -u` prints only unique lines, but it requires duplicates to be adjacent. `sort` guarantees adjacency.
* Piping avoids creating large intermediate files on disk.

---

## Key outputs / Evidence

```
$ sort data.txt | uniq -u
[REDACTED_PASSWORD_FOR_PUBLIC]
```

> Note: The output above is the password found during the session. When adding this to a public repository, replace the password with `REDACTED_FOR_PUBLIC` and store the real password in a private secure note.

---

## Final solution (private note)

* **Path to file:** `./data.txt`
* **Command used to read it:** `sort data.txt | uniq -u`
* **Password / flag:** `REDACTED_FOR_PUBLIC` 
* **Next step:** SSH into `bandit9` using the found password

---

## What I learned

* `uniq -u` prints only unique lines when duplicates are adjacent; use `sort` first to group duplicates.
* Piping (`|`) allows text processing without creating temporary files.
* Always save passwords privately and redact them in public documentation.

---

## Mistakes to avoid next time

* Running `uniq -u data.txt` without sorting — it misses non-adjacent duplicates.
* Publishing real passwords in public repos.

---

## References / Further reading

* `man sort`, `man uniq`
* Tutorials on Unix text processing and piping

---

## Git workflow notes

```
git add level08-09.md
git commit -m "docs: Bandit level08-09 find unique line with sort and uniq"
```
