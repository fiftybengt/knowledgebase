# Linux - Users and Privileges

##  Understanding File Permissions (`ls -la` & `drwxrwxrwx`)

In Linux, file and directory permissions are fundamental for security and access control. You can view permissions using:

```bash
ls -la
```

This command lists all files, including **hidden files**, along with their permissions. Example output:

```bash
drwxr-xr--  3 user group 4096 Feb 8 10:00 myfolder
-rw-r--r--  1 user group  123 Feb 8 10:01 myfile.txt
```

### **Breaking Down `drwxr-xr--`**
Each file or directory has a permission structure consisting of **three parts:**

| Section      | Represents      | Example |
|-------------|---------------|---------|
| **First character** | Type (directory/file) | `d` (directory), `-` (file), `l` (symlink) |
| **Next 3 (`rwx`)** | Owner permissions | `r` (read), `w` (write), `x` (execute) |
| **Next 3 (`r-x`)** | Group permissions | Similar to owner section |
| **Last 3 (`r--`)** | Others (everyone else) | Similar to previous sections |

Example:
- **`drwxr-xr--`** → Directory (`d`), owner has full rights (`rwx`), group has read & execute (`r-x`), others have read (`r--`).
- **`-rw-r--r--`** → Regular file, readable by everyone but writable only by owner.

---

##  Changing Permissions with `chmod`
**`chmod` (Change Mode)** modifies file permissions.

### **Using Numeric Mode (Octal Representation)**
Each permission type corresponds to a number:

| Permission | Binary | Octal Value |
|------------|--------|------------|
| `r--` (read) | 100 | 4 |
| `-w-` (write) | 010 | 2 |
| `--x` (execute) | 001 | 1 |
| `rwx` (full access) | 111 | 7 |

To grant **full access (777) to all users**:
```bash
chmod 777 myfile.txt
```

Example usage:
- `chmod 755 script.sh` → Owner can **read, write, execute**, others can **read and execute**.
- `chmod 644 document.txt` → Owner can **read & write**, others can **read only**.

### **Using Symbolic Mode**
Instead of numbers, you can use `u` (user/owner), `g` (group), `o` (others), and `a` (all).
```bash
chmod u+x script.sh  # Give execute permission to the owner
chmod g-w file.txt   # Remove write permission from group
chmod o+r file.txt   # Allow others to read the file
```

---

##  Managing Users
### **Adding a User**
To create a new user and set a password:
```bash
sudo adduser username
```
You'll be prompted to enter details such as **password, full name, and optional info**.

### **Viewing Users in Linux**
Linux users are stored in `/etc/passwd`:
```bash
cat /etc/passwd
```
Each user entry consists of:
```
username:x:1000:1000:Full Name:/home/username:/bin/bash
```

### **Managing Passwords (`/etc/shadow`)**
Passwords are stored in `/etc/shadow` in **hashed format**:
```bash
sudo cat /etc/shadow
```
To **crack password hashes**, tools like **John the Ripper** can be used:
```bash
john --wordlist=rockyou.txt hashfile.txt
```

---

##  Switching Users & Running Commands as Another User
### **Switching Users (`su` & `sudo`)
- `su username` → Switch to another user.
- `su - username` → Switch and load their environment.
- `exit` → Return to the previous user.

### **Using Sudo for Privileged Commands**
Regular users **cannot execute administrative commands** unless they have **sudo** permissions.
To run a command as a superuser:
```bash
sudo apt update
```
To allow a user to use `sudo`, they must be added to the **sudoers file**:
```bash
sudo usermod -aG sudo username
```
To manually edit sudoers (use caution!):
```bash
sudo visudo
```

---

##  Managing User Groups
### **Viewing Groups**
```bash
groups username
cat /etc/group
```
### **Creating & Modifying Groups**
- `sudo groupadd newgroup` → Create a new group.
- `sudo usermod -aG groupname username` → Add user to a group.
- `sudo gpasswd -d username groupname` → Remove user from a group.
- `sudo deluser username` → Remove a user.
- `sudo delgroup groupname` → Remove a group.

---

##  Useful Commands
| Command | Description |
|---------|------------|
| `whoami` | Show current logged-in user |
| `id` | Show user ID and group ID |
| `passwd` | Change user password |
| `finger username` | Get user details (install package if missing) |
| `last` | Show last logged-in users |
| `w` | Show currently logged-in users |
| `sudo !!` | Run the last command with `sudo` |

---

##  Conclusion
Understanding **users, groups, and permissions** is crucial for managing a Linux system securely. Using the correct permission structure, ensuring proper sudo configurations, and managing users effectively prevents unauthorized access and enhances security.


