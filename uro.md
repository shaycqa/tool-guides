# uro

## What it is
A tool by s0md3v designed to declutter URL lists for crawling and pentesting by removing duplicate parameters, 'useless' extensions (like images/fonts), and incremental paths.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-i` | Read URLs from a specific file instead of stdin |
| `-o` | Write output to a file |
| `-w` | Only keep URLs with the specified extensions |
| `-b` | Remove URLs with specified extensions |
| `-f` | Apply granular filters (hasparams, noparams, hasext, noext) |

---

## Examples

**Basic usage via stdin**
```bash
cat urls.txt | uro
```

**Filter for potential XSS/SQLi targets (parameters only)**
```bash
cat urls.txt | uro -f hasparams
```

**Keep only web pages and remove extensionless paths**
```bash
cat urls.txt | uro -w html php aspx -f hasext
```

**Blacklist specific extensions**
```bash
cat urls.txt | uro -b js css png jpg
```


## Important Setup & Advanced Tips
- **Vulnerability Filtering**: Newer versions support `-f vuln` which strictly filters for URLs containing parameters historically associated with vulnerabilities (SSRF, LFI, SQLi).
- **Custom Regexes**: Uro's power lies in its underlying patterns. Keep the tool updated to benefit from improved deduplication logic.


## Input & Output Examples

**Input File (`urls.txt`)**
```text
https://example.com/api/users?id=1
https://example.com/api/users?id=2
https://example.com/style.css
https://test.com/login.php
```

**Output File (`filtered_urls.txt`)**
```text
https://example.com/api/users?id=1
https://test.com/login.php
```
