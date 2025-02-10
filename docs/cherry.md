# Using Linux Cherrytree for Documentation

## Introduction
Cherrytree is a powerful **hierarchical note-taking application** that allows penetration testers and security professionals to **document findings, organize research, and store structured data**. It supports **rich text, code highlighting, and encryption**, making it an ideal tool for **security assessments and documentation**.

---

## Installing Cherrytree on Linux
Cherrytree can be installed on most Linux distributions via package managers.

### **Ubuntu/Debian**
```bash
sudo apt update && sudo apt install cherrytree -y
```

### **Arch Linux**
```bash
sudo pacman -S cherrytree
```

### **Kali Linux**
```bash
sudo apt install cherrytree -y
```

### **Flatpak (Any Linux Distribution)**
```bash
flatpak install flathub com.giuspen.cherrytree
```

---

## Navigating Cherrytree
### **1. Creating a New Notebook**
- Open Cherrytree.
- Click **File > New Instance** to create a new notebook.
- Save the file as **pentest-notes.ctb** (or `.ctx` for XML format).

### **2. Organizing Notes with Nodes & Subnodes**
- Click **“+”** to create a new **Node** (acts as a section).
- Right-click a node → **New Subnode** (nested categories).
- Rename nodes by double-clicking.

**Example Folder Structure for Pentesting:**
```
📂 Pentest Engagement
 ├── 🗂️ Recon
 │    ├── Nmap Scan Results
 │    ├── Subdomain Enumeration
 ├── 🗂️ Exploitation
 │    ├── Credentials & Payloads
 │    ├── Exploit PoCs
 ├── 🗂️ Post-Exploitation
 │    ├── Persistence Methods
 │    ├── Data Exfiltration Notes
```

---

## Documenting Findings
### **3. Adding Text & Code Blocks**
- Use **rich text formatting** for headers, bullet points, and highlights.
- Insert **code snippets** with syntax highlighting:
  - Click **Insert > Codebox**.
  - Choose the appropriate language (e.g., Bash, Python, SQL, etc.).

Example:
```bash
nmap -p- -A -T4 target.com
```

### **4. Inserting Images & Attachments**
- Drag & drop images into a node to include screenshots.
- Click **Insert > File** to attach external reports.

### **5. Encrypting Notes for Security**
- Click **File > Password Protection** to **encrypt the entire document**.
- Uses **AES encryption** to protect sensitive information.

### **6. Using Search for Quick Access**
- Use `CTRL + F` to search within notes.
- `CTRL + Shift + F` allows **searching across all nodes**.

---

## Best Practices for Documentation
### **7. Keep Everything Structured**
- Use **consistent naming conventions** for nodes (e.g., `Target - Service - Details`).
- Organize findings logically in **Recon > Exploitation > Post-Exploitation**.

### **8. Timestamp Key Findings**
- Use `CTRL + SHIFT + T` to insert a **timestamp**.
- Helps track when vulnerabilities were found and reported.

### **9. Backup Your Notes**
- Export notes to **plaintext, PDF, or HTML** for backups.
- Store backups securely in an **encrypted volume**.

Example Backup Command:
```bash
tar -czf pentest-notes-backup.tar.gz pentest-notes.ctb
```

### **10. Sync Notes Across Devices**
- Use **Nextcloud, Syncthing, or Encrypted USB** for syncing across machines.
- Avoid storing sensitive Cherrytree files in unencrypted cloud storage.

---

## Conclusion
Cherrytree is a **structured, secure, and versatile** note-taking tool for penetration testers and cybersecurity professionals. By following **best practices**, you can effectively document and protect findings throughout an assessment.

Stay organized, document findings properly, and secure your notes efficiently.

