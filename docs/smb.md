# SMB (Server Message Block) - Port 139 & 445

## 🔹 Introduction to SMB
**SMB (Server Message Block)** is a **network file sharing protocol** that allows applications or users to read and write files over a network. It enables **file sharing, printer sharing, and remote access** to Windows-based resources. SMB operates mainly over **port 139 (NetBIOS) and port 445 (Direct TCP/IP)**.

### **Ports Used by SMB:**
- **Port 139**: Used for SMB communication over NetBIOS.
- **Port 445**: Used for SMB communication directly over TCP/IP (modern implementations).

### **Common Use Cases:**
- File and folder sharing between **Windows and Linux systems**.
- Authentication and access control for shared resources.
- Network-based **privilege escalation and exploitation** in penetration testing.

---

## 🔹 Enumerating SMB Shares
To discover **shared folders**, we can use **smbclient** (a command-line tool for SMB access) to list available shares on a target system.

### **Listing SMB Shares**
```bash
smbclient -L \\192.168.0.0\ADMIN$
```
### **Breakdown:**
- **`smbclient`** → The tool used to interact with SMB shares.
- **`-L`** → Lists all available shares on the specified server.
- **`\\192.168.0.0\ADMIN$`** → The target **IP address** and **share name** (in this case, `ADMIN$`, a hidden administrative share).

**Example Output:**
```	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$         Disk      Remote Admin
	C$             Disk      Default share
	IPC$           IPC       Remote IPC
```

---

## 🔹 SMB Anonymous Access
Some SMB servers allow **unauthenticated (anonymous) access**, meaning that no username or password is required to view or access shared resources.

### **Checking for Anonymous SMB Access:**
```bash
smbclient -L \\192.168.0.0\ -N
```
- **`-N`** → Disables password prompt (attempts to access SMB shares without authentication).
- If anonymous access is **enabled**, the shares may be listed and **publicly accessible**.

### **Accessing an SMB Share Anonymously:**
```bash
smbclient \\192.168.0.0\public -N
```
- If successful, you'll get an **SMB interactive shell** where you can navigate and download files:
  ```
  smb: \> ls
  smb: \> get important_document.txt
  ```

---

## 🔹 Additional SMB Enumeration & Exploitation Tools
### **Nmap SMB Scripts**
Nmap has built-in scripts for **SMB enumeration** and **vulnerability detection**.
```bash
nmap -p 139,445 --script=smb-enum-shares,smb-enum-users 192.168.0.0
```
- **`smb-enum-shares`** → Lists shared folders.
- **`smb-enum-users`** → Enumerates SMB users.

### **Enum4Linux (SMB Enumeration on Linux)**
```bash
enum4linux -a 192.168.0.0
```
- Gathers **user accounts, shares, group memberships, and policies**.

### **Checking SMB Version & Vulnerabilities**
```bash
smbclient -V  # Displays installed SMB client version
nmap --script smb-vuln* -p 139,445 192.168.0.0  # Checks for known SMB vulnerabilities
```

---

## 🔹 SMB Exploits & Security Concerns
### **Common SMB Exploits:**
- **SMB Null Sessions** (unauthorized access to shared resources).
- **EternalBlue (MS17-010)** → Remote code execution vulnerability in older SMB versions.
- **Relay Attacks** (Intercepting SMB authentication for lateral movement).

### **Securing SMB:**
- **Disable SMBv1** (Older versions are vulnerable to exploits like EternalBlue).
- **Enforce authentication** for accessing shares.
- **Limit SMB access** to trusted IPs and networks.
- **Use strong credentials** and disable anonymous access.

---

## 🔹 Conclusion
SMB is a **powerful network protocol** for file sharing, but it also presents **security risks** when misconfigured. Understanding SMB enumeration techniques can help identify potential vulnerabilities and secure network resources.


