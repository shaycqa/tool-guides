# naabu

## What it is
A fast port scanner by ProjectDiscovery. Designed for speed and easy integration into recon pipelines. Supports SYN, CONNECT, and UDP scanning with nmap integration for service detection.

## Installation
```bash
go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-host` | Target host(s) |
| `-list / -l` | File with list of hosts |
| `-p` | Port(s) to scan (e.g., `80,443` or `1-1000`) |
| `-top-ports` | Scan top N ports (`100`, `1000`) |
| `-exclude-ports` | Exclude specific ports |
| `-rate` | Packets per second (default: 1000) |
| `-silent` | Only print results |
| `-o` | Output file |
| `-json` | JSON output |
| `-nmap-cli` | Pass results to nmap for service scan |
| `-passive` | Use Shodan InternetDB (no active scan) |
| `-Pn` | Skip host discovery |

---

## Examples

**Scan a single host (top 100 ports)**
```bash
naabu -host example.com -top-ports 100
```

**Scan specific ports**
```bash
naabu -host example.com -p 80,443,8080,8443
```

**Scan a list of hosts**
```bash
naabu -l hosts.txt -top-ports 1000 -o open_ports.txt
```

**Pipe from subfinder**
```bash
subfinder -d example.com -silent | naabu -silent
```
*Discover subdomains then scan their ports.*

**Full pipeline: subdomains → ports → http probe**
```bash
subfinder -d example.com -silent | naabu -silent | httpx -title -sc
```

**Passive scan using Shodan (no packets sent)**
```bash
naabu -host example.com -passive
```

**Pipe into nmap for service detection**
```bash
naabu -host example.com -p 80,443 -nmap-cli "nmap -sV -sC"
```

**High-speed scan with custom rate**
```bash
naabu -l hosts.txt -rate 5000 -top-ports 100 -silent -o results.txt
```


## Important Setup & Advanced Tips
- **Nmap Integration**: You can pipe naabu's fast port discovery directly into nmap for deep service fingerprinting using the `-nmap` flag.
- **CDN Exclusion**: By default, naabu excludes CDN IPs (Cloudflare, Akamai) to avoid scanning their entire edge network. Use `-exclude-cdn`.
- **Host Discovery**: Use `-host-discovery` to do a quick ping sweep before doing deep port scans.


## Input & Output Examples

**Input File (`hosts.txt`)**
```text
192.168.1.15
example.com
```

**Output File (`ports.txt`)**
```text
192.168.1.15:80
192.168.1.15:443
example.com:8443
```
