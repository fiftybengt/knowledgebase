# Mapping Hostnames to IPs Using /etc/hosts

## Introduction
When performing **penetration testing** or **web reconnaissance**, there are cases where a domain name does not resolve correctly, or a target system uses **virtual hosting**. By modifying the `/etc/hosts` file, you can **manually map an IP address to a hostname**, allowing you to interact with the domain without relying on external DNS resolution.

This technique is **particularly useful** when a target application has **multiple virtual hosts** or when conducting **subdomain enumeration** and **fuzzing attacks**.

---

## Editing /etc/hosts
The `/etc/hosts` file is a system file that **maps IP addresses to hostnames manually**. When a hostname is added to this file, the system resolves it **before querying external DNS servers**.

### Syntax:
```plaintext
<IP Address> <Hostname>
```

### Example Command:
```bash
echo "10.129.99.11 thetoppers.tbh" | sudo tee -a /etc/hosts
```

### Breakdown:
- **`echo "10.129.99.11 thetoppers.tbh"`** → Prepares the entry.
- **`sudo tee -a /etc/hosts`** → Appends (`-a`) the entry to `/etc/hosts` with elevated privileges.

---

## Why Modify /etc/hosts?
- **Bypass DNS Resolution**: If the target server does not have a public DNS record, adding the hostname manually allows direct access.
- **Enable Virtual Host Enumeration**: Some websites serve different content based on the hostname. By modifying `/etc/hosts`, you can interact with these vhosts.
- **Improve Web Fuzzing & Recon**: Many fuzzing tools (e.g., **FFUF, Gobuster, and Wfuzz**) require proper domain resolution for effective scanning.
- **Useful for Internal Networks**: When working inside an internal network, mapping known IPs to hostnames can simplify testing.

---

## Practical Use Cases
### 1. Browsing a Target Web Application
After adding an entry to `/etc/hosts`, you can now access the target domain in your browser:
```bash
firefox http://thetoppers.tbh
```

### 2. Using Curl for HTTP Requests
```bash
curl -I http://thetoppers.tbh
```

### 3. Fuzzing Virtual Hosts with FFUF
```bash
ffuf -u http://FUZZ.thetoppers.tbh -w /usr/share/wordlists/wfuzz/general/common.txt
```

### 4. Scanning the Target with Nmap
```bash
nmap -p 80,443 thetoppers.tbh
```

### 5. Testing with Wfuzz
```bash
wfuzz -c -w /usr/share/wordlists/wfuzz/general/common.txt --hc 404 http://thetoppers.tbh/FUZZ
```

---

## Best Practices
- **Always Backup `/etc/hosts` Before Editing**
  ```bash
  sudo cp /etc/hosts /etc/hosts.bak
  ```
- **Remove Unnecessary Entries After Testing**
  ```bash
  sudo sed -i '/thetoppers.tbh/d' /etc/hosts
  ```
- **Ensure Proper Permissions**
  ```bash
  ls -l /etc/hosts  # Should be writable by root only
  ```

---

## Conclusion
Manually mapping an IP address to a hostname using `/etc/hosts` is a **powerful technique** for **pentesting**, **virtual host enumeration**, and **web fuzzing**. This method allows **bypassing DNS dependencies**, improving **scanning accuracy**, and testing **subdomains efficiently**.

Use it wisely in authorized security assessments to **enhance reconnaissance capabilities**.

