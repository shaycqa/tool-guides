# katana

## What it is
A fast web crawler by ProjectDiscovery. Crawls websites to discover endpoints, links, and JavaScript-rendered content. Supports headless browsing for SPAs (React/Angular/Vue).

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-u` | Target URL |
| `-list / -l` | File with list of URLs |
| `-d` | Crawl depth (default: 3) |
| `-headless` | Use headless browser (for JS-heavy SPAs) |
| `-jc` | Parse JavaScript files for endpoints |
| `-aff` | Auto-fill forms |
| `-o` | Output file |
| `-json` | JSON output |
| `-silent` | Only print endpoints |
| `-scope` | Define scope by regex |
| `-field` | Output specific fields (url, path, fqdn, etc.) |
| `-proxy` | Route through proxy |
| `-H` | Custom header (e.g., auth cookies) |

---

## Examples

**Basic crawl**
```bash
katana -u https://example.com
```

**Crawl with depth 5 and JavaScript parsing**
```bash
katana -u https://example.com -d 5 -jc
```
*Finds endpoints hidden inside JS files.*

**Headless mode for JS-heavy apps (SPA)**
```bash
katana -u https://example.com -headless
```

**Crawl multiple targets from file**
```bash
katana -l urls.txt -d 3 -silent -o endpoints.txt
```

**Pipe from httpx**
```bash
subfinder -d example.com -silent | httpx -silent | katana -silent -o all_endpoints.txt
```

**Extract only paths**
```bash
katana -u https://example.com -field path -silent
```

**Authenticated crawl (send session cookie)**
```bash
katana -u https://example.com -H "Cookie: session=abc123"
```

**Route through Burp Proxy**
```bash
katana -u https://example.com -proxy http://127.0.0.1:8080
```


## Important Setup & Advanced Tips
- **Headless Crawling**: Use `-hl` to enable headless browser mode, which is essential for crawling Single Page Applications (React, Angular, Vue).
- **Field Extraction**: Katana can automatically extract JS files, endpoints, or emails during the crawl using `-f` (e.g., `-f qurl`).
- **Depth Control**: Use `-d` to limit crawl depth to prevent infinite loops or excessively long crawls.


## Input & Output Examples

**Input File (`urls.txt`)**
```text
https://example.com
https://test.com
```

**Output File (`crawled_urls.txt`)**
```text
https://example.com/about
https://example.com/contact
https://example.com/api/v1/status
https://test.com/login
```
