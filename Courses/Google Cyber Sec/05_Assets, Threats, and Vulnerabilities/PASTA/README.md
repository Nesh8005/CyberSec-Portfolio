# 🥾 Sneaker Company App – PASTA Threat Model

This repository documents a threat model of a sneaker company’s new mobile application using the **PASTA (Process for Attack Simulation and Threat Analysis)** framework.  
The goal is to identify business objectives, analyze risks, and propose security controls before launch.  

---

## 📌 Stage I – Define Business and Security Objectives
- The app has significant back-end processing (login system, customer/seller data, sneaker listings).  
- Proper **payment handling** is critical to avoid legal issues and protect users.  
- The app must securely **process transactions** and protect user data.  

---

## 📌 Stage II – Define the Technical Scope
**Technologies used by the application:**  
- **Application Programming Interface (API):** Enables communication between different software components.  
- **Public Key Infrastructure (PKI):** Provides encryption and digital certificates for secure communication and authentication.  
- **SHA-256:** Cryptographic hash function for securely storing and verifying data (e.g., passwords, digital signatures).  
- **SQL:** Structured Query Language for managing and querying data in relational databases.  

---

## 📌 Stage III – Decompose Application
- Users interact with the app via login, product browsing, and messaging.  
- API facilitates data exchange between front-end and back-end services.  
- SQL database stores users, products, and transactions.  
- PKI and SHA-256 secure authentication and sensitive data.  

*(See: Sample Data Flow Diagram resource)*  

---

## 📌 Stage IV – Threat Analysis
- **SQL Injection** due to lack of prepared statements.  
- **Weak login credentials** leading to account compromise.  

---

## 📌 Stage V – Vulnerability Analysis
Potential exploitable weaknesses:  
- Codebase issues (poor input validation, insecure authentication logic).  
- Database misconfigurations or unencrypted sensitive data.  
- Network flaws allowing interception of API traffic.  

---

## 📌 Stage VI – Attack Modeling
**Possible attack vectors include:**  
- SQL injection → Extract customer/seller/payment data.  
- Credential stuffing → Compromise user accounts.  
- Man-in-the-middle attack → Intercept unencrypted API traffic.  
- Exploiting code flaws → Escalate privileges or bypass authentication.  

*(See: Sample Attack Tree resource)*  

---

## 📌 Stage VII – Risk Analysis and Mitigation
**Security controls to reduce risk:**  
1. Use **prepared statements and parameterized queries** to prevent SQL injection.  
2. Implement **multi-factor authentication (MFA)** for account security.  
3. Conduct **regular code reviews and vulnerability scanning**.  
4. Enforce **network encryption (TLS/SSL)** for data in transit.  

---

## ✅ Key Takeaway
By applying the **PASTA framework**, the sneaker company can proactively identify risks, strengthen defenses, and ensure the app is safe to launch.  

