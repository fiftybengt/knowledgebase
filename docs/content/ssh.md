# SSH (Secure Shell) Guide

##  Introduction to SSH
**SSH (Secure Shell)** is a cryptographic network protocol used for **secure remote login and file transfers** over an unsecured network. It replaces older protocols like **Telnet and FTP** by providing **encryption and authentication**.

### **Ports Used by SSH:**
- **Default Port:** `22`
- Can be changed in `/etc/ssh/sshd_config` for security purposes.

### **Common Use Cases:**
- Secure **remote access** to a server.
- **Tunneling** traffic through SSH.
- **File transfers** using SCP and SFTP.
- **Port forwarding** for secure access to internal services.

---

##  Connecting to an SSH Server
### **Basic SSH Connection**
```bash
ssh username@192.168.1.1
```
- **`username`** → The user on the remote machine.
- **`192.168.1.1`** → The IP address or hostname of the SSH server.

### **Using a Custom Port**
```bash
ssh -p 2222 username@192.168.1.1
```
- **`-p 2222`** → Specifies a non-default SSH port.

### **Using an SSH Key for Authentication**
SSH keys offer a more secure alternative to passwords.
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa
ssh-copy-id -i ~/.ssh/id_rsa.pub username@192.168.1.1
```
- **`ssh-keygen`** → Generates a new RSA SSH key pair.
- **`ssh-copy-id`** → Copies the public key to the remote server.

---

##  File Transfers via SSH
### **Using SCP (Secure Copy Protocol)**
```bash
scp file.txt username@192.168.1.1:/home/username/
```
- Copies `file.txt` from local to the remote server.

```bash
scp username@192.168.1.1:/home/username/file.txt ./
```
- Copies `file.txt` from the remote server to the local machine.

### **Using SFTP (SSH File Transfer Protocol)**
```bash
sftp username@192.168.1.1
```
- Starts an interactive session similar to FTP.
- Use `get file.txt` to download a file.
- Use `put file.txt` to upload a file.

---

##  Port Forwarding with SSH
SSH can tunnel traffic securely by forwarding ports.

### **Local Port Forwarding**
Forwards a local port to a remote system.
```bash
ssh -L 8080:localhost:80 username@192.168.1.1
```
- Access `http://localhost:8080/` to securely reach the remote system’s port `80`.

### **Remote Port Forwarding**
Allows external access to a local service.
```bash
ssh -R 2222:localhost:22 username@192.168.1.1
```
- Remote users can SSH into the local machine using `ssh -p 2222 localhost`.

### **Dynamic Port Forwarding (SOCKS Proxy)**
Creates a **SOCKS proxy** to route all traffic securely.
```bash
ssh -D 9050 -N username@192.168.1.1
```
- Set your browser to use `localhost:9050` as a proxy.

---

##  Hardening SSH Security
### **Disable Root Login**
Edit `/etc/ssh/sshd_config` and set:
```ini
PermitRootLogin no
```
Then restart SSH:
```bash
sudo systemctl restart sshd
```

### **Change Default SSH Port**
Edit `/etc/ssh/sshd_config` and modify:
```ini
Port 2222
```
Restart SSH after changes:
```bash
sudo systemctl restart sshd
```

### **Use Key-Based Authentication**
Disable password-based logins by setting:
```ini
PasswordAuthentication no
```

### **Fail2Ban for SSH Protection**
Fail2Ban blocks repeated failed SSH login attempts.
```bash
sudo apt install fail2ban
```
- **Config File:** `/etc/fail2ban/jail.local`
- Enable SSH protection:
```ini
[sshd]
enabled = true
port = 22
bantime = 600
maxretry = 5
```
Restart Fail2Ban:
```bash
sudo systemctl restart fail2ban
```

---

##  SSH Enumeration & Penetration Testing
### **Enumerate SSH Version**
```bash
nmap -p 22 --script ssh-hostkey,sshv1 192.168.1.1
```
- Checks for outdated **SSH versions** and **weak keys**.

### **Brute Force SSH Credentials with Hydra**
```bash
hydra -l root -P rockyou.txt 192.168.1.1 ssh
```
- **`-l root`** → Attempts login as root.
- **`-P rockyou.txt`** → Uses a wordlist for password guessing.

### **Check for Weak SSH Keys**
```bash
ssh-audit 192.168.1.1
```
- Scans for weak cryptographic algorithms in SSH configuration.

---

##  Conclusion
SSH is an essential tool for **secure remote administration**, but it must be **properly configured** to prevent unauthorized access. Hardening SSH, using **key-based authentication**, and **limiting root login** are critical steps for securing SSH servers.

