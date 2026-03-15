# Information Gathering Tools

##  Introduction
Information gathering, also known as **reconnaissance**, is the first phase in penetration testing. It involves collecting **publicly available data** about a target before attempting an attack. The goal is to identify weaknesses, technologies in use, and potential entry points.

---

##  Useful Reconnaissance Tools & Websites

### **1️ Email & Breach Lookup**
#### **Hunter.io**
- **Use Case**: Finds publicly available emails associated with a domain.
- **Website**: [https://hunter.io](https://hunter.io)
- **Example Usage**:
  - Search a company domain and get a list of associated emails.
  - Identify email patterns (e.g., `firstname.lastname@company.com`).

#### **Have I Been Pwned**
- **Use Case**: Checks if an email or password has been compromised in data breaches.
- **Website**: [https://haveibeenpwned.com](https://haveibeenpwned.com)
- **Example Usage**:
  - Check if a target email appears in a past breach.
  - Find breached passwords that may be used elsewhere.

---

### **2️ Subdomain Enumeration**
#### **Sublist3r**
- **Use Case**: Finds subdomains of a target domain.
- **Command:**
  ```bash
  sublist3r -d example.com
  ```
- **Why It's Useful**:
  - Identifies alternative entry points.
  - Reveals test/staging environments that may be misconfigured.

#### **crt.sh**
- **Use Case**: Queries **Certificate Transparency Logs** for subdomains.
- **Website**: [https://crt.sh](https://crt.sh)
- **Why It's Useful**:
  - Finds subdomains from SSL certificates.
  - Identifies internal infrastructure if leaked.

#### **OWASP Amass**
- **Use Case**: Automated asset discovery and subdomain enumeration.
- **Command:**
  ```bash
  amass enum -d example.com
  ```
- **Why It's Useful**:
  - Uses multiple data sources for thorough enumeration.
  - Can perform passive and active recon.

---

### **3️ Technology Fingerprinting**
#### **BuiltWith**
- **Use Case**: Identifies the technologies used on a website.
- **Website**: [https://builtwith.com](https://builtwith.com)
- **Why It's Useful**:
  - Reveals CMS, JavaScript frameworks, hosting providers.
  - Identifies outdated or vulnerable software.

#### **WhatWeb**
- **Use Case**: A Linux tool for website reconnaissance.
- **Command:**
  ```bash
  whatweb example.com
  ```
- **Why It's Useful**:
  - Identifies web technologies and security configurations.
  - Can detect CMS, server type, analytics tools.

---

### **4️ HTTP/S Traffic Analysis**
#### **Burp Suite**
- **Use Case**: Web application security testing tool.
- **Capabilities**:
  - **Intercept HTTP/S traffic** between browser and server.
  - **Modify requests** for testing vulnerabilities (e.g., SQL Injection, XSS).
  - **Spider and crawl websites** for security flaws.
  - **Brute-force logins** and test credentials.
- **Why It's Useful**:
  - Essential for **manual testing** and deep web application security analysis.

---

### **5️ Google Dorking (Google-Fu)**
Google’s search operators help find **sensitive information** online.

#### **Common Google Dorks:**
| Operator  | Example | Use Case |
|-----------|----------------------------------|----------------------------------|
| `site:`   | `site:example.com` | Show results from a specific site |
| `filetype:` | `filetype:pdf site:example.com` | Find PDFs on a website |
| `intitle:` | `intitle:"Index of /"` | Look for open directories |
| `inurl:`  | `inurl:admin login` | Find admin panels |
| `ext:`    | `ext:log OR ext:txt` | Search for log or text files |
| `cache:`  | `cache:example.com` | View Google’s cached version |
| `intext:` | `intext:"Confidential" site:example.com` | Search for keywords on a site |

---

### **6️ Additional Reconnaissance Tools**
#### **TomNomNom’s Tools**
TomNomNom is a security researcher who has created powerful recon tools:
- **`assetfinder`** → Finds subdomains from multiple sources.
- **`httprobe`** → Checks which found subdomains are alive.
- **`waybackurls`** → Extracts URLs from the Wayback Machine.
- **Example usage:**
  ```bash
  assetfinder example.com | httprobe
  ```
  - Finds subdomains and checks which are alive.

#### **Shodan**
- **Use Case**: The “Google for hackers” that scans the internet for open services.
- **Website**: [https://www.shodan.io](https://www.shodan.io)
- **Why It's Useful**:
  - Finds **open ports, services, cameras, and IoT devices**.
  - Can identify **exposed industrial control systems**.

#### **FOFA**
- **Use Case**: A Shodan alternative, often used by researchers.
- **Website**: [https://fofa.info](https://fofa.info)
- **Why It's Useful**:
  - Searches for **web services and leaked assets**.

---

##  Conclusion
Reconnaissance is an essential phase in security assessments. Using the right tools and techniques can help gather **valuable intelligence** on a target. By leveraging **Google Dorking, subdomain enumeration, breach lookups, and traffic analysis**, professionals can uncover hidden vulnerabilities before an attack occurs.



