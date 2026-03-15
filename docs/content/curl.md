# cURL Reference for API Testing and Pentesting

A concise guide to using `curl` effectively for command-line HTTP interactions, useful in penetration testing, debugging, and scripting.

---

## Core Usage

```bash
curl https://example.com                   # Basic GET request
curl -I https://example.com                # HEAD request (headers only)
curl -o response.html https://example.com  # Save response to file
```

---

## Custom Headers and User Agent

```bash
curl -H "User-Agent: Mozilla/5.0" https://example.com
curl -H "Authorization: Bearer <token>" https://api.example.com/data
```

---

## POST Requests and Data Submission

```bash
# Form data
curl -X POST -d "username=admin&password=1234" https://target.com/login

# JSON payload
curl -X POST -H "Content-Type: application/json" \
     -d '{"user":"admin","pass":"1234"}' https://api.example.com/login
```

---

## File Uploads

```bash
curl -F "file=@payload.zip" https://target.com/upload
```

---

## Cookie Handling

```bash
curl -c cookies.txt https://target.com            # Save cookies
curl -b cookies.txt https://target.com/dashboard  # Send cookies
```

---

## Parsing JSON Output (requires `jq`)

```bash
curl https://ipinfo.io | jq '.ip'
```

---

## Alternate HTTP Methods

```bash
curl -X PUT -d '{"enabled":true}' https://target.com/api/feature
curl -X DELETE https://target.com/api/object/42
```

---

## Using a Proxy (e.g. with Burp Suite)

```bash
curl -x http://127.0.0.1:8080 https://target.com
```

---

## SSL/TLS and Certificate Handling

```bash
curl -v https://example.com               # Verbose SSL info
curl --insecure https://self-signed.site # Skip SSL verification (for testing only)
```

---

## DNS Overrides

```bash
curl --resolve example.com:443:10.0.0.5 https://example.com
```

> Useful for testing services before DNS records are live.

---

## Compression and Redirects

```bash
curl --compressed https://target.com     # Accept gzip/deflate
curl -L https://short.url                # Follow redirects
```

---

## Timing, Debugging, and Logging

```bash
curl -w "@format.txt" -o /dev/null -s https://target.com  # Custom output format
curl --trace-ascii trace.log https://target.com           # Log full request/response
```

---

## Tips

- Use `man curl` or `curl --help` to explore all available options.
- Combine with tools like `jq`, `grep`, or `awk` for advanced processing.
- Store common requests in scripts for repeatable testing.
- `curl` is stateless — use it to replicate and isolate HTTP behavior precisely.

---

## Example: GitHub API Query

```bash
curl https://api.github.com/users/octocat | jq '.public_repos'
```

Retrieves the number of public repositories for the specified GitHub user.

---
End of Reference

