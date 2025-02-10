# Burp Suite - Credential Stuffing & Password Spraying

## 🔹 Introduction
Burp Suite is a powerful **web security testing tool** used for **testing login security, performing credential stuffing, and executing password spraying attacks**. These techniques help identify **weak authentication mechanisms and misconfigured login systems**.

⚠️ **Warning:** These attacks can trigger **account lockouts**, so always test **ethically** and in a controlled environment.

---

## 🔹 Credential Stuffing
### **What is Credential Stuffing?**
Credential stuffing is an **automated attack** where attackers use **breached username/password pairs** in hopes that users have **reused their credentials** across multiple sites.

### **How to Perform Credential Stuffing in Burp Suite**
1️⃣ **Intercept Login Request:**
- Enable **Burp Suite Proxy**.
- Log in to the target website using **any credentials** (to capture the request).
- **Forward** the request to see how the login works.

2️⃣ **Send to Intruder:**
- Right-click on the login request → **Send to Intruder**.
- Clear existing positions (`Clear` button).
- Highlight **username** and **password** fields → Click `Add`.

3️⃣ **Select Attack Type - Pitchfork:**
- Use `Pitchfork Mode` (matches each username with its respective password in order).

4️⃣ **Configure Payloads:**
- Go to the **Payloads** tab.
- **Payload Set 1:** Add a **list of breached usernames**.
- **Payload Set 2:** Add a **list of breached passwords**.

5️⃣ **Analyze Responses:**
- Run the attack and analyze **response codes**.
- Look for **successful logins** (e.g., HTTP 200 instead of 401 or 403).
- Use **Grep Extract** to highlight error messages (e.g., `Cannot sign in`).

---

## 🔹 Password Spraying
### **What is Password Spraying?**
Password spraying is an attack where **a few common passwords** are tested against **many known usernames**. Unlike brute force attacks, it avoids account lockouts by limiting attempts per user.

### **How to Perform Password Spraying in Burp Suite**
1️⃣ **Capture a Login Request:**
- Enable Burp Suite Proxy.
- Log in with **any credentials** and **send the request to Intruder**.

2️⃣ **Modify the Intruder Attack:**
- Select **Sniper Mode** (focuses on one list at a time).
- Highlight the **password field** → Click `Add`.
- Set the **Payload Set 1** to include weak passwords (e.g., `Fall2024!`, `Password123!`).
- Set the **username field** to a known list of usernames.

3️⃣ **Control Attack Speed:**
- Run **only 1-2 attempts per user** to avoid triggering security mechanisms.

4️⃣ **Check Responses:**
- Analyze **status codes** or **error messages** to identify successful login attempts.

---

## 🔹 Best Practices & Detection Avoidance
- Use **low request rates** to avoid account lockouts.
- Monitor **response codes** to detect successful login attempts.
- Change **user agents & headers** to mimic normal traffic.
- Use **proxy rotation** (e.g., Burp Collaborator) to evade detection.

---

## 🔹 Conclusion
Burp Suite provides **powerful automation for testing authentication security**. Credential stuffing and password spraying can help identify **weak login protections**, but they should only be used in **authorized security testing engagements**.

