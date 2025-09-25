# 🛡️ Phishing Investigation Activity

This document contains the analysis of a **suspicious spear phishing email** received by an executive at **Imaginary Bank**. The exercise demonstrates how to detect phishing attempts by analyzing email headers, message body, and malicious links.

---

## 📌 Scenario

An executive at Imaginary Bank received a suspicious email asking them to download and install collaboration software called **ExecuTalk**. The executive reported it because the software had never been mentioned in board meetings.

As a **security analyst**, the task was to:
1. Investigate the email headers and body.
2. Identify clues of phishing.
3. Verify the legitimacy of the download links.
4. Decide whether the email should be quarantined.

---

## 📧 Suspicious Email Details

**Header:**
```css
From: imaginarybank@gmail.org

Sent: Saturday, December 21, 2019 15:05:05
To: cfo@imaginarybank.com

Subject: RE: You are been added to an ecsecutiv's groups
```
**Body:**
```css
Conglaturations! You have been added to a collaboration group ‘Execs.’

Downlode ExecuTalk to your computer.

Mac® | Windows® | Android™

You're team needs you! This invitation will expire in 48 hours so act quickly.

Sincerely,
ExecuTalk©
All rights reserved.
```
---



## 🔎 Analysis

### 1. **Email Header Analysis**
Two clear **red flags**:
- ❌ The sender is using a **different domain**: `@gmail.org` instead of the company’s domain `@imaginarybank.com`.  
- ❌ There is a **misspelling** in the subject line: “ecsecutiv's groups.”  

---

### 2. **Message Body Analysis**
The attacker used several tricks to make the email appear legitimate:
- ⏳ **Invitation time limit**: Creates urgency (expires in 48 hours).  
- 💻 **Download options for major operating systems**: Tries to appear professional and universal.  
- ™️ **Brand labeling**: Fake use of “ExecuTalk©” to mimic legitimacy.  

---

### 3. **Malicious Links**
- The download links redirected to:
  ```css
  my.site.net/pwnexecs/
  ```

- This page **looked like an official login screen**, but the **URL is suspicious**.  
- ✅ The **main clue**: The **URL** does not match the supposed vendor or company domain.  

---

## ✅ Final Decision
- This email is a **phishing attempt**.  
- It contains **misspellings, fake domains, false urgency, and malicious links**.  
- **Action**: 🚫 **Quarantine the email** to protect the executive and organization.  

---

## 📚 Key Takeaways
- Always check the **email domain** and look out for **spelling errors**.  
- Fake urgency and fake branding are common phishing tactics.  
- Always hover over links before clicking—URLs often reveal the attack.  
- When in doubt → quarantine and report.  

---

