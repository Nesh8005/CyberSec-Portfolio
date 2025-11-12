# Bandit Level 11 → Level 12

**Date:** `2025-11-09`

**Start point:** `bandit11@bandit` (home directory)

**Goal (as written):**

> The password for the next level is stored in the file `data.txt`, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions (ROT13).

---

## Thought process / Plan

* ROT13 is a simple substitution cipher that shifts letters by 13 positions. Applying ROT13 to the encoded text returns the original message.
* The file `data.txt` should contain a short ROT13-encoded sentence that, when decoded, reveals the password.

**Plan:**

1. Confirm `data.txt` exists and inspect it with `ls -la` and `cat`.
2. Apply a ROT13 transformation to the line to decode it. If there is no `rot13` command available, use an online ROT13 tool or a local alternative (for example `tr 'A-Za-z' 'N-ZA-Mn-za-m'`).
3. Save the decoded password privately and SSH to the next level.

---

## Commands tried (with short notes)

```bash
# Confirm file presence and permissions
ls -la

# View the encoded content
cat data.txt
# Output: Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4

# Tried 'rot13' command but it's not installed on the system
rot13 data.txt  # Command not found

# Alternative: use tr to perform ROT13 locally
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt

# Or use an online ROT13 tool and paste the string
# After decoding we obtain the password token
```

Notes:

* `tr 'A-Za-z' 'N-ZA-Mn-za-m'` performs ROT13 without installing extra packages.
* The system may not have handy utilities installed (`rot13` was not found, `hashid` not found). Sudo is not available for installing packages.
* Using a trusted online ROT13 decoder is acceptable for short strings if you cannot run `tr` locally, but local `tr` is preferable.

---

## Key outputs / Evidence

```
$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4

# Decoded with ROT13 (examples below show the decoded line)
The password is [REDACTED_PASSWORD_FOR_PUBLIC]
```

---

## Final solution (private note)

* **Path to file:** `./data.txt`
* **Command used to decode (local):**

  ```bash
  tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
  ```
* **Password / flag:** `[REDACTED_PASSWORD_FOR_PUBLIC]` (REDACTED in public docs)
* **Next step:** SSH into `bandit12` using the found password

---

## What I learned

* ROT13 can be implemented with `tr 'A-Za-z' 'N-ZA-Mn-za-m'` if a specialized utility is unavailable.
* Many small helper tools may not be installed on the remote challenge host; prefer simple built-in utilities.
* Never use `sudo` on challenge hosts; it will fail due to permissions and is unnecessary.

---

## Mistakes to avoid next time

* Relying on installing new packages (`rot13`, `hashid`) — they are often not available and `sudo` is restricted.
* Copying secret passwords into public files — always redact before committing.

---

## References / Further reading

* ROT13 on Wikipedia
* `man tr`

---

## Git workflow notes

```
git add level11-12.md
git commit -m "docs: Bandit level11-12 ROT13 decode using tr; notes and redacted password"
```
