
# Bandit Level 7 → Level 8

**Date:** `2025-11-09`

**Start point:** `bandit7@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in the file `data.txt` next to the word **millionth**.

---

## Thought process / Plan

* The hint tells us the password is in `data.txt` and appears **next to** the word `millionth`. That means we don’t need to scan the whole filesystem — just inspect `data.txt`.
* Plan:

  1. Confirm `data.txt` exists with `ls -la`.
  2. Search the file for the word `millionth` using `grep` to find the matching line(s).
  3. Read the matching line and pick the token next to `millionth` — that token is the password.
  4. Save the password privately and SSH into `bandit8`.

---

## Commands tried (with short notes)

```bash
# Confirm the file exists
ls -la

# Search for the word 'millionth' in data.txt and show the matching line
grep millionth data.txt

# Optionally inspect the file around the match for context
# (useful if grep prints multiple matches or long context is needed)
# sed -n '1,200p' data.txt | grep -n "millionth"

# Use the found token to login to the next level
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

**Notes:**

* `grep` prints the whole line containing the match; the password is the next non-space token after `millionth` on that line.
* `data.txt` in this level is large, but `grep` is fast and reads only what’s needed.

---

## Key outputs / Evidence

```
$ ls -la
total 4108
-rw-r----- 1 bandit8 bandit7 4184396 Oct 14 09:26 data.txt

$ grep millionth data.txt
[REDACTED_PASSWORD_FOR_PUBLIC]
```

---

## Final solution (private note)

* **Path to file:** `./data.txt` (in home directory)
* **Command used to read it:** `grep millionth data.txt` (or `cat data.txt | grep millionth`)
* **Password / flag:** `[REDACTED_PASSWORD_FOR_PUBLIC]
* **Next step:** SSH into `bandit8` using the found password

---

## What I learned

* `grep` is a fast way to locate specific words in very large files without opening them entirely.
* Read the matching line to extract the token next to the keyword.
* Always save passwords in a private location and never commit them to public repos.

---

## Mistakes to avoid next time

* Assuming the password is the entire line instead of the token next to the keyword.
* Forgetting to check for multiple matches; always verify which match is intended.

---

## References / Further reading

* `man grep`
* OverTheWire Bandit Level 8 instructions

---

## Git workflow notes

```
git add level07-08.md
git commit -m "docs: Bandit level07-08 grep extraction of token next to keyword"
```
