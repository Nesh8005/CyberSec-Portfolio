# Bandit Level 1 → Level 2

**Date:** `2025-11-09`

**Start point:** `bandit1@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in a file called `-` located in the home directory.

---

## Thought process / Plan

* The filename is a single dash (`-`). Many Unix commands treat `-` as an option or as a special token meaning stdin/stdout. So trying to `cat -` will usually make the command read from standard input instead of opening a file called `-`.
* Plan: list files to confirm `-` exists; then reference the filename in a way that avoids it being parsed as an option.
* Ways to reference the file safely:

  * `./-` (relative path)
  * `-- -` (end-of-options marker)
  * quoting: `'-'` or `"-"`
  * absolute path: `/home/bandit1/-`

---

## Commands tried (with short notes)

```bash
# Orientation
pwd                # confirm current directory is /home/bandit1
ls -la             # list files, look for a file named '-'

# Safe ways to read the file named '-'
cat ./-            # preferred: treat '-' as a pathname in current dir
cat -- -           # '--' stops option parsing, then '-' is a filename
cat '-'            # quoting the filename
cat /home/bandit1/-

# If you want to copy it to a normal name first
cp ./- ./dash-file
cat ./dash-file

# Check file type before reading (optional)
file ./-
```

Notes:

* `ls -la` will show a file named `-` among other files. It may be hard to spot visually but it will appear as a single dash on the listing line.
* Running `cat -` by itself **reads from stdin** and appears to hang until you type input followed by `Ctrl-D` — this is why referencing the file as `./-` or using `--` is important.

---

## Key outputs / Evidence

```
$ ls -la
-rw-r--r-- 1 bandit1 bandit1 33 Nov  9 12:05 -

$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

---

## Final solution (private note)

* **Path to file:** `./-` (in home directory)
* **Command used to read it:** `cat ./-` (or `cat -- -`)
* **Password / flag:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
* **Next step:** Logged in as `bandit2` using the found password

---

## What I learned

* Filenames beginning with `-` are interpreted as options by many commands; prefixing with `./` or using `--` avoids that.
* `cat -` reads from standard input, not a file named `-`.
* Quoting or using absolute paths are safe alternatives.

---

## Mistakes to avoid next time

* Typing `cat -` expecting the file contents (will read stdin instead).
* Forgetting to use `./` or `--` when the filename starts with a dash.

---

## References / Further reading

* Google search for “dashed filename”
* Advanced Bash-scripting Guide - Chapter 3 - Special Characters
* `man cat`, `man find`

---

## Git workflow notes

```
git add level01-02.md
git commit -m "docs: Bandit level01-02 handling filename '-' and safe reading notes"
```
