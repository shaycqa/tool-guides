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


## Important Setup & Advanced Tips
- **True Validation**: `kxss` only finds *reflection*. It does not confirm exploitability. Always follow up with a tool like `Dalfox` or manual testing.
- **Pipeline**: A standard pipeline is `waymore -> uro -> gf xss -> kxss -> dalfox`.
