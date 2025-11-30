# Identity Incident Simulation – Password Spray Attack
**Author:** Pasquale Fabio Cioffo  
**Role:** Identity & Access Security  
**Date:** _To be completed_

---

## 1. Scenario Overview
This document simulates a real-world **password spray attack** targeting Microsoft 365 / Entra ID accounts.  
Password spraying is one of the most common identity-based attacks, leveraging weak or reused passwords at scale.

The objective is to demonstrate:
- how such an attack appears in Entra ID logs  
- how to recognize early indicators  
- how to respond following a structured IAM process  
- how to mitigate future attempts using Conditional Access

---

## 2. Attack Description – What is a Password Spray?
A password spray attack attempts the **same password** across **multiple accounts**, avoiding account lockout policies.

### Typical attacker behavior:
- Uses common passwords (e.g., “Estate2024!”, “Password123”)  
- Targets large groups of users  
- Uses distributed IPs to avoid detection  
- Aims to compromise one weak account  
- Escalates from mailbox → OneDrive → Teams → lateral movement

---

## 3. Detection – Indicators in Entra ID Logs
During a password spray attempt, Entra ID typically records:

### 🔎 **Common Indicators**
- Multiple failed sign-ins across many accounts  
- Same **password** attempted by attacker → shown as “Incorrect password”  
- Attempts from:
  - anonymous IP addresses  
  - VPN exit nodes  
  - TOR  
  - unexpected geolocations  

### 🔎 **Log Fields to Monitor**
- **Status:** Failure  
- **Failure reason:** “Invalid username or password”  
- **Location:** unfamiliar country  
- **IP Type:** Anonymous / Untrusted  
- **Client App:** Legacy apps (if attacker tries old protocols)  

---

## 4. Impact Analysis
If successful, the attacker may gain:

- Access to Microsoft 365 mailbox  
- Access to files in OneDrive  
- Teams internal communication visibility  
- Lateral movement inside the environment  
- Potential for Business Email Compromise (BEC)

Even a single compromised non-admin account can be escalated.

---

## 5. Response Plan (IAM-Focused)

### **Step 1 — Identify all affected accounts**
- Filter by “Failed sign-in”  
- Same password attempted across multiple users  
- Confirm attack scope  

### **Step 2 — Reset password for targeted accounts**
- Enforce a strong password  
- Prevent attacker reuse  

### **Step 3 — Enforce MFA**
- Mandatory for ALL users  
- App-based authentication preferred  

### **Step 4 — Review risky users in Identity Protection**
- Mark non-compromised users as safe  
- Require password reset for flagged accounts  

### **Step 5 — Notify impacted users**
- Short, clear communication  
- Avoid unnecessary detail  

---

## 6. Mitigation – Conditional Access & Identity Protection

### 📌 **Recommended Conditional Access Policies**
- Block legacy authentication  
- Require MFA for all users  
- MFA for high-risk sign-ins  
- Block high-risk IP locations  
- Sign-in risk policy: Require MFA  
- User risk policy: Require password reset  

### 📌 **Additional Hardening**
- Enable “Security Defaults” if CA is not available  
- Require Authenticator App  
- Remove SMS as primary factor  
- Implement break-glass account monitoring  

---

## 7. Lessons Learned

- Identity is the primary attack vector in cloud environments  
- Password spraying is cheap and common  
- MFA dramatically reduces impact  
- Conditional Access is mandatory for proper defense  
- Logs must be monitored regularly  
- Even small organizations are frequent targets  

---

## 8. Signature
**Pasquale Fabio Cioffo**  
_Identity & Access Security_
