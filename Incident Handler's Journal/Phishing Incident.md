# Incident Handler's Journal

**Date:** October 16, 2025  
**Entry #:** 2 

## Description

This entry documents a phishing attempt targeting the HR department of Inergy. The attacker sent an email impersonating a job applicant, containing a password-protected executable file disguised as a resume attachment. The file’s hash matched a known malicious signature.

## Tool(s) used

File hash lookup (VirusTotal or internal threat intelligence database).

## The 5 W's

- **Who:** A threat actor using the alias “Def Communications” from the domain <76tguyhh6tgftrt7tg.su>.

- **What:** A phishing email with a malicious .exe attachment (bfsvc.exe) verified as malware.

- **When:** Wednesday, July 20, 2022, at approximately 9:30 a.m.

- **Where:** Inergy corporate email system (hr@inergy.com).

- **Why:** The attacker attempted to deliver malware under the guise of a job application to compromise the organization’s network.

## Additional notes

The email exhibited multiple phishing indicators including a mismatched sender domain, grammatical errors, and a password-protected executable attachment. The incident was escalated to Tier 2 for containment. Recommended follow-up actions include updating email filters with new indicators, reinforcing HR phishing awareness, and monitoring for similar sender domains or attachment hashes.
