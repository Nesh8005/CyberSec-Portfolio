# Access Control Incident Analysis
### Overview

In this lab, I investigated an access control incident in which a payroll deposit was made to an unauthorized bank account. By reviewing event logs and employee records, I identified authentication and authorization issues that allowed the incident to occur. I also recommended mitigations to strengthen security practices.

This exercise reinforced my understanding of access controls, accountability, and the importance of removing unused accounts to reduce security risks.

### Scenario

A suspicious payroll deposit was detected, but the finance manager denied making it. My role was to:

1. Review the event log to identify when and how the incident occurred.

2. Cross-reference employee records to identify possible threat actors.

3. Spot weaknesses in authentication and authorization practices.

4. Recommend mitigations to prevent future incidents.

## Tasks and Findings
### Task 1: Review Event Log
### Observations:

The event occurred on 10/03/2023 at 8:29:57 AM.

The payroll entry was created using Legal\Administrator on the computer “Up2-NoGud”.

The IP address used (152.207.255.255) matched Robert Taylor Jr.’s computer, even though his contract ended on 12/27/2019.

### Task 2: Identify Access Control Issues
Issues Found:

Inactive account not revoked: Robert Taylor Jr.’s account and computer were still active years after he left.

Excessive privileges: All employees had Admin rights, violating the principle of least privilege.

Shared Admin accounts: The event log showed Legal\Administrator instead of a unique user, reducing accountability.

#### Task 3: Recommend Mitigations
#### Recommendations:
```text
1. Revoke or deactivate accounts immediately when employees leave the company.
2. Implement Role-Based Access Control (RBAC) to limit permissions based on job roles.
3. Eliminate shared Admin accounts and require unique logins for all employees.
4. Enforce Multi-Factor Authentication (MFA) for sensitive systems such as payroll.
```
### Key Learnings

1. Event logs can be used to track unauthorized activities and link them to specific devices/IPs.

2. Deprovisioning former employees is critical for reducing insider threats.

3. Role-Based Access Control (RBAC) ensures least privilege and better accountability.

4. Shared Admin accounts are a major security risk and should be avoided.

5. Security controls like MFA provide stronger protection for financial transactions.
