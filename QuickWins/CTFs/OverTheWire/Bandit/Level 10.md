# Bandit Level 9 → Level 10 (session notes)

**Date:** `2025-11-09`

**Start point:** `bandit9@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in the file `data.txt` in one of the few human-readable strings, preceded by several `=` characters.

---

## Thought process / Plan

* The file is mostly binary-like but contains readable strings. The password appears in a readable string that is preceded by several `=` characters.
* Use `strings` to extract readable substrings, then search these for runs of `=` to locate the relevant line. Once located, strip the leading `=` characters to isolate the password.

---

## Commands run (session)

```bash
# attempted to run strings on the file (typo corrected)
strings -n 5 data.txt

# sample output (truncated) — readable strings are shown, including lines with runs of '='
...
========== the
...
========== password
...
E========== is
...
5========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
...
```

# Then filtered strings for '=' characters

strings -n 5 data.txt | grep '='

# grep output (relevant lines shown)

c\5D=
========== the
=vG*2P
========== password
k=ezG
E========== is
.?=Dm
O&A=n
5========== [REDACTED_PASSWORD_FOR_PUBLIC]

````

---

## Interpretation
- The `strings` output shows several lines containing `=` runs. The line containing `5========== FGUW5il...` looks like the readable token preceded by multiple `=` characters, matching the level hint.
- To extract the password you can remove everything up to and including the run of `=` characters. For example:
```bash
strings data.txt | grep -E '={3,}' | sed 's/.*={3,}//'
````

This will print the token(s) after the `=` run(s).

---

## Key outputs / Evidence (redacted for public)

```
# Matching readable line (redacted):
5========== [REDACTED_PASSWORD_FOR_PUBLIC]
```

---

## Final solution (private note)

* **Path to file:** `./data.txt`
* **Commands used to find it:**

  * `strings -n 5 data.txt`
  * `strings data.txt | grep -E '={3,}'`
  * `strings data.txt | grep -E '={3,}' | sed 's/.*={3,}//'`
* **Password / flag:** `REDACTED_FOR_PUBLIC` (store the real password privately)
* **Next step:** SSH into `bandit10` using the found password

---

## What I learned

* `strings` is the correct tool to pull readable substrings from binary-like files without corrupting the terminal.
* Use `grep -E '={3,}'` to find runs of three or more equals signs.
* `sed` can remove the prefix so only the password token remains.

---

## Mistakes to avoid

* Typo: `strings -n 5 data,txt` (comma) — ensure correct filename.
* Printing the raw binary file with `cat` — can garble the terminal. Use `strings` instead.
* Publishing real passwords in public documentation; always redact.

---

## Git workflow notes

```
git add level09-10-session.md
git commit -m "docs: Bandit level09-10 session output and extraction method (redacted)"
```
