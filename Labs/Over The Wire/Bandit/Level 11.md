# Bandit Level 10 → Level 11

**Date:** `2025-11-09`

**Start point:** `bandit10@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in the file `data.txt`, which contains base64 encoded data.

---

## Thought process / Plan

* The file is base64 encoded. Base64 is a common text encoding that represents binary data using ASCII characters. To get the hidden password you should decode the file using `base64 -d` (decode) or other tools that support base64 decoding.
* Plan:

  1. Confirm the file exists with `ls -la`.
  2. Use `base64 -d data.txt` to decode the contents and print the result to the terminal.
  3. Save the password privately and SSH into `bandit11`.

---

## Commands tried (with short notes)

```bash
# Confirm file exists and permissions
ls -la

# Decode base64 and print the decoded text
base64 -d data.txt

# Use the decoded password to login to next level
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

**Notes:**

* `base64 -d` decodes base64 input to the original bytes and prints them. If the decoded output is text, it will appear readable. If it’s binary, be careful not to corrupt the terminal.
* If `base64 -d` is not available, `openssl base64 -d -in data.txt` or `python -m base64 -d data.txt` are alternatives.

---

## Key outputs / Evidence

```
$ ls -la
-rw-r----- 1 bandit11 bandit10 69 Oct 14 09:25 data.txt

$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

---

## Final solution (private note)

* **Path to file:** `./data.txt`
* **Command used to read it:** `base64 -d data.txt`
* **Password / flag:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr` (REDACTED in public docs)
* **Next step:** SSH into `bandit11` using the found password

---

## What I learned

* Base64 is a reversible ASCII encoding useful for transporting binary data in text form.
* `base64 -d` decodes base64 and prints the result; other tools (openssl, python) can also decode.
* Always handle decoded output carefully — if it’s binary you may garble your terminal; use `strings` or redirect to a file first.

---

## Mistakes to avoid next time

* Running `cat` on a binary decoded output that can corrupt the terminal — use `strings` or redirect to file if unsure.
* Publishing actual passwords in public repositories.

---

## References / Further reading

* Base64 on Wikipedia
* `man base64`

---

## Git workflow notes

```
git add level10-11.md
git commit -m "docs: Bandit level10-11 decode base64 in data.txt to get password"
```
