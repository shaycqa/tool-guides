# ffuf

## What it is
Fuzz Faster U Fool — a fast web fuzzer for directory/file discovery, parameter fuzzing, subdomain enumeration, and vhost fuzzing. Uses `FUZZ` as a placeholder in the URL.

## Installation
```bash
go install github.com/ffuf/ffuf/v2@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-u` | Target URL (`FUZZ` marks the injection point) |
| `-w` | Wordlist path |
| `-H` | Custom header |
| `-X` | HTTP method |
| `-d` | POST body data |
| `-fc` | Filter by response code |
| `-mc` | Match by response code |
| `-fs` | Filter by response size |
| `-fw` | Filter by word count |
| `-r` | Follow redirects |
| `-recursion` | Recursive scanning |
| `-o` | Output file |
| `-of` | Output format (json, csv, html) |
| `-t` | Threads (default 40) |
| `-p` | Proxy |

---

## Examples

**Directory/file fuzzing**
```bash
ffuf -u http://example.com/FUZZ -w /opt/SecLists/Discovery/Web-Content/common.txt
```
*Discovers hidden paths and files.*

**Filter out 404 responses**
```bash
ffuf -u http://example.com/FUZZ -w wordlist.txt -fc 404
```

**Recursive scan**
```bash
ffuf -u http://example.com/FUZZ -w wordlist.txt -recursion
```

**Subdomain fuzzing**
```bash
ffuf -u http://FUZZ.example.com -w subdomains.txt -H "Host: FUZZ.example.com"
```

**Vhost fuzzing**
```bash
ffuf -u http://10.10.10.1 -H "Host: FUZZ.example.com" -w wordlist.txt -fs 0
```
*`-fs 0` filters zero-size responses (invalid vhosts).*

**GET parameter fuzzing**
```bash
ffuf -u http://example.com/search?q=FUZZ -w payloads.txt
```

**POST body fuzzing**
```bash
ffuf -u http://example.com/login -X POST \
  -d "username=admin&password=FUZZ" -w passwords.txt -fc 401
```

**Route through Burp**
```bash
ffuf -u http://example.com/FUZZ -w wordlist.txt -p http://127.0.0.1:8080
```


## Important Setup & Advanced Tips
- **Auto-Calibration**: Always use `-ac` to automatically calibrate filtering for custom 404s and WAF blocks.
- **Multiple Fuzz Points**: You can use multiple wordlists by specifying variables: `-w users.txt:W1 -w passwords.txt:W2 -u http://target/W1/W2`.
- **Match/Filter by Regex**: Use `-mr` or `-fr` to match/filter responses containing specific strings or regex patterns.


## Input & Output Examples

**Input File (`wordlist.txt`)**
```text
admin
login
api
dashboard
```

**Output File (`results.json` or CLI output)**
```text
admin                   [Status: 403, Size: 250, Words: 10, Lines: 5]
login                   [Status: 200, Size: 1540, Words: 120, Lines: 45]
api                     [Status: 301, Size: 0, Words: 1, Lines: 1]
```
