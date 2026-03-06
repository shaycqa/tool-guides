# gau

## What it is
Get All URLs (gau) fetches known URLs from AlienVault's Open Threat Exchange, the Wayback Machine, and Common Crawl for any given domain.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `--threads` | Number of workers to use |
| `--subs` | Include subdomains of target domain |
| `--json` | Output as JSON |
| `--o` | Output file |
| `--providers` | Specific data providers to use (wayback,otx,commoncrawl) |
| `--blacklist` | Extensions to skip (e.g., png,jpg,gif) |

---

## Examples

**Fetch URLs for a domain**
```bash
gau example.com
```

**Fetch URLs including all subdomains**
```bash
gau --subs example.com
```

**Save results to a file**
```bash
gau example.com --o urls.txt
```

**Filter out image and font extensions**
```bash
gau example.com --blacklist png,jpg,jpeg,gif,svg,woff,woff2
```

**Pipe domains from a file**
```bash
cat domains.txt | gau --threads 5
```
