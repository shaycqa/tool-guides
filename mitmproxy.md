# mitmproxy / mitmdump

## What it is
An interactive, SSL/TLS-capable intercepting HTTP proxy for penetration testers and software developers. The suite includes `mitmproxy` (interactive console), `mitmweb` (web-based UI), and `mitmdump` (command-line, tcpdump-like output). It is a highly scriptable alternative to Burp Suite, excelling at mobile app testing, thick client analysis, and headless automation.

## Installation
```bash
sudo apt install mitmproxy
```

---

## Key Flags (`mitmdump`)
| Flag | Description |
|------|-------------|
| `-w <file>` | Save captured traffic to a file for later analysis. |
| `-r <file>` | Read and replay flows from a saved file. |
| `-s <script.py>` | Run a Python script (Addon) to modify traffic on the fly. |
| `--anticache` | Strips headers like `If-None-Match` to force full `200 OK` responses instead of `304 Not Modified`. |
| `--anticomp` | Prevents servers from sending compressed (gzip) data, ensuring the body is readable in scripts. |
| `--ssl-insecure` / `-k` | Skips SSL certificate verification for upstream servers. |
| `--mode transparent` | Captures traffic redirected at the OS level (e.g., via `iptables`), useful for proxy-unaware apps. |
| `--ignore-hosts <regex>` | Prevents interception of specific domains (e.g., `^google\.com$`), reducing noise. |
| `-p <port>` | Specify the port to listen on (default is 8080). |

---

## Filter Expressions (Cheat Sheet)
Mitmproxy uses powerful filter expressions. Append these directly to your command (e.g., `mitmdump "~m POST"`).

| Filter | Description |
| :--- | :--- |
| `~u <regex>` | Match a specific URL pattern. |
| `~d <domain>`| Match a specific domain. |
| `~q` | Match only requests (useful for interception). |
| `~s` | Match only responses. |
| `~m <method>` | Match HTTP methods (e.g., `~m POST`). |
| `~b <regex>` | Match a string within the request or response body. |
| `~h <regex>` | Match specific headers (e.g., `~h "Authorization: Bearer"`). |
| `!(~a)` | Hides assets (CSS, JS, images) to focus on API/HTML traffic. |

---

## Examples

**Basic proxy on custom port**
```bash
mitmdump -p 8888
```

**Save all traffic to a file**
```bash
mitmdump -w traffic.flow
```

**Filter for specific domain and status code**
```bash
mitmdump "~d target.com & ~c 404"
```

**Find API keys in responses using regex**
```bash
mitmdump -q --anticomp "~b (AIza[0-9A-Za-z-_]{35})"
```

**Run a custom Python modification script**
```bash
mitmdump -s injector.py
```

---

## Input & Output Examples

**Input Script (`logger.py`)**
```python
from mitmproxy import http

def response(flow: http.HTTPFlow):
    auth = flow.request.headers.get("Authorization")
    if auth:
        print(f"[!] Found Token for {flow.request.url}: {auth}")
```

**Execution**
```bash
mitmdump -s logger.py "~u api.target.com"
```

**Output (CLI)**
```text
127.0.0.1:54321: clientconnect
[!] Found Token for https://api.target.com/v1/user: Bearer eyJhbGci...
127.0.0.1:54321: GET https://api.target.com/v1/user
 << 200 OK 1.2k
```

---

## Professional Tips & Tricks
- **Mobile App Testing**: Pair mitmproxy with **Frida** or **Objection** to bypass SSL pinning. Route the mobile device's traffic through mitmproxy to capture hidden API endpoints that aren't exposed in web browsers.
- **Thick Client Analysis**: Use `--mode transparent` combined with system-level iptables routing to capture traffic from desktop applications that do not respect proxy settings.
- **Auto-Injecting Payloads (Scripting)**: The true power of mitmproxy is the Python API. You can write scripts to automatically append payloads (like `';<script>alert(1)</script>`) to every URL parameter as it passes through the proxy.
- **Response Modification (Bypass)**: You can write scripts to dynamically rewrite JSON responses. E.g., changing `{"is_admin": false}` to `{"is_admin": true}` to test client-side authorization bypasses.
- **The Hybrid Workflow**: Run `mitmdump -w log.flow` in the background to capture everything while you browse the target. Later, load `log.flow` into `mitmweb` (the GUI) to analyze the history, or replay it through Burp Suite.
- **Piping to Nuclei**: Since `mitmdump` can output to `stdout`, you can extract live URLs dynamically and pipe them into vulnerability scanners or `grep` in real-time.
