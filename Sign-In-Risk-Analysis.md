# Identity Incident Simulation – Sign-In Risk Analysis
**Author:** Pasquale Fabio Cioffo  
**Role:** Identity & Access Security  
**Date:** _To be completed_

---

## 1. Scenario Overview
This document simulates an enterprise-level **Sign-In Risk analysis** using Microsoft Entra ID (formerly Azure AD) Identity Protection signals.

The goal is to demonstrate:
- how risky sign-ins are detected  
- how risk levels influence authentication  
- how to mitigate identity-based threats using Conditional Access and Identity Protection  
- how to respond to early indicators to prevent account compromise  

---

## 2. What is Sign-In Risk?
**Sign-In Risk** represents the likelihood that a given authentication attempt was performed by someone other than the legitimate user.

Microsoft assigns risk based on machine learning signals such as:
- unfamiliar or anonymous IP  
- impossible travel  
- malware-linked IP  
- leaked credentials  
- atypical token behavior  
- suspicious session characteristics  

Risk Levels:
- **Low**  
- **Medium**  
- **High**

---

## 3. Detection – Key Identity Protection Signals

### 🔎 **Suspicious Indicators**
A sign-in may be classified as risky when:
- login originates from an unfamiliar country  
- the location contradicts the user’s usual pattern (“impossible travel”)  
- the IP address belongs to TOR or an anonymous VPN  
- the token was replayed  
- leaked credentials were detected in breach repositories  
- login attempted with outdated authentication libraries  

### 🔎 **Typical Log Fields to Monitor**
- **Risk Level:** Low / Medium / High  
- **Risk Detail:** e.g., “Anonymous IP”, “Unfamiliar sign-in properties”, “Leaked credentials”  
- **Location:** unexpected country  
- **IP Type:** suspicious or anonymous  
- **Authentication Requirement:** MFA required / MFA denied  

---

## 4. Example: Simulated Risky Sign-In Event

### **Event Summary**
- **User:** operational employee  
- **Risk Level:** High  
- **Risk Detail:** “Anonymous IP address”  
- **Country:** Russia (unexpected)  
- **Status:** MFA failed  
- **Client App:** Modern Authentication  
- **Timestamp:** Night-time (02:13)

### **What it means**
- The attacker knows the user password  
- MFA prevented the login  
- The attacker attempted a login through a masked IP  
- The account is under active attack  

---

## 5. Impact Analysis

If MFA had not been enabled, attacker would gain:
- mailbox access  
- OneDrive access  
- Teams internal communication  
- potential privilege escalation  
- opportunity for Business Email Compromise (BEC)  
- sessions tokens enabling lateral movement  

Sign-In Risk analysis prevents early compromise by flagging suspicious attempts **before** the breach occurs.

---

## 6. Response Plan (IAM-Focused)

### **Step 1 – Review a**
