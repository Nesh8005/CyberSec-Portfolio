# Bandit Level 2 → Level 3

**Date:** `2025-11-09`

**Start point:** `bandit2@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in a file called `--spaces in this filename--` located in the home directory.

---

## Thought process / Plan

* This filename contains spaces. Most Linux commands interpret spaces as argument separators, so running `cat --spaces in this filename--` will break into multiple arguments and fail.
* Plan: safely reference filenames with spaces using:

  * Quoting: `'--spaces in this filename--'` or `"--spaces in this filename--"`
  * Escaping spaces with backslashes: `--spaces\ in\ this\ filename--`
  * Absolute path: `/home/bandit2/--spaces in this filename--`
  * Or using tab-completion in shell to avoid typing errors

---

## Commands tried (with short notes)

```bash
# Orientation
pwd                # confirm current directory
ls -la             # list files to find the filename with spaces

# Safe ways to read the file
cat '--spaces in this filename--'
cat "--spaces in this filename--"
cat --spaces\ in\ this\ filename--
cat /home/bandit2/--spaces\ in\ this\ filename--

# Optional: copy to a simpler filename before reading
cp '--spaces in this filename--' ./spacesfile
cat ./spacesfile

# Check file type before reading (optional)
file '--spaces in this filename--'
```

Notes:

* Always quote or escape filenames with spaces to avoid splitting into multiple arguments.
* Tab-completion helps avoid mistakes and reduces typing errors.

---

## Key outputs / Evidence

```
$ ls -la
-rw-r--r-- 1 bandit2 bandit2 33 Nov  9 12:10 --spaces in this filename--

$ cat ./--spaces\ in\ this\ filename--
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

```

---

## Final solution (private note)

* **Path to file:** `./--spaces in this filename--` (home directory)
* **Command used to read it:** `cat ./--spaces\ in\ this\ filename--`
* **Password / flag:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
* **Next step:** Logged in as `bandit3` using the password

---

## What I learned

* Filenames with spaces must be quoted or escaped to be interpreted correctly.
* Linux shell splits unquoted filenames on spaces.
* Tab-completion is very helpful for long filenames or filenames with spaces.

---

## Mistakes to avoid next time

* Forgetting quotes or escaping spaces, causing commands to fail.
* Miscounting spaces or special characters in filenames.
* Not using tab-completion to confirm the filename.

---

## References / Further reading

* Google search: “spaces in filename Linux”
* `man cat`, `man ls`
* Bash scripting guides on handling filenames with spaces

---

## Git workflow notes

```
git add level02-03.md
git commit -m "docs: Bandit level02-03 handling filenames with spaces"
```
