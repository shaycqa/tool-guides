# secretfinder

## What it is
A Python script by m4ll0k based on LinkFinder, used to discover sensitive data like API keys, access tokens, and passwords inside JavaScript files.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-i` | Input JS file or URL |
| `-e` | Extract specific regex pattern |
| `-o` | Output file or format (cli, html) |

---

## Examples

**Scan a single JavaScript URL**
```bash
python3 SecretFinder.py -i https://example.com/app.js -o cli
```

**Scan a local JavaScript file**
```bash
python3 SecretFinder.py -i app.js -o cli
```

**Scan multiple URLs from a file**
```bash
while read url; do python3 SecretFinder.py -i $url -o cli; done < js_urls.txt
```

**Output results as an HTML report**
```bash
python3 SecretFinder.py -i https://example.com/app.js -o report.html
```
