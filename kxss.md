# kxss

## What it is
A tool by EgeBalci (originally based on tomnomnom's work) used to find reflected characters in URLs, which is a strong indicator of potential Cross-Site Scripting (XSS) vulnerabilities.

---

## Key Flags
| Flag | Description |
|------|-------------|
| No specific flags | Usually takes URLs via stdin and checks for reflection of special characters like `<` `>` `"` `'`. |

---

## Examples

**Check a list of URLs for reflection**
```bash
cat urls.txt | kxss
```

**Pipe from waybackurls to find XSS candidates**
```bash
echo example.com | waybackurls | kxss
```

**Save potentially vulnerable URLs**
```bash
cat urls.txt | kxss > vulnerable_urls.txt
```
