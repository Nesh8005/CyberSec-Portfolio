# Bandit Level 4 → Level 5

**Date:** `2025-11-09`

**Start point:** `bandit4@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in the only human-readable file in the `inhere` directory. Tip: if your terminal is messed up, try the “reset” command.

---

## Thought process / Plan

* There are multiple files in the `inhere` directory, most of which are binary or unreadable.
* Goal is to find the **only human-readable file**.
* Plan:

  1. List all files using `ls -la`.
  2. Attempting to `cat` each file manually would be tedious.
  3. Use `file` command to determine file types.
  4. Filter output for files containing text (`grep -i text`).
  5. Once the human-readable file is found, read it with `cat` to get the password.

---

## Commands tried (with short notes)

```bash
# Enter the inhere directory
cd inhere
ls -la             # list all files

# Check file types for all files safely
find . -type f -exec file -- {} + | grep -i text

# Output shows the only human-readable file
# Read the password from it
cat ./-file07
```

Notes:

* Filenames beginning with `-` require `./` or `--` to prevent being interpreted as options.
* `file` command identifies file types; `grep -i text` filters only human-readable text files.

---

## Key outputs / Evidence

```
$ find . -type f -exec file -- {} + | grep -i text
./-file07: ASCII text

$ cat ./-file07
REDACTED_FOR_PUBLIC
```

---

## Final solution (private note)

* **Path to file:** `inhere/-file07`
* **Command used to read it:** `cat ./-file07`
* **Password / flag:** `REDACTED_FOR_PUBLIC`
* **Next step:** SSH into `bandit5` using this password

---

## What I learned

* Use `file` to quickly determine human-readable vs binary files.
* `grep -i text` filters out the ASCII or text files automatically.
* Filenames starting with `-` must be referenced with `./` or `--`.
* The `reset` command can fix terminal issues caused by printing binary data.

---

## Mistakes to avoid next time

* Trying `cat` on all files manually — time-consuming and can mess up the terminal.
* Forgetting to escape or prefix filenames with dashes.
* Ignoring the `reset` tip after printing unreadable/binary files.

---

## References / Further reading

* `man find` and `man file`
* OverTheWire Bandit Level 5 instructions
* Tutorials on handling binary vs text files in Linux

---

## Git workflow notes

```
git add level04-05.md
git commit -m "docs: Bandit level04-05 human-readable file identification with find and file"
```
