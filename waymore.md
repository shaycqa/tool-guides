# waymore

## What it is
A tool by xnl-h4ck3r used to discover URLs and download archived responses from multiple sources like the Wayback Machine, Common Crawl, Alien Vault OTX, and more. It effectively finds 'way more' than traditional Wayback tools.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-i` | Target domain or URL |
| `-mode` | Mode of operation: U (URLs only), R (Responses only), or B (Both) |
| `-n` | Do not include subdomains in the search |
| `-oU` | Specify a custom file path for the URL output |
| `-from` | Start date for the search (e.g., 2023) |
| `-to` | End date for the search (e.g., 2024) |
| `-xwm` | Exclude Wayback Machine from search |

---

## Examples

**Get all URLs for a domain (fastest)**
```bash
waymore -i example.com -mode U
```

**Download the last 50 archived responses for a specific path**
```bash
waymore -i example.com/admin -mode R -l -50
```

**Search within a specific date range**
```bash
waymore -i example.com -from 2022 -to 2024
```

**Pipe results to other tools**
```bash
waymore -i example.com -mode U | unfurl keys | sort -u
```


## Important Setup & Advanced Tips
- **API Keys**: Edit the `config.yml` (usually in `~/.config/waymore/`) to add keys for URLScan and VirusTotal for maximum coverage.
- **Memory Management**: If dealing with a massive scope, use `-mode U` first, filter the URLs, and only download responses (`-mode R`) for the interesting ones.
- **Filtering**: Waymore automatically handles some deduplication, but piping through `uro` is still recommended.


## Input & Output Examples

**Input File (`domains.txt`)**
```text
example.com
test.com
```

**Output File (`waymore_urls.txt`)**
```text
https://example.com/assets/main.js
https://example.com/api/v1/users?id=1
https://test.com/admin/login.php
```
