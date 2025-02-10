# Python Networking & Socket Programming Guide

## 🔹 Shebang for Python Scripts
The **shebang** (`#!`) tells the system which interpreter to use when executing a script.

For Python 3, use:
```python
#!/usr/bin/env python3
```
This ensures the script runs with the default `python3` interpreter in the system’s environment.

---

## 🔹 Importing & Using the `socket` Module
The **`socket`** module in Python allows for low-level networking. A socket provides a communication endpoint between two systems.

### **Common Socket Types**:
- **`AF_INET`** → IPv4 addressing.
- **`AF_INET6`** → IPv6 addressing.
- **`SOCK_STREAM`** → TCP (connection-oriented, reliable streaming).
- **`SOCK_DGRAM`** → UDP (connectionless, faster but unreliable).

### **Basic Socket Script**
```python
#!/usr/bin/env python3
import socket

# Create a TCP socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Define server details
host = '127.0.0.1'  # Localhost
port = 8080

# Bind socket to an address and port
s.bind((host, port))

# Start listening for connections (backlog of 5)
s.listen(5)
print(f"[*] Listening on {host}:{port}")

# Accept connections
target, addr = s.accept()
print(f"[+] Connection received from {addr}")
target.send(b'Hello, you are connected!')
target.close()
```

### **Explanation:**
1. **`socket.socket(socket.AF_INET, socket.SOCK_STREAM)`** → Creates an **IPv4 TCP socket**.
2. **`s.bind((host, port))`** → Binds the socket to a local IP and port.
3. **`s.listen(5)`** → Listens for incoming connections with a backlog of 5.
4. **`s.accept()`** → Accepts a new connection and returns the target socket and address.
5. **`target.send()`** → Sends a response to the connected client.

---

## 🔹 `nc -nvlp` Terminal Command Explained
`nc -nvlp <port>` is a **Netcat** command used to **listen for incoming connections**.
```bash
nc -nvlp 8080
```
### **Breakdown:**
- **`-n`** → No DNS resolution (faster lookup).
- **`-v`** → Verbose mode (shows detailed output).
- **`-l`** → Listen mode (waits for incoming connections).
- **`-p`** → Specifies the port number.

This is useful for testing socket scripts by opening a listener on a port and waiting for incoming connections.

---

## 🔹 Python Port Scanner
A **simple Python script** to scan for **open ports** on a target machine.

```python
#!/usr/bin/env python3
import socket

# Define target IP
host = "127.0.0.1"  # Change this to the target IP
ports = [22, 80, 443, 8080]  # List of ports to scan

for port in ports:
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(1)  # Timeout to prevent hanging
    result = s.connect_ex((host, port))  # 0 = open, other = closed
    if result == 0:
        print(f"[+] Port {port} is open")
    else:
        print(f"[-] Port {port} is closed")
    s.close()
```

### **Explanation:**
1. **Defines a target IP and a list of common ports**.
2. **Creates a new socket for each port scan**.
3. **`connect_ex((host, port))`** → Returns `0` if the port is open.
4. **Prints the result** (open or closed).

### **Running the Scanner**
```bash
chmod +x scanner.py
./scanner.py
```
This will output which ports are **open or closed** on the target machine.

---

## 🔹 Conclusion
Python’s `socket` module allows for powerful **network programming**, from creating simple **server-client** connections to **port scanning**. Understanding **Netcat (`nc`), socket types, and proper implementation** is key for networking and cybersecurity applications.

