# gau

## What it is
Get All URLs (gau) fetches known URLs from AlienVault's Open Threat Exchange, the Wayback Machine, and Common Crawl for any given domain.

## Installation
```bash
go install github.com/lc/gau/v2/cmd/gau@latest
```

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


## Important Setup & Advanced Tips
- **Configuration**: Create a `~/.gau.toml` file to add API keys for URLScan, VirusTotal, and OTX to get significantly more results.
- **Thread Tuning**: Default threads might be too low or too high. Adjust `--threads` based on your network speed.
- **Combine with Uro**: Always pipe `gau` output into `uro` to remove noisy and duplicate URLs.


## Input & Output Examples

**Input File (`domains.txt`)**
```text
example.com
test.com
```

**Output File (`urls.txt`)**
```text
https://example.com/about
https://example.com/api/v1/users?id=1
https://test.com/admin/login.php
```


## Professional Tips & Tricks
- **Provider Tuning**: If you are in a rush, limit the providers. OTX and URLScan are usually faster than Wayback Machine: `--providers otx,urlscan`.
- **JSON Output**: Always use `--json` when building automated pipelines so you can extract HTTP status codes and MIME types directly with `jq`.
