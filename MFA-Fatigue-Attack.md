# Identity Incident Simulation – MFA Fatigue Attack (Push Bombing)
**Author:** Pasquale Fabio Cioffo  
**Role:** Identity & Access Security  
**Date:** _To be completed_

---

## 1. Scenario Overview
This document simulates an **MFA Fatigue Attack** (also known as *Push Bombing*), one of the most common modern techniques used by attackers to bypass weak MFA configurations, especially those based on simple push notifications.

The goal is to demonstrate:
- how the attack occurs  
- how it appears in Entra ID logs  
- how an organization should respond  
- which protections are required to stop it  

---

## 2. Attack Description – What is MFA Fatigue?
Attackers already know the victim’s **password** (from leaks or brute-force).  
The attacker then repeatedly sends **MFA push notifications** to the user, hoping they approve one out of annoyance, distraction, or confusion.

### Typical attacker pattern:
- Gains user password  
- Sends dozens of MFA prompts per minute  
- Attempts login mostly at night  
- Spoofs internal phone numbers or locations  
- Tries to trick the user into “accidentally approving”  
- If successful → full account takeover

---

## 3. Detection – Indicators in Entra ID Logs

### 🔎 Common Log Patterns
- Multiple MFA prompts in a short time window  
- MFA requests from unusual geolocations  
- Repeated MFA denials by user  
- Attempts from:
  - TOR  
  - VPN exit nodes  
  - Anonymous proxies  
- Sudden spike in “MFA denied” or “MFA failed”

### 🔎 Log Fields to Monitor
- **Status:** “MFA denied”, “MFA failed”, “User declined MFA”  
- **Location:** unfamiliar or impossible travel  
- **IP Category:** anonymous, untrusted  
- **Correlation IDs:** repeated attempts with same attacker session

---

## 4. Impact Analysis
If successful, attacker gains:
- Full access to mailbox  
- Visibility into internal communication via Teams  
- Access to OneDrive files  
- Ability to escalate attacks (BEC, impersonation)  
- Potential lateral movement inside the tenant  

This attack bypasses **weak MFA implementations**, especially:

- push-only  
- SMS MFA  
- voice call authentication

---

## 5. Response Plan (IAM-Focused)

### **Step 1 – Identify the impacted user**
Check:
- MFA prompted events  
- MFA denials  
- login attempts  
- unusual geolocation  

### **Step 2 – Force password reset**
Immediately reset the user’s password.  
Prevent attacker reuse.

### **Step 3 – Enforce strong MFA**
Switch user from:
- push notifications → **number matching**  
- SMS → **Authenticator App**  

### **Step 4 – Review sign-in logs for lateral movement**
Analyze:
- Access attempts  
- New devices  
- Token refresh events  
- Conditional Access blocks (if present)

### **Step 5 – Contact user**
Send a simple, non-technical notification:
> “If you receive MFA prompts you did not initiate, decline them and notify IT.”

---

## 6. Mitigation (Permanent Fix)

### ✔ Recommended Conditional Access policies
- Require **Authenticator App** with number matching  
- Block SMS as primary factor  
- Require MFA for all users  
- Enable sign-in risk policy  
- Block high-risk geolocations  
- Disable legacy authentication  

### ✔ Additional Hardening
- Educate users about MFA prompts  
- Monitor “impossible travel” alerts  
- Enforce passwordless (FIDO2) for privileged users  
- Monitor break-glass accounts

---

## 7. Lessons Learned
- MFA is only strong if configured correctly  
- Push-based MFA without number matching is vulnerable  
- Identity Protection signals are crucial for detection  
- User awareness is part of the defense  
- Conditional Access is mandatory  
- Password hygiene alone is not sufficient  

---

## 8. Signature
**Pasquale Fabio Cioffo**  
_Identity & Access Security_
