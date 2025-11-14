# Bandit Level 5 → Level 6

**Date:** `2025-11-09`

**Start point:** `bandit5@bandit` (home directory `~/inhere`)

**Goal (as written):**

> The password for the next level is stored in a file somewhere under the `inhere` directory and has all of the following properties:
>
> * human-readable
> * 1033 bytes in size
> * not executable

---

## Thought process / Plan

* Use `find` to search recursively for files that match the three properties: size exactly 1033 bytes, not executable, and human-readable.
* Narrow results quickly by size (very selective) then check executability and readability.
* Avoid typing long pipelines from memory — test smaller parts first, then combine.

---

## Commands tried (with short notes)

```bash
# Go to the inhere directory
cd ~/inhere

# I initially mistyped the predicate; correct form is:
find . -type f -size 1033c ! -executable

# This returned the candidate file
./maybehere07/.file2

# Display the file contents
cat ./maybehere07/.file2
```

---

## Key outputs / Evidence

```
$ find . -type f -size 1033c ! -executable
./maybehere07/.file2

$ cat ./maybehere07/.file2
[REDACTED_PASSWORD_FOR_PUBLIC]
```

> Note: The real password is present on your session. Do not commit actual passwords to public repositories. Store it in a private notes file or password manager.

---

## Final solution (private note)

* **Path to file:** `inhere/maybehere07/.file2`
* **Command used to read it:** `cat ./maybehere07/.file2`
* **Password / flag:** `REDACTED_FOR_PUBLIC` (copy it to your private notes)
* **Next step:** SSH into `bandit6` using the found password

---

## What I learned

* `find`'s `-size 1033c` is precise — `c` means bytes and is critical for exact-size matches.
* `! -executable` filters out binaries or scripts that are executable.
* Splitting the problem into small tests helps catch typos (`-excecutable` vs `-executable`).
* Always redact passwords when saving public documentation.

---

## Mistakes to avoid next time

* Typos in `find` predicates (watch spelling of options).
* Printing binary files to the terminal which can corrupt the display — use `reset` if that happens.

---

## References / Further reading

* `man find`
* `man file`

---

## Git workflow notes

```
git add level05-06.md
git commit -m "docs: Bandit level05-06 find by size and executability; notes"
```
