# Scanning & Enumeration

##  Introduction
Scanning and enumeration are essential steps in **penetration testing** and **network reconnaissance**. These techniques help identify **live hosts, open ports, running services, and potential vulnerabilities** within a network.

---

##  Network Discovery
Before scanning a target, we need to identify **active devices** in a network.

### **Netdiscover**
- **Use Case**: Passive and active ARP scanning to find live hosts.
- **Command:**
  ```bash
  sudo netdiscover
  ```
- **What It Does:**
  - Detects **live devices** on the same subnet.
  - Lists **IP addresses** and corresponding **MAC addresses**.
  - Useful for discovering **unauthorized devices** in a network.

### **ARP Scan**
- **Use Case**: Similar to Netdiscover but built into many Linux distributions.
- **Command:**
  ```bash
  sudo arp-scan -l
  ```
- **What It Does:**
  - Scans for devices on the **local network** using ARP requests.
  - Lists IP & MAC addresses of connected devices.
  - Faster than Netdiscover but **limited to local subnet only**.

---

##  Port Scanning & Service Enumeration
### **Nmap - Network Mapper**
Nmap is one of the most powerful **port scanners** for network reconnaissance.

#### **Command:**
```bash
sudo nmap -t4 -p- -A <target>
```
#### **Breakdown:**
- **`-t4`** → Aggressive timing for faster scanning.
- **`-p-`** → Scans **all 65,535 ports** (not just common ports).
- **`-A`** → Enables **OS detection, service version detection, and traceroute**.
- **`<target>`** → The IP/domain to be scanned.

#### **Example Usage:**
```bash
sudo nmap -sS -sV -O -p 22,80,443 <target>
```
- **`-sS`** → SYN scan (stealthy scanning).
- **`-sV`** → Service version detection.
- **`-O`** → OS fingerprinting.
- **`-p 22,80,443`** → Scans only ports 22 (SSH), 80 (HTTP), 443 (HTTPS).

---

##  Web Vulnerability Scanning
### **Nikto - Web Server Scanner**
- **Use Case**: Scans web servers for **misconfigurations, outdated software, and vulnerabilities**.
- **Command:**
  ```bash
  nikto -h http://target.com
  ```
- **What It Does:**
  - Detects **default files**, outdated software, security misconfigurations.
  - Checks for **common vulnerabilities** (e.g., XSS, LFI, outdated Apache versions).

#### **Example Usage:**
```bash
nikto -h http://target.com -p 8080
```
- **`-p 8080`** → Specifies a custom port (useful when scanning web apps running on non-standard ports).

---

##  Directory & File Enumeration
Many web applications **hide directories or files** that may contain sensitive information. Tools like **Dirbuster, Dirb, and Gobuster** help discover them.

### **Dirbuster**
- **Use Case**: GUI-based directory brute-forcing.
- **Important Note**: Always use the **full URL with ports**.
- **Command:**
  ```bash
  dirbuster
  ```
- **What It Does:**
  - Uses **wordlists** to find hidden directories & files.
  - Can detect **admin panels, login pages, backup files**.

### **Dirb**
- **Use Case**: Command-line tool for directory brute-forcing.
- **Command:**
  ```bash
  dirb http://target.com/
  ```
- **Example:**
  ```bash
  dirb http://target.com/ wordlist.txt
  ```
  - Uses a **custom wordlist**.

### **Gobuster**
- **Use Case**: Faster and more efficient than Dirb, supports **DNS and directory fuzzing**.
- **Command:**
  ```bash
  gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt
  ```
- **Why It’s Useful:**
  - Faster than **Dirb**.
  - Supports **DNS enumeration** (`gobuster dns` command).

---

##  What to Look For During Scanning & Enumeration
### **Key Information to Gather:**
- **Live hosts** (IPs and MAC addresses).
- **Open ports and running services.**
- **Software versions** (can reveal vulnerable applications).
- **Backend directories** (e.g., `/admin`, `/backup`, `/config`).
- **Leaked credentials** or source code in public directories.
- **Potential vulnerabilities** using Nikto scans.

### **Additional Recon Techniques:**
- **Checking robots.txt:**
  ```bash
  curl -s http://target.com/robots.txt
  ```
- **Extracting metadata from documents:**
  ```bash
  exiftool file.pdf
  ```
- **Checking SSL/TLS configurations:**
  ```bash
  sslyze --regular target.com
  ```

---

##  Conclusion
**Scanning & enumeration** are crucial in any security assessment. Using **Nmap, Netdiscover, Nikto, and directory busters**, you can **map out a network, identify vulnerabilities, and find hidden resources**.

