# httpx

## What it is
A fast HTTP probing tool by ProjectDiscovery. Takes a list of hosts and checks which ones are alive, while also extracting titles, status codes, technologies, and more.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-l` | Input file with hosts |
| `-title` | Show page title |
| `-status-code / -sc` | Show HTTP status code |
| `-tech-detect` | Detect web technologies |
| `-follow-redirects` | Follow HTTP redirects |
| `-location` | Show redirect location |
| `-cl` | Content length |
| `-ct` | Content type |
| `-server` | Show server header |
| `-ip` | Show resolved IP |
| `-cdn` | Detect CDN/WAF |
| `-path` | Probe a specific path |
| `-probe` | Show success/fail status |
| `-silent` | Only print results |
| `-o` | Output file |
| `-json` | JSON output |

---

## Examples

**Basic probe on a single host**
```bash
echo "https://example.com" | httpx
```

**Probe with title, status code, and tech detection**
```bash
echo "https://example.com" | httpx -title -status-code -tech-detect
```

**Probe a list of hosts**
```bash
httpx -l hosts.txt -title -status-code -tech-detect -follow-redirects
```

**Pipe from subfinder**
```bash
subfinder -d example.com -silent | httpx -title -status-code
```
*Discover live subdomains from passive recon.*

**Check if /robots.txt exists**
```bash
httpx -l hosts.txt -path /robots.txt -sc
```

**Get IP, CDN, and server info**
```bash
echo "https://example.com" | httpx -ip -cdn -server
```

**Full recon pipeline**
```bash
subfinder -d example.com -silent | httpx -silent | nuclei -t cves/
```

**Save output to file**
```bash
httpx -l hosts.txt -title -sc -o live_hosts.txt
```


## Important Setup & Advanced Tips
- **Title & Tech**: Use `-title` and `-tech-detect` (powered by wappalyzer) to quickly identify the software running on the hosts.
- **Status Code Filtering**: Only keep alive/interesting endpoints: `-mc 200,301,302,403`.
- **Follow Redirects**: By default `httpx` doesn't follow redirects. Use `-fr` to follow them to the final destination.
