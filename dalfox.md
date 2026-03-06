# dalfox

## What it is
A fast, automated XSS scanner and parameter analyzer written in Go. Detects reflected, stored, and DOM-based XSS. Also catches open redirects, SSTI, and SQL injection hints. Integrates easily into pipelines.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `url` | Scan a single URL |
| `file` | Scan URLs from a file |
| `pipe` | Read URLs from stdin |
| `sxss` | Stored XSS mode |
| `-p` | Specify parameter to test |
| `-b / --blind` | Blind XSS callback URL |
| `-t / --trigger` | URL to trigger stored XSS payload |
| `--custom-payload` | File with custom payloads |
| `--waf-evasion` | Enable WAF bypass techniques |
| `--deep-domxss` | Deep DOM XSS scan (headless) |
| `--proxy` | Route through proxy |
| `-o` | Output file |
| `--format` | Output format (json, plain) |
| `--found-action` | Shell command to run on finding XSS |
| `--skip-bav` | Skip basic auth / verification |

---

## Examples

**Scan a single URL**
```bash
dalfox url "https://example.com/search?q=test"
```

**Scan a specific parameter**
```bash
dalfox url "https://example.com/page" -p query
```

**Blind XSS with callback**
```bash
dalfox url "https://example.com/contact" -b "https://your.xss.ht/callback"
```
*Great for stored XSS in forms where output isn't immediately visible.*

**Pipe URLs from a file**
```bash
cat urls.txt | dalfox pipe
```

**Scan from file**
```bash
dalfox file targets.txt
```

**Stored XSS mode**
```bash
dalfox sxss https://example.com/post -p comment -t https://example.com/view
```
*Injects into `comment` param, then visits `/view` to check if payload executed.*

**WAF evasion + custom payloads**
```bash
dalfox url "https://example.com/?q=test" \
  --custom-payload payloads.txt --waf-evasion
```

**Deep DOM XSS scan**
```bash
dalfox url "https://example.com/#q=test" --deep-domxss
```

**Save results as JSON**
```bash
dalfox url "https://example.com/?search=test" -o results.json --format json
```

**Route through Burp + execute action on find**
```bash
dalfox url "https://example.com/?q=test" \
  --proxy http://127.0.0.1:8080 \
  --found-action 'echo "XSS Found!" >> xss_hits.txt'
```

**Full pipeline from URLs**
```bash
katana -u https://example.com -silent | dalfox pipe -b "https://your.xss.ht"
```


## Important Setup & Advanced Tips
- **Blind XSS**: Use the `-b` flag to specify your XSS Hunter or Interactsh payload for out-of-band/blind XSS detection.
- **Custom Payloads**: Use `--custom-payload` to feed specific bypasses if a WAF is blocking standard payloads.
- **Deep DOM Extraction**: Dalfox has built-in DOM parsing to find hidden sinks.
