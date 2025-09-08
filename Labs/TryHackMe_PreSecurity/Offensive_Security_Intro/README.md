# Offensive_Security_Intro

## Quick Win / Lab Overview
In this lab, I completed the TryHackMe **Offensive Security Intro** room. The goal was to hack my first website legally in a safe environment and experience an ethical hacker's workflow.

**Key objectives:**
- Understand what offensive security is.
- Learn basic ethical hacking techniques.
- Use the `dirb` tool to find hidden URLs in a web application.
- Add funds to a test account on the FakeBank application.

---

## Steps Completed

1. **Learned Offensive Security basics:**  
   - Offensive security involves simulating attacks to identify vulnerabilities.  
   - Ethical hackers think like attackers to improve system defenses.

2. **Started the Virtual Machine** for the FakeBank application.

3. **Opened Terminal** in the VM.

4. **Used `dirb` to find hidden URLs:**
```bash
dirb http://fakebank.thm
