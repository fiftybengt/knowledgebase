# Bash Scripting Guide

## 🔹 Introduction to Bash Scripting
Bash scripting automates tasks and enhances productivity by executing commands in sequence. Scripts are commonly used for **networking, automation, and system administration**.

To create and edit a Bash script:
```bash
mousepad script.sh  # Open a text editor (use nano, vim, etc.)
```
Add the shebang (`#!`) at the beginning to specify the interpreter:
```bash
#!/bin/bash   # Standard shebang for Bash scripts
```
> Some systems may use `#!/usr/bin/bash`, but `/bin/bash` is widely compatible.

---

## 🔹 Understanding a Simple Ping Script
### Example Command:
```bash
ping 192.168.1.1 -c 1 > ip.txt
cat ip.txt | grep "64 bytes" | cut -d " " -f4 | tr -d ":"
```
### Breakdown:
1. **`ping 192.168.1.1 -c 1 > ip.txt`** → Sends **one ICMP echo request** (`-c 1`) and saves output to `ip.txt`.
2. **`cat ip.txt`** → Reads the contents of `ip.txt`.
3. **`grep "64 bytes"`** → Filters lines that contain `"64 bytes"`, indicating a successful ping.
4. **`cut -d " " -f4`** → Splits the line by spaces (`-d " "`), extracts **4th field (IP address)**.
5. **`tr -d ":"`** → Removes trailing `:`.

✅ **Corrected One-Liner:**
```bash
ping -c 1 192.168.1.1 | grep "64 bytes" | cut -d " " -f4 | tr -d ":"
```

---

## 🔹 IP Sweep Script (`ipsweep.sh`)
### **Purpose:**
This script pings all **254 hosts** in a subnet (`x.x.x.1 - x.x.x.254`) and returns live hosts.

### **Script:**
```bash
#!/bin/bash

if [ "$#" -ne 1 ]; then
    echo "Usage: ./ipsweep.sh <network-prefix>"
    exit 1
fi

for ip in $(seq 1 254); do
    ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f4 | tr -d ":" &
done
wait
```

### **Explanation:**
- **`$1`** → First argument passed to the script (e.g., `192.168.1`).
- **`seq 1 254`** → Loops from **1 to 254** (valid host addresses).
- **`ping -c 1 $1.$ip`** → Pings each IP in the subnet.
- **`grep "64 bytes"`** → Filters successful responses.
- **`cut -d " " -f4 | tr -d ":"`** → Extracts and cleans up the responding IP.
- **`&`** → Runs pings in parallel for speed.
- **`wait`** → Ensures all background processes complete before script exits.

### **Executing the Script:**
```bash
chmod +x ipsweep.sh  # Make it executable
./ipsweep.sh 192.168.1  # Run the script with a subnet prefix
```

---

## 🔹 One-Liner Nmap Scan Script
### **Script:**
```bash
for ip in $(cat ips.txt); do nmap -sn $ip; done
```

### **Explanation:**
- **`cat ips.txt`** → Reads IPs from `ips.txt` (each IP on a new line).
- **`for ip in $(cat ips.txt); do ... done`** → Iterates over each IP.
- **`nmap -sP $ip`** → Runs a **ping scan** (`-sn` checks if host is up).

---

## 🔹 Additional Useful Scripts

### **Port Scanner Using Netcat**
```bash
#!/bin/bash

if [ "$#" -ne 2 ]; then
    echo "Usage: ./portscan.sh <IP> <Port-Range>"
    exit 1
fi

for port in $(seq $2); do
    (echo > /dev/tcp/$1/$port) >/dev/null 2>&1 && echo "Port $port is open" || echo "Port $port is closed"
done
```
### **Explanation:**
- **`/dev/tcp/$1/$port`** → Uses **Bash TCP sockets** to check port status.
- **`>/dev/null 2>&1`** → Suppresses errors for closed ports.
- **`echo "Port $port is open"`** → Prints open ports.

### **Executing the Script:**
```bash
chmod +x portscan.sh
./portscan.sh 192.168.1.1 80-100  # Scan ports 80-100
```

---

## 🔹 Script for Automated Backups
```bash
#!/bin/bash
BACKUP_DIR="$HOME/backup"
mkdir -p $BACKUP_DIR
tar -czf $BACKUP_DIR/backup_$(date +%F).tar.gz $HOME/Documents
```

### **Explanation:**
- **`mkdir -p $BACKUP_DIR`** → Creates backup directory if not exists.
- **`tar -czf`** → Compresses files into a `.tar.gz` archive.
- **`$(date +%F)`** → Appends current date to backup file name.

### **Executing the Script:**
```bash
chmod +x backup.sh
./backup.sh
```

---

## 🔹 Conclusion
Bash scripting is a powerful tool for **networking, automation, and security tasks**. This guide covered:
- **Ping sweeps & Nmap automation**
- **Loops, arguments (`$1`), and conditionals**
- **Useful scripts for scanning & backups**

