# subfinder

## What it is
A passive subdomain discovery tool by ProjectDiscovery. Uses +40 online data sources (VirusTotal, Shodan, Censys, etc.) to find subdomains without directly touching the target.

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
