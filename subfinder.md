# subfinder

## What it is
A passive subdomain discovery tool by ProjectDiscovery. Uses +40 online data sources (VirusTotal, Shodan, Censys, etc.) to find subdomains without directly touching the target.

## Installation
```bash
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-d` | Target domain |
| `-dL` | File with list of domains |
| `-o` | Output file |
| `-oJ` | Output as JSON |
| `-all` | Use all sources (slower but thorough) |
| `-silent` | Only print subdomains (clean output) |
| `-v` | Verbose |
| `-recursive` | Recursively find subdomains |
| `-exclude-sources` | Exclude specific data sources |

---

## Examples

**Basic subdomain discovery**
```bash
subfinder -d example.com
```

**Save results to file**
```bash
subfinder -d example.com -o subdomains.txt
```

**Use all sources for maximum coverage**
```bash
subfinder -d example.com -all -o subdomains.txt
```

**Scan multiple domains from file**
```bash
subfinder -dL domains.txt -o subdomains.txt
```

**Recursive subdomain discovery**
```bash
subfinder -d example.com --recursive -o subdomains.txt
```

**Silent output (clean, for piping)**
```bash
subfinder -d example.com -silent
```

**Pipe into httpx to find live hosts**
```bash
subfinder -d example.com -silent | httpx -silent -o live.txt
```

**Full recon pipeline**
```bash
subfinder -d example.com -silent | httpx -silent | nuclei -t cves/
```
*Subdomain discovery → probe for live hosts → vulnerability scan.*


## Important Setup & Advanced Tips
- **API Configurations**: Subfinder's default sources are decent, but configuring API keys in `~/.config/subfinder/provider-config.yaml` (Shodan, Censys, SecurityTrails, Chaos) dramatically increases results.
- **Chaining**: Standard pipeline: `subfinder -silent -d target.com | httpx -silent > alive.txt`.
- **Recursive Searches**: Use `--recursive` to find sub-subdomains, but be aware this significantly increases scan time.


## Input & Output Examples

**Input File (`domains.txt`)**
```text
example.com
test.com
```

**Output File (`subdomains.txt`)**
```text
api.example.com
dev.example.com
admin.test.com
```


## Professional Tips & Tricks
- **Recursive Bruteforcing**: Combine subfinder with a custom wordlist and dnsx: `subfinder -d target.com -silent | dnsx -silent | awk '{print $1}' > subs.txt`. Then take the resolved subdomains, append wordlist items to them, and resolve again.
- **API Keys are Everything**: A subfinder without API keys misses up to 40% of the attack surface. Prioritize getting keys for Shodan, Censys, SecurityTrails, Chaos, and GitHub.
