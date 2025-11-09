# Bandit Level 0 

**Date:** `2025-11-09`

**Start point:** `local terminal`

**Goal (as written):**

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

---

## Thought process / Plan

* The game tells me to connect to a remote Linux machine using SSH (Secure Shell).
* SSH lets me log into another computer securely over a network.
* I need to specify:

  * The **host**: `bandit.labs.overthewire.org`
  * The **port**: `2220`
  * The **username**: `bandit0`
  * The **password**: `bandit0`

So the plan is:

1. Open the terminal.
2. Run the `ssh` command with the correct username, host, and port.
3. Enter the password when prompted.
4. Confirm I’m logged in by checking the welcome message.

---

## Commands tried (with short notes)

```bash
# Connect to Bandit server using SSH
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

* `ssh` = command for Secure Shell login.
* `bandit0@...` = tells SSH which user to log in as.
* `-p 2220` = specifies the custom port since it’s not the default SSH port (22).

When I pressed enter, SSH asked:

```
The authenticity of host 'bandit.labs.overthewire.org (xxx.xxx.xxx.xxx)' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

I typed `yes`, then entered the password `bandit0`.

After logging in, I saw:

```
Welcome to OverTheWire: Bandit
bandit0@bandit:~$
```

This confirmed I successfully connected.

---

## Key outputs / Evidence

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
bandit0@bandit.labs.overthewire.org's password:
Welcome to OverTheWire: Bandit
bandit0@bandit:~$
```

---

## Final solution (private note)

* **Connection successful** ✅
* **Next step:** Visit Level 1 instructions while staying logged in.

---

## What I learned

* How to use the `ssh` command to log into a remote server.
* The difference between `ssh user@host` and specifying a custom port with `-p`.
* SSH uses encrypted communication for secure logins.

---

## Mistakes to avoid next time

* Forgetting to include `-p 2220` (default SSH port is 22).
* Not typing `yes` when prompted to trust the host key.
* Confusing `@` placement in the SSH command.

---

## References / Further reading

* [Secure Shell (SSH) on Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell)
* [How to use SSH with a non-standard port – It’s FOSS](https://itsfoss.com/ssh-port/)
* [How to use SSH with ssh-keys – wikiHow](https://www.wikihow.com/Use-SSH-Keys)

---

## Git workflow notes

```
git add level00-01.md
git commit -m "docs: Bandit level00-01 SSH login instructions"
```
