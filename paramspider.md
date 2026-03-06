# paramspider

## What it is
A tool by devanshbatham for mining parameters from web archives (Wayback Machine). Essential for discovering hidden parameters vulnerable to XSS, SQLi, or SSRF.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-d` | Target domain |
| `-s` | Subdomain inclusion (set to false to exclude) |
| `-l` | List of domains to scan |
| `-e` | Extensions to exclude (e.g. woff,css,png) |
| `-o` | Output file |

---

## Examples

**Basic parameter mining for a domain**
```bash
paramspider -d example.com
```

**Mine parameters and exclude useless extensions**
```bash
paramspider -d example.com --exclude woff,css,js,png,svg,jpg
```

**Scan a list of domains**
```bash
paramspider -l domains.txt
```

**Save output to a specific file**
```bash
paramspider -d example.com -o params.txt
```
