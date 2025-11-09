# Bandit Level 6 → Level 7

**Date:** `2025-11-09`

**Start point:** `bandit6@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored somewhere on the server and has all of the following properties:
>
> * owned by user `bandit7`
> * owned by group `bandit6`
> * 33 bytes in size

---

## Thought process / Plan

* The level identifies the file by **metadata** (owner user, owner group, exact size) rather than content. That suggests using `find` with metadata filters.
* High-level plan:

  1. Decide where to start the search. The whole server (`/`) is acceptable since the file could be anywhere.
  2. Use `find` filters for `-user`, `-group`, and `-size` to narrow results dramatically.
  3. Add `-readable` or redirect stderr to `/dev/null` to focus on accessible files and avoid permission noise.
  4. Verify the candidate with `cat` or `file`, then use the password to SSH to `bandit7`.

---

## Commands tried (with short notes)

```bash
# Full-system search (produces many permission errors)
find / -type f -user bandit7 -group bandit6 -size 33c

# Cleaner: show only readable matches and hide permission errors
find / -type f -user bandit7 -group bandit6 -size 33c -readable 2>/dev/null

# After finding the path, inspect the file
cat /var/lib/dpkg/info/bandit7.password

# Use the found password to login
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

Notes:

* Running `find /` produces many `Permission denied` messages because system directories block access. Redirecting stderr to `/dev/null` or adding `-readable` keeps output focused.
* `-size 33c` uses the `c` suffix to mean bytes which is crucial for exact matches.

---

## Key outputs / Evidence

```
# A readable matching file was found:
/var/lib/dpkg/info/bandit7.password

# Reading it produced the password (redacted here for safety)
[REDACTED_PASSWORD_FOR_PUBLIC]
```

---

## Final solution (private note)

* **Path to file:** `/var/lib/dpkg/info/bandit7.password`
* **Command used to read it:** `cat /var/lib/dpkg/info/bandit7.password`
* **Password / flag:** `REDACTED_FOR_PUBLIC` (store real password privately)
* **Next step:** SSH into `bandit7` using the found password

---

## What I learned

* `find` is ideal for metadata searches (`-user`, `-group`, `-size`).
* Searching `/` is noisy; use `2>/dev/null` or `-readable` to silence permission errors.
* Always redact real passwords in public docs.

---

## Mistakes to avoid next time

* Forgetting the `c` suffix for byte-precise size checks.
* Not using `-readable` or redirecting stderr when scanning system directories.

---

## References / Further reading

* `man find`
* OverTheWire Bandit Level 7 instructions

---

## Git workflow notes

```
git add level06-07.md
git commit -m "docs: Bandit level06-07 metadata-based find; notes and redacted results"
```
