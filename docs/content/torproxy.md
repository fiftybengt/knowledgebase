# Connecting to Tor via Proxychains

## Introduction
**ProxyChains** is a tool that routes network traffic through **multiple proxies**, including **Tor**, to **anonymize** connections. This guide covers how to configure ProxyChains and use it with Tor for enhanced privacy.

**Warning:** While ProxyChains and Tor improve anonymity, they are **not foolproof**. Always follow best practices to avoid leaks.

---

## Installing Tor & ProxyChains
### Install Tor
```bash
sudo apt update && sudo apt install tor -y
```
- **Tor** routes your traffic through an **encrypted onion network**.

### Install ProxyChains
```bash
sudo apt install proxychains
```
- **ProxyChains** forces applications to route traffic through proxies (Tor, SOCKS, HTTP, etc.).

---

## Configuring ProxyChains
### Edit ProxyChains Configuration File
```bash
sudo nano /etc/proxychains.conf
```
- Scroll to the **bottom** and ensure the following lines are set:

#### Important Configurations:
```ini
strict_chain
proxy_dns
socks5 127.0.0.1 9050  # Tor default SOCKS proxy
```
- **`strict_chain`** → Forces traffic through each proxy in the order listed.
- **`proxy_dns`** → Prevents DNS leaks.
- **`socks5 127.0.0.1 9050`** → Directs traffic through Tor’s SOCKS5 proxy.

### Save & Exit
- Press **CTRL + X**, then **Y**, then **ENTER** to save the changes.

---

## Starting Tor & Using ProxyChains
### Start the Tor Service
```bash
sudo systemctl start tor
```
- To enable Tor at boot:
  ```bash
  sudo systemctl enable tor
  ```
- To check the status:
  ```bash
  systemctl status tor
  ```

### Running Applications Through ProxyChains
#### Check IP Address Before & After
```bash
curl ifconfig.me
proxychains curl ifconfig.me
```
- The second command should return a **Tor exit node IP**.

#### Browse Anonymously Using Firefox
```bash
proxychains firefox
```

#### Run Nmap Through Tor (Stealth Scan)
```bash
proxychains nmap -sT -Pn -n <target>
```
- **`-sT`** → TCP Connect Scan (Tor does not support SYN scans `-sS`).
- **`-Pn`** → No Ping (Tor blocks ICMP requests).
- **`-n`** → Disables DNS resolution (prevents leaks).

---

## Additional Tips
- **Use `proxychains -q`** to suppress ProxyChains logs.
- **Combine with VPN** for extra security.
- **Modify exit nodes** in `/etc/tor/torrc` for specific geolocations.
- **Use bridges** if Tor is blocked in your country.

---

## Conclusion
ProxyChains with Tor provides an **extra layer of anonymity** for web browsing, network scanning, and other activities. However, **no system is 100% anonymous**, so always use caution.

