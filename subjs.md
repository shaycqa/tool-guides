# subjs

## What it is
A Go-based utility by lc used to quickly fetch JavaScript files from a list of URLs or subdomains. Great for starting client-side analysis.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-i` | Input file containing a list of URLs or subdomains |
| `-c` | Concurrency (number of workers) |
| `-t` | HTTP timeout in seconds |
| `-ua` | Custom User-Agent string to use for requests |
| `-wayback` | Includes JS files found in the Wayback Machine |

---

## Examples

**Basic usage via stdin**
```bash
echo 'https://example.com' | subjs
```

**Scanning a list of subdomains with high concurrency**
```bash
cat subdomains.txt | subjs -c 100
```

**Fetching historical JS files using the Wayback Machine**
```bash
echo 'example.com' | subjs -wayback
```

**Saving output to a file**
```bash
subjs -i urls.txt > javascript_files.txt
```


## Important Setup & Advanced Tips
- **Authentication**: If the target requires auth, pass headers using `-H "Authorization: Bearer <token>"`.
- **Parsing Limits**: `subjs` is fast but might miss dynamically loaded chunks (like Webpack chunks). Use a headless browser crawler for deep SPA applications.
- **Combine**: Best paired with `SecretFinder` or `LinkFinder`: `cat subdomains.txt | subjs | xargs -I % python3 SecretFinder.py -i % -o cli`.


## Input & Output Examples

**Input File (`urls.txt`)**
```text
https://example.com/index.html
https://test.com/dashboard
```

**Output File (`javascript_files.txt`)**
```text
https://example.com/assets/app.js
https://example.com/assets/vendor.js
https://test.com/js/main.js
```
